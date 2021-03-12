



#### promise理解：

Promise对象可以理解为一次执行的异步操作，使用promise对象之后可以使用一种链式调用的方式来组织代码，避免**回调地狱**问题。

#### promise原理：

`Promise` 基本结构，创建构造函数`promise`实例，，并对实例传入resolve()和reject()两个函数作为参数，

`promise`有三个状态：

`pending(进行中)`

`fulfilled（已成功）`

`rejected（已失败）`

状态只能由 `Pending` 变为 `Fulfilled` 或由 `Pending` 变为 `Rejected` ，且状态改变之后不会在发生变化，会一直保持这个状态

`resolve()` 和 `reject()` 两个函数参数，用于改变 `Promise` 的状态和传入 `Promise` 的值。

`下面说一说 `Promise` 的核心: `then` 方法`

`.then()`方法指定当promise的状态由`pending`变为`fulfilled`,或者`rejected`时刻不同回调函数。

`.catch()`方法是`.then()`方法的别名，是用来是指定promise错误状态时对应的回调函数。

上述两者方法都返回一个promise对象，因此后续可以链式调用两者方法





#### promise案例讲解：

```js
const promise = new Promise((resolve, reject)=>{
		  console.log(1);
		  resolve();
		  console.log(2);
		})
promise.then(()=>{
    console.log(4);
})
console.log(5);

运行结果是： 1,2,5,4
遇到Promise构造函数立即执行
解释：promise的构造函数是同步执行，promise.then中的函数是异步执行。
```



```js
const promise = new Promise((resolve, reject) => {
		  resolve('success1')
		  reject('error')
		  resolve('success2')
		})
promise.then((res) => {
    console.log('then: ', res)
})
    .catch((err) => {
    console.log('catch: ', err)
})
运行结果：then: success1
解释：构造函数中的 resolve 或 reject 只有第一次执行有效，多次调用没有任何	
作用。promise 状态一旦改变则不能再变。
promise 有 3 种状 态： pending、fulfilled 或 rejected。
状态改变只能是 pending->fulfilled 或者 pending-> rejected，
状态一旦改变则不能再变。
```



```js
const promise = new Promise((resolve, reject) => {
	  setTimeout(() => {
	    console.log('once')
	    resolve('success')
	  }, 3000)
	})
console.log('wwwww')
const start = Date.now()
promise.then((res) => {
  console.log(res, Date.now() - start)
})
promise.then((res) => {
  console.log(res, Date.now() - start)
})   
运行结果：wwwww
		once
		success 3005
		success 3007
解释：promise 的 .then 或者 .catch 可以被调用多次，但这里 Promise 构造函数
	只执行一次。或者说 promise 内部状态一经改变，并且有了一个值，那么后续每
	次调用 .then 或者 .catch 都会直接拿到该值。
```


```js
console.log('start');
new Promise(function(resolve,reject){
    setTimeout(function(){    //定时器模拟异步
        resolve('hello');    //修改promise状态调用then中的第一个函数
    },2000);
}).then((value)=>{
    	console.log(value);    //接收resolve传来的值
    	return new Promise(function(resolve){ //该then()返回一个新的promise实例，后面可以继续接then
	        setTimeout(function(){
	            resolve('world');  //修改新promise的状态，去调用then
	        },3000)
	    })  
	}).then((value)=>{
	   console.log(value);
	})
//输出结果：
/*
    立即输出   start
    两秒输出   hello
    再三秒     world
 */
```

```js
console.log('start');
new Promise(function(resolve,reject){
    setTimeout(function(){  
        resolve('hello');    
    },2000);
}).then((value)=>{
    console.log(value);  
    (function(){
        return new Promise(function(resolve){   
            setTimeout(function(){
                resolve('world');       
            },3000)
        })  
    })();  
    return false; 
}).then((value)=>{
   console.log(value);
})
/*
    结果：
       立即输出   start
       两秒输出   hello
       三秒输出   false
*/
	根据上面的运行结果来看，如果在一个then（）中没有返回一个新的promise，则
	return 什么下一个then就接受什么，在上面的实例代码中return的是false，下一个
	then中接受到的value就是false，如果then中没有return，则默认return的是	undefined.

```

```
then（）中包含.then（）的嵌套情况
then()的嵌套会先将内部的then()执行完毕再继续执行外部的then();在多个then嵌套时建议将其展开，将then()放在同一级，这样代码更清晰
	
console.log('start');
new Promise((resolve,reject)=>{
    setTimeout(function(){
        console.log('step');
        resolve(110);
    },1000)
})
.then((value)=>{
    return new Promise((resolve,reject)=>{
        setTimeout(function(){
            console.log('step1');
            resolve(value);
        },1000)
    })
    .then((value)=>{
        console.log('step 1-1');
        return value;
    })
    .then((value)=>{
        console.log('step 1-2');
        return value;
    })
})
.then((value)=>{
    console.log(value);
    console.log('step 2');
})
/*
 start
 step
 step1
 step 1-1
 step 1-2
 110
 step 2
*/
 
//展开之后的代码
console.log('start');
new Promise((resolve,reject)=>{
    setTimeout(function(){
        console.log('step');
        resolve(110);
    },1000)
})
.then((value)=>{
    return new Promise((resolve,reject)=>{
        setTimeout(function(){
            console.log('step1');
            resolve(value);
        },1000)
    })
})
.then((value)=>{
        console.log('step 1-1');
        return value;
    })
.then((value)=>{
    console.log('step 1-2');
    return value;
})
.then((value)=>{
    console.log(value);
    console.log('step 2');
})

```



