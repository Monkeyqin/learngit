# JavaScript随笔

## 1.基础语法： 变量声明、数据类型、循环、闭包、内置对象等； ##

+  数据类型：String / Number / Boolean / Null / Undefined / Object

## 2.闭包 ##
### 在一个函数中声明另一个函数，并且这个函数能够访问父函数作用域中的变量；闭包访问3个域的变量（自己的作用域，父函数作用域，全局作用域）。

## 3.函数 ##
+ 函数有属性，可以连接到构造方法;
+ 可以像一个变量存储在内存中；
+ 可以作为参数传递给其他函数；
+ 可以返回其他函数；

## 4.函数原型链
+ Js中没有继承的概念,但Js在Function对象中建立了原型对象prototype，并以function为主线,从上至下，在内部构造了一条原型链。
+ 简单的说就是建立变量查找机制，当访问一个对象的属性时，先找对象本身是否存在，若不存在就去找该对象所属的原型链上去找，直到找到Object为止,如果都没找到该属性，则返回Undefined。


## 5.在JS中清空数组中的内容 ##
+ 方法一：直接改变变量所直的对象
+ 方法二：设置length=0清空数组元素

# ES6——学习笔记
## 解构
ES6按照一定模式，从数组和对象中提取值，并对变量赋值，这叫做解构。
### (1).数值的解构赋值
```
let [a,b,c]=[1,2,3];
console.log(a,b,c);  //1,2,3
```
解构允许赋值默认值。
```
let [foo=true]=[];
console.log(foo);   //true
```

### (2).对象的解构赋值
对象的解构与数组有一组重要的不同是：数组的元素是按照次序排列的，变量的取值按照位置决定；而对象的属性是没有次序的，所以变量必须与属性同名，才能取到相同的值。
```
    let { foo , bar }={ foo : "one" , bar :"two" }
    console.log(foo,bar);   //"one" "two"

    let obj={ first : "hello" ,second : "world"}
    let { first : f , second : s}= obj;
    console.log(f,s);  // "hello" "world"
```
对象的解构赋值内部机制：是先找同名属性，再赋值给对应的变量。

和数组一样，解构赋值也可以用于嵌套的对象。
```
  let obj={
      p:[
        "hello",
        {y:"world"}
      ]
  }

  let { p : [ a ,{ y }]} = obj;   //"hello"  "world"
```
对象的解构也可以指定默认值( 生效条件：属性值严格等于Undefined );
```
var { x = 3 }={};  //x=3
var { x , y = 5 } = { x : 1 };  //x=1,y=5

var { x = 3}={ x:Undefined };    //x=3

var { a = 2} = { a : null};     // a=null
```
如果属性等于null，就不严格等于Undefined,则默认值就不生效。


### (3).字符串的解构赋值
字符串被转换成一个类似数组的对象。
```
   let [a,b,c,d,e]="hello";
   console.log(a,b,c,d,e);
```

### (4).布尔值的解构赋值
如果等号右边是数值或布尔值，就先转换为对象。
```
  let {toString : s } = 123;
  s == Number.prototype.toString   //true

  let { toString : s } = true;
  s == Boolean.prototype.toString    //true
```
以上代码可以看出，Number和Boolean的包装对象都有toString属性，因此变量s能够取到值。

### (5).函数参数的解构赋值
```
  function add([x,y]){
    return x+y;
  }
  add([2,3]);     //5
```
解构赋值的用途：
  +  交换变量的值
  +  从函数中返回多个值
  +  函数参数的定义
  +  提取JSON数据
  +  遍历Map结构


## 字符串的扩展
###  1. codePointAt(); ( 定义在字符串实例对象上 )
在js中,字符是以UTF-16格式来储存的,每个字符为2个字节,有些字符是4个字节，js中就叫做2个字符。此codePointAt()方法能够处理4个字节存储的字符，返回一个字符的码点。
```
    var s="吉"；
    console.log(s.codePointAt(0));     //21513
```

