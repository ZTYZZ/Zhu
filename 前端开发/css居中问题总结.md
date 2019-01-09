## **题外话**

耽搁了半年的学习，发现如今还得重头学，我真是个天才！！

居中问题大概可以分为水平居中和竖直居中，同时又分为行内元素和块级元素。现在我就跟随我一起总结一下。

## **一、利用text-align:center实现水平居中**

你一定想问text-align是啥，来一起探讨一下text-align是个什么东西

关于text-align 在w3school中是这样解释的：

![img](https://pic2.zhimg.com/80/v2-29ed9dd3c9ce7bcaef0525ac326d6659_hd.png)

**意思就是对一个元素内部的文本进行水平对齐**

有如下的选项 （这就相当于word文件的对齐方式一样的 有左对齐、右对齐、居中对齐）

```text
left：居左对齐 
right：右对齐 
center：居中 
start：如果方向是左向右（ltf）的话=left end：同上 
justify：两端对齐，最后一行无效 
justify-all：强制最后一行两端对齐 
match-parent：和inherit类似，区别在于start和end的值根据父元素的direction确定，并被替换为恰当的left或者right。
```



> **单个内联元素**

然而在实际测试中会发现不仅仅对文本元素有效！嘿嘿嘿，我们一起来看一下。

我们就不测试文本元素了，我们先从div块开始，然后用cssz将他display:inline一下，看一下效果

html中的代码如下：（为了便于观看设置边框并把父级元素设置成了 100px高度。）

```text
<div class="father">
			<div class="son">
			</div>
		</div>
```

css代码如下

```text
.father {
	border: 1px solid #000;
	height: 100px;
}

.son {
	/*display: inline;*/
	border: 1px solid #ccc;/*变为内联元素之后，由于是内联元素，高度对其不起作用*/
	height: 50px;
}
```

显示效果如图：

![img](https://pic3.zhimg.com/80/v2-c6824c83bee2535af75c21e8fceb66ea_hd.png)

将css中注释去掉，加上text-align:center可以发现：

![img](https://pic4.zhimg.com/80/v2-af0da974172c130655e377ecd5913c4b_hd.png)

可以发现！居中了，所以我们可以知道**这个text-align不仅仅对文本有效果，对于inline都有居中的效果。**

之后在尝试display:inline-block

```text
.father {
	border: 1px solid #000;
	height: 100px;
	text-align: center;
}

.son {
	display: inline-block;
	border: 1px solid #ccc;
	height: 50px;
}
```

![img](https://pic3.zhimg.com/80/v2-ffa3e157f246926db3c64b2109e188e6_hd.png)

也可以居中！所以**text-align的第二个作用，就是对inline-block也有居中效果！**

> **多个内联元素（一个内联标签+一个图片标签）**

对于我来说，在探究内联标签的时候，我总会考虑到图片的标签，总觉得图片和他们不太一样。

这是html代码

```text
	<div class="father">
		<img src="location.png">
		<span>这是内联元素</span>
	</div>
```

同样在只加边框的效果是这样的。

![img](https://pic4.zhimg.com/80/v2-a3ecd1e2c861b60bbd576ec13674cdc3_hd.png)

图片撑开了father容器，并且文本以图片底端对齐，在之前的文章中探讨过这个问题。

再加入了样式之后

```text
.father {
	border: 1px solid #ccc;
	text-align: center;
}
```

![img](https://pic2.zhimg.com/80/v2-0e71b7d4a690ed4e28e2e410c01b8775_hd.png)

还是一样的。

除了用text-align之外，还可以用flex布局的justify-content。以下是实例；

```text
.father {
	border: 1px solid #ccc;
	display: flex;
	justify-content: center;
}
```

![img](https://pic2.zhimg.com/80/v2-b6ed277e19cadf7d300abc36602a9d45_hd.png)

同样成功了！想了解flex布局的话，推荐看一下这个内容

Flex 布局语法教程 | 菜鸟教程www.runoob.com![图标](https://pic2.zhimg.com/v2-0293a224e0b376ca4aa2cedee41c7c41_ipico.jpg)

【小节】行内元素不管是几个都是可以用text-align进行水平居中的。

## **所以总结一下：**

1. **行内元素水平居中比较简单，只需要在父容器加入text-align:center这行代码**
2. **text-align对于具有inline属性的元素都有水平居中的效果。**
3. **适用于多个元素。**



## 二、利用margin：auto



margin:auto这个属性的意思是，**父元素-子元素/2的外边距**。所以如果给定了父子宽高的话话，会很容易居中。

既然我们对内联元素居中不了，那我们就将他变身，变成易于操控的块！只有一个内联元素，首先将这个元素变为block，然后设置margin:auto（**前提是需要设置 宽度 auto的原理就是确认好元素宽度 用(父元素宽度-元素宽度)/2**）

按照常理来讲，我们将父子元素设置宽高之后，应用margin:auto自适应，就会出现垂直居的效果，可是造化弄人，人生难免几多风雨(┬＿┬)。

```text
	<style>
		.father {
			height: 100px;
			background-color: #ccc;
			
		}
		.son {
			height: 50px;
			width: 50px;
			background-color: blue;
			margin: auto;
		}
	</style>
</head>
<body>
	<div class="father">
		<div class="son">
		</div>
	</div>
</body>
```

![img](https://pic2.zhimg.com/80/v2-65a9575b6967df2d75a9dc774baa1499_hd.png)

可以看出，水平元素居中了，但是垂直方向有点问题，这是为什么呢？

[狠狠的点击这篇文章](https://stackoverflow.com/questions/34552116/why-doesnt-margin-auto-center-an-element-vertically)

这是因为，如果 `margin-top`或者` margin-bottom` 设置为` auto`，他们的值就被设置为0。

// 有时间应该好好研读一下文档。

#### **如何用`margin:auto`实现垂直居中呢？**

#### 1. 可以使用`position:absolute` cffg

在上面的代码中加入

```
	<style>
		.father {
			height: 100px;
			background-color: #ccc;
			position: relative;
			
		}
		.son {
			height: 50px;
			width: 50px;
			background-color: blue;
			margin: auto;
			top: 0;
			bottom: 0;
			left: 0;
			right: 0;
			position: absolute;
					
		}
	</style>
</head>
<body>
	<div class="father">
		<div class="son">
		</div>
	</div>
</body>
```

将定位设置为绝对定位，然后将`top bottom left right `设置为0，同时`margin:auto`，在父元素加上 `position:relative`,可以将元素相对父元素，水平居中对齐。

其中张鑫旭大神的一篇文章提到了这个问题：[狠狠的点击](https://www.zhangxinxu.com/wordpress/2013/11/margin-auto-absolute-%E7%BB%9D%E5%AF%B9%E5%AE%9A%E4%BD%8D-%E6%B0%B4%E5%B9%B3%E5%9E%82%E7%9B%B4%E5%B1%85%E4%B8%AD/)



## **三、使用`vertical-align`垂直居中**



1. **vertical-align和line-height**

关于line-height，张鑫旭写的一篇文章，[css行高line-height的一些深入理解及应用](https://www.zhangxinxu.com/wordpress/2009/11/css%E8%A1%8C%E9%AB%98line-height%E7%9A%84%E4%B8%80%E4%BA%9B%E6%B7%B1%E5%85%A5%E7%90%86%E8%A7%A3%E5%8F%8A%E5%BA%94%E7%94%A8/)，推荐看看。

类似于对块级元素的height，行高是针对于**内联元素**起作用的。

块级元素有一个box盒子模型，而内联元素也有一个inlinebox 模型，这个模型中每一行都是一个line（哈哈哈哈 说的好有趣），所谓line-height 就是这些行的高度啦。具体在上述链接中已经有详细内容。

所以**对于单行文字**，直接使用`line-height`设置为父元素盒子宽度即可。



```text
.father {
	height: 100px;
	border: 1px solid #ccc;
	line-height: 100px;
}
```



效果如图：

![img](https://pic4.zhimg.com/80/v2-029f9d1ef24441a0d6bc24862ceede23_hd.jpg)

但是这个图片好像并没有居中，这是为 什么呢？需要深刻理解line-height和vertical-align属性

[CSS深入理解vertical-align和line-height的基友关系 ](https://www.zhangxinxu.com/wordpress/2015/08/css-deep-understand-vertical-align-and-line-height/)

[彻底搞定vertical-align垂直居中不起作用疑难杂症 - 掘金juejin.im](https://juejin.im/post/5a7d6b886fb9a06349129463)



经过两个文本的学习 ，我们有了大概的了解。因为默认的是 基线baseline 对齐，所以我们需要将两个元素 都改为vertical-align:middle改为中间线对齐（x的中心2/3处）

//以下内容出现了一些疑惑，先记下来，日后来解决

现在我们把图片拿掉，并且在代码中加入 “X”

```text
	<div class="father">
		<span>这是内联元素X</span>
	</div>
```

css代码如下

```text
.father {
	height: 100px;
	border: 1px solid #ccc;
}

.father span{
	vertical-align: middle;
	background-color: red;
}
```

在加入vertical-align:middle 和 不加入 两者对比如下。



![img](https://pic2.zhimg.com/80/v2-4c3bf57f9cc8652ba475620f23a3b925_hd.jpg)

发现 在加入 vertical-align:middle的时候，会下沉一点，而且对比了一下如果默认是基线对齐的话，在未加入vertical-align：middle的时候，应该更下沉才是，然而经过测量，在未加入的时候，是100%对齐的，这让我百思不得其解。



另外需要注意的是，在去掉line-height:100px之后，会发现 元素顶端会和边框有一个空隙，这是因为文本默认会有一个line-height，取决于用户端。桌面浏览器（包括Firefox）使用默认值，约为1.2，这取决于元素的font-family。

//以上是我的疑惑，现在这里停下。



经历了小插曲之后，我们在father的子元素 全部添加了vertical-align:middle之后，成功解决了，当然这只是一个近似居中的效果。

![img](https://pic1.zhimg.com/80/v2-69b6b3c1fbbdaf60dfcd630432ec732c_hd.jpg)



**对于多行文字，**可以使用在文字的后面加一个空白元素。然后利用inlinebox的特点，用line-height将父级元素撑开，然后居中显示。具体代码如下

```
	<style>
		.father {
			height: 200px;
			background-color: #ccc;
			
			
		}
		.son {
			display: inline-block;
			vertical-align: middle;
		}
		.son1 {
			width: 0;
			line-height: 200px;
			font-size: 0;
			display: inline-block;
			vertical-align: middle;
		}
	</style>
</head>
<body>

	<div class="father">
		
		<span class="son">这多行文字，怎么回事啊？小老弟？啊！你看起来很骄傲的样子。我真想狠狠的踢爆你的屁股！哦我的上帝！瞧瞧这该死的居中！垂直方向上的还是多行的</span><span class="son1">&nbsp;</span>
	</div>
</body>
```

![1546428131487](assets\1546428131487.png)

瞧瞧这漂亮的居中！需要注意的是 我们进行的是` vertical-align:middle`按照中线居中的！没有这个是不行的哦。



## **三、利用flexbox**



flex 盒子 ，就是为了解决垂直居中的困难，在flex中有一个属性，为`align-items:center;`可以垂直居中。

设置了之后会形成居中的效果。css代码如下

```text
.father {
	height: 100px;
	border: 1px solid #ccc;
	display: flex;
	align-items: center;
}
```

效果如图



![img](https://pic2.zhimg.com/80/v2-761c679c5b519d723f02e22e7aaac9a1_hd.jpg)



设置`justify-content: space-between;`可以水平居中。更多资料请狠狠的点击这里[Flex布局教程：语法篇](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)

## **四、推算法**

正如名字一样，所谓推算，就是你需要知道一些已知条件，然后在进行推理。放在这里就是，我们必须知道子元素的宽高才能实现。

在进行之前可以看一下这篇文章，看完之后，我忽然感觉之前学的都是假的！！！[position定位](https://segmentfault.com/a/1190000014736711)

#### 推算top法



```
	<style>
/* CSS代码 */

.father {
	width: 300px;
	height: 500px;
	border: 1px solid #cdcdcd;
	position: relative;
}
.box{
    background-color: #cdcdcd;
    position: absolute;
   	top: 224px;/*(父元素高度-子元素高度-边框高度)/2*/
   	left: 124px;/*同上*/
   	width: 50px;
   	height: 50px;
}
	</style>
</head>
<body>
	<div class="father">
		<div class="box"></div>
	</div>

</body>
```

![1546434242642](assets\1546434242642.png)

#### 推算margin法

```
	<style>
/* CSS代码 */

.father {
	width: 300px;
	height: 500px;
	border: 1px solid #cdcdcd;
	position: relative;
}
.box{
    background-color: #cdcdcd;
    position: absolute;
   	top: 50%;
   	left: 50%;
   	width: 50px;
   	height: 50px;
   	margin-top: -26px;/*子元素的一半*/
   	margin-left: -26px;/*同上*/
}
	</style>
</head>
<body>
	<div class="father">
		<div class="box"></div>
	</div>

</body>
```

![1546434478475](assets\1546434478475.png)

## 五、transform

上述方法中，如果不知道元素宽高如何实现呢。

需要用到transform属性，`transform: translate(-50%,-50%);`

```
	<style>
/* CSS代码 */

.father {
	width: 300px;
	height: 500px;
	border: 1px solid #cdcdcd;
	position: relative;
}
.box{
    background-color: #cdcdcd;
    position: absolute;
   	top: 50%;
   	left: 50%;
   	width: 50px;
   	height: 50px;
   	transform: translate(-50%,-50%);
}
}
	</style>
</head>
<body>
	<div class="father">
		<div class="box"></div>
	</div>

</body>
```

