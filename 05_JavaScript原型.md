```javascript
知识点
	- 编程思想
	- 原型
	- 原型链
	- 继承
	- this
```

### 编程思想

面向对象编程 —— Object Oriented Programming，简称 OOP ，是一种编程开发思想。

### 面向对象的特性:封装,继承,多态

- 封装：

```javascript
封装:就是包装
    * 一个值存储在一个变量中--封装
    * 一坨重复代码放在一个函数中--封装
    * 一系列的属性放在一个对象中--封装
    * 一些功能类似的函数(方法)放在一个对象中--封装
    * 好多相类似的对象放在一个js文件中---封装
```

- 继承：

```javascript
继承是一种关系,类(class)与类之间的关系,JS中没有类,但是可以通过构造函数模拟类,然后通过原型来实现继承
```

- 多态：

```javascript
一个对象有不同的行为,或者是同一个行为针对不同的对象,产生不同的结果,要想有多态,就要先有继承,js中可以模拟多态,但是不会去使用,也不会模拟.
```

### 构造函数和实例对象的关系

在每一个实例对象中的 `__proto__` 中同时有一个 constructor 属性，这个属性指向创建这恶实例对象的构造函数

```javascript
// 推荐：属性私有化、方法公有化

function Person(name, age){
    this.name = name
    this.age = age
}
var p1 = new Person('周杰伦'， 18)
var p2 = new Person('刘德华', 18)

console.log(p1.constructor === Person) // => true
console.log(p2.constructor === Person) // => true
console.log(p1.constructor === p2.constructor) // => true

instanceof // => 检测对象的类型
console.log(p1 instanceof Person) // => true
console.log(p2 instanceof Person) // => true

// 小结
1、实例对象是通过构造函数创建，创建的过程叫做实例化
2、判断实例化对象是不是这个数据类型？
	1、通过构造器的方式 实例对象.构造器 == 构造函数名字
	2、instanceof （推荐）
3、实例对象使用的属性或者方法,先在实例中查找,找到了则直接使用,找不到则,去实例对象的__proto__指向的原型对象prototype中找,找到了则使用,找不到则报错
```

### 原型

```javascript
原型的作用：
1、数据共享 节省内存空间
2、实现继承
// 案例
function Person(name){
    this.name = name
    this.eat = function(){
        console.log('吃饭啦～')
    }
}
var p1 = new Person('刘德华')
var p2 = new Person('周杰伦')
// 这里每个实例对象都会单独创建自己的 eat 方法，方法的作用一致，浪费空间
console.log(p1.eat == p2.eat)  // => false 


Person.prototype.show = funciotn(){
    console.log('原型方法')
}
// 实例对象的 prototype 原型上的方法可以共享数据，节省内存空间
console.log(p1.eat == p2.eat) // true 同一个方法 占用一块内存空间

// 原型的简单写法=>需要手动添加构造器
Person.prototype = {
    constructor：Person
    sex:'男'，
    sayhi：function(){
    	console.lof('原型方法')
	}
}

// 原型中的方法是可以相互访问的
```

### 构造函数、实例、原型三者之间的关系

- 构造函数可以实例化对象
- 构造函数中有一个属性叫prototype,是构造函数的原型对象
-  构造函数的原型对象(prototype)中有一个constructor构造器,这个构造器指向的就是自己所在的原型对象所在的构造函数
- 实例对象的原型对象(__proto__)指向的是该构造函数的原型对象
-  构造函数的原型对象(prototype)中的方法是可以被实例对象直接访问的

![](D:\桌面\note\JavaScript基础\三者之间的关系.png)

### 原型链

实例对象和原型对象之间的关系是通过`__proto__`原型来联系起来的,这个关系就是原型链

```javascript
// 实例对象的原型 __ptoto__ 和构造函数的原型 prototype 指向是相同的
// 实例对象中的 __proto__ 指向的是构造函数中的原型 prototype
```

##### 原型指向可以改变原型链

- 实例对象的原型`__proto__`指向的是该对象所在的构造函数的原型对象
- 构造函数的原型对象(prototype)指向如果改变了,实例对象的原型(`__proto__`)指向也会发生改变
- 如果原型指向改变了,那么就应该在原型改变指向之后添加原型方法

```javascript
// 一个神奇的原型链
var divObj=document.getElementById("dv");
  console.dir(divObj);

//divObj.__proto__--->HTMLDivElement.prototype的__proto__--->HTMLElement.prototype的__proto__---->Element.prototype的__proto__---->Node.prototype的__proto__---->EventTarget.prototype的__proto__---->Object.prototype没有__proto__,所以,Object.prototype中的__proto__是null
```

### 继承

- 利用原型链实现继承

```javascript
// 改变原型链指向是实现继承
function Person(name){ // 构造函数
    this.name = name
}
Person.prototype.eta = function(){ // 给构造函数添加原型方法
    console.log(this.name + '吃饭啦')
}
function Student(sex){ // 构造函数
    this.sex = sex
}
Student.prototype = new Person('周杰伦') // 通过改变原型链的指向实现了继承 但是后续所有 Student 的实例对象中的 name 属性值默认都是'周杰伦'
var zhou = new Student('男') // 实例化对象
var liu = new Student('女') // 实例化对象
zhou.eat() // 调用继承的 eat 方法 --> 周杰伦吃饭啦  
liu.eat() // 调用继承的 eat 方法 --> 周杰伦吃饭啦  

// 缺点
// 因为改变原型指向的同时实现继承,直接初始化了属性，不同的实例化对象，继承过来的属性的值都是一样的。
```

