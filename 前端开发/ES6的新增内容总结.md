## 一、前言

虽然目前仍在学习ES5，但是难免会遇到一些ES6的知识点，不如现在慢慢积累，遇到的就在这篇文章中先记录下来，不断更新。

## 二、 模板字符串

在ES5中，我们拼接字符串是这样进行的。

```
var s1 = "hello";
var s2 = "world";
var s3 = s1 + " " + s2;
```

在ES6中，我们出现了代替品。

是这样的：

```
var s1 = "hello";
var s2 = "world";
var s3 = `${s1} ${s2}`;
console.log(s3);
```

模板字符串替代了`''`或`""`。可以进行多行输入，在进行特殊字符的时候要进行转义。(&{ 或者`),同时能够进行一些表达式的运算。更加深入的在下面的文章。

参考资料：

- [MDN 模板字符串](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/template_strings)
- [深入浅出：模板字符串](https://www.infoq.cn/article/es6-in-depth-template-string)
- [ES6: depth template string](https://hacks.mozilla.org/2015/05/es6-in-depth-template-strings-2/)

（未完待续）