### 2. String.fromCodePoint(); ( 定义在String对象上 )
用于从码点返回字符串。
```
    String.fromCodePoint(21513);     // 吉
```

### 3.字符串的遍历器接口
ES6对字符串添加了遍历器接口,使字符串能够被for···of循环遍历。
```
    for(let codePoint of "hello"){
      console.log(codePoint);        //"h" "e" "l" "l" "o"
    }
```
优点：此遍历器能够识别大于0xFFFF的码点;

### 4. at();
at()方法可以识别Unicode编码大于0xFFFF的字符,并返回相应的字符。
```
      'abc'.at(0)     // "a"
      '𠮷'.at(0)      // "𠮷"
```

### 5. includes() / StartsWith() / EndWith();
+ includes 返回布尔值，表示是否找到字符串
+ StartsWith 返回布尔值，表示参数字符串是不是在源字符串的头部
+ EndWith 返回布尔值，表示参数字符串是否在源字符串的尾部
```
    var s="Hello world";
    console.log(
      s.includes('w');        //true
      s.StartsWith('H');      //true
      s.EndWith('h');         //true
      );

      var s="Hello world";
      console.log(
        s.includes('world',2);        //true
        s.StartsWith('H', 0);      //true
        s.EndWith('h',5);         //true
        );
```
以上代码看出这三个方法都支持第二个参数，表示开始搜索的位置，其中EndWith的搜索顺序是从后往前查询。

### 6.repeat();
repeat()返回一个新的字符串，并将源字符串重复n次。
如果repeat()的参数是负数或Infinity,会报错;参数在0-1之间的小数，则会返回空;参数是NaN,则返回空字符串;

### 7.padStart(); padEnd();
ES6中引入了字符串补全长度的功能。 如果某个字符串长度不够,则padStart()方法是在头部补全,padEnd()方法是在尾部补全。
```
    "X".padStart(5,"ab");     //"ababX"
    "X".padEnd(3,"ab");     //"Xaba"

    "XX".padStart(2,"ab");     //"XX"
    "XX".padEnd(2,"ab");     //"XX"

    'abc'.padStart(10, '0123456789')   // "0123456789"

    'x'.padStart(4)         // '   x'
    'x'.padEnd(4)           // 'x   '
```
以上代码得出,padStart()和padEnd()方法共接收2个参数,第一个参数指定字符串最小长度,第二个是指要补全的字符串;
如果原字符串的长度大于或者等于字符串最小长度,那么返回原字符串本身;
如果原字符串和补全字符串的长度超过指定最小长度，那么就会截出超出位数的补全字符串;
如果省略第二个参数，就会默认用空格补全。

### 8.模板字符串
模板字符串(templete String)是增强版字符串,用("反引号")来表示,可以当作普通字符串来使用，也可当作多行字符串来使用，还可以在字符串中嵌入变量。

### 9.标签模板
模板字符串可以紧跟在函数名后面,该函数将被调用来处理模板字符串,这被称为标签模板功能。
如果模板字符串中有变量，那么就先把模板字符串处理成多个参数,再调用函数。
```
    var a=5,b=10;
    tag `Hello ${a+b} world ${a*b}`       //tag(["Hello","world",""],15,50);
```

### 10. String.raw()
String.raw()方法用来充当模板字符串的处理函数。
```
  String.raw `hello \n${2+6}`;       //hello\\n8
```
String.raw()方法也可以当作正常函数来使用;这时,第一个参数是一个具有raw属性的对象,raw属性值应该是一个数组。
```
    String.raw( {raw : " test " },1,2,3);
    //相当于   String.raw( { raw: [ "t" , "e" ,"s" ,"t"] } ,1,2,3);
```

