关于块元素，内联元素等的基础知识已经讲解完成，同时在两篇也探究了块级元素和内联元素在垂直方向上的定位，下面让我们再深层的挖掘关于定位的问题。



## css定位

首先什么是css定位呢？？我曾看到过很好的一个比喻：如果把新闻报纸未被排版过的新闻内容当作是HTML结构的话，那么定位就意味这把这些内容剪下来，去贴到属于他的位置上，从而更加美观，这很类似于剪报。

![img](https://pic4.zhimg.com/80/v2-8213e1fa20c926e6f345da4f21d86d3f_hd.jpg)





今天就来讲一讲定位的方方面面，定位分为三种，文档流，脱离文档流的两种：浮动和绝对定位。

> 相对定位

position：relative

相对定位是一个很简单的概念，所谓相对，它相对的是谁呢？

答案是他自己，他自己在文档流中本来有一个位置，他只相对于他自己的有一定的偏移。

那么在实际应用中，他是怎么是应用的呢？用什么来表示偏移量呢？



先好好想一下。



我猜你会想到margin 或者是其他的什么东西。首先margin是很不对的，因为之前我们已经解释过，margin可以认为是多个元素的分隔！而我们这一次不是与其他元素进行分隔，而是相对于自己进行偏移。

类似于下面这张图。

![img](https://pic3.zhimg.com/80/v2-31adc82bee9d725e0991710318d45f66_hd.jpg)

我们需要用到新的定位属性了，那就是top，left，right，bottom ，与margin-top，...，margin-bottom不同的是，前者是相对于**某个元素**的偏移，而后者相对于紧邻的元素。

注意这里说的是某个元素，为什么这么说呢？

因为如果我们把top等和相对定位（position:relative）组合在一起的话，那么它就是相对于自己做偏移，之后我们在说和绝对定位（position：relative）组合在一起的情况。



我们不妨这样认为top等和position:relative是一位形影不离的好朋友，甚至可以说是处于热恋期的恋人，两者互相离不开对方，一旦某一方离开了，那么它的作用也随之消失。



![img](https://pic3.zhimg.com/80/v2-838b9fd4b1479c06174cc60a43f37ece_hd.jpg)

还有一点需要注意的就是，position:relative并不脱离文档流，它还霸占着原来的地盘，因此移动它会导致覆盖到其他框。



> 绝对定位

经过前面的铺垫，你现在应该已经知道了绝对定位会脱离文档流。

所谓的脱离文档流，在第一篇文章已经讲过，就像飘在水面上的小船一样，我们该如何对他定位呢？

定位就是需要有一个作为参照物，而绝对定位的参照物就是：**距离他最近的已经定位的元素**

这里所谓的已经定位的元素是指：position不为static的元素。包括（relative，absolute，fixed）

**注：当不设置position属性的时候，默认就是static，如果所有祖先都没有position的话，那就相对于根元素定位。**

```text
<div class="father">
        <div class="son"></div>
</div>


.father {
    background-color:green;
    width:250px;
    height:250px;
}

.son {
    background-color:red;
    width:100px;
    height:100px;
}
```

原始效果图：

![img](https://pic2.zhimg.com/80/v2-d0d057dd2dcb0b7404e7bdf31b755de5_hd.jpg)

**增加子元素增加position:absolute;left:20px;top:20px;**

![img](https://pic4.zhimg.com/80/v2-4ff3c3e2a4591d03cae4dbf39684a0d3_hd.jpg)注意他不是相对于father定位，而是body

**增加父元素position:relative;**

![img](https://pic4.zhimg.com/80/v2-2622aa18de4f72d086b54ec5b2dbe75f_hd.jpg)明显偏移

**修改父元素position:absolute;**

效果不变

**修改父元素为position:fixed;**

同样效果不变。

由此可以证明以上说法。



top，left...遇到absolute后又爱上了它，现在的它更像是脚踏两只船的人。



同时需要注意的是：绝对定位，脱离文档流之后，其他的元素要依次进行顶替他原来的位置。这个估计你已经很清楚了，就不一一阐述。



> 浮动



关于浮动（float）这一话题，我们已经知道他会脱离文档流，但是和绝对定位又有什么不同呢？



最重要的一点是：他只能向左或者向右浮动，换个角度想，对于它上面的内容，是不受影响的，而对于下面的内容，我们进行推测（由于脱离文档流）所以，下面的内容会占据它原本的位置。但是事实却不是这么简单。



我们模拟一下：

```text
<!DOCTYPE html>
<html>

<head>
    <meta charset="UTF-8" />
    <title>测试</title>
    <link rel="stylesheet" type="text/css" href="test.css" />
</head>

<body>
    <div class="father">
        <p>“网络一线牵珍惜这段缘”发展经历
            该词走红之后，常常作为网络吐槽用语被大家使用，
            同时《极限挑战》节目组还制作了一系列的相关的“网络一线牵珍惜这段缘”中老年表情包，
            受到的大家的热烈追捧，被大量的使用和转载开来。
        </p>
        <div class="son"></div>
        <p>
            “网络一线牵珍惜这段缘”相关段子
            请问被网友阴阳怪气时有什么万能回复吗？
            我的朋友教会我使用「祝您阖家幸福」、「
            您是不是觉得自己很幽默啊」、「一听您的谈吐，就知道您是位土
            生土长的中国人，失敬失敬」、「多谢您不吝赐教，不敢当不敢当」，「
            网络一线牵珍惜这段缘」，「谢谢您的关心，也希望您涌有美满的性生活」
            。现在觉得这种温柔的回复实在是太好啦。
        </p>
    </div>
</body>

</html>

.father {
    background-color:#ccc;
    width:500px;
    height:500px;
}

.son {
    float:left;
    background-color:red;
    width:100px;
    height:100px;
    left:20px;
    top:20px;
}
```

上面的代码就是在浮动元素的上方和下方加入了块级元素。

效果展示：

![img](https://pic2.zhimg.com/80/v2-435ab922c37f47786d4b8df01f9971c5_hd.jpg)

如图可以看出，上面的内容丝毫未变，而它下面的内容本该占据它原来的位置，现在却围绕着这个浮动元素进行展示。

**我们再为p元素加上边框显示：**

![img](https://pic2.zhimg.com/80/v2-5538a223139a8ea91449d9af6d3e7699_hd.jpg)

由此可以发现，确实子元素p**确实是占据了浮动元素原来的位置，只是里面的内容被分散开**





**在加入图片之后：**

![img](https://pic2.zhimg.com/80/v2-ed67e0a7f3bd9a596e6ef9b8f954b215_hd.jpg)

可以看出图片元素也是围绕着浮动显示。



**再加入块状元素：**

```text
<body>
    <div class="father">
        <p>“网络一线牵珍惜这段缘”发展经历
            该词走红之后，常常作为网络吐槽用语被大家使用，
            同时《极限挑战》节目组还制作了一系列的相关的“网络一线牵珍惜这段缘”中老年表情包，
            受到的大家的热烈追捧，被大量的使用和转载开来。
        </p>
        <div class="son"></div>
        <div>
            <div class="sonofson"></div>
        </div>
        <img src="test.gif"/>
        <p>
            “网络一线牵珍惜这段缘”相关段子
            请问被网友阴阳怪气时有什么万能回复吗？
            我的朋友教会我使用「祝您阖家幸福」、「
            您是不是觉得自己很幽默啊」、「一听您的谈吐，就知道您是位土
            生土长的中国人，失敬失敬」、「多谢您不吝赐教，不敢当不敢当」，「
            网络一线牵珍惜这段缘」，「谢谢您的关心，也希望您涌有美满的性生活」
            。现在觉得这种温柔的回复实在是太好啦。
        </p>
    </div>
</body>


.father {
    background-color:#ccc;
    width:500px;
    height:500px;
}
p {
    border:1px solid yellow;
}
img {
    width:50px;
    height:50px;
    border:1px solid yellow;
}
.son {
    float:left;
    background-color:red;
    width:100px;
    height:100px;
    left:20px;
    top:20px;
}
.sonofson {
    background-color:blue;
    width:100px;
    height:150px;
}
```

![img](https://pic3.zhimg.com/80/v2-ccad01643b2cd5c697f3e7f27a45dab2_hd.jpg)

由上面的所有，我们可以得出：对于文本（文字+图片）对浮动的处理是围绕在它旁边，可以把它认为是文本围绕图像的一种效果。

但是对于块状等其显示就是直接覆盖。



上面说完了，非浮动对于浮动元素的定位，下面来说一下：浮动元素对于浮动元素的定位。



如果你还记的那条小船的话，应该很好理解，小船虽然不再水中，但是对于其他的小船来说，他还是占着空间的！！！所以不难想到，如果我对很多个元素同时应用float的话，它会显示出如图效果：

![img](https://pic3.zhimg.com/80/v2-2e5aa2f51e25468e19b030695efb5e0a_hd.jpg)



you know，人都是善变的，当你喜欢上了浮动之后，又出现了新的问题：我的文本不想环绕了怎么办？我不想让他们在一行显示怎么办？它擅作主张，这样显的很聪明，但是有的情况下，就不是了。该怎么解决？



答案是：**清除浮动：clear**

clear属性的值可以是：left，right，both，none。

它的作用是：框的那一边不包含浮动元素。

刚开始你可能不理解，什么叫做清除浮动啊，什么是不包含清除浮动啊？

不妨给你打个形象的比方：还是那个漂浮的小船为例，本来小船在水面上漂浮，占据着水面的位置，其他的元素依然可以在小船的下面排布，而清除浮动就是，要把漂浮在水面上的小船压到水里面，让他和其他元素一样，占据着里面的位置。

![img](https://pic4.zhimg.com/80/v2-f9b401131f0ff1d575f07ebbb6639ef3_hd.jpg)搞笑一下，哈哈哈

更进一步的，上面的解释只是我的yy版本，当然不是完全一致的，由于清除浮动是作用在某个元素上的，所以其主体是这个元素，故很容易得出，清除浮动是作用在这个元素上的，它只相对于**左右相邻的元素**有作用。

分别清晰的讲解：

1. clear:left; 元素的左边不包括浮动元素（把它左边的小船压到水底。）
2. clear：right:元素的右边不包括浮动元素（把他右边的小船压到水底）
3. clear：both：该元素的左右两边都不包含浮动元素。（把它左右两边的小船都压到水底）

```text
<body>
    <div>
        <div class="block1"></div>
        <div class="block2"></div>
        <div class="block3"></div>
    </div>
</body>
/*前两个元素设置成浮动，最后一个元素不设置*/

.block1 {
    float:left;
    background-color:#ccc;
    height:50px;
    width:50px;
}
.block2 {
    float:left;
    background-color:blue;
    height:50px;
    width:50px;
}
.block3 {
    background-color:red;
    height:100px;/*block3的高度设置成是其他两个的两倍*/
    width:50px;
}
```

效果图：

![img](https://pic4.zhimg.com/80/v2-23b3b73a4a07680700b2f32ccca13a43_hd.jpg)

当我加入clear:left时，可以看出区别，请看效果图：

![img](https://pic3.zhimg.com/80/v2-c3073be4fd316dcb5d65f6100502c1da_hd.jpg)

clear:right;clear:both同理，在此不再一一阐述。

## 关于浮动所引发的一些副作用及其解决办法

假设我们要写一个双栏设计，左边元素向左浮动，右边元素向右浮动，使之产生一个双栏的效果。

```text
<body>
    <div class="double">
        <div class="primary"></div>
        <div class="secondary"></div>
    </div>
</body>

/*为产生效果，为总框加一个边框,并加入了宽度为300px*/
.double {
    border:1px solid black;
    width:300px;
}
.primary {
    height:500px;
    width:100px;
    float:left;
    background-color:#ccc;
}

.secondary {
    height:500px;
    width:100px;
    float:right;
    background-color:#ccc;
}
```

![img](https://pic1.zhimg.com/80/v2-6f48f1e9894094bd30215aa438dd6acc_hd.jpg)

咦，上面的黑色边框怎么变成了这么点？？为什么不随着内容区的增大，而进行扩大呢？

想一下：



原因是：

它中间的两个元素，均设置了浮动，他已经脱离了文档流，容器框的是水下，水上的小船他当然管不到了。



这是一个副作用，我们该怎么让他变成我们想要的呢？

四种方法（均已测试完毕）：

> \1. 添加元素法

在容器的末尾，添加一个空的新元素，并为它清除浮动！这就会导致它所处的位置会在所有元素的最后面，并且占据住了文档流的位置，作为父级元素就会包括他了。

```text
<body>
    <div class="double">
        <div class="primary"></div>
        <div class="secondary"></div>
        <div class="last"></div>
    </div>
</body>

/*为产生效果，为总框加一个边框,并加入了宽度为300px*/
.double {
    border:1px solid black;
    width:300px;
}
.primary {
    height:500px;
    width:100px;
    float:left;
    background-color:#ccc;
}

.secondary {
    height:500px;
    width:100px;
    float:right;
    background-color:#ccc;
}
.last {
    clear:left;
}
```

效果图：

![img](https://pic1.zhimg.com/80/v2-6412b0467af9038d7928217ce1c3c06c_hd.jpg)

> **2. 浮动容器法**

如果说第一种方法，是通过添加某个元素，让他前面的小船压入水底的话，那么还有一种方法，那就是将这个范围的东西全部浮出水面。这种方法虽然可以做到，但是又很多弊端，我不能为了吃鱼，而把海给填了。

```text
代码和上面的差不太多，自行修改，添加
.double {
    float:left;
}
```



非常不建议使用。



> **3. 另辟蹊径法**

其实，有一个属性可以为我们解决这一个问题。

overflow属性，他主要是针对，指定内容太大而超出容器指定大小，内容会溢出框外的情况。

关于overflow详细的讲述，请查阅资料。

其中，overflow：hidden和overflow：auto的副作用就是，自动清理包含的任何浮动元素。

所以你应该想到了解决办法。

```text
在父元素overflow：设置成hidden或auto

.double {
    overflow:auto;
}
```



建议使用overflow：auto;因为如果内容被修剪，则浏览器会显示滚动条以便查看其余的内容。



> **4. 添加伪类法**

关于：after和 ：before这两个伪类，没有好好说过，现在重点探讨一下吧。



这个after 和 before的理解很重要，请注意：**是在指定的现有内容的末尾或开头加入新的内容。**

这很重要，意思就是说，我加入的这个类（before或者after）不是与本元素同级，而是与它的子元素同级。

所以这种方法，和第一种方法有着异曲同工之妙。

```text
/*在该容器的末尾加入空元素*/
.double:after {
    content:"";/*加入空内容*/
    display:block;/*以块状形式展示*/
    clear:both;
}
```



