## 一、前言

在进行学习的时候，发现对于`click`事件和`change`事件，还有一点模糊的地方。

## 二、简述

`click`事件，[根据MDN上面的描述](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/click_event)就是鼠标在一个元素上被按下和放开时，此事件会被触发。但是由于鼠标如果不按下去的话，就没法放开，所以可以理解为在按下鼠标的那一刻，`click`事件就会触发了。里面有很多的属性，在这里就不一一讲解了。



`change`事件 [根据MDN上面的描述](https://developer.mozilla.org/zh-CN/docs/Web/Events/change)是被三个元素触发的。有`<input>` `<select>` `<textarea>`当用户提交对元素值的更改时，会被触发。

在进行学习的过程中，出现了一个疑问，那就是在进行按钮操作的时候，再点击鼠标的同时，发生两个操作，①按钮被选中。②触发click 或change时间。那么问题来了这两个事件哪个先，哪个后呢？

## 三、 实践

方法很简单。

```
<input type="radio">这是一个单选按钮
<script>
    var input = document.querySelector("input");
    input.addEventListener("click", function () {
        console.log("我在监听内部");
        console.log("当前的按钮的状态是：" + input.checked);
    }, false);
</script>
```

可以发现在点击屏幕的时候，首先按钮被选中，然后进入到监听函数内部，同时`input.checked`为`true`;

## 四、其他

在使用`event.preventDefault()`的时候，我们发现，在使用`click`进行监听的时候，会发现能够阻止他的默认行为（选中单选框）。然而在使用`change`事件的时候，则不会阻止默认行为（选中单选框）。