## 正则的扩展
### 1.RegExp构造函数
在ES5中,RegExp的构造函数有两种情况；
第一种情况是：第一个参数是字符串,第二个表达正则表达式的修饰符(flag)。
```
    var reg=new RegExp('abc','i');   //相当于  var reg=/abc/i;
```
第二种情况是：参数是正则表达式,这时会返回一个原正则表达式的拷贝。
```
    var reg=new RexExp(/abc/i);      //相当于  var reg=/abc/i;
```
但是ES5中不允许使用第二个参数添加修饰符,会报错。
在ES6中改变了这个行为，只要第一个参数是正则表达式,那么就能够使用第二个参数指定修饰符;而且返回的正则表达式会忽略原有的参数指定修饰符,只使用新的指定修饰符。
```
  new RegExp(/abc/ig,'i').flag;      //原有的"ig"修饰符被"i"覆盖了
```
### 2.字符串的正则方法
字符串对象共有4个方法,可以使用正则表达式split()/match()/replace()/search()。ES6将这4种方法,在语言内部全调用在RexExp实例方法上,从而做到与正则相关的方法全都定义在RexExp对象上。
+ String.prototype.match  =>  RexExp.prototype[symbol,match]
+ String.prototype.split  =>  RegExp.prototype[symbol,split]
+ String.prototype.replace  => RegExp.prototype[symbol,replace]
+ String.prototype.search  => RexExp.prototype.[symbol,search]

### 3.u修饰符
ES6对正则表达式添加了u修饰符,能够正确处理大于"\uffff"的Unicode字符;能够正确处理UTF-16的编码。
```
    /^\uD83D/u.test('\uD83D\uDC2A')       // false  (加了u修饰符,那么ES6就识别成一个字节,就返回false)

    /^\uD83D/.test('\uD83D\uDC2A')        // true  (ES5中不支持四字节的UTF-16的编码,会识别成2个字节,则返回true)    
```
一旦加上u修饰符,就会改变下面正则表达式的行为：
 + 点(.)字符
  点(.)字符在正则表达式中表示除了换行符的其他任意单个字符。对于码点大于0xFFFF的Unicode字符,点(.)字符不能识别,必须加上u修饰符。
 + Unicode字符表示法
 ES6中新增了使用大括号表示Unicode字符,这种表示法在正则表达式中必须要加上u修饰符,才能够识别大括号中的内容,否则被视为量词。
 + 量词
 使用u修饰符的正则表达式，都会正确识别大于0xFFFF的Unicode字符。
 ......


## 数值的扩展
### 1.二进制和八进制的写法
在ES6中,新增了对二进制和八进制的写法,分别是用0b(或0B)/0o(或0O)表示。
```
    0b111110111 === 503        // true
    0o767 === 503              // true
```
从ES5开始,在严格模式中八进制不允许使用0作为前缀,ES6进一步表明了要使用0o来表示。
```
  (function(){
    console.log(0o11 === 011);
    })();             //true

    (function(){
      "use strict"
      console.log(0o11 === 011);
      })();           //false
```
如果将0b和0o所表示的二进制和八进制转换成十进制,都要使用Number方法。
```
  Number(0o11);      //9
  Number(0b111110111);      //503
```

### 2.Number.isFinite() / Number.isNaN();
ES6在Number对象上,新增了Number.isFinite() / Number.isNaN()两种方法；
+ Number.isFinite(); 用来检查一个数值是否为有限的。
+ Number.isNaN(); 用来检查一个值是否为NaN。
这两个方法与传统全局的isFinite()和isNaN()方法的区别在于：传统方法调用Number()将非数值转化为数值,再进行判断;只是此方法对数值才有效。
#### Number.isfinite()对非数值一律返回false,Number.isNaN()只对NaN返回true,其余一律返回false。

### 3.Number.parseInt() / Number.parseFloat();
ES6将全局对象方法parseInt()和parseFloat(),移植到Number对象上,行为一直保持不变。
```
    // ES5的写法
    parseInt('12.34') // 12
    parseFloat('123.45#') // 123.45

    // ES6的写法
    Number.parseInt('12.34') // 12
    Number.parseFloat('123.45#') // 123.45
```
这样做的目的：是逐渐减少全局性方法,使得语言模块化。

### 4.Number.isInteger();
Number.isInteger()用来判断一个值是否为整数。在JavaScript中,整数和浮点数都是相同的储存方法,所以1和1.0被称为同一个值。
