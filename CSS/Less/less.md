<https://blog.csdn.net/qq_36407875/article/details/83411082>

# 如何使用Less？一篇博客就够了



## CSS的缺点

​    CSS是一门典型的`标记型语言`，使用起来非常的简单粗暴，但是CSS并不具有很强的逻辑性，甚至说其实没什么逻辑性，并不像一门正儿八经的编程语言。一旦我们的css文件量大、嵌套深，就会导致我们维护样式变得非常的麻烦，可能修改某个地方的样式，都要去找半天。
​    但是往往就是因为各种疑难杂症的问题才会引领着我们技术的发展。没错，正是因为CSS的 **“落后”** ,为了让我们的样式文件更具有逻辑性，于是涌现了一波非常神奇的语言——`CSS预处理语言`。

## CSS预处理语言

​    CSS预处理语言的诞生，让CSS成为了一门可以使用变量、循环、继承等多种特性的标记型语言。得以让CSS文件变得更具逻辑性，大大的增加了其可阅读性和维护性。
​    目前，在我所了解的范围内，有三款预处理语言：`Less`、`Sass`、`Stylus`，本篇博客介绍的是其中的`Less`。

## Less简单介绍

​    Less 诞生于 2009 年，受Sass的影响创建的一个开源项目。 它扩充了 CSS 语言，增加了诸如`变量`、`混合（mixin）`、`函数`等功能，让 CSS 更易维护、方便制作主题、扩充（**引用于官网**）。

## Less的使用

​    我们需要在页面中引入`less.js`文件，并且在引入JS文件之前，写上link标签，注意`link`标签的`rel`为`stylesheet/less`。

```javascript
<link rel="stylesheet/less" href="style.less">
<script src="../bower_components/less/dist/less.min.js"></script>
12
```

### 变量的使用

​    Less的变量非常的强大，万物皆可化变量。

##### 值变量

```css
/*LESS文件*/
@color: #ccc;
@width: 100px;
@height: 100px;
#test {
    width: @width;
    height: @height;
    background-color: @color;
}
123456789
/*生成后的CSS*/
#test {
    width: 100px;
    height: 100px;
    background-color: #ccc;
}
123456
```

​    定义变量使用`@`，在使用变量的使用同样需要加上`@`，在平时的开发当中，一般我们将这些变量单独的存放到一个less文件当中，便于管理：

```css
@backGroundColor: red;
@baseWidth: 200px;
@baseHeight: 250px;
@borderColor: #ccc;
@ButtonBgColor: #463573;
12345
```

##### 选择器变量

​    选择器变量可以让我们的选择器成为动态的。

```css
/* Less */
@Selector: #box;
@Content: box;
@{Selector}{
  color: #999;
  width: 50%;
}
.@{Content}{
  color:#ccc;
}
#@{Content}{
  color:#666;
}
12345678910111213
/*生成后的CSS*/
#box {
  color: #999;
  width: 50%;
}
.box {
	color:#ccc;
}
#box {
	color:#666;
}
1234567891011
```

​    定义选择器变量有两种方式：
①直接跟上选择器`@Selector: #box`，对应使用方法：`@{Selector}`
②一种是只跟上名字`@Content: box`，对应使用方法：`#@{Content}`、`.@{Content}`

##### 属性变量

​    属性变量可以大大减少我们的代码书写量

```css
/*Less*/
@bgc: background-color;
#box {
	@{bgc}: red;
}
12345
/*CSS*/
#box {
	background-color: red;
}
1234
```

##### URL变量

​    当我们项目目录发生变化的时候，就不需要一个一个去修该路径了。只需要修改路径变量即可：

```css
/*Less*/
@imgUrl: "../imgs";
#box {
	background: url("@{imgUrl}/beautiful.jpg");
}
12345
/*CSS*/
#box {
	background: url("../imgs/beautiful.jpg");
}
1234
```

##### 申明变量

​    有点类似于函数的感觉，将所有样式包在一起使用。

```css
/*Less*/
@boxStyle: {
	width: 100px;
	height: 100px;
	background-color: red;
}
#box {
	@boxStyle();
}
123456789
/*CSS*/
#box {
	width: 100px;
	height: 100px;
	background-color: red;
}
123456
```

##### 变量的运算

​    Less的变量还可以进行计算使用，简单体会下：

```css
/*Less*/
@width: 200px;
@height: 200px;
@color: #333;
#box {
	width: @width + 100;
	height: @height * 2;
	background-color: @color + #111;
}
123456789
/*CSS*/
#box {
	width: 300px;
	height: 400px;
	background-color: #444;
}
123456
```

##### 变量的作用域

