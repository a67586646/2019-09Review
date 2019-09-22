## Request & Response Message

无论是请求报文还是响应报文，都由三部分组成：start line, header和body

### Request

\<method>\<request-URL>\<version>
\<headers>
\<entity-body>

### Response

\<version>\<status>\<reason-phrase>
\<headers>
\<entity-body>

## 版本变化

### version 0.9

请求中只包含方法和URL，响应中只包含body，只支持GET方法。

### version 1.0

添加了版本号，各种HTTP首部，一些额外方法和对多媒体对象的处理。

### version 1.1

当前使用，引入性能优化措施，删除一些不好的特性。

## TCP/IP

### 三次握手

- 第一次握手： 建立连接。客户端发送连接请求报文段，将SYN位置为1，Sequence Number为x；然后，客户端进入SYN_SEND状态，等待服务器的确认；
- 第二次握手： 服务器收到SYN报文段。服务器收到客户端的SYN报文段，需要对这个SYN报文段进行确认，设置Acknowledgment Number为x+1(Sequence Number+1)；同时，自己自己还要发送SYN请求信息，将SYN位置为1，Sequence Number为y；服务器端将上述所有信息放到一个报文段（即SYN+ACK报文段）中，一并发送给客户端，此时服务器进入SYN_RECV状态；
- 第三次握手： 客户端收到服务器的SYN+ACK报文段。然后将Acknowledgment Number设置为y+1，向服务器发送ACK报文段，这个报文段发送完毕以后，客户端和服务器端都进入ESTABLISHED状态，完成TCP三次握手。

### 四次挥手

- 第一次分手： 主机1（可以使客户端，也可以是服务器端），设置Sequence Number，向主机2发送一个FIN报文段；此时，主机1进入FIN_WAIT_1状态；这表示主机1没有数据要发送给主机2了；
- 第二次分手： 主机2收到了主机1发送的FIN报文段，向主机1回一个ACK报文段，Acknowledgment Number为Sequence Number加1；主机1进入FIN_WAIT_2状态；主机2告诉主机1，我“同意”你的关闭请求；
- 第三次分手： 主机2向主机1发送FIN报文段，请求关闭连接，同时主机2进入LAST_ACK状态；
- 第四次分手： 主机1收到主机2发送的FIN报文段，向主机2发送ACK报文段，然后主机1进入TIME_WAIT状态；主机2收到主机1的ACK报文段以后，就关闭连接；此时，主机1等待2MSL后依然没有收到回复，则证明Server端已正常关闭，那好，主机1也可以关闭连接了。

## 缓存

### 强制缓存

对于强制缓存，服务器响应的header中会用两个字段来表明——Expires和Cache-Control。

#### Expires

Exprires的值为服务端返回的数据到期时间。当再次请求时的请求时间小于返回的此时间，则直接使用缓存数据。但由于服务端时间和客户端时间可能有误差，这也将导致缓存命中的误差，另一方面，Expires是HTTP1.0的产物，故现在大多数使用Cache-Control替代。

#### Cache-Control

Cache-Control有很多属性，不同的属性代表的意义也不同。
- private：客户端可以缓存
- public：客户端和代理服务器都可以缓存
- max-age=t：缓存内容将在t秒后失效
- no-cache：需要使用协商缓存来验证缓存数据
- no-store：所有内容都不会缓存。

### 协商缓存

协商缓存需要进行对比判断是否可以使用缓存。浏览器第一次请求数据时，服务器会将缓存标识与数据一起响应给客户端，客户端将它们备份至缓存中。再次请求时，客户端会将缓存中的标识发送给服务器，服务器根据此标识判断。若未失效，返回304状态码，浏览器拿到此状态码就可以直接使用缓存数据了。

#### Last-Modified

Last-Modified: 服务器在响应请求时，会告诉浏览器资源的最后修改时间。

if-Modified-Since: 浏览器再次请求服务器的时候，请求头会包含此字段，后面跟着在缓存中获得的最后修改时间。服务端收到此请求头发现有if-Modified-Since，则与被请求资源的最后修改时间进行对比，如果一致则返回304和响应报文头，浏览器只需要从缓存中获取信息即可。
从字面上看，就是说：从某个时间节点算起，是否文件被修改了.

- 如果真的被修改：那么开始传输响应一个整体，服务器返回：200 OK
- 如果没有被修改：那么只需传输响应header，服务器返回：304 Not Modified

if-Unmodified-Since: 从字面上看, 就是说: 从某个时间点算起, 是否文件没有被修改

- 如果没有被修改:则开始`继续'传送文件: 服务器返回: 200 OK
- 如果文件被修改:则不传输,服务器返回: 412 Precondition failed (预处理错误)

#### Etag

服务器响应请求时，通过此字段告诉浏览器当前资源在服务器生成的唯一标识（生成规则由服务器决定）

If-None-Match： 再次请求服务器时，浏览器的请求报文头部会包含此字段，后面的值为在缓存中获取的标识。服务器接收到次报文后发现If-None-Match则与被请求资源的唯一标识进行对比。

- 不同，说明资源被改动过，则响应整个资源内容，返回状态码200。
- 相同，说明资源无心修改，则响应header，浏览器直接从缓存中获取数据信息。返回状态码304.

## HTTPS

HTTP over SSL

1. 客户端和服务端建立 SSL 握手，客户端通过 CA 证书来确认服务端的身份；
2. 互相传递三个随机数，之后通过这随机数来生成一个密钥；
3. 互相确认密钥，然后握手结束；
4. 数据通讯开始，都使用同一个对话密钥来加解密；

## HTTP 2.0

新特性：
- 新的二进制格式（Binary Format），HTTP1.x的解析是基于文本。基于文本协议的格式解析存在天然缺陷，文本的表现形式有多样性，要做到健壮性考虑的场景必然很多，二进制则不同，只认0和1的组合。基于这种考虑HTTP2.0的协议解析决定采用二进制格式，实现方便且健壮。
- 多路复用（MultiPlexing），即连接共享，即每一个request都是是用作连接共享机制的。一个request对应一个id，这样一个连接上可以有多个request，每个连接的request可以随机的混杂在一起，接收方可以根据request的 id将request再归属到各自不同的服务端请求里面。
- header压缩，如上文中所言，对前面提到过HTTP1.x的header带有大量信息，而且每次都要重复发送，HTTP2.0使用encoder来减少需要传输的header大小，通讯双方各自cache一份header fields表，既避免了重复header的传输，又减小了需要传输的大小。
- 服务端推送（server push），同SPDY一样，HTTP2.0也具有server push功能。

参考链接
[关于 TCP/IP，必知必会的十个问题](https://juejin.im/post/598ba1d06fb9a03c4d6464ab#heading-19)
[HTTP----HTTP缓存机制](https://juejin.im/post/5a1d4e546fb9a0450f21af23)
[面试精选之http缓存](https://juejin.im/post/5b3c87386fb9a04f9a5cb037)
[HTTP1.0、HTTP1.1 和 HTTP2.0 的区别](https://juejin.im/entry/5981c5df518825359a2b9476)
[HTTPS加密原理](https://juejin.im/entry/5a9ac15bf265da239e4d8831)