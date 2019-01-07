## 1.说明display:none与visibility:hidden的区别

#### display:none不在文档中占位，不会被加载渲染到页面里，就好像这个元素不存在（render树上当然不会有，但是dom树上元素还是存在的，要不然怎么会响应事件呢），元素的子元素当然也不会出现在页面中，并且由于元素根本没有加载到页面中，所以即使子元素设置如display:block;也是无济于事。

#### visibility:hidden在文档中占位，子元素允许覆盖值（设置visibility:visible;元素可见），毕竟visibility:hidden;应用的元素 dom树，render树上都存在，所以这样的结果也是有迹可循。

## 2.flex用法

#### 任何一个容器都可以指定为 Flex 布局`display: flex;`，行内元素也可以使用 Flex 布局`display: inline-flex;`

#### `flex-direction`属性决定主轴的方向（即项目的排列方向）	

- `row`（默认值）：主轴为水平方向，起点在左端。
- `row-reverse`：主轴为水平方向，起点在右端。
- `column`：主轴为垂直方向，起点在上沿。
- `column-reverse`：主轴为垂直方向，起点在下沿。

#### `flex-wrap`属性定义

- `nowrap`（默认）：不换行。
- `wrap`：换行，第一行在上方。
- `wrap-reverse`：换行，第一行在下方

#### `flex-flow`属性是`flex-direction`属性和`flex-wrap`属性的简写形式，默认值为`row nowrap`。

- flex-flow: <flex-direction> || <flex-wrap>;

#### `justify-content`属性定义了项目在主轴上的对齐方式。

- `flex-start`（默认值）：左对齐
- `flex-end`：右对齐
- `center`： 居中
- `space-between`：两端对齐，项目之间的间隔都相等。
- `space-around`：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。

#### `align-items`属性定义项目在交叉轴上如何对齐。

- `flex-start`：交叉轴的起点对齐。
- `flex-end`：交叉轴的终点对齐。
- `center`：交叉轴的中点对齐。
- `baseline`: 项目的第一行文字的基线对齐。
- `stretch`（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。

#### `align-content`属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。

- `flex-start`：与交叉轴的起点对齐。
- `flex-end`：与交叉轴的终点对齐。
- `center`：与交叉轴的中点对齐。
- `space-between`：与交叉轴两端对齐，轴线之间的间隔平均分布。
- `space-around`：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
- `stretch`（默认值）：轴线占满整个交叉轴。

#### `order`属性定义项目的排列顺序。数值越小，排列越靠前，默认为0。

#### `flex-grow`属性定义项目的放大比例，默认为`0`，即如果存在剩余空间，也不放大。

#### `flex-shrink`属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。

#### `flex-basis`属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为`auto`，即项目的本来大小。

#### `flex`属性是`flex-grow`, `flex-shrink` 和 `flex-basis`的简写，默认值为`0 1 auto`。后两个属性可选。

#### `align-self`属性允许单个项目有与其他项目不一样的对齐方式，可覆盖`align-items`属性。默认值为`auto`，表示继承父元素的`align-items`属性，如果没有父元素，则等同于`stretch`。

## 3.用css写下拉动画（下拉盒子样式类名box，高100px,动画类名animate）

```css
.box{
  height:0;
}
.box.animate{
  height:100px;
  transition: all 2s linear;
}
```

## 下拉盒子样式类名box，高不确定,动画类名animate

```css
.box{  
  transform: scaleY(0);  
  transition: all 2s linear;
  transform-origin: center top 0;
}
.box.animate{ 
  transform: scaleY(1);
}
```

## 4.less和sass用法

```less
/*以less为例*/
	/*导入color.less*/
@import "color"
	/*定义变量*/
@mainColor:#f40; 
	/*使用变量*/
.box{
  color:@mainColor; 
} 
	/*Mixin混入*/
.redFont{ 
  color:red;
}
.redBorder{ 
  border: 1px solid red; 
}
.redFontBorder{
  .redFont(); 
  .redBorder(); 
}
	/*定义方法*/
.greenFont-fun(){
  color:green;
}
.greenBorder-fun(){
  border: 1px solid green;
}
	/*使用方法*/
.greenFontBorder-class{
  .greenFont-fun();
  .greenBorder-fun();
}
	/*嵌套*/
a{
  display:block;
  color:red;
  &:hover{
    img{
      display:block;
    }
  }
}
	/*函数与运算*/
@gray:#333*2;				  /*#666*/
@highLight:lighten(#333,20%); /*亮度增加20%*/
```

## 5.实现一个半径50px的圆形图片水平方向居中，垂直方向距离底部100px。（页面没有滚动条，外面盒子占满整个屏幕，屏幕宽度不固定）

#### 利用绝对定位（假设图片类名.img）

