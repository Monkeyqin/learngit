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
    "X".padStart(5,"ab");                //"ababX"
    "X".padEnd(3,"ab");                  //"Xaba"

    "XX".padStart(2,"ab");              //"XX"
    "XX".padEnd(2,"ab");                //"XX"

    'abc'.padStart(10, '0123456789')   // "0123456789"

    'x'.padStart(4)                    // '   x'
    'x'.padEnd(4)                      // 'x   '
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

### 5.Number.EPSILON
ES6在新增的Number对象上，新增了Number.EPSILON代表着极少的常量。
Number.EPSILON    //2.220446049250313e-16
只要是浮点数计算的误差能够小于Number.EPSILON这个常量,就能够得到正确的结果：
```
  function abc(a,b){
    return (a+b) < Number.EPSILON
  }
  abc(0.1+0.2,0.5);     //false
  abc(0.2+0.22,0.1);    //false
```

## Math对象的扩展
ES6在Math对象上增加了17个方法,所有的方法都是静态方法,只能在Math对象上使用。

## 1.Math.trunc()
Math.trunc方法用于把一个数的小数部分去掉,只保留整数部分：
```
  Math.trunc(4.1)                // 4
  Math.trunc(4.9)                // 4
  Math.trunc(-4.1)               // -4
  Math.trunc(-4.9)               // -4
  Math.trunc(-0.1234)            // -0
```
对于非数值的值，Number.trunc内部使用Number方法将其转为数值;对于空值和无法截取的值返回NaN。

## 2.Math.sign()
Math.sign()用来判断一个值是否为正数、负数、零;对于非数值，会先转为数值。
### 此方法返回5个值:
    + 值若是正数返回+1;
    + 值若是负数返回-1;
    + 值若是0返回0;
    + 值若是-0返回-0;
    + 其他的值则返回NaN;

## 3.Math.cbrt()
Math.cbrt方法用来计算一个数的立方根。
### 对于非数值,此方法内部使用Number方法转换为数值,再进行计算;对于字符串的文字则返回NaN。
......

## 函数的扩展
### 1.函数参数的默认值
ES6允许为函数的参数设定默认值,直接写在参数定义的后面。
```
  function str(x,y="hello"){
    console.log(x,y);
  }
  str("hey");                  //"hey" "hello"
```
使用参数默认值时，函数不能用同名参数;另外参数默认值是不传值的,而是每次都重新计算表达式的值,也就是说参数传值是惰性传值。
```
  let x=1;
  function math( p = x + 100 ){
    console.log(p);
  }

  math();      //101
  x=111;
  math();      //211
```
与解构赋值默认值结合使用;参数默认值的位置;

### 2.rest参数
ES6引入rest参数(...变量名),用于获取多个函数的多个参数;rest参数搭配的变量是一个数组,这个变量将多个参数放入数组中。
rest参数之后不能有其他参数,否则会报错。函数的length属性不包括rest参数。
...

##  数组的扩展
### 1.扩展运算符...
扩展运算符是用(...)表示,用来将一个数组用逗号分隔的参数序列。

### 2.Array.from();
该方法用来将两种类型的对象:类似数组的对象和可遍历的对象包括(Set和Map数据解构),转化成真正的数组。

### 3.Array.of();
该方法用来将一组值转化为数组;并不存在由于参数的不同导致的重载,行为非常统一。
Array.of();总是返回参数值组成的数组;若没有参数就返回空数组。

### 4.数组实例对象find()和findIndex();
find();方法用于找出第一个符合条件的数组成员。
findIndex();方法用于返回第一个符合条件的数组成员位置。

### 5.数组实例fill();
数组fill();方法使用给定值,填充一个数组。该方法对空数组初始化非常方便,数组中已有的值会被全部抹去。

### 6.数组实例entries() / key() / value();
ES6提供该三个方法用来遍历数组。可以用for...of...进行遍历。

