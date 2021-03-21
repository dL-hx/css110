# 常用css 样式

> 拿到一个标签(看标签的个数), 是连接就用 a ,文字(div/p, title ->h  ,) , 先想  宽, 高, 背景颜色,  然后是 display(显示行内, 块 , 行内块 )显示
>
> 最后是 内外边距的考虑

> 使用栅格布局(Col, Row)
>
> 然后考虑   flex   弹性布局

**标签就是盒子的概念**

> 盒子之间可以通过 display 进行转换

​			  行内元素中不要放块级元素

​			 a 特殊,  a 中可以放块级元素

​			 css :层级不宜太多

``` html
<p>
	<div>123</div>
</p>
```



### 居中：

左右居中

```
//文本或图片等内容物居中
 text-align: center;
//块居中
margin:0 auto;
父级
{
  text-align: center;
}
子级
{
  display:inline-block;
}
```

## React写法

>  <Acomponent	 style={{ width: '260px', height: '260px', margin: '0 auto' }} />



https://blog.csdn.net/TaooLee/article/details/73921142



## 元素浮动

### 1. z-index

> z-index属性指定了元素及其子元素的[z顺序]，而[z顺序]可以决定
> 当元素发生覆盖的时候，哪个元素在上面。通常一个较大z-index值的元素会覆盖较低的那一个。

> 只有当元素的position为：relative,absolute,fixed等脱离了文档流的定位时，z-index才会生效。

> 实战意义, 用来解决 **模糊搜索**中 文本框浮动的问题



1. https://www.jianshu.com/p/c2145034f7da

2. https://www.jianshu.com/p/046f1b7e3b00?utm_campaign=maleskine&utm_content=note&utm_medium=seo_notes&utm_source=recommendation

### 2. CSS3伸缩布局盒模型Flex布局

https://www.jianshu.com/p/4d066aa08d46

> 

```
  display: flex;
```

- `justify-content`: 将 flex 元素与主轴对齐

  >  start; center;space-between;space-around;

- `align-items`:竖直上对齐多个元素

  > 元素之间的距离

  

  > stretch;center;start;end;

- `flex-direction`: 定义主轴的方向

  > flex-direction`和`flex-wrap`两个属性经常会一起使用，所以有缩写属性`flex-flow`。这个缩写属性接受两个属性的值，两个值中间以空格隔开。
  >
  > 举个例子，你可以用`flex-flow: row wrap`去设置行并自动换行。

  

  ## 1. `flex-direction`和`align-content`的组合

  

  > row;
  >
  > row-reverse;
  >
  > column;
  >
  > column-reverse;

  ### 2.`flex-direction`和`flex-wrap`的组合。

  flex-direction:column;
  flex-wrap:wrap

  

- `align-content`: 当竖直的轴上有多余的空间时候, 对齐容器内的轴线

  > 决定行与行之间隔多远。这个属性接受这些值

  > ```css
  > flex-start;
  > flex-end;
  > center;
  > space-between;
  > space-around;
  > stretch; 
  > ```
  >
  > 



- **flex-wrap**

  > 是否被强制到" 一行  "或 换到" 多行 "

  nowrap;|wrap;|wrap-reverse;

- `flex-direction`和`flex-wrap`两个属性经常会一起使用，所以有缩写属性`flex-flow`。这个缩写属性接受两个属性的值，两个值中间以空格隔开。

  举个例子，你可以用`flex-flow: row wrap`去设置行并自动换行。

  

- **order**

  > 默认值: 0

  > 决定元素的排列顺序

  > 给每个元素指定 order 值, 决定元素的排列顺序

  容器中的项目按升序值排序

  [CSS](https://developer.mozilla.org/zh-CN/docs/CSS) **order** 属性规定了弹性容器中的可伸缩项目在布局时的顺序。元素按照 `order` 属性的值的增序进行布局。

  拥有相同 `order` 属性值的元素按照它们在源代码中出现的顺序进行布局。

  



### 用`order`和`align-self`的组合

>align-self:flex-end;
>order:1



> - `flex-start`: 多行都集中在顶部。
> - `flex-end`: 多行都集中在底部。
> - `center`: 多行居中。
> - `space-between`: 行与行之间保持相等距离。
> - `space-around`: 每行的周围保持相等距离。
> - `stretch`: 每一行都被拉伸以填满容器。