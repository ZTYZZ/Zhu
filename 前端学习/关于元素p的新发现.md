## 常识

关于p元素，大家都很熟悉，也经常用它，你们到底有没有发现它有什么不对劲吗？当你在写页面的时候，有没有觉得会有点问题？



p元素属性：块级元素

作用：段落元素，用来添加文本内容。



so easy！ 然而我有话要说！！p元素绝对是最特殊的块级元素！



## 最特殊的块级元素



首先我们看一下它特殊在哪里

```text
<body>
    <div class="father">
        <div class="block1"></div>
        <p>我是最特殊的元素！</p>
    </div>

</body>

CSS:
/*更加清晰，在body加入边框*/
body{
    border:1px solid black;
}
.block1 {
    width:20px;
    height:20px;
    background-color:#ccc;
}

p {
    background-color:#ccc;
}
```

效果图：

![img](https://pic3.zhimg.com/80/v2-aca2d2e59060fe9a6d5667661657e98a_hd.jpg)

首先可以确定的是，上面的20*20的div是没有外边距的，那么如果p元素不带外边距的话，那么两个元素应该是紧挨着的，这就是p元素和其他div元素的不同之处！



p元素作为最特殊的块级元素来说，它自带了一个外边距，所以说如果你想要定位你的p元素，但是文本的位置却总也不对，那么可能是这个自带光环效果的外边距搞的鬼！



## 解决办法

> \1. 统筹大局

在每次css的时候，在第一行就加入

```text
* {
    margin:0px;
    padding:0px;
}
```



这样就可以有效的解决定位容易出现的问题



> \2. 在本身设置

它自带的外边距，当然可以通过自己清除掉，只需要加入margin=0；即可。



![img](https://pic1.zhimg.com/80/v2-61dfc56e1037fe4dda83d5b1360b89ac_hd.jpg)

通过测试！



## 关于一切文本的元素的发现

设想一下以下场景，你想要用相对定位或者绝对定位，来将一行的元素垂直对齐。假设容器的高度是50px，将文字大小设置成10px，按照计算只需要top设置成20px即可。

下面我们来看一下实际的效果！

```text
<body>
    <div class="father">
        
        <p>设置居中</p>
    </div>
</body>

/*设置背景颜色*/
.father {
    background-color:#ccc;
    height:50px;
}

.father p {
    position:relative;
    top:20px;
    font-size:10px;
    border:1px solid black;
}
```

![img](https://pic1.zhimg.com/80/v2-3c5aafc0e9b6dfe229f2baf882914858_hd.jpg)

看起来并没有居中啊！而且边框里面似乎还有空隙啊！这究竟是什么呢？根据之前的基础，[细究内联元素（你一定不知道的东西）](https://zhuanlan.zhihu.com/p/31645001)最里面的是内容区，对于块级元素来说，似乎是一个padding，然而我们将padding设置为0，并没有变化。对于文本只有一个东西能真正的占据空间，那就是行高line-height!!

也就是说文本内容默认有一个行高，而这个行高就使得垂直方向没有完全居中！所以我们的思路是将行间距调成0，也就是line-height=文字大小。



![img](https://pic4.zhimg.com/80/v2-86695a56a7b47212a53e167f943a1b03_hd.jpg)

AMAZING！！这看起来就好了！



你有可能会对margin这个点有这样的疑问：p元素应该自带的margin不起作用了？



我也有这样的疑问，我目前是这样认为的，在相对定位和绝对定位的情况下，top具有更高的优先级吧，毕竟是互相配套的啊，然而margin并不是不存在！在接下来加入元素来看

![img](https://pic2.zhimg.com/80/v2-6b01f574300fb7899d8a17cc322c975d_hd.jpg)

确实存在！

## 总结

看完之后，可以继续观看：[CSS文本的布局]