### 7.数组实例includes();
Array.prototype.includes方法返回一个布尔值,用来表示一个数组中是否包含指定值。该方法的第二个参数表示查询的起始位置,默认是0。

### 8.数组的空位
数组的空位是指在一个数组中某一个位置为空值。
#### 注意：数组的空值不代表是undefined,一个位置的值为undefined依然是有值,空位是没有任何值的。


## 对象的扩展
### 1.属性的简介表示法
ES6允许在对象中,直接写变量名,这时:属性名是变量名,属性值为变量的值。

### 2.属性名表达式
ES6允许定义字面量对象时,用表达式作为对象的属性名,即把表达式放在方括号内。
该表达式也可用于定义方法名。

### 3.方法的name属性
函数的name属性,返回函数名;对象方法也是函数,因此也有name属性。
#### 有两种情况: 第一种是Function构造函数创造的函数,返回anonymous;bind()方法创造的函数,name属性返回bound和原函数名。
如果对象的方法是symbol值,则name值返回的是symbol值的描述。

### 4.Object.is();
该方法用来表示两个值是否严格相等,与严格比较运算符(===)的行为一致。

### 5.Object.assgin();
该方法用于对象的合并,将源对象的可枚举性,复制到目标对象。第一个参数是目标对象,第二个参数是源对象。
此方法的用途:
  + 为对象添加属性
  + 为对象添加方法
  + 克隆对象(只能克隆对象自身的值,不能克隆继承的值)
  + 合并多个对象
  + 为属性指定默认值
  + 属性的可枚举型

### 6.属性的遍历
+ for...in  用来循环遍历自身和可枚举性属性。
+ Object.is(keys)   返回一个新数组,只包括对象自身的可枚举属性,不包括继承的可枚举属性。
+ Object.getOwnPropertyNames(obj);  返回一个数组,包括对象的所有属性(不包括symbol属性)。
+ Object.getOwnPropertySymbols(obj);  返回一个数组,包括对象自身的symbol属性。
+ Reflect.ownKeys(obj);  返回一个数组,包括自身的所有属性(不管属性名是symbol或字符串,不管是不是可枚举性);

### 7.proto属性
proto属性用来设置当前对象的prototype属性。在实现上,proto调用的是Object.prototype.__proto__

### 8.Object.setPrototypeof();
该方法用来设置一个对象的prototype属性。返回参数对象本身。

### 9.Object.getPrototypeof();
该方法用来读取一个对象的prototype属性。

### 10.Object.getOwnPropertyDescriptor();
返回某个对象属性的描述对象。


## Symbol
### 1.知识点
ES6新增了一种数据类型叫symbol,表示独一无二的值;是第七种数据类型;
如果Symbol的参数是一个对象,那么就会调用该对象的方法;
Symbol参数是对当前Symbol值的描述,因此相同参数返回的返回值是不一样的;
Symbol值可以转为Boolean值,不能转为数值。

### 2.作为属性名的symbol
symbol作为对象属性名时不能使用点运算符;symbol类型还可以定义一组常量,保证这组常量的值是不相等的。
symbol作为属性名时是公开属性,不是私有属性。

### 3.属性名的遍历
symbol作为属性名,该属性不出现在for...of.../for...in...循环中,也不会出现在Object.keys()/Object.getOwnPropertyNames()/JSON.stringify()返回;但是有一种Object.getOwnPropertySymbols()方法,该方法可以获取指定对象的所有symbol属性名。

### 4.symbol.for();
该方法接受一个字符串的参数,然后搜索到有没有以此参数作为symbol的值,如果有就返回这个symbol值。
symbol.for()和symbol()这两种方法都会返回一个新的symbol值,前者是在全局中搜索,而后者不会;
symbol.for()方法不会每次调用都返回一个新的值,而是先查询keys值是否存在,若不存在才会返回一个新的值。

### 5.symbol.keyFor();
该方法返回一个已登记的symbol类型值的key。

### 6.内置symbol值
ES6提供了11个内置symbol值,指向语言内部的方法。


