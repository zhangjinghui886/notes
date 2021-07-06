## Number

### 1-Number的方法

Number.isNaN()

```js
// 参数 不限制
// 返回值  Boolean

// Number.isNaN  与全局的isNaN的区别
// 全局的会将参数隐式转为数字类型，再判断是否为NaN
Number.isNaN(NaN)
// true
Number.isNaN('NaN')
// false
isNaN('nan')
// true
isNaN('NaN')
// true
isNaN(undefined)
// true
isNaN({})
// true
```

Number.isInteger()

```js
// 参数：Number
// 返回值：Boolean
// 功能：要判断此参数是否为整数
Number.isInteger('111')
// false
Number.isInteger(NaN)
// false
Number.isInteger(Infinity)
// false
```

> 注意：次方法不会对参数进行隐式转换

Number.parseFloat()

```js
// 参数：String【传递数字也没问题，没啥必要】
// 返回值：Number【被解析为浮点数的结果 】
// 功能：解析传递的字符串中的数字部分，如果解析不出结果 返回NaN
Number.parseFloat('100.1qqq11')
// 100.1
Number.parseFloat('100.111qqq')
// 100.111
Number.parseFloat('aaa100.111')
// NaN
```

> 与全局的parseFloat()方法一样

Number.parseInt()

```js
// 参数：String[, Number]
// 返回值：Number
// 功能：解析传递的字符串中的数字部分，如果解析不出来，返回NaN
[1,2,3,4].map(parseInt) // [1, NaN, NaN, NaN]
[1,2,3,4].map((item, index) => parseInt(item)) // [1, 2, 3, 4]
```



## Array

### 1-Array的方法

Array.from()

```js
// param：arrayLike[, mapFn, thisArg]
// return: Array
// function: 将类似数组或者可迭代对象浅拷贝为一个数组实例
Array.from('foo');
// [ "f", "o", "o" ]  字符串为可迭代对象
const set = new Set(['foo', 'bar', 'baz', 'foo']);
Array.from(set);
// [ "foo", "bar", "baz" ] set实例也是可迭代对象
const map = new Map([[1, 2], [2, 4], [4, 8]]);
Array.from(map);
// [[1, 2], [2, 4], [4, 8]]  map实例也是可迭代对象
function f() {
  return Array.from(arguments);
}
f(1, 2, 3);
// [ 1, 2, 3 ]   arguments类数组
Array.from([1, 2, 3], x => x + x);
// [2, 4, 6]  使用箭头函数
```

Array.prototype.copywithin()

```js
/** 参数：target start end */
/** 功能：将数组中的一部分，复制到同一数组的另一个位置，并返回他，不改变数据的长度  */
```

Array.prototype.concat()

```js
/** 参数 (vaule/Array) */
/** 功能：合并两个或者多个数据，此方法不改变现有数组，而是返回一个新数组  */
/** 如果没有参数，则是对调用数组的一次浅拷贝  */
```

Array.prototype.entries()

```js
/** 参数：no  */
/** 功能：返回一个数组的迭代器对象 */
/** 使用for of进行遍历  */
```

Array.prototype.every()

```js
/** 参数： function(item, index, arr) */
/** 返回值： boolean 【当数组为空的时候，都是返回true】 */
/** 功能描述，遍历元素，如何第一个元素不满足函数的条件，则直接返回false */
```