- 借用构造函数实现继承(对象冒充)

```javascript
// 调用父级的构造函数来为属性赋值，只继承私有属性和方法
function Person(name){ // 父级构造函数
    this.name = name
}
Person.prototype.play = function(){
    console.log(this.name + '出来嗨啊')
}
function Studend(name){
    // 借用构造函数 第一个参数：当前对象 第二个：需要的传递的参数
    Person.call(this, name) // this 是当前的构造函数的实例对象
}
var s1 = new Studend('周杰伦')
var s2 = new Studend('刘德华')
console.log(s1.name) // 周杰伦
console.log(s2.name) // 刘德华
s1.play() // 报错
s2.play() // 报错

// 优点
// 解决了原型链继承中属性值重复的问题

// 缺点
// 无法继承到父级构造函数的原型上面的方法
```

- 组合继承

```javascript
// 原型链继承+借用构造函数继承=组合继承
function Person(name, age, sex){ // 父级构造函数
  this.name = name
  this.age = age
  this.sex = sex
}
Person.prototype.sayHi = function(){ // 添加原型方法
  console.log(this.name + '吃了么');
}

function Student(name, age, sex){ // 子级构造函数
  Person.call(this, name, age, sex)
}
Student.prototype = new Person() // 改变原型链指向

var s1 = new Student('周杰伦', 18, '男') // 实例化对象
var s2 = new Student('刘德华', 18, '男') // 实例化对象

s1.sayHi() // 调用借用构造函数继承的方法 -- > 周杰伦吃了么 
s2.sayHi() // 调用借用构造函数继承的方法 -- > 刘德华吃了么
console.log(s1.name+s1.age+s1.sex) // 输出改变原型链继承的属性 --> 周杰伦18男
console.log(s2.name+s2.age+s2.sex) // 输出改变原型链继承的属性 --> 周杰伦18男
```

- 拷贝继承

```javascript
// 把一个对象中的属性和方法复制到另一个对象中
// 1、改变地址指针指向
var obj1 = {
  name:'周杰伦',
  age:18,
  eat:function(){
    console.log('好饿啊')
  }
}    
var obj2 = obj1 // 仅仅改变了地址指向，实际没有开辟空间
console.log(obj2.name) // 周杰伦
obj2.eat() // 好饿啊

// 2、拷贝对象内容（浅拷贝）
var obj1 = {
  name:'周杰伦',
  age:18,
  eat:function(){
    console.log('好饿啊')
  }
}
var obj2 = {} // obj2 有自己独立的空间
for (const key in obj1) {
  obj2[key] = obj1[key]
}
console.log(obj2.name) // 周杰伦
obj2.eat() // 好饿啊

// 3、拷贝继承 
function Obj1(){}
Obj1.prototype.name = '周杰伦'
Obj1.prototype.age = 18
Obj1.prototype.eat = function(){
    console.log('好饿啊')
}
var obj2 = {}
for (const key in Obj1.prototype) { // 原型对象 prototype 也是对象，也可以遍历
  obj2[key] = Obj1.prototype[key]
}
console.log(obj2.name) // 周杰伦
obj2.eat() // 好饿啊
```

- 小结继承

```javascript
//继承,是类与类之间的关系,面向对象的语言的继承是为了多态服务的,
//js不是面向对象的语言,但是可以模拟面向对象.模拟继承.为了节省内存空间
    // 原型作用: 数据共享 ，目的是:为了节省内存空间,
    // 原型作用: 继承  目的是:为了节省内存空间
    // 原型继承:改变原型的指向
    // 借用构造函数继承:主要解决属性的问题
    // 组合继承:原型继承+借用构造函数继承
    // 既能解决属性问题,又能解决方法问题
    // 拷贝继承:就是把对象中需要共享的属性或者犯法,直接遍历的方式复制到另一个对象中
```

### 函数角色

```javascript
// 推荐使用函数表达式
// 函数的角色：
// 1、函数的声明 放在 if-else 中，在低版本浏览器中会出现问题
if(true){
  function f1() {
    console.log("我是 true")
  }
}else{
  function f1() {
    console.log("我是 false")
  }
}
f1() // 在 IE8 中，结果是 '我是false'
// 2、函数表达式
var ff
if (true) {
  ff = function () {
    console.log("我是 true");
  }
} else {
  ff = function () {
    console.log("我是 false")
  }
}
ff() // 结果都是 '我是true'

// 扩展
// 函数是对象,对象不一定是函数
// 所有的函数实际上都是Function的构造函数创建出来的实例对象
// 对象中有__proto__原型,是对象
// 函数中有prototype原型,是对象
```

### this指向

```javascript
// 普通模式下：
// 普通函数中的this	--> window
// 定时器方法中的this --> window
// 对象、方法中的this --> 实例对象
// 构造函数中的this	--> 实例对象
// 原型对象方法中的thi --> 实例对象
```

### isPrototypeOf与instanceof

```javascript
// isPrototypeOf
语法：  prototypeObj.isPrototypeOf(object)
参数：  object  在该对象的原型链上搜寻
返回值：  Boolean，表示调用对象是否在另一个对象的原型链上。
描述：isPrototypeOf 方法允许你检查一个对象是否存在于另一个对象的原型链上

// instanceof
语法: object instanceof constructor
参数: object 要检测的对象. constructor 某个构造函数
描述:instanceof 运算符用来检测 constructor.prototype 是否存在于参数 object 的原型链上。

// 小结
A.isPrototypeOf(B) 判断的是A对象是否存在于B对象的原型链之中
A instanceof B  判断的是B.prototype是否存在与A的原型链之中
```























