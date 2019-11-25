---
title: "常用Sting对象方法"
date: 2019-11-25 18:00:36
tags:
---

![image](/assets/mdImg/str-title.png)

### [String对象的方法](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/fill)

##### charAt()

>返回指定索引位置的字符

```js
var str = 'abcdefg';
var indexC = str.charAt(2) // 'c'
```

##### charCodeAt()

>返回指定索引位置字符的 Unicode 值

```js
var str = 'abcdefg';
var indexC = str.charCodeAt(2) // 99
```

##### concat()

>连接两个或多个字符串，返回连接后的字符串

```js
var str1 = 'abc', str2 = 'def';
var str = str1.concat(str2); // "abcdef"
```

##### String.fromCharCode()

>将 Unicode 转换为字符串

```js
String.fromCharCode(65,66,67) // ABC
```

##### indexOf()

>返回字符串中检索指定字符第一次出现的位置,没有找到返回-1

```js
var str = 'aabababa'
str.indexOf('b') // 2
```

##### lastIndexOf()

>返回字符串中检索指定字符最后一次出现的位置，没有找到返回-1

```js
var str = 'aabababa'
str.lastIndexOf('b') // 6
```

##### localeCompare()

>用本地特定的顺序来比较两个字符串

```js
// 本地按中文字母开头排序
var array = ['白鸽', '麻雀', '大象', '狗', '猫', "鸡"];
array = array.sort(function compareFunction(item1, item2) {
    return item1.localeCompare(item2);
});
//["白鸽", "大象", "狗", "鸡", "麻雀", "猫"]
```

##### match()

>找到一个或多个正则表达式的匹配

```js
var str="1 plus 2 equal 3"
str.match(/\d+/g) // ['1', '2', '3']

```

##### replace()

>替换与正则表达式匹配的子串

```js
var str="1 plus 2 equal 3"
str.replace(/\d+/g , 1) // "1 plus 1 equal 1"
```

##### search()

>方法用于检索字符串中指定的子字符串，或检索与正则表达式相匹配的子字符串。

```js
var str="1 plus 2 equal 3 我，你 all"
var my = new RegExp('我')
str.search(my) // 17
str.search(/p/) // 2

// 忽略大小写
var str="Visit W3School!"
document.write(str.search(/w3school/i))
```

##### slice()

>提取字符串的片断，并在新的字符串中返回被提取的部分

```js
var str="1 plus 2 equal 3"
var strs = str.slice(0, 3) // "1 p"
```

##### split()

>把字符串分割为子字符串数组

```js
var str = 'abcdef'
str.split('c') // ['ab', 'def']
```

##### substr()

>从起始索引号提取字符串中指定数目的字符

```js
var str = 'abcdef'
str.substr(1)  // "bcdef"
str.substr(-1) // "f"
```

##### substring()

>提取字符串中两个指定的索引号之间的字符

```js
var str = 'abcdef'
str.substring(1,2) // "b"
str.substring(2) // "cdef"
```

##### toLocaleLowerCase()

>根据主机的**语言环境把字符串转换为小写**，只有几种语言（如土耳其语）具有地方特有的大小写映射

```js
var str = 'Hello World'
undefined
str.toLocaleLowerCase()
"hello world"
```

##### toLocaleUpperCase()

>根据主机的语言环境把字符串**转换为大写**，只有几种语言（如土耳其语）具有地方特有的大小写映射

```js
var str = 'Hello World'
undefined
str.toLocaleLowerCase()
"HELLO WORLD"
```

##### toLowerCase()

>把字符串转换为小写

```js
var str = 'Hello World'
undefined
str.toLowerCase()
"hello world"
```

##### toUpperCase() 把字符串转换为大写

```js
//
```

##### toString()

>方法可把一个逻辑值转换为字符串，并返回结果

```js
booleanObject.toString()
var boo = new Boolean(true)
boo.toString() // true
```

##### trim()

>移除字符串首尾空白

```js
var str = '  ss ss s  '
str.trim() // "ss ss s"
```
