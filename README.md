# CSSNotes
CSS笔记

## 目录
* [盒模型](#盒模型)
* [定位](#定位)
* [阴影](#阴影)
* [渐变](#渐变)
* * [线性渐变](#线性渐变)
* * [径向渐变](#径向渐变)
* [元素水平垂直居中](#元素水平垂直居中)
* [盒子横向排序不换行](#盒子横向排序不换行)
* [BFC](#bfc)

## 盒模型
包括 margin border padding content

> 标准盒模型 border padding content会改变盒子大小，margin不会，width height只包含content
>
> IE8+浏览器可以通多**`box-sizing`**控制盒模型
>
> * `content-box` 标准盒模型
> * `border-box` 怪异盒模型，border padding 不会改变盒子大小，width height 包含 content + padding + border
> * `inherit`从父元素继承

## 定位
position有4个属性

> * `static` 默认值，left、top、bottom、right不起作用
> * `relative` 相对自己定位，**不脱离文档流**
> * `absolute` 绝对定位，相对最近的带有position属性（值不能为static）的父级定位，**脱离文档流**
> * `fixed` 固定定位，相对于浏览器窗口定位，不会因为出现滚动条变化，**脱离文档流**

## 阴影
box-shadow: h-shadow v-shadow blur spread color inset;

> * `h-shadow	` 必需，水平阴影的位置，允许负值
> * `v-shadow` 必需，垂直阴影的位置，允许负值
> * `blur` 模糊距离
> * `spread` 阴影尺寸
> * `color` 阴影颜色
> * `outset` `inset` 外部阴影、内部阴影

## 渐变
> CSS渐变代替图片，可以加快页面载入时间、减小带宽占用
>
> 渐变由浏览器直接生成的，在页面缩放时的效果比图片更好
>
> 浏览器支持两种类型渐变
>
> > 线性渐变 通过 `linear-gradient` 函数定义
> >
> > 重复线性渐变 `repeating-linear-gradient`函数定义
> >
> > 径向渐变 通过 `radial-gradient` 函数定义
> >
> > 重复径向渐变 `repeating-radial-gradient`函数定义

### 线性渐变
	linear-gradient([ [ <angle> | to <side-or-corner> ] ,]? <color-stop>[, <color-stop>]+)
> `<angle>`	使用角度值或方向指定渐变方向
>
> >  角度是渐变线以顺时针方向旋转的角度
> >
> > **角度为0是从下向上渐变**
>
> `<side-or-corner>` 值为 `[left | right] || [top | bottom]`
> > * to top（0deg）
> > * to right top
> > * to right （90deg）
> > * to right bottom
> > * to bottom（180deg）默认值
> > * to left bottom
> > * to left（270deg）
> > * to left top

#### 简单线性渐变
	background: linear-gradient(to bottom, blue, white);
	background: linear-gradient(to right, blue, white); 
	background: linear-gradient(to bottom right, blue, white);

#### 使用角度

	background: linear-gradient(70deg, black, white);
#### 色标
> 渐变线的颜色停止点在该位置有特定的颜色，该位置可以为线长度的百分比或绝对长度
，可以指定任意多个颜色停止点
	
	//3个色标
	background: linear-gradient(to bottom, blue, white 80%, orange);
	//等间距色标
	background: linear-gradient(to right, red, orange, yellow, green, blue);
	
#### 透明渐变
> 渐变支持透明度
	
	background: linear-gradient(to right, rgba(255,255,255,0), rgba(255,255,255,1)), url(http://foo.com/image.jpg);

### 径向渐变
	radial-gradient(shape size at position, color stop +)

> 渐变形状shape
>
> * `circle` 圆形
> * `ellipse` 椭圆
>
> 渐变尺寸size
>
> * `closest-side` 半径长度为从圆心到离圆心最近的边
> * `closest-corner` 半径长度为从圆心到离圆心最近的角
> * `farthest-side` 半径长度为从圆心到离圆心最远的边
> * `farthest-corner` 半径长度为从圆心到离圆心最远的角
> * 直接写数值
>
>  *  `circle` 正圆支持 `length`， 只能是一个值，表示直径长度
>  *  `ellipse` 支持 `length` 和 `percentage`，需写2个值 
>
> 圆心位置position
>
> * 2个参数，第一个表示横坐标，第二个表示纵坐标
> * 如果只提供一个，第二值默认为50%，即center
> * 数值类型可为`length`,`percentage`,`left`,`right`,`top`,`bottom`
>
> 渐变起止颜色color-stop
>
> * 颜色值 `length` | `percentage`

#### 简单径向渐变
> 渐变范围（渐变结束线）为中心到最远边角距离作为渐变结束线
>
> size 默认值为 `farthest-corner`

	background: radial-gradient(yellow, red);
	background: radial-gradient(circle, yellow, red);
	
#### 指定渐变尺寸

    background: radial-gradient(closest-side circle at 50px 50px, yellow, red);
    // 色标（效果相同）
    background: radial-gradient(closest-side circle, yellow, orange, red, white);
    background: radial-gradient(closest-side circle, yellow, orange 33.33%, red 66.666%, white);
    // 椭圆渐变
    background: radial-gradient(50px 100px ellipse, transparent 40px, yellow 41px, red);
        
## 元素水平垂直居中
> .container 父元素 .content 子元素

### 方法1（外边距margin）
	.container {
		display: flex;
	}
	.content {
		margin: auto;
	}
	
### 方法2（弹性盒）
	.container {
		display: flex;
		align-items: center;
		justify-content: center;
	}
	
### 方法3	（定位position+平移translate）
	.container {
		position: relative;
	}
	.content {
		position: absolute;
		left: 50%;
		top: 50%;
		transform: translate(-50%, -50%);
	}
### 方法4	（定位position + 外边距margin）

	.container {
		position: relative;
	}
	.content {
		position:absolute;
		margin:auto;
		top:0;
		bottom:0;
		left:0;
		right:0;
	}
	
### 方法5 （table-cell）
	
	.container {
		displat: table-cell;
		text-align: center;
		verticle-align: middle;
	}
	.content {
		display: inline-block;
	}
  
##	盒子横向排序不换行
### 并排宽度小于外层宽度
	// 1
	.content {
		float: left
	}
	// 2
	.container {
		display: flex;
	}
	
### 并排宽度大于外层宽度
	.container {
		overflow: auto;
		white-space: nowrap;
	}
	.content {
		display: inline-block;
	}
	
## BFC
#### 常见定位方案
> 普通流
> > 元素按照其在 HTML 中的先后位置至上而下布局
> > 
> > 行内元素水平排列，直到当行被占满然后换行
> > 
> > 块级元素独占一行
> > 
> > 除非另外指定，否则所有元素默认都是普通流定位
> 
> 浮动
> > 元素首先按照普通流的位置出现，然后根据浮动的方向尽可能的向左边或右边偏移，效果与文本环绕相似
>
> 绝对定位
> > 元素会整体脱离普通流，因此绝对定位元素不会对其兄弟元素造成影响，而元素具体的位置由绝对定位的坐标决定

#### BFC定义
> BFC（Block formatting context）直译为”块级格式化上下文”
>
> 它是页面中的一块渲染区域，决定了其子元素将如何定位，以及和其他元素的关系和相互作用

#### BFC形成
> body根元素
> 
> 浮动元素：float值为`left` `right`
> 
> 定位元素：position值为`absolute` `fixed`	
> 
> display值为`table-cell` `table-caption` `inline-block` `flex` `inline-flex`
> 
> overflow除了visible以外的值`hidden` `auto` `scroll`

#### BFC布局规则
> 内部的Box会在垂直方向，按顺序排列
> 
> Box垂直方向的距离由margin决定。属于同一个BFC的两个相邻Box的margin会发生重叠
> 
> BFC的box都默认左对齐，并且它们的左边距可以触及到容器container的左边，浮动元素依然遵循这个原则
> 
> BFC的区域不会与float box重叠
> 
> BFC是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素
> 
> 计算BFC的高度时，浮动元素也参与计算


#### BFC作用
> 解决垂直margin重叠（同一个BFC下外边距会发生折叠，创建一个新的BFC即可）
> 
> 可以包含浮动元素，清除浮动（子元素设置float，父元素无高度，给父元素写overflow:hidden，高度塌陷）
> 
> 阻止元素被浮动元素覆盖（不让文本环绕）
> 
> 实现两列自适应布局
		
