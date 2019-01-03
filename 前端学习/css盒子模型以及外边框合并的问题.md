## 盒子模型

我们把布局里面的所有东西都可以想象成一个盒子，盒子里面又装着小盒子，小盒子里面又装着小小盒子......

所以布局的万物基于盒子。即使一个小小的元素p，也可以把它**抽象**成为一个盒子。

你现在心里有很多疑问，没关系，接着看。



以下是标准的盒子模型。（[图片来源](http://link.zhihu.com/?target=https%3A//www.google.co.jp/url%3Fsa%3Di%26rct%3Dj%26q%3D%26esrc%3Ds%26source%3Dimages%26cd%3D%26cad%3Drja%26uact%3D8%26ved%3D0ahUKEwjiksvGs-rXAhXBJ5QKHQLhBbAQjRwIBw%26url%3Dhttps%253A%252F%252Fguxinyan.github.io%252F2016%252F05%252F09%252FCSS%2525E7%25259B%252592%2525E6%2525A8%2525A1%2525E5%25259E%25258B%252F%26psig%3DAOvVaw13l3u_uxwvUE3nixDTZCX3%26ust%3D1512272310804700)）

![img](https://pic3.zhimg.com/80/v2-1c7edd49c7111272bb68402ecd202812_hd.jpg)



我们平常给元素加上的width，height实际上就是给内容区域加宽和高。我们增加内外边距的时候不改变内容区域的大小，**却会改变整体的大小。**如果我们为元素加一个1像素的框的话，那么我们能看见的只是框里面的东西（内边距+内容区域），如果在元素上添加背景，背景也会应用于这一区域，而外边距是不可见的，它是用来分隔各个元素。



虽然外边距是不可见的，但是我们算元素的总宽度或者总高度的时候，要加上外边距。

即：

height总=margin-top+border+padding-top+height+padding-bottom+border+margin-bottom

width总=margin-left+border+padding-left+width+padding-right+border+margin-right



如果只在视觉上固定框的大小不用加入margin进行计算。这里和《精通CSS 高级web标准解决方案（第二版）》有不同的意见。（P39-P40，我认为书中出错）







## 外边距的合并问题



合并问题的前提是：**处于普通流两个或多个块元素垂直方向上相遇，会造成的margin 折叠**

除去普通流、两个或多个、块元素、垂直很好理解之外

这个相遇要好好解释一下了，就是说两个元素碰到了一起。一般可以分为：



Ⅰ：父元素的上外边距和第一个子元素的上外边距

![img](https://pic2.zhimg.com/80/v2-067cd5de357cca4030936022aca920fd_hd.jpg)

或许这么看还是很不直观，来看代码，包你看懂！

```text
<div class="father">
    <div class="son"></div>
</div>

/*为了效果更加明显，为body添加背景颜色*/
body{
    background-color:#ccc;
}
.father{
    background-color:blue;
    height:100px;
    width:100px;
    margin-top:20px;
}
.son{
    background-color:red;
    height:20px;
    width:20px;
    margin-top:20px;
}
```

效果图

![img](https://pic4.zhimg.com/80/v2-300fc614b03a8d97168c46e14248a207_hd.jpg)

可以看出来红色方块原本应该在蓝色方块的下方20px处，然而却合并了！

当我们继续把蓝色块（father）margin-top调成0或者根本就不设置外边距，观察现象。

![img](https://pic4.zhimg.com/80/v2-eb54f7b8704ea2afed7e03bb0c300fd7_hd.jpg)

由上面的可以看出，即使外边距是0，一样可以合并！



这种合并有时候是一种便利，而在有些情况却成为了不知何处的bug。所以在后面会讲怎么消除这种浮动。



Ⅱ：父元素的下外边距和最后一个子元素的下外边距

bottom与bottom合并，与上一个类似，不再阐述。



Ⅲ：相邻兄弟姐妹元素

![img](https://pic4.zhimg.com/80/v2-696f90c66226b0c1451df96331693787_hd.jpg)

![img](https://pic1.zhimg.com/80/v2-6c3d0838f188aa7386173158cfa4d4c4_hd.jpg)外边距为40px的情况

```text
<div class="block1"></div>
<div class="block2"></div>

.block1 {
    background-color:red;
    height:50px;
    width:50px;
    margin-bottom:20px;
}
.block2 {
    background-color:blue;
    height:50px;
    width:50px;
    margin-top:20px;
}
```

![img](https://pic1.zhimg.com/80/v2-5c62737f34a6e935ed2efefa225bccf8_hd.jpg)实际效果图

由此可见，相邻同胞元素确实发生了合并。



Ⅳ：空元素 ，自己的上外边距会和自己的下外边距合



```text
<p style="margin-bottom: 0px;">这个段落的和下面段落的距离将为20px</p>
        
<div style="margin-top: 20px; margin-bottom: 20px;"></div>
        
<p style="margin-top: 0px;">这个段落的和上面段落的距离将为20px</p>
        
```

这样第一个p元素和第三个p元素之间距离为20px

图解：

![img](https://pic1.zhimg.com/80/v2-cddf62a4a90fb1bc12659f787373c7dc_hd.jpg)



## 阻止自动合并

上面说了，只有处于普通流的块元素才会合并。

> 所以最通用的方法就是：

display:inline/inline-block position:absolute float:left/right



关于display:inline的说明：用此方法来清除合并有一些情况，因为转换为inline之后，width，margin-top，等等都不起作用了，所以如果设置外边距还是达不到效果。

> 针对父子元素的方法

- 设置了清除浮动属性
- 因为margin需要直接接触才能合并，所以父元素或子元素中有border或padding，或者二者之间有元素



## 注意

如果有负外边距，合并后外边距为最大正边距加上最小负边距（绝对值最大的一个），如上面元素下边距为20px，下面元素上边距为-20px，则最后为0px.

## 非块元素如何显示？

为此我专门写了一篇文章：**《细究内联元素（你一定不知道的东西）》**

