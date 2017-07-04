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







## 2.字符串的扩展
+ includes 返回布尔值，表示是否找到字符串
+ StartsWith 返回布尔值，表示参数字符串是不是在源字符串的头部
+ EndWith 返回布尔值，表示参数字符串是否在源字符串的尾部
这三个方法都支持第二个参数，表示开始搜索的位置。
