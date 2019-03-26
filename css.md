## 1.说明display:none与visibility:hidden的区别

- display:none不在文档中占位，不会被加载渲染到页面里，就好像这个元素不存在（render树上当然不会有，但是dom树上元素还是存在的，要不然怎么会响应事件呢），元素的子元素当然也不会出现在页面中，并且由于元素根本没有加载到页面中，所以即使子元素设置如display:block;也是无济于事。

- visibility:hidden在文档中占位，子元素允许覆盖值（设置visibility:visible;元素可见），毕竟visibility:hidden;应用的元素 dom树，render树上都存在，所以这样的结果也是有迹可循。

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

## 11.介绍css3

- 选择器

```scss
[href$=‘.pdf’] //表示 href属性中以.pdf结尾的被选中
[href^=‘mailto’] //表示href属性中以mailto开头的被选中
[href*=‘item’] //表示href属性中含有item的都被选中
[title~=flower] //	选择 title 属性包含单词 "flower" 的所有元素。	
[lang|=en] //选择 lang 属性值以 "en" 开头的所有元素。
p~ul  //选择前面有 <p> 元素的每个 <ul> 元素。
div>p //选择父元素为 <div> 元素的所有 <p> 元素
div+p	//选择紧接在 <div> 元素之后的所有 <p> 元素。
:nth-of-type(odd)
:nth-of-type(even)
:nth-child
:checked :enabled  :target ::selection  :not :empty  :root :before :after
```

- 背景

```
background-clip  background-origin
background-size: contain 缩小图片以适合元素（维持像素长宽比）
	cover 扩展元素以填补元素（维持像素长宽比）
background-image:url(img_flwr.gif),url(img_tree.gif); // 多背景
```

- 边框

```
border-image	边框图像
border-radius	圆角
box-shadow	附加一个或多个盒子的阴影
```

- 渐变

```
// 线性渐变（Linear Gradients）- 向下/向上/向左/向右/对角方向
background: linear-gradient(direction, color-stop1, color-stop2,...);
// 径向渐变（Radial Gradients）- 由它们的中心定义
background: radial-gradient(center, shape size, start-color,...,last-color);
```

- 文本效果

