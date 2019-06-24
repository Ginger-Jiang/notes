```javascript
知识点
	- 面向对象
	- 面向过程
	- 创建对象
	- 自定义对象
	- 内置对象
```

### 编程思想

```javascript
// 面向过程：所有代码全部自己编写，每个逻辑都需要知道，注重过程
// 面向对象：根据需求找对象，所有事情都由对象来完成，注重的是最后的结果

// 面向对象的特性：封装、继承、多态
// js不是面向对象的语言，是基于对象的语言，可以模拟面向对象的思想。

// 什么是对象：有特征(属性)与行为(方法)，具体特指的某一个事物。

// 创建对象
// 一、调用系统构造函数创建对象
var obj = new Object() // 创建(实例化)一个对象
obj.name = '周杰伦' // 为对象添加属性
obj.eat = function(){ // 添加方法
    console.log('吃吃吃')
}
console.log(obj.name)  // 获取对象的属性
obj.eat() // 调用对象的方法

// 二、自定义构造函数创建对象
function Preson(){ // 自定义构造函数
    this.name = '周杰伦' // 添加属性
    this.eat = function(){ // 添加方法
        console.log('吃吃吃')
    }
}
var obj = new Preson() // 使用自定义构造函数创建对象(实例化一个对象)
// 重点：自定义构造函数做的四件事
// 1、在内存中开辟(申请)了一块空间，存储创建的新对象
// 2、把this设置为当前对象
// 3、设置对象的属性和方法
// 4、把this这个对象返回

// 三、字面量方式创建对象
var obj = {} // 空对象
obj.name = '周杰伦' // 添加属性
obj.eat = function(){ // 添加方法
    console.log('吃')
}
// 简写
var obj = {
    name:'周杰伦',
    eat:function(){
        console.log('吃')
    }
}

// 设置和获取属性
var obj = {
    name:'周杰伦'
}
一、点语法
console.log(obj.name) // 获取
obj.name = '刘德华' // 设置

二、中括号
console.log(obj['name'])
obj['name'] = '刘德华' // 设置

```
### JSON格式的数据与遍历
```javascript
var json = { // json格式的数据，键值对方式存在
    'name':'周杰伦',
    'sex':'男'
}
// 遍历json对象
for (var key in json){
    console.log(key) // 获取json对象的键
    console.log(json[key]) // 获取值
}
```

### 简单类型与复杂类型