总结一句话就是：`就近原则`

```css
/*Less*/
@width: 100%;
@temp: @width;
#box {
	@width: 80%;
	width: @temp;
}
1234567
/*CSS*/
#box {
	width: 80%;
}
1234
```

##### &的使用

`&`在嵌套的样式中，可以表示上一层的选择器

```css
/*Less*/
#header {
  &:after {
 	content: "Hello"; 
  }
  .title {
 	color: red; 
  }
  &_max { //不会嵌套进去
 	width: 200px; 
  }
}
123456789101112
/*CSS*/
#header:after {
  content: "Hello";
}
#header .title {
  color: red;
}
#header_max {
  width: 200px;
}
12345678910
```

### 混合方法的使用

混合方法有点像之前说的变量申明。

##### 无参数方法

```css
/*Less*/
.fun() {
	color: red;
	font-size: 16px;
}
#test {
	.fun();
}
12345678
/*CSS*/
#test {
	color: red;
	font-size: 16px;
}
12345
```

**PS**:方法前缀除了可以写 `.` 还可以写 `#`，调用方法的时候，可以写`()`,也可以不写（推荐定义和调用都加上()来避免混淆）

##### 带参数方法

less中的混合方法可以带参数，同时支持默认参数，参数必须要带单位。和JS类似，`@arguments`指代是所有的参数。

```css
/* Less */
.border(@a:10px,@b:50px,@c:30px,@color:#000){
    border:solid 1px @color;
    box-shadow: @arguments;//指代的是 全部参数
} 
#main{
   .border(0px,5px,30px,red);//必须带着单位 
} 
#wrap{
   .border(0px);
}
#content{
   .border();
}
1234567891011121314
/*CSS*/
#main {
  border: solid 1px red;
  box-shadow: 0px 5px 30px red;
}
#wrap {
  border: solid 1px #000000;
  box-shadow: 0px 50px 30px #000000;
}
#content {
  border: solid 1px #000000;
  box-shadow: 10px 50px 30px #000000;
}
12345678910111213
```

##### 方法的命名空间

方法的命名空间是为了让方法的定义和使用更加的规范。

```css
/*Less*/
.father() {
	background-color: red;
    .son(@w:100px) {
  	   width: @w;
  }
}

#content{
	.father > .son
}
1234567891011
/*CSS*/
#content {
  width: 100px;
}
1234
```

如果存在嵌套的方法定义，想要使用子方法，必须`父方法 > 子方法` 的形式调用，并且父方法不能带`()`

##### 方法的条件筛选

在Less中，没有`if...else`，但是有`when`
**and运算符**： 相当于`&&`，必须全部满足条件才会运行。
**not运算符**： 相当于非运算符`!`，条件不符合才会运行。
**，运算符**： 相当于或运算符`||`，条件符合其中一个就会运行。

```css
/*Less*/
.fontsize(@size) when (@size > 12px) and (@size < 16px){
	font-size: @size;
}
#test {
	.fontsize(13px);
}
1234567
/*CSS*/
#test {
  font-size: 13px;
}
1234
```

### 继承

`extend` 是 Less 的一个伪类。它可以继承指定申明中的所有样式。

```css
/*Less*/
.father {
	color: red;
  	width: 100px;
}
.son {
	&:extend(.father);
}
12345678
/*CSS*/
.father,
.son {
  color: red;
  width: 100px;
}
123456
```

### 导入

导入less文件可以带后缀名`.less`，也可以不带，并且可以在任意位置导入。

```css
/*下面两种方式豆科鱼*/
@import "style"; 
@import "style.less";
123
```

并且位置可以随便放

```css
#box {
	width: 200px;
}
@import "style.less";
1234
```

##### reference

`reference`表示导入less文件，可以使用，但不会去编译它。

```css
@import (reference) "bootstrap.less"; 
1
```

##### once

是less导入的默认行为，表明导入相同的文件只会被导入一次，重复导入，不会去解析。

```css
@import (once) "style.less";
@import (once) "style.less"; //重复导入，会被忽略
12
```

##### multiple

使用`@import (multiple)`允许导入多个同名文件。
假如`style.less`文件内容如下：

```css
#test {
	color: red;
}
123
```

重复引入结果如下:

```css
@import (multiple) "style.less";
@import (multiple) "style.less";
   
/* 生成后的 CSS */
#test {
	color: red;
}
#test {
	color: red;
}
12345678910
```

### 总结

Less常用的一些点基本上就是这些了，Less其实还提供了一些函数供我们使用，比如判断颜色，数字等等。感兴趣可以参考官方文档[Less函数手册](http://lesscss.cn/functions/)


  