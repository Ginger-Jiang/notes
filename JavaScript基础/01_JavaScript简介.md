#### JavaScript --> 简称js

> JavaScript历史

​	1995年，网景公司希望能在静态HTML页面上添加一些动态效果, 让Brendan Eich设计出了JavaScript语言(用时2周)

> JavaScript分为三个部分:

- ECMAScript标准----js的基本语法
- DOM---Document Object Model 文档对象模型
- BOM---Browser Object Model    浏览器对象模型

> JavaScript是什么?

- 是一门脚本语言
- 是一门解释性语言
- 是一门弱类型的语言
- 是一门动态类型的语言
- 是一门基于对象的语言

> JavaScript代码写在哪里

```javascript
第一种:写在html文件中-->使用script标签包裹代码
<script>
	alert('这对script标签中的就是js代码)    
</script>
第二种:可以单独写在js文件中-->js文件中不需要使用<script>标签
```

> <script>标签的属性:

- src 表示要引入的外部文件
- type 表示脚本语言的类型  text/javascript,默认值就是它.
- language已废弃。原来用于代码使用的脚本语言。由于大多数浏览器忽略它，所以不要用了。
- defer：可选。(等页面加载完成后,才执行js)表示脚本可以延迟到文档完全被解析和显示之后再执行。由于大多数浏览器不支持，故很少用。
- charset：可选。表示通过 src 属性指定的字符集。由于大多数浏览器忽略它，所以很少有人用它。
- async:可选,能简单实现js的异步加载.

> 注意事项

- <script>标签尽量放在<body>标签内,放在结束的</body>标签前

- 一个<script>标签如果用于引入外部js文件,就不要在标签内写script代码
- html文件中可以同时存在多对<script>标签,浏览器会依次解析执行