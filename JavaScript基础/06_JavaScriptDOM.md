```javascript
知识点
	- DOM概念
	- DOM操作
	- 元素操作
	- 属性操作
	- 节点操作
	- 事件
	- 三大系列
```

###  DOM概念

文档对象模型（Document Object Model，简称DOM），是[W3C](http://baike.baidu.com/item/W3C)组织推荐的处理可扩展标志语言的标准编程接口。

+ 文档：一个 HTML 文件就可以看成是一个文档，也可以看成是一个对象
+ 节点：页面中所有的内容都是节点，标签、属性、文本、注释都是节点。
+ 元素：页面中的每个标签都是一个元素
+ 属性，标签的属性

### DOM操作

+ 获取元素
+ 创建元素
+ 操作元素
+ 处理事件

### 初体验

```javascript
<button id="btn">点击</button>
<script>
  // 根据 id属性的值 从整个文档中获取这个元素 返回一个元素对象并且为这个元素注册点击事件
  document.getElementById('btn').onclick=function(){
    alert('我被点了') // 执行点击事件处理函数
  }
</script>
// 案列功能：按钮被点击，弹出对话框
// 事件：就是做了一件事，事件需要有触发和响应以及事件源
// 按钮：事件源
// 点击：事件名字
// 鼠标点击：触发了
// 弹框：响应了
```

### 获取元素

```javascript
// 根据 id 获取元素
var div = document.getElementById('main');
console.log(div);
// 获取到的数据类型 HTMLDivElement，对象都是有类型的
// HTMLDivElement <-- HTMLElement <-- Element  <-- Node  <-- EventTarget

// 根据标签名获取元素
var divs = document.getElementsByTagName('div')
for (var i=0; i< divs.length; i++){
    var div = divs[i]
    console.log(div)
}

// 根据 name 获取元素
var spans = document.getElementsByName('uname')
for (var i=0; i< spans.length; i++){
    var span = spans[i]
    console.log(span)
}

// 根据类名获取元素
var ps = document.getElementsByClassName('content');
for (var i = 0; i < ps.length; i++) {
  var p = ps[i];
  console.log(p);
}

// 根据选择器获取元素
var text = document.querySelector('#text');
console.log(text);

var boxes = document.querySelectorAll('.box');
for (var i = 0; i < boxes.length; i++) {
  var box = boxes[i];
  console.log(box);
}

// 小结
熟练掌握
	getElementById()
	getElementsByTagName()
大概了解
	getElementsByName()
	getElementsByClassName()
	querySelector()
	querySelectorAll()
```

### 创建元素

```javascript
// document.write()
document.write('这是创建的一个<p>P标签</p>')

// innerHTML
var div = document.getElementById('box')
box.innerHTML = '这也是创建出来的一个<P>P标签</P>'

// document.createElement()
var span = document.createElement('span')
document.body.appendChild(span)

// 性能
- innerHTML方法由于会对字符串进行解析，需要避免在循环内多次使用。
- 可以借助字符串或数组的方式进行替换，再设置给innerHTML
- 优化后与document.createElement性能相近
```

### 属性操作

```javascript
// 获取常见属性：href、title、id、src、className
var link = document.getElementById('link')
var pic = document.getElementById('pic')
console.log(link.href)
console.log(link.title)
console.log(pic.src)

// 获取表单属性
- value 用于大部分表单元素的内容获取(option除外)
- type 可以获取input标签的类型(输入框或复选框等)
- disabled 禁用属性
- checked 复选框选中属性
- selected 下拉菜单选中属性

// 设置与获取自定义属性
- getAttribute() 获取标签行内属性
- setAttribute() 设置标签行内属性
- removeAttribute() 移除标签行内属性
- 与element.属性的区别: 上述三个方法用于获取任意的行内属性。

// 样式操作
var box = document.getElementById('box') // 获取元素
box.style.width = '100px' //设置样式
box.style.height = '100px' //设置样式
box.style.backgroundColor = 'red' //设置样式

// 类名操作
var box = document.getElementById('box');
box.className = 'clearfix';

// innerHTML和innerText方法
var box = document.getElementById('box')
box.innerHTML = '我是文本<p>我会生成为标签</p>'
console.log(box.innerHTML)
box.innerText = '我是文本<p>我不会生成为标签</p>'
console.log(box.innerText)

// HTML 转义符
"		&quot;
‘		&apos;
&		&amp;
<		&lt;    //less than  小于
>		&gt;   // greater than  大于
空格	   &nbsp;
©		&copy;
```

### 节点操作

```javascript
var body = document.body // 获取元素
var div = document.createElement('div') // 创建元素
body.appendChild(div) // 将创建的元素追加到 body 元素中

var firstEle = body.children[0] // 获取 body 元素下的一个元素
body.insertBefore(div,firstEle) // 将创建的元素插入 firstEle 元素之前

body.removeChild(firstEle) // 删除 body 元素下的的一个元素

var text = document.createElement('p') // 创建元素
body.replaceChild(text, div) // 用 p 元素，替换 div 元素
```

### 节点的层级

```javascript
var box = document.getElementById('box')
console.log(box.parentNode) // 查找父级节点
console.log(box.childNodes) // 查找子节点
console.log(box.children) // 查找后代节点
console.log(box.nextSibling) // 查找下一个兄弟节点
console.log(box.previousSibling) // 查找前一个兄弟节点
console.log(box.firstChild) // 查找第一个子节点
console.log(box.lastChild) // 查找最后一个子节点

childNodes和children的区别：
 - childNodes获取的是子节点
 - children获取的是子元素

nextSibling和previousSibling获取的是节点，
extElementSibling和previousElementSibling获取的是元素

nextElementSibling和previousElementSibling有兼容性问题，IE9以后才支持

// 小结
节点操作，方法
	appendChild()
	insertBefore()
	removeChild()
	replaceChild()
节点层次，属性
	parentNode
	childNodes
	children
	nextSibling/previousSibling
	firstChild/lastChild
```

### 事件：触发-响应

 ··· 三要素 ···

- 事件源:触发(被)事件的元素
- 事件类型:事件的触发方式(例如鼠标点击或键盘点击)
- 事件处理程序:事件触发后要执行的代码(函数形式)

##### 注册|移除事件

```javascript
var box = document.getElementById('box')
box.onclick = function () {
  console.log('点击后执行')
};
box.onclick = null

box.addEventListener('click', eventCode, false)
box.removeEventListener('click', eventCode, false)

box.attachEvent('onclick', eventCode)
box.detachEvent('onclick', eventCode)

function eventCode() {
  console.log('点击后执行')
}
```

##### 事件的三个阶段

+ 捕获阶段
+ 当前目标阶段
+ 冒泡阶段

##### 事件对象

```javascript
// 事件对象.eventPhase属性可以查看事件触发时所处的阶段
// 事件对象的属性和方法
- event.type 获取事件类型
- clientX/clientY     所有浏览器都支持，窗口位置
- pageX/pageY       IE8以前不支持，页面位置
- event.target || event.srcElement 用于获取触发事件的元素
- event.preventDefault() 取消默认行为
```

##### 阻止事件冒泡

```javascript
- 标准方式 event.stopPropagation();
- IE低版本 event.cancelBubble = true; 标准中已废弃
```

##### 常用事件

```javascript
- onmouseup 鼠标按键放开时触发
- onmousedown 鼠标按键按下触发
- onmousemove 鼠标移动触发
- onkeyup 键盘按键按下触发
- onkeydown 键盘按键抬起触发
```

### offset系列

```javascript
// offsetParent用于获取定位的父级元素
// offsetParent和parentNode的区别

var box = document.getElementById('box')
console.log(box.offsetParent) // 获取带有定位属性的父级元素
console.log(box.offsetLeft) // 获取元素的左边距
console.log(box.offsetTop) // 获取元素的上边距
console.log(box.offsetWidth) // 获取元素的宽
console.log(box.offsetHeight) // 获取元素的高
```

### client系列

```javascript
var box = document.getElementById('box')
console.log(box.clientLeft) // 元素左边框的厚度
console.log(box.clientTop) // 元素上边框的厚度
console.log(box.clientWidth) // 可见区宽度
console.log(box.clientHeight) // 可见区高度
```

### scroll系列

```javascript
var box = document.getElementById('box');
console.log(box.scrollLeft) // 向左卷曲出去的距离
console.log(box.scrollTop) // 向上卷曲出去距离
console.log(box.scrollWidth) // 页面宽
console.log(box.scrollHeight) // 页面高
```

