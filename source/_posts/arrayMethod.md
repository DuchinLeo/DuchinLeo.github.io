---
layout: post
title: "常用Arrar方法"
date: 2019-11-25 17:14:51
tags:
  - Array
  - 方法
toc: true # 
comments: true
---

![image](/assets/mdImg/arr-title.png)

### [Arrar的方法](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/fill)

#### 1、 slice(start,end);   ---返回选区

> 从某个已有的数组返回选定的元素  

* start   必需。规定从何处开始选取。如果是负数，那么它规定从数组尾部开始算起的位置。也就是说，-1 指最后一个元素，-2 指倒数第二个元素，以此类推。
* end 可选。规定从何处结束选取。该参数是数组片断结束处的数组下标。如果没有指定该参数，那么切分的数组包含从 start 到数组结束的所有元素。如果这个参数是负数，那么它规定的是从数组尾部开始算起的元素。

<!-- more -->
```js
var _arr=[6687, 8778, 5582, 2814, 328, 4655, 2336, 9769];
console.log(_arr.slice(5,6));
//表示获取一个区间的元素，并返回一个数组。不改变原有的值。
console.log(_arr[5]);返回第五个
console.log(_arr);返回所有
```

#### 2、 toString(); 转字符串---返回str

>支持随机数36位  
 方法返回一个表示该对象的字符串。

```js
/**
 * 生成一个随机的字符串
 */
const getNoncestr = () => {
  return Math.random()
    .toString(36)
    .substr(2, 15);
};
```

#### 3、getLength(); 返回长度

>获取数组长度的属性。

#### 4、... ES6 扩展运算符

```js
console.log(...[1, 2, 3])
// 1 2 3
```

#### 5、Array.from;  类对象value转数组

>方法用于将两类对象转为真正的数组：

```js
let arrayLike = {
    '0': 'a',
    '1': 'b',
    '2': 'c',
    length: 3
};

// ES5的写法
var arr1 = [].slice.call(arrayLike); // ['a', 'b', 'c']

// ES6的写法
let arr2 = Array.from(arrayLike); // ['a', 'b', 'c']
```

#### 6、splice();    删除/替换---改变原有数组

>方法向/从数组中添加/删除项目	(index,howmany，item)

1、仅删除

```js
var  _arr=[1, 2, 3, 4]
_arr.splice(2,1)  // 从第二个开始删除，删除1个
 _arr=[1, 2, 4]
```

2、删除并替换

```js
 _arr=[10,11,88,12,13,14]
_arr.splice(2,1,99)	// 从第二个开始删除，删除1个，替换成第三个参数99
 _arr=[10,11,99,12,13,14]
```

#### 7、 unshift()  从开头元素添加---返回长度

>向数组的开头添加一个或更多元素，并返回新的长度。

```js
var arr = [1, 2, 3, 4]
length = arr.unshift(0);
console.log(length) // 5
console.log(arr) // [0, 1, 2, 3, 4]
```

#### 8、shift() 从开头元素删除---返回删值

>删除并返回被删除的元素即数组的第一个元素

```js
var arr = [1, 2, 3, 4]
el = arr.shift();
console.log(el) // 1
console.log(arr) // [2, 3, 4]
```

#### 9、pop() 从结尾元素删除---返回删值

>删除并返回删除掉的元素即数组的最后一个元素

```js
var arr = [1, 2, 3, 4]
el = arr.pop()
console.log(el)  // 4
console.log(arr) // [1, 2, 3]
```

#### 10、push() 从结尾元素添加---返回长度

>向数组的末尾添加一个或更多元素，并返回新的长度；改变原有数组

```js
var arr = [1, 2, 3, 4]
length = arr.push(5)
console.log(length) // 5
console.log(arr) // [1, 2, 3, 4, 5]
```

#### 11、[findIndex](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex) ---查询条件索引

>方法返回数组中满足提供的测试函数的第一个元素的索引。否则返回-1。

