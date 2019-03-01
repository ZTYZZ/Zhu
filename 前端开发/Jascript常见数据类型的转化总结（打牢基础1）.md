## 前言

在实际过程中，会经常用到，这些数据类型的相互转化，而且Javascript是弱类型语言，而且不区分整型和浮点型，比如`5 / 2`在Java这种强类型语言中，结果为`2`，而对于Javascript来说，结果却是`2.5`。下面我们来讲解怎么来相互转化这些类型，有哪些默认的行为，我们没有清晰地知道。

## 一 、基本数据类型和typeof操作符

基本数据类型有以下几个

`number`

`string`

`boolean`

`object` 包括 `对象`和`null`

`undefined`

`function`

我们使用`typeof`来判断一个变量或者数值字面量的类型。

```
var message = "hello world";
typeof message;//"string"
typeof 30;//"number"
```



对于undefined类型：

```
var message;
typeof message;//"undefined"
passage;//产生错误
typeof passage;//"undefined"
```

## 二、 浮点数和整型的相互转换

注意：由于浮点数需要的内存空间是保存整数的两倍。所以ECMAScript会将“整数”的浮点数 转换为整数。

如：

```
var x = 10.0;
x;//10
```

#### 1. 浮点数==>整型

使用`parseInt()`能够将浮点数转换为整型数字。

```
parseInt(3.6);//3
```

#### 2. 整型==>浮点型

本质上整型是没有办法转换为浮点型的。正如前面所说的，ECMAScript会将浮点数为整的直接转换为整型数。所以即使我们使用`parseFloat()`，还是转换不了，当然也没有必要转换。弱类型语言没有必要再去判断是不是浮点数。

```
parseFloat(2);//2
```

## 三、 数字与字符串的相互转换

我们会发现，字符串的操作最为频繁，他与谁都要转换一下~。

#### 1. 数字==>字符串

+ `toString()`任何类型都有这个方法，除了`null`和 `undefined`。对于数字而言，还可以指定进制。

+ ```
  var num = 10;
  console.log(num.toString(2));//1010
  ```

- `String()`此方法能够将任何类型转换为`String`
  1. 如果这个类型有`toString()`方法。则调用无参方法。、
  2. `null`返回`“null”`, `undefined`返回 `"undefined"`



#### 2. 字符串==>数字

+ `Number()`
  1. `Number()`只能转化为10进制数。
  2. 字符串为空，转换为`0`
  3. 字符串包含除数字之外的其他字符，则为`NAN`

```
Number("hello world 123");//NAN
Number("4.7");//4.7
Number("123");//123
Number("0001");//1
Number("1.0");//1
```

+ `parseInt()`

  从名字就能看出来，这个方法会更加细腻。

  1. 从字符串第一个开始，遇到空格，继续向下查找。
  2. 出现数字或负号，保留。
  3. 否则返回`NAN`

  不仅能识别10进制，`0x`开头的是十六进制， `0`开头的会识别为八进制(受浏览器版本影响，**(ie 6-8 识别为 8 进制，低版本Firefox 识别为8进制， 高版本Firefox， Chrome 识别为10进制，IE 9 之后  识别为 10进制**）。

  可以指定第二个参数为进制，进行精确的转换。

  ```
  parseInt("2.3");//2
  parseInt("  2.3");//2
  parseInt("123boom");//123
  parseInt("boom123");/NAN
  parseInt("0xf");//15
  parseInt("010");//10 chrome浏览器
  parseInt("010",8);//8
  ```

+ `parseFloat()`和 `parseInt()`类似，但其直接解析10进制，并且为浮点数。无第二个参数。

  ```
  parseFloat("0xf");//0
  parseFloat("22.5");//22.5
  parseFloat("3.125e7");//31250000
  ```

  

## 四、 字符串与数组的相互转换

#### 1. 字符串==>数组

比如，有这样一个字符串`s = "1,2,3,4,6,7"`将其转为`["1","2","3","4","5","6","7"]`的数组。

`split()` 两个参数，第一个必须，提供`字符串或正则表达式`，第二个参数指定转换为数组的最大长度，如果超过则去除。

```
var s = "1,2,3,4,6,7";
var arr = s.split(",");
console.log(arr);
```

#### 2. 数组==>字符串

+ `toString()`默认用`,`连接。

  ```
  var s1 = [ '1', '2', '3', '4', '6', '7' ]
  var s2 = s1.toString();
  console.log(s2);//1,2,3,4,6,7
  
  ```

+ `join()`能够指定符号连接。

  ```
  var s1 = [ '1', '2', '3', '4', '6', '7' ]
  var s2 = s1.join("++");
  console.log(s2);//1++2++3++4++6++7
  ```

  

## 五、 其他各种类型与boolean值的转换

####  其他类型 ==> boolean

```
			  true		false
String		非空字符串	空字符串
Number		非零数字	 零
Object		任何对象	 null
Undefined 	 --			undefined
```

将一个值转换为boolean，可以使用`Boolean()`或者在应用布尔表达式的地方。

#### 



##  六、对象与字符串的相互转换

#### 对象==> 字符串

+ `toString()`返回对象的字符串表示。

+ `valueOf()`返回字符串对象的字符串、数值或者布尔值表示。通常与`toString()`方法返回相同。

  