```javascript
// 原始数据类型 string number boolean object null undefined
// 基本类型(值类型、简单类型)：number string boolean
// 复杂类型(引用类型)：object
// 空类型：null undefined

// 重点：
// 值类型的值储存在栈中(占一块空间)
// 引用类型的值储存在堆中，地址存储在栈中(占两块空间)

//值类型与引用类型的传递
var num = 100
var num1 = num // 值类型的传递，传递的是值(100)

var obj = {
    name:'周杰伦'
}
function obj1(obj){
    obj.name = '刘德华'
}
obj1(obj)
console.log(obj.name) // 刘德华 引用类型的传递，传递的是地址
```
### 内置对象
```javascript
/* 
Math 算术函数和常量 
Math.abs( ) 计算绝对值 
Math.acos( ) 计算反余弦值 
Math.asin( ) 计算反正弦值 
Math.atan( ) 计算反正切值 
Math.atan2( ) 计算从x轴到一个点之间的角度 
Math.ceil( ) 对一个数上舍入 
Math.cos( ) 计算余弦值 
Math.E 算术常量e 
Math.exp( ) 计算ex 
Math.floor( ) 对一个数下舍入 
Math.LN10 算术常loge10 
Math.LN2 算术常量loge2 
Math.log( ) 计算一个数的自然对数 
Math.LOG10E 算术常量log10e 
Math.LOG2E 算术常量log2e 
Math.max( ) 返回最大的参数 
Math.min( ) 返回最小的参数 
Math.PI 算术常量PI 
Math.pow( ) 计算xy 
Math.random( ) 返回一个伪随机数 
Math.round( ) 舍入到最接近的整数 
Math.sin( ) 计算正弦值 
Math.sqrt( ) 计算平方根 
Math.tan( ) 计算正切值 
*/

/*
Date  操作日期和时间的对象 
Date.getDate( ) 返回一个月中的某一天 
Date.getDay( ) 返回一周中的某一天 
Date.getFullYear( ) 返回Date对象的年份字段 
Date.getHours( ) 返回Date对象的小时字段 
Date.getMilliseconds( ) 返回Date对象的毫秒字段 
Date.getMinutes( ) 返回Date对象的分钟字段 
Date.getMonth( ) 返回Date对象的月份字段 
Date.getSeconds( ) 返回Date对象的秒字段 
Date.getTime( ) 返回Date对象的毫秒表示 
Date.getTimezoneOffset( ) 判断与GMT的时间差 
Date.getUTCDate( ) 返回该天是一个月的哪一天(世界时) 
Date.getUTCDay( ) 返回该天是星期几(世界时) 
Date.getUTCFullYear( ) 返回年份(世界时) 
Date.getUTCHours( ) 返回Date对象的小时字段(世界时) 
Date.getUTCMilliseconds( ) 返回Date对象的毫秒字段(世界时) 
Date.getUTCMinutes( ) 返回Date对象的分钟字段(世界时) 
Date.getUTCMonth( ) 返回Date对象的月份(世界时) 
Date.getUTCSeconds( ) 返回Date对象的秒字段(世界时) 
Date.getYear( ) 返回Date对象的年份字段(世界时) 
Date.parse( ) 解析日期/时间字符串 
Date.setDate( ) 设置一个月的某一天 
Date.setFullYear( ) 设置年份，也可以设置月份和天 
Date.setHours( ) 设置Date对象的小时字段、分钟字段、秒字段和毫秒字段 
Date.setMilliseconds( ) 设置Date对象的毫秒字段 
Date.setMinutes( ) 设置Date对象的分钟字段和秒字段 
Date.setMonth( ) 设置Date对象的月份字段和天字段 
Date.setSeconds( ) 设置Date对象的秒字段和毫秒字段 
Date.setTime( ) 以毫秒设置Date对象 
Date.setUTCDate( ) 设置一个月中的某一天(世界时) 
Date.setUTCFullYear( ) 设置年份、月份和天(世界时) 
Date.setUTCHours( ) 设置Date对象的小时字段、分钟字段、秒字段和毫秒字段(世界时) 
Date.setUTCMilliseconds( ) 设置Date对象的毫秒字段(世界时) 
Date.setUTCMinutes( ) 设置Date对象的分钟字段和秒字段(世界时) 
Date.setUTCMonth( ) 设置Date对象的月份字段和天数字段(世界时) 
Date.setUTCSeconds( ) 设置Date对象的秒字段和毫秒字段(世界时) 
Date.setYear( ) 设置Date对象的年份字段 
Date.toDateString( ) 返回Date对象日期部分作为字符串 
Date.toGMTString( ) 将Date转换为世界时字符串 
Date.toLocaleDateString( ) 回Date对象的日期部分作为本地已格式化的字符串 
Date.toLocaleString( ) 将Date转换为本地已格式化的字符串 
Date.toLocaleTimeString( ) 返回Date对象的时间部分作为本地已格式化的字符串 
Date.toString( ) 将Date转换为字符串 
Date.toTimeString( ) 返回Date对象日期部分作为字符串 
Date.toUTCString( ) 将Date转换为字符串(世界时) 
Date.UTC( ) 将Date规范转换成毫秒数 
Date.valueOf( ) 将Date转换成毫秒表示 
*/

/*
String 对字符串的支持 
String.charAt( ) 返回字符串中的第n个字符 
String.charCodeAt( ) 返回字符串中的第n个字符的代码 
String.concat( ) 连接字符串 
String.fromCharCode( ) 从字符编码创建—个字符串 
String.indexOf( ) 检索字符串 
String.lastIndexOf( ) 从后向前检索一个字符串 
String.length 字符串的长度 
String.localeCompare( ) 用本地特定的顺序来比较两个字符串 
String.match( ) 找到一个或多个正则表达式的匹配 
String.replace( ) 替换一个与正则表达式匹配的子串 
String.search( ) 检索与正则表达式相匹配的子串 
String.slice( ) 抽取一个子串 
String.split( ) 将字符串分割成字符串数组 
String.substr( ) 抽取一个子串 
String.substring( ) 返回字符串的一个子串 
String.toLocaleLowerCase( ) 把字符串转换小写 
String.toLocaleUpperCase( ) 将字符串转换成大写 
String.toLowerCase( ) 将字符串转换成小写 
String.toString( ) 返回字符串 
String.toUpperCase( ) 将字符串转换成大写 
String.valueOf( ) 返回字符串 
*/

/*
Array  对数组的内部支持 
Array.concat( ) 连接数组 
Array.join( ) 将数组元素连接起来以构建一个字符串 
Array.length 数组的大小 
Array.pop( ) 删除并返回数组的最后一个元素 
Array.push( ) 给数组添加元素 
Array.reverse( ) 颠倒数组中元素的顺序 
Array.shift( ) 将元素移出数组 
Array.slice( ) 返回数组的一部分 
Array.sort( ) 对数组元素进行排序 
Array.splice( ) 插入、删除或替换数组的元素 
Array.toLocaleString( ) 把数组转换成局部字符串 
Array.toString( ) 将数组转换成一个字符串 
Array.unshift( ) 在数组头部插入一个元素 
*/
```