```js
var arr = [{id: 1, name: 'zs'},{id: 2, name: 'ls'},{id:3, name: 'ww'}]
var index = arr.findIndex(item => item.name === 'ww')
console.log(index) // 2
```

#### 12、filter() --- 返回新数组(通过测试规则的)

>方法创建/返回一个新数组, 其包含通过所提供函数实现的测试的所有元素。

```js

var arr = [{id: 1, name: 'zs'},{id: 2, name: 'ls'},{id:3, name: 'ww'}]
var _arr = arr.filter(item => item.id > 1)
console.log(_arr) //[{id: 2, name: 'ls'},{id:3, name: 'ww'}]
```

#### 13、find() --- 返回通过测试的子元素

```js
var arr = [{id: 1, name: 'zs'},{id: 2, name: 'ls'},{id:3, name: 'ww'}]
var chiid = arr.find(item => item.id === 2)
console.log(child) // {id: 1, name: 'zs'}
```

#### 14、fill(value[, start[, end]])

>value 用来填充数组元素的值。  
start 起始索引，默认值为0。
end 终止索引，默认值为 this.length

```js
[1, 2, 3].fill(4);               // [4, 4, 4]
[1, 2, 3].fill(4, 1);            // [1, 4, 4]
[1, 2, 3].fill(4, 1, 2);         // [1, 4, 3]
[1, 2, 3].fill(4, 1, 1);         // [1, 2, 3]
```

#### 15、map() 遍历数组的item 返回一个新的数组

>1、方法创建一个新数组，其结果是该数组中的每个元素都调用一个提供的函数后返回的结果。  
2、类似forEach、不过forEach没有返回数组

```js
var arr = [1, 2, 3]
var _arr = arr.map(item => item * 2)
console.log(_arr) // [2, 4, 6]

================================================================

var arr = [{ id: 1, name: 'zs' }, { id: 2, name: 'ls' }, { id: 3, name: 'ww' }]

var _arr = arr.map(item => {
  var obj = {}
  obj[item.id] = item.id + '_007';
  obj[item.name] = item.name;
  return obj
})
console.log(_arr) // [{1: "1_007", zs: "zs"}, {1: "1_007", zs: "zs"}, {3: "3_007", ww: "ww"}]
```

#### 16、concat()  连接数组---返回新的

>连接两个或更多的数组，并返回结果。

```js
var arr1 = [1, 2 ,3] , arr2 = [4, 5, 1];
var arr = arr1.concat(arr2)
console.log(arr) // [1, 2, 3, 4, 5, 1]
```

#### 17、join()   修改分隔符转字符串---返回分隔好的字符串

>把数组的所有元素放入一个字符串。元素通过指定的分隔符进行分隔。

```js
var arr = ['a', 'b', 'c', 'd']
var str = arr.join('$')
console.log(str) // "a$b$c$d"
```

#### 18、 reverse()   颠倒顺序

>颠倒数组中元素的顺序。

```js
var arr = [1, 2, 3, 4]
arr.reverse()
console.log(arr) // [4, 3, 2, 1]
```

#### 19、sort() ； 直接生成从小到大排序

>对数组的元素进行排序

```js
function sortNumber(a,b){
    return a - b
}
arr.sort(sortNumber)// 数字小到大
var arr = [2, 3, 1, 'c', 'a', 'b', 'B', 'A', 'C']
arr.sort()
console.log(arr) // [1, 2, 3, "A", "B", "C", "a", "b", "c"]

====================================
var arr = [{py: 'B'}, {py: 'S'}, {py: 'A'}]
arr.sort((a , b) => a.py - b.py)

[
    0: {py: "A"}
    1: {py: "B"}
    2: {py: "S"}
]

var _arr = arr.sotr((a, b) => {
    return a.py.charCodeAt() - b.py.charCodeAt()
})

[
    0: {py: "A"}
    1: {py: "B"}
    2: {py: "S"}
]
```

