# Array

## 遍历

### Array.every

every() 方法测试一个数组内的所有元素是否都能通过某个指定函数的测试。它返回一个布尔值。

### Array.filter

filter() 方法创建一个新数组, 其包含通过所提供函数实现的测试的所有元素。 

### Array.find

find() 方法返回数组中满足提供的测试函数的第一个元素的值。否则返回 undefined。

### Array.findIndex

findIndex()方法返回数组中满足提供的测试函数的第一个元素的索引。否则返回-1。

### Array.forEach

forEach() 方法对数组的每个元素执行一次提供的函数。

### Array.map

map() 方法创建一个新数组，其结果是该数组中的每个元素都调用一个提供的函数后返回的结果。

### Array.reduce

reduce() 方法对数组中的每个元素执行一个由您提供的reducer函数(升序执行)，将其结果汇总为单个返回值。

### Array.reduceReight

reduceRight() 方法接受一个函数作为累加器（accumulator）和数组的每个值（从右到左）将其减少为单个值。

### Array.some

some() 方法测试数组中是不是有元素通过了被提供的函数测试。它返回的是一个Boolean类型的值。

## 常用

### Array.concat

concat() 方法用于合并两个或多个数组。此方法不会更改现有数组，而是返回一个新数组。

### Array.join

join() 方法将一个数组（或一个类数组对象）的所有元素连接成一个字符串并返回这个字符串。如果数组只有一个项目，那么将返回该项目而不使用分隔符。

### Array.indexOf

indexOf()方法返回在数组中可以找到一个给定元素的第一个索引，如果不存在，则返回-1。

### Array.lastIndexOf

lastIndexOf() 方法返回指定元素（也即有效的 JavaScript 值或变量）在数组中的最后一个的索引，如果不存在则返回 -1。从数组的后面向前查找，从 fromIndex 处开始。

### Array.pop

pop()方法从数组中删除最后一个元素，并返回该元素的值。此方法更改数组的长度。

### Array.push

push() 方法将一个或多个元素添加到数组的末尾，并返回该数组的新长度。

### Array.reverse

reverse() 方法将数组中元素的位置颠倒，并返回该数组。该方法会改变原数组。

### Array.shift

shift() 方法从数组中删除第一个元素，并返回该元素的值。此方法更改数组的长度。

### Array.slice

slice() 方法返回一个新的数组对象，这一对象是一个由 begin 和 end 决定的原数组的浅拷贝（包括 begin，不包括end）。原始数组不会被改变。

### Array.sort

sort() 方法用原地算法对数组的元素进行排序，并返回数组。默认排序顺序是在将元素转换为字符串，然后比较它们的UTF-16代码单元值序列时构建的

由于它取决于具体实现，因此无法保证排序的时间和空间复杂性。

### Array.splice

splice() 方法通过删除或替换现有元素或者原地添加新的元素来修改数组,并以数组形式返回被修改的内容。此方法会改变原数组。

## 其他

### Array.from

> Array.from(arrayLike[, mapFn[, thisArg]])

Array.from() 可以通过以下方式来创建数组对象：

 - 伪数组对象（拥有一个 length 属性和若干索引属性的任意对象）
 - 可迭代对象（可以获取对象中的元素,如 Map和 Set 等）

Array.from() 方法有一个可选参数 mapFn，让你可以在最后生成的数组上再执行一次 map 方法后再返回。也就是说 Array.from(obj, mapFn, thisArg) 就相当于 Array.from(obj).map(mapFn, thisArg), 除非创建的不是可用的中间数组。 这对一些数组的子类,如  typed arrays 来说很重要, 因为中间数组的值在调用 map() 时需要是适当的类型。


### Array.entries

entries() 方法返回一个新的Array Iterator对象，该对象包含数组中每个索引的键/值对。

### Array.fill

fill() 方法用一个固定值填充一个数组中从起始索引到终止索引内的全部元素。不包括终止索引。

### Array.flat

flat() 方法会按照一个可指定的深度递归遍历数组，并将所有元素与遍历到的子数组中的元素合并为一个新数组返回。

### Array.flatMap

flatMap() 方法首先使用映射函数映射每个元素，然后将结果压缩成一个新数组。它与 map 和 深度值1的 flat 几乎相同，但 flatMap 通常在合并成一种方法的效率稍微高一些。

### Array.includes

includes() 方法用来判断一个数组是否包含一个指定的值，根据情况，如果包含则返回 true，否则返回false。

注意：对象数组不能使用includes方法来检测。

### Array.keys

keys() 方法返回一个包含数组中每个索引键的Array Iterator对象。