```css
.img{
  position:absolute;
  left:50%;
  bottom:100px;
  margin-left:-50px;
}
```

#### 多加一层包裹盒子（假设图片类名.img,图片外新加包裹盒子类名.imgBox）

```css
.imgBox{
  position:absolute;
  left:0;
  bottom:100px;
  width:100%;
}
.img{
  display:block;
  margin:0 auto;
}
```

## 修改条件，图片半径不固定，其他条件要求不变

#### 行内属性（假设图片类名.img,图片外新加包裹盒子类名.imgBox）

```css
.imgBox{
  position:absolute;
  left:0;
  bottom:100px;
  width:100%;
  text-align:center;
}
.img{
  display:inline-block;
}
```

#### flex（假设图片类名.img,图片外新加包裹盒子类名.imgBox）

```css
.imgBox{
  position:absolute;
  left:0;
  bottom:100px;
  width:100%;
  display: flex;
  justify-content: center;
}
```
## 6.css3选择器

#### div的下一个不是p的子元素

```css
div :nth-child(1):not(p)
div :first-child:not(p)
```

#### 选中有data-age="11"属性的元素

```css
[data-age=11]		/*这样是错误的*/
[data-age='11']
[data-age="11"]
```
## 7.清除浮动方法

- #### 父级div定义 height 

- #### 结尾处加空div标签 clear:both 

- ```css
  .clearfloat:after{display:block;clear:both;content:"";visibility:hidden;height:0} 
  .clearfloat{zoom:1} 
  ```

- #### 父级div定义 overflow:hidden （浏览器会自动检查浮动区域的高度 ）

- #### 父级div 也一起浮动

- #### 父级div定义 display:table 

## 8.盒模型

盒模型的组成：由里向外content,padding,border,margin.

盒模型是有两种标准的，一个是标准模型，一个是IE模型。

![img](https://images2017.cnblogs.com/blog/1265396/201711/1265396-20171119143703656-1332857321.png)

![img](https://images2017.cnblogs.com/blog/1265396/201711/1265396-20171119144229156-49945808.png)

 

 从上面两图不难看出在标准模型中，盒模型的宽高只是内容（content）的宽高，

而在IE模型中盒模型的宽高是内容(content)+填充(padding)+边框(border)的总宽高。

- css如何设置两种模型

这里用到了CSS3 的属性 box-sizing

```
/* 标准模型 */
box-sizing:content-box;

 /*IE模型*/
box-sizing:border-box;
```

- JS获取宽高

通过JS获取盒模型对应的宽和高，有以下几种方法：

为了方便书写，以下用dom来表示获取的HTML的节点。

1.  dom.style.width/height 

　　这种方式只能取到dom元素内联样式所设置的宽高，也就是说如果该节点的样式是在style标签中或外联的CSS文件中设置的话，通过这种方法是获取不到dom的宽高的。

2. dom.currentStyle.width/height 

　　这种方式获取的是在页面渲染完成后的结果，就是说不管是哪种方式设置的样式，都能获取到。

　　但这种方式只有IE浏览器支持。

3. window.getComputedStyle(dom).width/height

　　这种方式的原理和2是一样的，这个可以兼容更多的浏览器，通用性好一些。

4. dom.getBoundingClientRect().width/height

　　这种方式是根据元素在视窗中的绝对位置来获取宽高的

5. dom.offsetWidth/offsetHeight

　　这个就没什么好说的了，最常用的，也是兼容最好的。

### 详情请参考:

https://www.cnblogs.com/chengzp/p/cssbox.html

## 9.display

- display:none; 此元素将不被显示
- display: block; 块级元素
- display: inline; 行内元素
- display：inline-block;  行内块
- display:inherit; 从父元素继承 display 属性的值
- display: table; 显示成 table样式
- display: flex; 弹性布局   http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html
- display: grid; 网格布局  https://blog.csdn.net/u012657197/article/details/79083258
- display: list-item; 列表 
- 。。。

 https://baijiahao.baidu.com/s?id=1599614277825293572&wfr=spider&for=pc

## 10.定位

**position 属性规定元素的定位类型**

##### 属性：

- absolute生成绝对定位的元素，相对于 static 定位以外的第一个父元素进行定位。元素的位置通过 "left", "top", "right" 以及 "bottom" 属性进行规定。

- fixed生成绝对定位的元素，相对于浏览器窗口进行定位。元素的位置通过 "left", "top", "right" 以及 "bottom" 属性进行规定。
- relative生成相对定位的元素，相对于其正常位置进行定位。因此，"left:20" 会向元素的 LEFT 位置添加 20 像素。

- static默认值。没有定位，元素出现在正常的流中（忽略 top, bottom, left, right 或者 z-index 声明）。
- inherit规定应该从父元素继承 position 属性的值。