#### 20、indexOf();

>返回数组当中第一个匹配的元素的索引值，如果没有找到：返回-1；
返回值大于-1

```js
var arr = [1, 2, 3, 4]
var index = arr.indexOf(3)
console.log(index)  // 3
```

#### 21、[arr.reduce(callback,[initialValue])](https://www.jianshu.com/p/e375ba1cfc47)

>reduce 为数组中的每一个元素依次执行回调函数，不包括数组中被删除或从未被赋值的元素，接受四个参数：初始值（或者上一次回调函数的返回值），当前元素值，当前索引，调用 reduce 的数组

```js
// 最简单的用法，求乘积
var  arr = [1, 2, 3, 4];
var sum = arr.reduce((x,y)=>x+y)
var mul = arr.reduce((x,y)=>x*y)
console.log( sum ); //求和，10
console.log( mul ); //求乘积，24

// 案例2，处理对象key、val

    const userList = [
      { text: '苹果', value: 1},
      { text: '香蕉', value: 2}
    ]

    const userObj = userList.reduce((arr, person) => {
      return {
        ...arr,
        [person.value]: person.text
      }
      // or
      arr[person.value]=arr.text
      return arr
    }, {})
  // userObj = { '1' : '苹果' , '2' : '香蕉' }
```

#### 22、Array.isArray()  ---返回boolean是否为Array

>用于确定传递的值是否是一个 Array。

```js
Array.isArray([1, 2, 3]);  
// true
Array.isArray({foo: 123}); 
// false
```

#### 23、Array.of()

>Array.of( )方法总会创建一个包含所有传入参数的数组，而不管参数的数量与类型

```js
let items = Array.of(1, 2);
console.log(items.length); // 2
console.log(items[0]); // 1
console.log(items[1]); // 2
items = Array.of(2);
console.log(items.length); // 1
console.log(items[0]); // 2

```

#### 24、Array.some(function)

>some() 方法用于检测数组中的元素是否满足指定条件（函数提供）。  
不会对空数组进行检测  
不会改变原始数组

```js
var ages = [3, 10, 18, 20];

function checkAdult(age) {
    return age >= 18;
}

function myFunction() {
    document.getElementById("demo").innerHTML = ages.some(checkAdult);
}

// vue路由权限设置，路由meta里面requireAuth：为true则需要token
to.matched.some(record => record.meta.requireAuth)
```

#### 25、Array..flat([depth])

>flat() 方法会按照一个可指定的深度递归遍历数组，并将所有元素与遍历到的子数组中的元素合并为一个新数组返回。

```js
var arr1 = [1, 2, [3, 4]];
arr1.flat(); 
// [1, 2, 3, 4]

var arr2 = [1, 2, [3, 4, [5, 6]]];
arr2.flat();
// [1, 2, 3, 4, [5, 6]]

var arr3 = [1, 2, [3, 4, [5, 6]]];
arr3.flat(2);
// [1, 2, 3, 4, 5, 6]

//使用 Infinity，可展开任意深度的嵌套数组
var arr4 = [1, 2, [3, 4, [5, 6, [7, 8, [9, 10]]]]];
arr4.flat(Infinity);
// [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

#### 26、includes()

>方法用来判断一个数组是否包含一个指定的值，如果是返回 true，否则false。

```js
[1, 2, 3].includes(2);     // true
[1, 2, 3].includes(4);     // false
[1, 2, 3].includes(3, 3);  // false
[1, 2, 3].includes(3, -1); // true
[1, 2, NaN].includes(NaN); // true
```

语法  
arr.includes(searchElement, fromIndex)

```js
searchElement   //必须。需要查找的元素值。

fromIndex   //可选。从该索引处开始查找 searchElement。如果为负值，则按升序从 array.length + fromIndex 的索引开始搜索。默认为 0。
```