## Set和Map数据结构
### Set
它类似于数组,但是数值都是唯一,没有重复的值。
```
[...new Set(array)]  //除去数组的重复值
```
在Set内部,2个NaN是相等的;由于2个空对象不相等,那么相当于2个不同的值。
Array.from()可以将set解构转换为数组。
Array.from(new Set(array));    //并且除去数组的重复值


#### 1.遍历操作
keys()：返回键名的遍历器
values()：返回键值的遍历器
entries()：返回键值对的遍历器
forEach()：使用回调函数遍历每个成员

#### 2.遍历的应用
扩展符(...)内部使用的是for...of循环,可以用于set结构。

### Map
它类似与对象,也有键值对的集合,但"键"的范围不限于字符串，各种类型的值(或对象)也能称为值。


## Proxy
Proxy这个词的原意是代理,在这里用来表示代理某些操作,也可译为代理器。
ES6提供Proxy构造函数,用来生成Proxy的实例对象。
```
  let proxy = new Proxy ( target ,handler );
```
### this问题
在proxy代理的情况下,this关键字是指的proxy代理。

## promise
### promise的含义
它是一个对象,从它可以获取异步操作的消息。
#### promise对象的特点:
+ 对象自身的状态不受外界的影响;promise对象代表一个异步操作,有三种状态:Pending(进行中)/resolve(已完成)/rejected(已失败),只有异步操作的结果才可以决定当前是哪种状态,任何其他操作都改变不了这个状态。
+ 一旦状态改变,结果就不会改变,任何时候都能得到状态的结果。
+ 当处于Pending状态,无法得到目前进展到哪一个阶段。

Promise对象创建就会立即执行。

### Promise.prototype.then();
Promise实例具有then对象,也就是说,then是定义在Promise.prototype原型对象上,它的作用是为Promise实例添加状态改变时的回调函数;
第一个参数是resolve状态的回调函数,第二个是rejected状态的回调函数。
then方法返回的是一个新的promise实例,因此可以采用链式写法,即then方法后调用另一个then方法。

### Promise.prototype.catch();
该方法用来制定发生错误时的回调函数。如果Promise对象的状态是resolve,那么这时抛出的错误是无效的。

### Promise.all();
该方法用于将多个Promise实例,包装成新的Promise实例。

### Promise.race();
该方法也是用于将多个Promise实例,包装成新的Promise实例。

### Promise.resolve();
该方法是把现有对象转化为Promise对象。Promise.resolve()方法的参数返回4种情况:
+ 参数是Promise实例(该方法将不做任何修改,原封不动的返回这个实例)
+ 参数是thenable对象(thenable对象是指具有then的方法)
+ 参数不是具有then方法的对象,或根本就不是对象(Promise.resolve()方法则返回一个新的Promise实例,状态为resolve)
+ 不带任何参数(Promise.resolve()方法允许调用时参数为空,直接返回一个状态为resolve的promise对象)

### Promise.rejected();
该方法也是返回一个新的Promise实例,该实例的状态是rejected;该方法的参数会原封不动的作为reject的理由,变成后续方法的参数。



## Iterator和for...of..循环
### Iterator遍历器
它是一个遍历器接口,为不同数据结构提供统一的访问机制。它的本质也是一个指针对象。
+ 第一次调用指针对象的next方法,可以指向数据结构的第一个成员
+ 第二次调用指针对象的next方法,可以指向数据结构的第二个成员
+ 不断调用next方法,直到它指向数据结构结束的位置

### 默认Iterator接口
Iterator接口的目的是指:为所有数据结构,提供统一的访问机制,即是for...of..循环。
当for...of..循环遍历某种数据结构时,该循环会自动去找iterator接口。
#### ES6规定,默认的Iterator接口部署在Symbol.Iterator属性;一个数据结构只要有该属性,说明该数据结构是"可遍历"的;Symbol.Iterator属性本身是一个函数,就是指的当前数据结构默认的遍历器生成函数。凡是部署了Symbol.Iterator的属性,就称为部署了遍历器接口。