#### typeof判断数据类型

typeof运算符用于判断基本变量的类型，但是对于一些创建的对象，例如（const a=[]），它们都会返回'object'，有时我们需要判断该实例是否为某个对象的实例，那么这个时候需要用到instanceof运算符，后续记录instanceof运算符的相关用法

#### instanceof：

```
A instanceof B，这里B一定要是个引用数据类型的关键字，否则都会判断结果为false，因为instanceof用来判断引用数据类型（复杂数据）属于什么样引用类型数据。也可以通俗理解（instanceof判断变量对象属于那种类型对象）
```

#### 两种理解方法

·instanceof用来判断引用数据类型（复杂数据）属于什么样对象类型。

·instanceof运算符用来判断一个构造函数的prototype属性所指向的对象是否存在另外一个要检测对象的原型链上

对于非引用数类型用instanceof（）判断那就是扯淡，不是一个种类，因为变量分为：基本数据类型（null,undefined,string,number,bullean）,引用数据类型（复杂数据）。

```
function Person() {}

console.log(String instanceof String);   //false
//第一个String的原型链：String=>
//String.__proto__=>Function.prototype=>Function.prototype.__proto__=>Object.prototype
//第二个String的原型链：String=>String.prototype

console.log(Boolean instanceof Boolean); //false,
//第一个Boolean的原型链：Boolean=>
//Boolean.__proto__=>Function.prototype=>Function.prototype.__proto__=>Object.prototype
//第二个Boolean的原型链：Boolean=>Boolean.prototype

console.log(Person instanceof Person); //false
//第一个Person的原型链：Person=>
//Person.__proto__=>Function.prototype=>Function.prototype.__proto__=>Object.prototype
//第二个Person的原型链：Person=>Person.prototype,第二个person根本不属于引用类型数据，就是一个基本类型变量
```



### 原型链完整图

![figure1](C:\Users\Administrator\Desktop\figure1.jpg)

##### 常见html强调标签：

<h>标签在浏览器中的表现是字体大小的变化

<strong>标签在浏览器中的表现为加粗

<em>,<i>标签在浏览器中的显示效果为斜体,也有强调意思



##### 常见的行内块元素

input、img



##### css继承属性

常用的css不可继承的属性

display：规定元素应该生成的框的类型

text-decoration：规定添加到文本的装饰

text-shadow：文本阴影效果

white-space：空白符的处理

盒子模型的属性：width、height、margin 、border、padding

背景属性：background

定位属性：float、clear、position、top、right、bottom、left、min-width、min-height、max-width、max-height、overflow、clip、z-index

常用的css可继承的属性：

font：组合字体

font-family：规定元素的字体系列

font-weight：设置字体的粗细

font-size：设置字体的尺寸

font-style：定义字体的风格

text-indent：文本缩进

text-align：文本水平对齐

line-height：行高

color：文本颜色

visibility：元素可见性

光标属性：cursor

所有元素可以继承的

1、元素可见性：visibility

2、光标属性：cursor

内联元素可以继承的属性

1、字体系列属性

2、除text-indent、text-align之外的文本系列属性

块级元素可以继承的属性

text-indent、text-align

inherit（继承）值

每一个属性可以指定值为“inherit”，即：对于给定的元素，该属性和它父元素相对属性的计算值取一样的值。继承值通常只用作后备值，它可以通过显式地指定“inherit”而得到加强，例如：

p { font-size: inherit; }



##### 变量提升：

```
Js代码执行前，浏览器会给一个全局作用域window

Window分两个模块一个是存储模块一个是执行模块

存储模块找到所有的var和function 关键字给这些变量添加内存地址

执行模块，代码从上到下执行，遇到变量就会去存储模块查找，有和没有

有就看你赋值没有，赋值了就是后面的值，没有赋值就是undefined。

没有结果就是xxx is not defined
```

```
var x = 10;
function fn() {
    console.log(x)
}
function show(f) {
    var x= 20;
    f();
}
show(fn);//10
```

```
for(var i = 0;i < 5;i++){
	setTimeout(function (){
		console.log(i++);
	},400)
}
console.log(i);//5 5 6 7 8 9
```

```
for(var i = 0;i < 5;i++){
	setTimeout(function (){
		console.log(++i);
	},400)
}
console.log(i);// 5 6 7 8 9 10


for(var i = 0;i < 5;i++){
    (function (x) {
        setTimeout(function (){
            console.log(x++);
        },400)
    })(i);
}//  0 1 2 3 4
```



##### 闭包

###### 概念：

能够读取其他函数内部变量的函数，

也可以是内部函数总是可以访问其所在的外部函数中声明的参数和变量，即使在其外部函数被返回（寿命终结）了之后。

###### 作用：

延申变量的作用范围

###### 缺点：

1.可以重复使用变量，并且不会造成变量污染

2.由于闭包会使得函数中的变量都被保存在内存中，内存消耗很大，所以不能滥用闭包

```
for (var i = 0; i < 4; i++) {
    setTimeout(
      (function(num) {
        return function() {
          console.log(num);
        };
      })(i),  //立即执行函数产生闭包
      1000
)}

   // 0 1 2 3
 //for循环属于同步执行代码，在主线程中先处理完毕，循环共产生四个定时器异步任务放入事件队列等待，但在定时器中包含一个立即执行函数，开辟四个立即执行函数空间，每次循环将i具体数值附给num，立即执行函数内部函数的num再次产生闭包，每次log打印出的是每个num具体值的副本。
```

##### 变量声明规则

函数内部声明变量的时候，一定要使用var命令。如果不用的话，你实际上声明了一个全局变量

