## 它是干什么的

我们知道display:inline 和display:block的用发了，他们的作用是将块级元素转化为内联元素或者是内联元素转化为块级元素。

现在的这个貌似是两个的结合体：inline-block

从英文中可以初步理解到：-代表的前缀，意思应该是block 具备 inline的性质，也可以说，让块级元素在一行显示的性质。



## 1.作用在block上面的display:inline-block



你可能会问：让block具备inline的性质，直接用display:inline不就可以了？

如果你有这个疑问，那就一起探究一下：

```text
<body>
    <div class="father">
        <div class="block"></div>
        <div class="block"></div>
        <div class="block"></div>
        <div class="block"></div>
        <div class="block"></div>
    </div>

</body>

css:

.block {
    width:50px;
    height:50px;
    background-color:#ccc;
    margin:10px;
}
```



![img](https://pic2.zhimg.com/80/v2-43fc931c90439f57d9224fde570b56c9_hd.jpg)效果图

接下来就是加入display:inline;你会发现神奇的东西：

![img](https://pic1.zhimg.com/80/v2-8bbc5e58b676b37d12cd10c958a5fc94_hd.jpg)

wow！理解了吗？像我们讲过的一样，转化为inline之后，除了图像之外 ，就不能设置宽高了！

这就是display:inline-block 的意义所在了



这个时候，我们加入display:inline-block;神奇的事情发生了！

![img](https://pic2.zhimg.com/80/v2-2ac382a238ab697c67da0501085f6f61_hd.jpg)

我们明白了：**inline-block是元素具备了两种（块级和内联）元素的功能，inline最重要的一点就是：元素能够在一行展示，而inline元素所缺失的设置宽高，也是block 元素的功能，从而两个联手，展现出了如图的效果。**



如果说设置inline-block的元素具备了两个功能， 那么被作用这个元素不只局限在块级元素上面。下面就看一下内联元素的展示：

## 2.作用在inline的display:inline-block

代码：

```text
<body>
    <div class="father">
        <span>hello</span>
        <span>hello</span>
        <span>hello</span>
        <span>hello</span>
        <span>hello</span>
        <span>hello</span>
    </div>
</body>


div {
    border:1px solid black;
}
span {
    background-color:#ccc;
}
```

![img](https://pic2.zhimg.com/80/v2-f634eeb7130802faa1b2b9cd27018909_hd.jpg)

可以看到内联元素整整齐齐的排列，由于关于内联元素的布局，前面已经说过，在此不再阐述。

**加入display:inline-block 并为它设置宽度之后：**

```text
div {
    border:1px solid black;
}
span {
    display:inline-block;
    background-color:#ccc;
    width:20px;
    height:20px;
}
```

![img](https://pic1.zhimg.com/80/v2-c9927f79795dde9b202c267b4d54b960_hd.jpg)

可以看出来确实可以设置宽和高了！

**这时将最后一个元素添加last类，然后为其设置高度**

```text
.last {
    width:50px;
    height:30px;
}
```

你可能猜到了我的用意，我在想这个时候的span元素是不是真正的变成了inline-block，还是说它只是表现成了inline-block；

![img](https://pic2.zhimg.com/80/v2-fe2f320a533dabb7a5030cfc988a5245_hd.jpg)

当看到结果的时候，我觉得我们可以认为它真的具备了block的属性，确确实实的改变了！



## 3. inline-block的高度不同的情况

我们之前设置的元素，在inline-block的时候，他们的大小都是相同的，但是现实来说，很有可能有高度大小不一样的情况，它们在排布的时候会不会和我们想的不一样呢？

```text
<body>
    <div class="father">
        <div class="block1"></div>
        <div class="block2"></div>
        <div class="block3"></div>
        <div class="block4"></div>
        <div class="block5"></div>
    </div>

</body>



.father .block1 {
    display:inline-block;
    width:100px;
    height:50px;
    background-color:#ccc;
}
.father .block2 {
    display:inline-block;
    width:50px;
    height:100px;
    background-color:#ccc;
}
.father .block3 {
    display:inline-block;
    width:150px;
    height:40px;
    background-color:#ccc;
}
.father .block4 {
    display:inline-block;
    width:200px;
    height:150px;
    background-color:#ccc;
}
.father .block5 {
    display:inline-block;
    width:100px;
    height:20px;
    background-color:#ccc;
}
```



![img](https://pic2.zhimg.com/80/v2-72af94b813c114867de2ef6f55799ad5_hd.jpg)

和你想的一样吗？让我们来思考一下为什么会这个样子吧！
记住inline-block最根本的东西，万变不离其宗：**它同时具备了block和inline两者的功能。**

也就是说，当元素高度不一致的时候，它是以inline方式对齐的，记得之前类比的word排版吗？同样的道理，它是以文本的基线进行对齐！

不信的话再后面加一个span文本元素

![img](https://pic2.zhimg.com/80/v2-604613a211be5dec07cd9efa0e71ea21_hd.jpg)



## 总结

暂时想到这么多。

看完本文可以重回到 [CSS文本的布局](https://zhuanlan.zhihu.com/p/31848738)