原生具备iterator接口的数据结构:
+ Map/Set/String/Array/函数的argument对象

### 调用Iterator接口的场合
+ 解构赋值(对数组或Set结构进行赋值)
+ 扩展运算符

### 字符串的Iterator接口
字符串是一个类似数组对象,原生具有iterator接口。

### for...of..循环
该循环用于遍历所有数据结构的统一方法;该循环内部调用的是数据结构的Symbol.iterator方法。
该循环只返回含有数字索引的属性。

### Set和Map结构
这2种结构也具有iterator接口。


## Generator函数的语法
在语法上,Generator函数是一个状态机,封装了多个内部状态;在形式上,Generator函数是一个普通的函数,有2个不同的特征:
+ function关键字与函数名之间有一个*符号
+ 函数体内使用yield表达式
Generator函数是分段执行的,yield表达符是暂停执行标记,而next表达式是可以恢复继续执行。

### yield表达式
该表达式指的是可暂停执行的函数。
+ 遇到yield表达式,就暂停执行后面的操作,并将紧跟yield后的表达式的值作为返回对象的value属性值。
+ 下次调用next方法时,再继续往下执行,直到遇到下一个yield表达式。
+ 如果没有再遇到新的yield表达式，就一直运行到函数结束，直到return语句为止，并将return语句后面的表达式的值，作为返回的对象的value属性值。
+ 如果该函数没有return语句,则返回的对象的value值就是Undefined。
+ yield表达式只能使用在Generator函数中,用在其他地方都会报错。
+ yield表达式用在其他表达式中,必须放在圆括号中。

### 与Iterator接口的关系
由于Generator函数就是遍历器生成的函数,因此可以把Generator赋值给对象的Symbol.iterator属性上,使得该对象具有Iterator接口。

### Generator中的for...of..循环
for..of..循环可以自动遍历Generator函数生成的Iterator的对象,且不需要调用next方法。

### Generator.prototype.throw();
Generator函数返回的遍历器对象,都含有throw()方法,可以在函数体外抛出错误,并在Generator函数体内捕获。
throw();方法可以接收一个参数,该参数会被catch语句接收,建议抛出Error实例。


## Generator函数的异步调用
### 传统的异步调用方法
回调函数/事件监听/发布.订阅/Promise对象

### 协程
协程是指多个线程互相合作,完成异步任务。协程有点像函数,也有点像线程。

### Generator函数的数据交换和错误处理
next返回值的value属性,是Generator函数向外输出的数据,next还可以接收参数,向Generator函数中输入参数。
Generator函数内部可以部署错误处理代码,捕获函数体外抛出的错误。

### Thunk函数
Thunk函数是自动执行Generator函数的一种方式。Thunk函数的含义是指:先将参数传入一个临时函数中,再将这个临时函数传入函数体,这个临时函数是指的Thunk函数。该函数是一种"传名调用"的策略,用来替换某个表达式。
+ 一种意见是"传值调用"
+ 一种意见是"传名调用"

### JavaScript函数中的Thunk函数
在Js函数中,Thunk函数替换的不是表达式,而是多参数函数,将其替换成一个只接受回调函数作为参数的单参数函数。

### Generator的流程管理
Generator函数可以自动执行。

### co 模块
该模块用于Generator函数自动执行。co方法返回一个Promise对象,因此可以用then方法添加回调函数。
co模块的原理:当异步操作有了执行结果,就自动交回执行权。
两个方法可以做到这一点:
+ 回调函数(将异步操作包装成Thunk函数,在回调函数里交回执行权)
+ Promise对象(将异步操作包装成Promise对象,在then方法的回调函数中交回执行权)
co模块是将2种自动执行器,包装成一个模块;使用co模块的前提是:Generator函数中的yield表达式后只能是Thunk函数或者是Promise对象。
