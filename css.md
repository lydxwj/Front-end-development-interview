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