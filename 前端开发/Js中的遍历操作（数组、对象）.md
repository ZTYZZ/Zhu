## 一、 前言

对于遍历操作，是很重要的，我作为一个小白，进行总结一下！！嘻嘻嘻嘻嘻 。

## 二、 几种遍历数组方法

#### 1. for(循环）

这个用的十分常见，主要是用在数组中和一些dom操作中。

```
for(var i = 0 ; i < arr.length ; i++) {
    //执行相关操作
}
```

#### 2. for 优化版

由于一些dom操作，在进行的时候，是动态更新的，所以会导致`length`是不断变化的，同时也为了减少操作，可以将`arr.length`存储在变量里面。

```
for(var i = 0,length=arr.length;i<length;i++) {
	//执行相关操作
}
```

#### 3. 其他迭代方法

`every()`

`some()`

`filter()`

`forEach()`

`map()`



#### 4. for...in循环

精准的迭代，可以迭代对象的元素。也可以迭代数组。

【注意】使用`for ... in`，迭代的是元素（keys），对于数组来说，则为下标（0,1,2...,length-1）

```
for(var key in arr) {
    //执行相关操作
}
```

#### 5. for...of循环（ES6支持）

```
for(let item of arr) {
    //执行相关操作
}
```

和`for...in`不同的是，`for...of`迭代出来的是值（value），对于数组来说，则是一个元素值。

关于更加详细的区别，请狠狠的点击这里[for...of 和 for...in的区别](https://segmentfault.com/q/1010000006658882)

## 三、对象的遍历的方法

#### 1. for...in遍历

```
var book = {
    name: "hello",
    id: "2",
    author: "ztyzz",
    time: "2018.2.30"

};
for(var el in book) {
    console.log(book[el]);
}
```

#### 2. for ... of遍历

此方法，不能遍历普通对象，需要和`Object.keys()`搭配使用，先获取对象的所有key的数组
然后遍历：

```
var book = {
    name: "hello",
    id: "2",
    author: "ztyzz",
    time: "2018.2.30"

};
for(var key of Object.keys(book)) {
    console.log(book[key]);
}
```

【注意】`Object.values()`返回对象所有的键值组成的数组，但是由于无法获取到key值，功能会比较残缺。

同时，由于`Object.keys()`返回一个数组,包括对象自身的(不含继承的)所有可枚举属性(不含Symbol属性).所以我们可以使用forEach()等上面的方法，来进行数组的遍历，再通过对象的访问来进行值的访问。

#### 3. Object.getOwnPropertyNames(obj)遍历

  返回一个数组,包含对象自身的所有属性(不含Symbol属性,但是包括不可枚举属性).

所以同样可以使用上面的访问数组的方式，来遍历key，再获取对象值。

#### 4. Reflect.ownKeys(obj)遍历

 返回一个数组,包含对象自身的所有属性,不管属性名是Symbol或字符串,也不管是否可枚举.  