| 属性                                                         | 描述                                                    |
| ------------------------------------------------------------ | ------------------------------------------------------- |
| [hanging-punctuation](http://www.runoob.com/cssref/css3-pr-hanging-punctuation.html) | 规定标点字符是否位于线框之外。                          |
| [punctuation-trim](http://www.runoob.com/cssref/css3-pr-punctuation-trim.html) | 规定是否对标点字符进行修剪。                            |
| text-align-last                                              | 设置如何对齐最后一行或紧挨着强制换行符之前的行。        |
| text-emphasis                                                | 向元素的文本应用重点标记以及重点标记的前景色。          |
| [text-justify](http://www.runoob.com/cssref/css3-pr-text-justify.html) | 规定当 text-align 设置为 "justify" 时所使用的对齐方法。 |
| [text-outline](http://www.runoob.com/cssref/css3-pr-text-outline.html) | 规定文本的轮廓。                                        |
| [text-overflow](http://www.runoob.com/cssref/css3-pr-text-overflow.html) | 规定当文本溢出包含元素时发生的事情。                    |
| [text-shadow](http://www.runoob.com/cssref/css3-pr-text-shadow.html) | 向文本添加阴影。                                        |
| [text-wrap](http://www.runoob.com/cssref/css3-pr-text-wrap.html) | 规定文本的换行规则。                                    |
| [word-break](http://www.runoob.com/cssref/css3-pr-word-break.html) | 规定非中日韩文本的换行规则。                            |
| [word-wrap](http://www.runoob.com/cssref/css3-pr-word-wrap.html) | 允许对长的不可分割的单词进行分割并换行到下一行。        |

- 字体

```
@font-face{
	font-family: myFirstFont;
	src: url(sansation_light.woff);
}
div{
	font-family:myFirstFont;
}
```

-  转换和变形

```
transform	适用于2D或3D转换的元素
transform-origin	允许您更改转化元素位置
```

| 函数                            | 描述                                     |
| ------------------------------- | ---------------------------------------- |
| matrix(*n*,*n*,*n*,*n*,*n*,*n*) | 定义 2D 转换，使用六个值的矩阵。         |
| translate(*x*,*y*)              | 定义 2D 转换，沿着 X 和 Y 轴移动元素。   |
| translateX(*n*)                 | 定义 2D 转换，沿着 X 轴移动元素。        |
| translateY(*n*)                 | 定义 2D 转换，沿着 Y 轴移动元素。        |
| scale(*x*,*y*)                  | 定义 2D 缩放转换，改变元素的宽度和高度。 |
| scaleX(*n*)                     | 定义 2D 缩放转换，改变元素的宽度。       |
| scaleY(*n*)                     | 定义 2D 缩放转换，改变元素的高度。       |
| rotate(*angle*)                 | 定义 2D 旋转，在参数中规定角度。         |
| skew(*x-angle*,*y-angle*)       | 定义 2D 倾斜转换，沿着 X 和 Y 轴。       |
| skewX(*angle*)                  | 定义 2D 倾斜转换，沿着 X 轴。            |
| skewY(*angle*)                  | 定义 2D 倾斜转换，沿着 Y 轴。            |

3D转换属性

下表列出了所有的转换属性：

| 属性                                                         | 描述                                 | CSS  |
| ------------------------------------------------------------ | ------------------------------------ | ---- |
| [transform](http://www.runoob.com/cssref/css3-pr-transform.html) | 向元素应用 2D 或 3D 转换。           | 3    |
| [transform-origin](http://www.runoob.com/cssref/css3-pr-transform-origin.html) | 允许你改变被转换元素的位置。         | 3    |
| [transform-style](http://www.runoob.com/cssref/css3-pr-transform-style.html) | 规定被嵌套元素如何在 3D 空间中显示。 | 3    |
| [perspective](http://www.runoob.com/cssref/css3-pr-perspective.html) | 规定 3D 元素的透视效果。             | 3    |
| [perspective-origin](http://www.runoob.com/cssref/css3-pr-perspective-origin.html) | 规定 3D 元素的底部位置。             | 3    |
| [backface-visibility](http://www.runoob.com/cssref/css3-pr-backface-visibility.html) | 定义元素在不面对屏幕时是否可见。     | 3    |

3D 转换方法

| 函数                                                         | 描述                                      |
| ------------------------------------------------------------ | ----------------------------------------- |
| matrix3d(*n*,*n*,*n*,*n*,*n*,*n*, *n*,*n*,*n*,*n*,*n*,*n*,*n*,*n*,*n*,*n*) | 定义 3D 转换，使用 16 个值的 4x4 矩阵。   |
| translate3d(*x*,*y*,*z*)                                     | 定义 3D 转化。                            |
| translateX(*x*)                                              | 定义 3D 转化，仅使用用于 X 轴的值。       |
| translateY(*y*)                                              | 定义 3D 转化，仅使用用于 Y 轴的值。       |
| translateZ(*z*)                                              | 定义 3D 转化，仅使用用于 Z 轴的值。       |
| scale3d(*x*,*y*,*z*)                                         | 定义 3D 缩放转换。                        |
| scaleX(*x*)                                                  | 定义 3D 缩放转换，通过给定一个 X 轴的值。 |
| scaleY(*y*)                                                  | 定义 3D 缩放转换，通过给定一个 Y 轴的值。 |
| scaleZ(*z*)                                                  | 定义 3D 缩放转换，通过给定一个 Z 轴的值。 |
| rotate3d(*x*,*y*,*z*,*angle*)                                | 定义 3D 旋转。                            |
| rotateX(*angle*)                                             | 定义沿 X 轴的 3D 旋转。                   |
| rotateY(*angle*)                                             | 定义沿 Y 轴的 3D 旋转。                   |
| rotateZ(*angle*)                                             | 定义沿 Z 轴的 3D 旋转。                   |
| perspective(*n*)                                             | 定义 3D 转换元素的透视视图。              |

- 过渡

| 属性                                                         | 描述                                         |
| ------------------------------------------------------------ | -------------------------------------------- |
| [transition](http://www.runoob.com/cssref/css3-pr-transition.html) | 简写属性，用于在一个属性中设置四个过渡属性。 |
| [transition-property](http://www.runoob.com/cssref/css3-pr-transition-property.html) | 规定应用过渡的 CSS 属性的名称。              |
| [transition-duration](http://www.runoob.com/cssref/css3-pr-transition-duration.html) | 定义过渡效果花费的时间。默认是 0。           |
| [transition-timing-function](http://www.runoob.com/cssref/css3-pr-transition-timing-function.html) | 规定过渡效果的时间曲线。默认是 "ease"。      |
| [transition-delay](http://www.runoob.com/cssref/css3-pr-transition-delay.html) | 规定过渡效果何时开始。默认是 0。             |

- 动画

| 属性                                                         | 描述                                                     |
| ------------------------------------------------------------ | -------------------------------------------------------- |
| [@keyframes](http://www.runoob.com/cssref/css3-pr-animation-keyframes.html) | 规定动画。                                               |
| [animation](http://www.runoob.com/cssref/css3-pr-animation.html) | 所有动画属性的简写属性，除了 animation-play-state 属性。 |
| [animation-name](http://www.runoob.com/cssref/css3-pr-animation-name.html) | 规定 @keyframes 动画的名称。                             |
| [animation-duration](http://www.runoob.com/cssref/css3-pr-animation-duration.html) | 规定动画完成一个周期所花费的秒或毫秒。默认是 0。         |
| [animation-timing-function](http://www.runoob.com/cssref/css3-pr-animation-timing-function.html) | 规定动画的速度曲线。默认是 "ease"。                      |
| [animation-delay](http://www.runoob.com/cssref/css3-pr-animation-delay.html) | 规定动画何时开始。默认是 0。                             |
| [animation-iteration-count](http://www.runoob.com/cssref/css3-pr-animation-iteration-count.html) | 规定动画被播放的次数。默认是 1。                         |
| [animation-direction](http://www.runoob.com/cssref/css3-pr-animation-direction.html) | 规定动画是否在下一周期逆向地播放。默认是 "normal"。      |
| [animation-play-state](http://www.runoob.com/cssref/css3-pr-animation-play-state.html) | 规定动画是否正在运行或暂停。默认是 "running"。           |

- 多列

| 属性                                                         | 描述                                     |
| ------------------------------------------------------------ | ---------------------------------------- |
| [column-count](http://www.runoob.com/cssref/css3-pr-column-count.html) | 指定元素应该被分割的列数。               |
| [column-fill](http://www.runoob.com/cssref/css3-pr-column-fill.html) | 指定如何填充列                           |
| [column-gap](http://www.runoob.com/cssref/css3-pr-column-gap.html) | 指定列与列之间的间隙                     |
| [column-rule](http://www.runoob.com/cssref/css3-pr-column-rule.html) | 所有 column-rule-* 属性的简写            |
| [column-rule-color](http://www.runoob.com/cssref/css3-pr-column-rule-color.html) | 指定两列间边框的颜色                     |
| [column-rule-style](http://www.runoob.com/cssref/css3-pr-column-rule-style.html) | 指定两列间边框的样式                     |
| [column-rule-width](http://www.runoob.com/cssref/css3-pr-column-rule-width.html) | 指定两列间边框的厚度                     |
| [column-span](http://www.runoob.com/cssref/css3-pr-column-span.html) | 指定元素要跨越多少列                     |
| [column-width](http://www.runoob.com/cssref/css3-pr-column-width.html) | 指定列的宽度                             |
| [columns](http://www.runoob.com/cssref/css3-pr-columns.html) | 设置 column-width 和 column-count 的简写 |

-  盒模型

```
resize：none | both | horizontal | vertical | inherit
box-sizing: content-box | border-box | inherit
outline:outline-color outline-style outline-width outine-offset
```

resize属性指定一个元素是否应该由用户去调整大小。

box-sizing 属性允许您以确切的方式定义适应某个区域的具体内容。

outline-offset 属性对轮廓进行偏移，并在超出边框边缘的位置绘制轮廓。

- 伸缩布局盒模型(弹性盒)

| 属性                                                         | 描述                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [display](http://www.runoob.com/cssref/pr-class-display.html) | 指定 HTML 元素盒子类型。flex                                 |
| [flex-direction](http://www.runoob.com/cssref/css3-pr-flex-direction.html) | 指定了弹性容器中子元素的排列方式                             |
| [justify-content](http://www.runoob.com/cssref/css3-pr-justify-content.html) | 设置弹性盒子元素在主轴（横轴）方向上的对齐方式。             |
| [align-items](http://www.runoob.com/cssref/css3-pr-align-items.html) | 设置弹性盒子元素在侧轴（纵轴）方向上的对齐方式。             |
| [flex-wrap](http://www.runoob.com/cssref/css3-pr-flex-wrap.html) | 设置弹性盒子的子元素超出父容器时是否换行。                   |
| [align-content](http://www.runoob.com/cssref/css3-pr-align-content.html) | 修改 flex-wrap 属性的行为，类似 align-items, 但不是设置子元素对齐，而是设置行对齐 |
| [flex-flow](http://www.runoob.com/cssref/css3-pr-flex-flow.html) | flex-direction 和 flex-wrap 的简写                           |
| [order](http://www.runoob.com/cssref/css3-pr-order.html)     | 设置弹性盒子的子元素排列顺序。                               |
| [align-self](http://www.runoob.com/cssref/css3-pr-align-self.html) | 在弹性子元素上使用。覆盖容器的 align-items 属性。            |
| [flex](http://www.runoob.com/cssref/css3-pr-flex.html)       | 设置弹性盒子的子元素如何分配空间。                           |

- 媒体查询

```
// css2媒体查询
<link rel="stylesheet" type="text/css" href="layout.css" media="screen and (max-width: 960px)" />
<style type="text/css" media="screen and (max-width: 960px)"></style>

@media(min-width:800px)and(max-width:1200px)and(orientation:portrait){...}
```

- 反射（倒影）

```
-webkit-box-reflect:方向[ above-上 | below-下 | right-右 | left-左 ]，偏移量，遮罩图片
```

### 详情请参考:

https://blog.csdn.net/chandoudeyuyi/article/details/69206236

https://segmentfault.com/a/1190000010780991#articleHeader25

## 12. sass、 less的scope

- Sass的变量

  Sass声明变量必须是`$`开头，后面紧跟变量名和变量值，而且变量名和变量值需要使用冒号（`：`）分隔开。就像CSS属性设置一样

- LESS的变量

  LESS样式中声明变量和调用变量和Sass一样，唯一的区别就是变量名前面使用的是`@`字符

- 作用域（Scope）

  CSS预处理器语言中的变量和其他程序语言一样，可以实现值的复用，同样它也存在生命周期，也就是Scope（变量范围，开发人员习惯称之为作用域），简单点讲就是局部变量还是全局变量的概念，查找变量的顺序是先在局部定义中找，如果找不到，则查找上级定义，直至全局。下面我们通过一个简单的例子来解释这三款CSS预处理器的作用域使用。

  - Sass的作用域

    Sass中作用域在这三款预处理器是最差的，可以说在Sass中是不存在什么全局变量。

  - #### LESS的作用域

    LESS中的作用域和其他程序语言中的作用域非常的相同，他首先会查找局部定义的变量，如果没有找到，会像冒泡一样，一级一级往下查找，直到根为止。

### 详情请参考:

https://www.cnblogs.com/hedgerow/p/4128055.html

## 13.对于BFC的理解

- 浮动元素和绝对定位元素，非块级盒子的块级容器（例如 inline-blocks, table-cells, 和 table-captions），以及overflow值不为“visiable”的块级盒子，都会为他们的内容创建新的BFC（块级格式上下文）。

- 一个HTML元素要创建BFC，则满足下列的任意一个或多个条件即可：

  1、float的值不是none。
  2、position的值不是static或者relative。
  3、display的值是inline-block、table-cell、flex、table-caption或者inline-flex
  4、overflow的值不是visible

  BFC是一个独立的布局环境，其中的元素布局是不受外界的影响，并且在一个BFC中，块盒与行盒（行盒由一行中所有的内联元素所组成）都会垂直的沿着其父元素的边框排列。

- 利用BFC避免外边距折叠
- BFC包含浮动

### 详情请参考:

https://www.cnblogs.com/libin-1/p/7098468.html

https://www.cnblogs.com/dojo-lzz/p/3999013.html

## 14.实现垂直水平居中

```
1.
{
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%,-50%);
}
2.
{
    display: flex;
    justify-content: center;
    align-items: center;
}
3.
.box {
    display: table;
}
.content {
    display: table-cell;
    vertical-align: middle;
    text-align: center;
}
4.
{
    margin-top: 50%;
    margin-left: auto;
    margin-right: auto;
    transform: translate(0%,-50%);
}
```

## 15.css的基本语句构成

- 选择器：{属性：属性值;}

## 16.css引入的方式，link和@import的区别

- 行内式

  ```
  <span style="color:red;">行内式</span>
  ```

- 嵌入式

  ```
  <style></style>
  ```

- 链接式

  ```
  <link href="test.css" type="text/css" rel="stylesheet" />
  ```

- 导入式

  ````
  @import(url(demo.css))
  ````

- 区别

  - 从属关系区别
    `@import`是 CSS 提供的语法规则，只有导入样式表的作用；`link`是HTML提供的标签，不仅可以加载 CSS 文件，还可以定义 RSS、rel 连接属性等。

  - 加载顺序区别
    加载页面时，`link`标签引入的 CSS 被同时加载；`@import`引入的 CSS 将在页面加载完毕后被加载。

  - 兼容性区别
    `@import`是 CSS2.1 才有的语法，故只可在 IE5+ 才能识别；`link`标签作为 HTML 元素，不存在兼容性问题。
  - DOM可控性区别
    可以通过 JS 操作 DOM ，插入`link`标签来改变样式；由于 DOM 方法是基于文档的，无法使用`@import`的方式插入样式。

#### 详情参考：

https://www.cnblogs.com/my--sunshine/p/6872224.html

## 17.写出div（包含文字的）最后的font-size和color

```
<style>
div{
  width: 1rem;
  color: blue;
}
.class1{
  font-size: .32rem;
  color: red;
}
#id1{
  color: #333;
}
#id1 div{
  color: #666;
}
.class1 div{
  color: #999;
}
.class1 .class2 div{
  color: #aaa;
}
</style>
html
<div class="class1">
  <div id="id1" class="class2">
    <div>文字</div>
  </div>
</div>
```

font-size: .32rem; color: #666;

## 18.css权重优先级计算

```
！important>行间样式>id选择器>class选择器 属性选择器>标签选择器>通配符

第一等级：代表 内联样式，如 style=""，权值为 1,0,0,0；
第二等级：代表 ID选择器，如 #id="", 权值为 0,1,0,0；
第三等级：代表 calss | 伪类 | 属性 选择器，如 .class | :hover,:link,:target | [type], 权值 0,0,1,0；
第四等级：代表 标签 | 伪元素 选择器，如 p | ::after, ::before, ::fist-inline, ::selection, 权值 0,0,0,1；
此外，通用选择器（*），子选择器（>）， 相邻同胞选择器（+）等选择器不在4等级之内，所以它们的权值都为 0,0,0,0；
```

#### 详情参考：

https://www.cnblogs.com/cnblogs-jcy/p/8574177.html

https://blog.csdn.net/gaoshanyangzhi_1999/article/details/80726580

## 19.如何居中浮动元素

```
// html
<div class="outerbox">  
     <div class="innerbox">我是浮动的</div>  
</div>
// css
.outerbox{  
	float:left;   
	position:relative;   
	left:50%;   
}   
.innerbox{    
	float:left;   
	position:relative;   
	right:50%;   
}
// 第二种
.outerbox{
    display: flex;
    justify-content: center;
}
```

#### 详情参考：

https://mp.weixin.qq.com/s/UxY7VWqMMOjvgE6L_dlixA

## 20.浏览器兼容问题

- 不同浏览器的标签默认的margin和padding不

  解决方案： css 里增加通配符 * { margin: 0; padding: 0; }或者其他样式初始化

- IE6双边距问题；在 IE6中设置了float , 同时又设置margin , 就会出现边距问题
  解决方案：设置display:inline;

- 当标签的高度设置小于10px，在IE6、IE7中会超出自己设置的高度
  解决方案：超出高度的标签设置overflow:hidden,或者设置line-height的值小于你的设置高度

- 图片默认有间距
  解决方案：使用float 为img 布局

- IE9一下浏览器不能使用opacity
  解决方案：
  opacity: 0.5;filter: alpha(opacity = 50);filter: progid:DXImageTransform.Microsoft.Alpha(style = 0, opacity = 50);

- 边距重叠问题；当相邻两个元素都设置了margin 边距时，margin 将取最大值，舍弃最小值；
  解决方案：为了不让边重叠，可以给子元素增加一个父级元素，并设置父级元素为overflow:hidden；

- cursor:hand 显示手型在safari 上不支持
  解决方案：统一使用 cursor:pointer

- 两个块级元素，父元素设置了overflow:auto；子元素设置了position:relative ;且高度大于父元素，在IE6、IE7会被隐藏而不是溢出；

  解决方案：父级元素设置position:relative

#### 详情参考：

https://blog.csdn.net/wanmeiyinyue315/article/details/79654984

## 21.常用hack技巧

- ```
  /*类内部hack：*/ 
  .header {_width:100px;}            /* IE6专用*/
  .header {*+width:100px;}        /* IE7专用*/ 
  .header {*width:100px;}            /* IE6、IE7共用*/ 
  .header {width:100px\0;}        /* IE8、IE9共用*/ 
  .header {width:100px\9;}        /* IE6、IE7、IE8、IE9共用*/ 
  .header {width:330px\9\0;}    /* IE9专用*/  /*选择器Hack：*/
  *html .header{}        /*IE6*/ 
  *+html .header{}    /*IE7*/ 
  ```

- ```
  ie内核浏览器识别
  <!--[if IE]><![endif]-->
  ie6内核浏览器识别
  <!--[if IE 6]><![endif]-->
  ie7及其以上内核浏览器识别
  <!--[if gte IE 7]><![endif]-->
  ie7及其以下内核浏览器识别
  <!--[if lte IE 7]><![endif]-->
  非ie内核浏览器识别
  <!--[if !IE]><![endif]-->
  非ie7及其以下内核浏览器识别
  <!--[if !(lte IE 7)]><!-->
  ```

#### 详情参考：

https://blog.csdn.net/u598975767/article/details/51242773

## 22.对css动画做优化



## 选择题

- 以下关于css3 box-sizing的描述正确的是（ACDE）

  A.content-box, border和padding不计算入width之内

  B.content-box, border计算入width之内

  C.padding-box, padding计算入width之内

  D.border-box, border计算入width之内

  E.border-box, border和padding计算入width之内

- div的最终颜色（D）

  ```
  <div id="divId" class="div_class"></div>
  <style>
  div{background: #f00;height:10px;}
  .div_class{background:#0f0;}
  .class{background:#000!important;}
  #divId{background:#00f;}
  div.div_class{background:#aaa;}
  </style>
  ```

  A.#f00

  B.#0f0

  C.#000

  D.#00f

  E.#aaa

- 