## CSS 布局

```html
<div id="box clearFix">
  <div class="one"></div>
  <div class="two"></div>
  <div class="three"></div>
  <div class="four"></div>
</div>
```

```css
.clearFix::befter {
  content: '';
  display: block;
  clear: both;
}
```

### 左右布局

    给父级元素`#box`上加`clearFix`类,然后给所有子元素width:50%;float:left;

```css
#box div {
  float: left;
  width: 50%;
}
```

### 左中右布局

    给父级元素`#box`加`clearFix`类,给子元素float:left;width:33.33%

```css
#box div {
  float: left;
  width: 33.33%;
}
```

### 垂直居中

    让子元素行高与父元素高度一致

```css
#box {
  height: 100px;
}
#box div {
  line-height: 100px;
}
```

### 水平居中

    如果是子元素是行级元素,就给父元素加上 text-align: center;
    如果子元素是块元素,就用display:inline 变成行级元素.然后执行上一步

```css
#box {
  text-align: center;
}
#box div {
  display: inline;
}
```

### 等其他小技巧

    也可以根据设计稿,使用padding配合行高计算实现居中

```css
#box {
  width: 200px;
  height: 100px;
  border: 1px solid red;
  padding: 25px 75px;
}
#box div {
  width: 50px;
  height: 50px;
}
```
