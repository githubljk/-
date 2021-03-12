#### 浏览器加载顺序

- 浏览器加载一个页面时，是按照自上到下顺序加载的
- 读取到一行代码就执行一行，如果将<srcipt>标签写到代码前头部位，此时页面还没有加载好，js中的代码操作便无法执行对DOM的一些操作
- 通常在js代码放置到`window.onload()`中，`onload()`事件会在整个页面加载完毕后触发
  - 该事件的响应函数会在页面加载完毕后执行
  - 这样可以确保我们代码JS执行时所有的DOM对象(页面的标签，元素，文本，图片等等)都已经加载完毕
  - 可以将js代码全部写在`window.onload()`事件触发函数中
  - 缺点：对于`window.onload()`中的代码放置在最前面，浏览器也是先加载代码，但不执行，因此也是稍微耗时间

#### 元素，结点，文档

- 文档：document
- 元素（element）：页面中所有的标签(以后遇见，元素就等价标签)
- 根元素:`html标签`
- 节点（node）：
  - 页面中所有的内容，包括标签、属性（标签的属性）、文本(文字,换行,空格,回车)),
  - 节点是勾构成网页的最基本组成部分，网页中的每一部分都可以看作是一个节点
  
    

![](F:\前端总结\个人总结文档\img\dom.png)

#### 获取元素节点方法

##### 方案一：

- `document.getElementById('#id名')`
  
- 获取对应`id`的元素
  
- `docunment.getElementsByTagName('div')`

  - 获取对应标签的所有元素

- `docunmen.getElementsByName()`

  - 获取具有 name 属性元素数组,一般用于表单获取，表单都会设置`name`属性

  ```js
  <html>
  <head>
  <script type="text/javascript">
  function getElements()
    {
    var x=document.getElementsByName("myInput");
    alert(x.length);
    }
  </script>
  </head>
  <body>
  
  <input name="myInput" type="text" size="20" /><br />
  <input name="myInput" type="text" size="20" /><br />
  <input name="myInput" type="text" size="20" /><br />
  <br />
  <input type="button" onclick="getElements()"
  value="How many elements named 'myInput'?" />
  </body>
  </html>
  ```

- `document.body`

  - 获取页面的唯一一个`body`标签

  - `var body = document.body`

- `document.documentElement`

  - 获取页面根标签`html`

  - `var html = document.documentElement`

- `document.all`
  - 获取`html`页面的所有标签
  - 等价于`ducument.getElementByTagName(*)`

##### 方案二：

`通过CSS选择器方法来获取标签`

`语法：document.querySelector(.class div)`参数可以传递CSS选择器的写法，`下属方法只能返回一个元素`

- `document.querySelector(.class div)`
- `document.querySelector(div)`
- `document.querySelector(.class)`

`下属方法返回一个数组`

- `document.querySelectorAll(.class div)`
- `document.querySelectorAll(div)`
- `document.querySelectorAll(.class)`

###### 子节点/元素获取

- `var city = document.getElementById(#city)`

  1. 

  - `city.childNodes`//获取`id是city`元素内获取所有的`节点`，这个节点是个全部的细节包含(换行)
  - `city.firstChild`//获取`id是city`元素内获取第一个`节点`
  - `city.lasttChild//获取`id是city`元素内获取最后一个节点`

  1. 

  - `city.children`//获取点前元素中所有包含的`子元素`，子元素也就是子标签，这个属性更加符合实际需求
  - `city.firstElementChild`//获取当前元素第一个子元素
  - `city.lastElementChild`//获取当前元素最后一个子元素

###### 父节点，兄弟节点获取

- `parentNode`
  - 当前节点的父节

- `previousSibling`
  - 当前节点前一个兄弟节点

- `nextSibling`
  - 当前节点后一个兄弟节点

### DOM

- DOM，全称Document Object Model`文档对象模型`。

-  JS中通过DOM来对HTML文档进行操作。只要理解了DOM就可以随心所欲的操作WEB页面

- 文档
  – 文档表示的就是整个的HTML网页文档
-  对象
  – 对象表示将网页中的每一个部分都转换为了一个对象。
- 模型
  – 使用模型来表示对象之间的关系，这样方便我们获取对象

##### DOM查询

1. 元素方式查询

- ``document``.`getElementsByTagName("li")`
   - 通过标签名查询当前`document`元素的指定后代元素`li`

```js
	- 元素.childNodes
		- 获取当前元素的所有子节点
		- 会获取到空白的文本子节点
	
	- 元素.children
		- 获取当前元素的所有子元素
	
	- 元素.firstChild
		- 获取当前元素的第一个子节点
	
	- 元素.lastChild
		- 获取当前元素的最后一个子节点
	
	- 元素.parentNode
		- 获取当前元素的父元素
	
	- 元素.previousSibling
		- 获取当前元素的前一个兄弟节点
	
	- 元素.nextSibling
		- 获取当前元素的后一个兄弟节点
		
innerHTML和innerText
	- 这两个属性并没有在DOM标准定义，但是大部分浏览器都支持这两个属性
	- 两个属性作用类似，都可以获取到标签内部的内容，
		不同是innerHTML会获取到html标签，而innerText会自动去除标签
	- 如果使用这两个属性来设置标签内部的内容时，没有任何区别的	
	
读取标签内部的文本内容
	<h1>h1中的文本内容</h1>
	- 元素.firstChild.nodeValue
```

- 
  document.all
   - 获取页面中的所有元素，相当于document.getElementsByTagName("*");

- document.documentElement
   - 获取页面中html根元素

- document.body
   - 获取页面中的body元素

- document.getElementsByClassName()
   - 根据元素的class属性值查询一组元素节点对象
  - 这个方法不支持IE8及以下的浏览器

2. CSS选择器查询

- document.querySelector(参数)
   - 根据CSS选择器去页面中查询一个元素
   - 参数可以是 id, 类, 类型, 属性, 属性值等来选取元素
  - 如匹配到的元素有多个，则它会返回查询到的第一个元素	

- document.querySelectorAll(参数)	
   - 根据CSS选择器去页面中查询一组元素
   - 参数可以是 id, 类, 类型, 属性, 属性值等来选取元素
  - 会将匹配到所有元素封装到一个数组中返回，即使只匹配到一个

##### DOM修改

- document.createElement()
    - 可以根据标签名创建一个元素节点对象

	document.createTextNode()
		- 可以根据文本内容创建一个文本节点对象
		
	父节点.appendChild(子节点)
		- 向父节点中添加指定的子节点
		
	父节点.insertBefore(新节点,旧节点)
		- 将一个新的节点插入到旧节点的前边
		
	父节点.replaceChild(新节点,旧节点)
		- 使用一个新的节点去替换旧节点
		
	父节点.removeChild(子节点)
		- 删除指定的子节点
		- 推荐方式：子节点.parentNode.removeChild(子节点)
##### DOM操作CSS

###### 内联样式设置：

- 使用js代码区修改css内联样式，也即是行内样式
- 修改元素内联样式，`style`，具有较高样式优先级，(最高优先级是`!important`)
  - 语法：`元素.style.属性 = 值`；
  - 例子：`div.style.color = "red";`
  - 对于属性为横杠`-`连接的属性，需要改为驼峰式
    - `div.style.backGroundColor = 'pink'`

- 获取当前浏览器显示的样式/修改
  - 语法：`元素.currentStyle.color = "属性值"；`
  - 语法：`getComputuedStyle(元素,null).width；`

##### DOM事件对象

```js
/*
		 * onmousemove
		 * 	- 该事件将会在鼠标在元素中移动时被触发
		 * 
		 * 事件对象
		 * 	- 当事件的响应函数被触发时，浏览器每次都会将一个事件对象作为实参传递进响应函数,
		 * 		在事件对象中封装了当前事件相关的一切信息，比如：鼠标的坐标  键盘哪个按键被按下  鼠标滚轮滚动的方向。。。
		 */
		areaDiv.onmousemove = function(event){
			
			/*
			 * 在IE8中，响应函数被处罚时，浏览器不会传递事件对象，
			 * 	在IE8及以下的浏览器中，是将事件对象作为window对象的属性保存的
			 */
			/*if(!event){
				event = window.event;
			}*/
			
			//解决事件对象的兼容性问题
			event = event || window.event;
			
			/*
			 * clientX可以获取鼠标指针的水平坐标
			 * cilentY可以获取鼠标指针的垂直坐标
			 */
			var x = event.clientX;
			var y = event.clientY;
			
			//alert("x = "+x + " , y = "+y);
			
			//在showMsg中显示鼠标的坐标
			showMsg.innerHTML = "x = "+x + " , y = "+y;
			
		};
		
	};

</script>
```

##### 事件冒泡

 * 	所谓的冒泡指的就是事件的向上传导，当子代元素上的`事件`被触发时，其祖先元素的`相同事件`也会被触发
 * 	在开发中大部分情况冒泡都是有用的
 * 	如果不希望发生事件冒泡,可以通过事件对象`event`中的**event.stopPropagation()**来取消冒泡

```js
<script type="text/javascript">			
			window.onload = function(){		
				/*
				 * 事件的冒泡（Bubble）
				 * 	- 所谓的冒泡指的就是事件的向上传导，当后代元素上的事件被触发时，其祖先元素的相同事件也会被触发
				 * 	- 在开发中大部分情况冒泡都是有用的,如果不希望发生事件冒泡可以通过事件对象来取消冒泡
				 * 
				 */
				
				//为s1绑定一个单击响应函数
				var s1 = document.getElementById("s1");
				s1.onclick = function(event){
					event = event || window.event;
					alert("我是span的单击响应函数");
					
					//取消冒泡
					//可以将事件对象的cancelBubble设置为true，即可取消冒泡
					event.cancelBubble = true;
				};
				
				//为box1绑定一个单击响应函数
				var box1 = document.getElementById("box1");
				box1.onclick = function(event){
					event = event || window.event;
					alert("我是div的单击响应函数");
					
					event.cancelBubble = true;
				};
				
				//为body绑定一个单击响应函数
				document.body.onclick = function(){
					alert("我是body的单击响应函数");
				};
	
			};	
		</script>
	</head>
	<body>
		
		<div id="box1">
			我是box1
			<span id="s1">我是span</span>
		</div>
		
	</body>
```

##### 事件委派

- 指将事件统一绑定给元素的共同的祖先元素，这样当后代元素上的事件触发时，会一直冒泡到祖先元素

从而通过祖先元素的响应函数来处理事件，通过`event`可以获取当前页面发生的事件对象所有信息。

- 事件委派是利用了冒泡，通过委派可以减少事件绑定的次数，提高程序的性能

##### 元素事件绑定多个处理函数         

- 使用`addEventListener()`方法

```
window.onload = function(){
				
				/*
				 * 点击按钮以后弹出一个内容
				 */
				//获取按钮对象
				var btn01 = document.getElementById("btn01");
				
				/*
				 * 使用 对象.事件 = 函数 的形式绑定响应函数，
				 * 	它只能同时为一个元素的一个事件绑定一个响应函数，
				 * 	不能绑定多个，如果绑定了多个，则后边会覆盖掉前边的
				 */
				
				//为btn01绑定一个单击响应函数
				/*btn01.onclick = function(){
					alert(1);
				};*/
				
				//为btn01绑定第二个响应函数
				/*btn01.onclick = function(){
					alert(2);
				};*/
===================================================================				
				/*
				 * addEventListener()
				 * 	- 通过这个方法也可以为元素绑定响应函数
				 *  - 参数：
				 * 		1.事件的字符串，不要on
				 * 		2.回调函数，当事件触发时该函数会被调用
				 * 		3.是否在捕获阶段触发事件，需要一个布尔值，一般都传false
				 * 
				 * 使用addEventListener()可以同时为一个元素的相同事件同时绑定多个响应函数，
				 * 	这样当事件被触发时，响应函数将会按照函数的绑定顺序执行
				 * 
				 * 这个方法不支持IE8及以下的浏览器
				 */
				/*btn01.addEventListener("click",function(){
					alert(1);
				},false);
				
				btn01.addEventListener("click",function(){
					alert(2);
				},false);
				
				btn01.addEventListener("click",function(){
					alert(3);
				},false);*/
===================================================================					
				/*
				 * attachEvent()
				 * 	- 在IE8中可以使用attachEvent()来绑定事件
				 *  - 参数：
				 * 		1.事件的字符串，要on
				 * 		2.回调函数
				 * 
				 *  - 这个方法也可以同时为一个事件绑定多个处理函数，
				 * 		不同的是它是后绑定先执行，执行顺序和addEventListener()相反
				 */
				/*btn01.attachEvent("onclick",function(){
					alert(1);
				});
				
				btn01.attachEvent("onclick",function(){
					alert(2);
				});
				
				btn01.attachEvent("onclick",function(){
					alert(3);
				});*/
				
				/*btn01.addEventListener("click",function(){
					alert(this);
				},false);*/
				
				/*btn01.attachEvent("onclick",function(){
					alert(this);
				});*/
				
				bind(btn01 , "click" , function(){
					alert(this);
				});
			
				
			};
			
			//定义一个函数，用来为指定元素绑定响应函数
			/*
			 * addEventListener()中的this，是绑定事件的对象
			 * attachEvent()中的this，是window
			 *  需要统一两个方法this
			 */
			/*
			 * 参数：
			 * 	obj 要绑定事件的对象
			 * 	eventStr 事件的字符串(不要on)
			 *  callback 回调函数
			 */
			function bind(obj , eventStr , callback){
				if(obj.addEventListener){
					//大部分浏览器兼容的方式
					obj.addEventListener(eventStr , callback , false);
				}else{
					/*
					 * this是谁由调用方式决定
					 * callback.call(obj)
					 */
					//IE8及以下
					obj.attachEvent("on"+eventStr , function(){
						//在匿名函数中调用回调函数
						callback.call(obj);
					});
				}
			}
			
		</script>
	</head>
	<body>
		
		<button id="btn01">点我一下</button>
	</body>
```

##### 事件的传播

###### 三个阶段

1.捕获阶段

- 在捕获阶段时从最外层的祖先元素，向目标元素进行事件的捕获，但是默认此时不会触发事件(设置可`addEventListener()的第三个参数设置为true`在捕捉阶段可以触发事件执行，一般我们不喜欢这样)

2.目标阶段

- 事件捕获到目标元素，捕获结束开始在目标元素上触发事件

3.冒泡阶段

- 事件从目标元素向他的祖先元素传递，依次触发祖先元素上的事件
  - IE8及以下的浏览器中没有捕获阶段

#### BOM

- `BOM`浏览器对象模型

- `BOM`可以使我们通过JS来操作浏览器

- 在`BOM`中为我们提供了一组对象(以下五个)，用来完成对浏览器的操作 `BOM`对象

  - `Window`
        - 代表的是整个浏览器的窗口，同时window也是网页中的全局对象
   - `Navigator`
     - 代表的当前浏览器的信息，通过该对象可以来识别不同的浏览器
-  `Location`
    - 代表当前浏览器的`地址栏信息`，通过Location可以获取地址栏信息，或者操作浏览器跳转页面
  
- ` History`
    - 代表浏览器的历史记录，可以通过该对象来操作浏览器的历史记录
    - 由于隐私原因，该对象不能获取到具体的历史记录，只能操作浏览器向前或向后翻页
    - 而且该操作只在当次访问时有效
  
- `Screen`
    - 代表用户的屏幕的信息，通过该对象可以获取到用户的显示器的相关的信息

​       \*   这些五个`BOM`对象在浏览器中都是作为`window对象`的属性保存的，

​       \*    可以通过window对象来使用，也可以直接使用

```js
			 * Navigator
			 * 	- 代表的当前浏览器的信息，通过该对象可以来识别不同的浏览器
			 * 	- 由于历史原因，Navigator对象中的大部分属性都已经不能帮助我们识别浏览器了
			 * 	- 一般我们只会使用userAgent来判断浏览器的信息，
			 * 		userAgent是一个字符串，这个字符串中包含有用来描述浏览器信息的内容，
			 * 		不同的浏览器会有不同的userAgent
			 
			var ua = navigator.userAgent;
			
			console.log(ua);
			
			if(/firefox/i.test(ua)){
				alert("你是火狐！！！");
			}else if(/chrome/i.test(ua)){
				alert("你是Chrome");
			}else if(/msie/i.test(ua)){
				alert("你是IE浏览器~~~");
			}else if("ActiveXObject" in window){
				alert("你是IE11，枪毙了你~~~");
			}
```

```
history对象包含用户（在浏览器窗口中）访问过的 URL
history.back();
history.go(-2);


location对象包含有关当前 URL 的信息
```

```
window对象定时器
setInterval() 
//关闭定时器
clearInterval() 
```



##### CSS中类(class)的操作

```js
<script type="text/javascript">
			
			window.onload = function(){
				//获取box
				var box = document.getElementById("box");
				//获取btn01
				var btn01 = document.getElementById("btn01");
				
				//为btn01绑定单击响应函数
				btn01.onclick = function(){
					//修改box的样式
					/*
					 * 通过style属性来修改元素的样式，每修改一个样式，浏览器就需要重新渲染一次页面
					 * 	这样的执行的性能是比较差的，而且这种形式当我们要修改多个样式时，也不太方便
					 */
					/*box.style.width = "200px";
					box.style.height = "200px";
					box.style.backgroundColor = "yellow";*/
					
					/*
					 * 我希望一行代码，可以同时修改多个样式
					 */
					
					//修改box的class属性
					/*
					 * 我们可以通过修改元素的class属性来间接的修改样式
					 * 这样一来，我们只需要修改一次，即可同时修改多个样式，
					 * 	浏览器只需要重新渲染页面一次，性能比较好，
					 * 	并且这种方式，可以使表现和行为进一步的分离
					 */
					//box.className += " b2";
					//addClass(box,"b2");
					
					//alert(hasClass(box,"hello"));
					
					//removeClass(box,"b2");
					
					toggleClass(box,"b2");
				};
				
			};
			
			//定义一个函数，用来向一个元素中添加指定的class属性值
			/*
			 * 参数:
			 * 	obj 要添加class属性的元素
			 *  cn 要添加的class值
			 * 	
			 */
			function addClass(obj , cn){
				
				//检查obj中是否含有cn
				if(!hasClass(obj , cn)){
					obj.className += " "+cn;
				}
				
			}
			
			/*
			 * 判断一个元素中是否含有指定的class属性值
			 * 	如果有该class，则返回true，没有则返回false
			 * 	
			 */
			function hasClass(obj , cn){
				
				//判断obj中有没有cn class
				//创建一个正则表达式
				//var reg = /\bb2\b/;
				var reg = new RegExp("\\b"+cn+"\\b");
				
				return reg.test(obj.className);
				
			}
			
			/*
			 * 删除一个元素中的指定的class属性
			 */
			function removeClass(obj , cn){
				//创建一个正则表达式
				var reg = new RegExp("\\b"+cn+"\\b");
				
				//删除class
				obj.className = obj.className.replace(reg , "");
				
			}
			
			/*
			 * toggleClass可以用来切换一个类
			 * 	如果元素中具有该类，则删除
			 * 	如果元素中没有该类，则添加
			 */
			function toggleClass(obj , cn){
				
				//判断obj中是否含有cn
				if(hasClass(obj , cn)){
					//有，则删除
					removeClass(obj , cn);
				}else{
					//没有，则添加
					addClass(obj , cn);
				}
				
			}
			
		</script>
	</head>
	<body>
		
		<button id="btn01">点击按钮以后修改box的样式</button>
		
		<br /><br />
		
		<div id="box" class="b1 b2"></div>
```



#### JSON

- 就是一个`特殊格式的字符串`
- JSON在开发中主要用来数据的交互

```js
			 * 	- JS中的对象只有JS自己认识，其他的语言都不认识
			 * 	- JSON就是一个特殊格式的字符串，这个字符串可以被任意的语言所识别，
			 * 		并且可以转换为任意语言中的对象，
			 * 	- JSON
			 * 		- JavaScript Object Notation JS对象表示法
			 * 		- JSON和JS对象的格式一样，只不过JSON字符串中的属性名必须加双引号
			 * 			其他的和JS语法一致
			 * 		JSON分类：
			 * 			1.对象 {}
			 * 			2.数组 []
			 * 
			 * 		JSON中允许的值：
			 * 			1.字符串
			 * 			2.数值
			 * 			3.布尔值
			 * 			4.null
			 * 			5.对象
			 * 			6.数组
			 */
			
			//创建一个JSON对象
			var arr = '[1,2,3,"hello",true]';			
			var obj2 = '{"arr":[1,2,3]}';
			var arr2 ='[{"name":"孙悟空","age":18,"gender":"男"},{"name":"孙悟空","age":18,"gender":"男"}]';
			/*
			 * 将JSON字符串转换为JS中的对象
			 * 	在JS中，为我们提供了一个工具类，就叫JSON
			 * 	这个对象可以帮助我们将一个JSON转换为JS对象，也可以将一个JS对象转换为JSON
			 */

			/*
			 * json --> js对象
			 * 	 JSON.parse()
			 * 		- 可以将以JSON字符串转换为js对象
			 * 		- 它需要一个JSON字符串作为参数，会将该字符串转换为JS对象并返回
			 */
			var json = '{"name":"孙悟空","age":18,"gender":"男"}';
			var o = JSON.parse(json);
			var o2 = JSON.parse(arr);
			
			/*
			 * JS对象 ---> JSON
			 * 	JSON.stringify()
			 * 		- 可以将一个JS对象转换为JSON字符串
			 * 		- 需要一个js对象作为参数，会返回一个JSON字符串
			 */
			var obj3 = {name:"猪八戒" , age:28 , gender:"男"};			
			var str = JSON.stringify(obj3);
			
			/*
			 * JSON这个对象在IE7及以下的浏览器中不支持，所以在这些浏览器中调用时会报错
			 */

```





#### 数据类型

- 基本数据类型：
  - 具体的值存放在栈中

- 引用数据类型（复杂数据类型）：
  - 在栈中存放是指针，指针指向堆中，具体的值存放在堆中

#### var，let，const区别

var声明变量存在变量提升，let和const不存在变量提升

var 类型变量没有块级作用域，导致变量名冲突

let 类型变量具有块级作用域(以大括号为准则)，不属于全局变量，具有暂存死区特性（只要块级作用域内存在`let`命令，它所声明的变量就“绑定”（binding）这个块区域，不再受外部的影响）

```js
var tmp = 123;

if (true) {
   tmp = 'abc'; // ReferenceError
   let tmp;
}

//上面代码中，存在全局变量tmp，但是块级作用域内let又声明了一个局部变量tmp，导致后者绑定这个块级作用域，所以在let声明变量前，对tmp赋值会报错
```

`const` 类型变量具有块级作用域，用来定义常量`const`实际上保证的，并不是变量的值不得改动，而是变量指向的那个内存地址不得改动。对于简单类型的数据（数值、字符串、布尔值），值就保存在内存地址中，因此等同于常量。当改变值时创建新的内存地址存放值，那么原先的内存地址就变了。

但对于复合类型的数据（主要是对象和数组），变量指向的内存地址，保存的只是一个指针，`const`只能保证这个指针是固定的，至于它指向的数据结构是不是可变的，就完全不能控制了

例子：

```
const foo = {};//新建const常量，开辟一块内存地址用来存储变量值或者指针(对于复杂数据类型),foo存储的是一个地址，这个地址指向这个对象{}

// 为 foo 添加一个属性，可以成功
foo.prop = 123;
foo.prop // 123

// 将 foo 指向另一个对象，就会报错，因为新建了一个内存，改变地址指针指向
foo = {}; // TypeError: "foo" is read-only
```



#### async/await

`async` 是一个修饰符，调用`async` 定义的函数会默认的返回一个Promise对象(async定义的函数返回一个promise对象)，因此对async函数可以直接进行then操作,返回的值即为then方法的传入参数

**await** 关键字 只能放在 async 函数内部， await关键字的作用 就是获取 Promise中返回的内容， 获取的是Promise函数中resolve或者reject的值，如果await 后面并不是一个Promise的返回值，则会按照同步程序返回值处理

```
async/await是基于promises的语法糖


```

#### 事件三要素

事件源，事件类型，事件处理函数

##### 事件捕捉：

事件捕获会从document开始触发，一级一级往下传递，依次触发，直到真正事件目标为止。

##### 事件目标：

当到达目标元素之后，执行目标元素该事件相应的处理函数。如果没有绑定监听函数，那就不执行

##### 事件冒泡：

事件冒泡会从当前触发的事件目标一级一级往上传递，依次触发，直到document为止。(我们平时都是默认冒泡的，冒泡是一直冒到document根文档为止)

![1](C:\Users\Administrator\Desktop\1.jpg)

事件委托：

事件委托由事件冒泡原理实现，所谓的事件委托，不是给每个子元素节点增加事件监听器，而是给父元素节点增加事件监听器，利用冒泡原理从而由父元素事件去反过来影响并设置子元素节点。

```
<body>
    <ul>
        <li>知否知否，点我应有弹框在手！</li>
        <li>知否知否，点我应有弹框在手！</li>
        <li>知否知否，点我应有弹框在手！</li>
        <li>知否知否，点我应有弹框在手！</li>
        <li>知否知否，点我应有弹框在手！</li>
    </ul>
    <script>
        // 事件委托的核心原理：给父节点添加侦听器， 利用事件冒泡影响每一个子节点
        var ul = document.querySelector('ul');
        ul.addEventListener('click', function(e) {
            // alert('知否知否，点我应有弹框在手！');
            // e.target 这个可以得到我们点击的对象
            e.target.style.backgroundColor = 'pink';

        })
    </script>
</body>

//function(e) 中的e(event)是个形参(里面包含很多浏览器DOM页面发生的具体信息)，系统帮我们设定为事件对象，不需要传递实参过去。
当我们注册事件时， event 对象就会被系统自动创建，并依次传递给事件监听器（事件处理函数）。

```

![](F:\前端总结\个人总结文档\img\event.png)

通过监听一个父元素，来给不同的子元素绑定事件，减少监听次数，从而提升速度

##### 阻止事件冒泡：

在对应的元素的监听事件函数中添加：event.stopPropagation()

事件流：

事件发生时在元素节点之间按照特定顺序进行传播，这个传播过程称为事件流。可以是由外到里（事件捕捉），也可以是由里到外（事件冒泡）。其中包括：捕获阶段，目标阶段，冒泡阶段



#### 类数组和数组区别

- 相同点：都可用下标访问每个元素，都有length属性
- 不同点：类数组是一个普通对象类型，而真实的数组是`Array`类型
  - 数组遍历可以用 for in和for循环
  - 类数组只能用for循环遍历。

常见的类数组有: 函数的隐含参数 arguments, DOM 对象列表(比如通过 document.querySelectorAll 得到的列表), jQuery 对象 (比如 $(“div”)).

##### 类数组与数组的转化

###### 数组转变成类数组:

```js
//第一种方法
Array.prototype.slice.call(arrayLike, start);
//第二种方法
[...arrayLike];
//第三种方法:
Array.from(arrayLike);

```

#### 数组API

不改变原数组：

- 将数组转化为字符串（String）

```
var arr=[1,2,3];
var str=String(arr);
console.log(str); //1,2,3
console.log(arr); //[1,2,3]

```

- 把数组所有元素放入一个字符串join()
  - 含义：将数组元素连接起来以构建一个字符串

```js
<script type="text/javascript">
var arr = new Array(3)
arr[0] = "George"
arr[1] = "John"
arr[2] = "Thomas"
document.write(arr.join())//默认连接符为逗号
//'George,John,Thomas'为一个字符串
</script>
=========================================================
<script type="text/javascript">
var arr = new Array(3)
arr[0] = "George"
arr[1] = "John"
arr[2] = "Thomas"
document.write(arr.join("."))//连接符为原点号
//'George.John.Thomas'为一个字符串
</script>
```

- 数组拼接（concat）

```
var arr = [1,2,3];
var newArr = arr.concat(4,[5,6]);
console.log(newArr); //[1,2,3,4,5,6]
console.log(arr); //[1,2,3]

```

- 数组选取，获取子数组（slice 含头不含尾）

```
var arr=[1,2,3];
var newArr=arr.slice(0,2);
console.log(newArr); //[1,2]
console.log(arr); //[1,2,3]

```

- 返回某个指定的字符串值在字符串中首次出现的位置（indexOf）

```
var arr=[1,3,2];
var num=arr.indexOf(3); 
console.log(num); //1
console.log(arr); //[1,3,2]

```

改变原数组

- 从数组中添加/删除项目，然后返回`被删除的项目`（splice(i,n)从第i个开始的n个元素）

```js
var arr = [1,2,3];
var newArr1 = arr.splice(0,2);
var newArr2 = arr.splice(0,0,4,5);
console.log(newArr1); //[1,2]
console.log(newArr2);//[]
console.log(arr); //[4,5,3]

```

- 反转数组元素（reverse）

```js
var arr = [1,3,2];
var newArr = arr.reverse();
console.log(newArr); //[2,3,1]
console.log(arr); //[2,3,1]

```

- 对数组的元素进行排序（sort），`需要传递一个回调函数`

```
var arr=[1,3,2];
var newArr=arr.sort(return a-b ); //
console.log(newArr); //[1,2,3]
console.log(arr); //[1,2,3]

```

迭代方法（以下方法都不会修改数组中包含的值）：
every():对数组中的每一项运行给定的函数，如果该函数对每一项都返回true，则返回true。
filter():对数组中的每一项运行给定的函数，返回该函数会返回true的项组成的数组。
forEach():对数组中的每一项运行给定的函数。这个方法没有返回值。
map():对数组中的每一项运行给定的函数，返回每次函数调用的结果组成的数组。
some():对数组中的每一项运行给定的函数，如果该函数对任一项返回true，则返回true。

```js
var numbers=[1,2,3,4,5,4,3,1];
var everyResult=numbers.every(function(item,index,array){
   return (item>2);
})
console.log(everyResult); //false

var someResult=numbers.some(function(item,index,array){
   return (item>2);
})
console.log(someResult); //true

var filterResult=numbers.filter(function(item,index,array){
   return (item>2);
})
console.log(filterResult); //[3,4,5,4,3]

var mapResult=numbers.map(function(item,index,array){
   return item*2;
})
console.log(mapResult); //[2,4,6,8,10,8,6,2]

var sum=0;
var forEachResult=numbers.forEach(function(item,index,array){
   array[index] == item;   //true 
   sum+=item; 
})
console.log(sum); //23

```

#### apply,call,bind区别

共同点 :

-  都可以改变this指向 

不同点: 

-  call 和 apply 会调用函数, 并且改变函数内部this指向.
-  call 和 apply传递的参数不一样,call传递参数使用逗号隔开,apply使用数组传递
-  bind 不会调用函数执行, 但可以改变函数内部this指向. 

应用场景：

1. call 经常做继承.
2. apply经常跟数组有关系. 比如借助于数学对象实现数组最大值最小值 
3. bind 不调用函数,但是还想改变this指向. 比如改变定时器内部的this指向.

#### new的原理：

四个步骤：

1. 创建一个新对象；[var o = {};]
2. 将构造函数的作用域赋给新对象（因此this指向了这个新对象）；
3. 执行构造函数中的代码(为这个新对象添加属性)；
4. 返回新对象。

构造函数和自己实现new:

```js
//构造函数
function Person(name, age, job) {
        this.name = name;
        this.age = age;
        this.job = job;
        this.sayName = function () {
            alert(this.name);
        };
    }
 
 
//自己实现new
let New = function (P,...arguments) {
        let o = {};//创建新的对象
        
        o.__proto__ = P.prototype;//继承原型对象的方法
        P.prototype.constructor = P;
       
        P.apply(o,arguments);//将P构造函数的作用域赋给新对象(this指向o)，并传入参数arguments，执行P构造函数，对o对象添加P里包含的属性
        
        return o;
    };
let p1 = New(Person,"Ysir",24,"stu");
let p2 = New(Person,"Sun",23,"stus");
console.log(p1.name);//Ysir
console.log(p2.name);//Sun
console.log(p1.__proto__ === p2.__proto__);//true
console.log(p1.__proto__ === Person.prototype);//true
```

#### 创建函数的三种方法：

- 声明函数：

```
function sum1(n1,n2){
        return n1+n2;
    };
```

- 创建匿名函数表达式，又叫做函数字面量

```js
var sum2=function(n1,n2){
        return n1+n2;
};
```

- Function() 构造函数

```
var myFunction = new Function("a", "b", "return a * b");

var x = myFunction(4, 3);
//不推荐使用
```

#### 构造函数

- 定义：

在 JavaScript 中，用 new 关键字来调用的函数，称为构造函数。构造函数首字母一般大写



#### 作用域（scope）

##### 全局作用域：

- 定义在<script>标签中的js代码都是全局作用域
- 全局作用域在页面关闭时销毁
- 全局作用域中有一个全局对象window，它由浏览器创建
- 全局作用域的所有属性和方法都是window对的属性和方法



变量声明提前：

使用var声明的变量都会变量声明提前，变量声明提前的含义是当整个代码在执行前先将声明函数和var关键字的变量放置在代码最前面进行声明，但并不赋值，所以此时变量值是undefined。

```
console.log(a)
var a =10
//undefined

分析：上述两行当代码值执行时产生如下效果：
var a   //a 变量声明提前，但并未赋值
console.log(a)  //因此在这里打印的a的值是undefined
a = 10
```



函数声明提前：

- 使用`声明函数方法(function f1(){})`建立的函数是存在函数声明提前特性，使用`函数表达式`建立的函数则不会产生函数声明提前特性



##### 函数作用域：

- 调用函数时创建函数作用域，函数执行完毕，函数作用域销毁
- 每调用一次函数都建立一个新的函数作用域，之间互不影响
- 在函数作用域中可以访问到全局作用域变量
- 在全局作用域中无法访问到函数作用域
- 在函数作用域中操作一个变量时，先找函数自身作用域的内部是否有该变量，如果没有则向`上一级`作用域链查，如果还没有就报错
- 如果想在函数作用域中使用全局作用域的变量，则可以使用全局对象window下的属性进行直接访问
- 对于一个函数内也是存在变量声明提前特性，当前是把该函数当做一个小的全局环境，在函数中（小的全局环境）进行变量声明提前。同样也存在函数声明特性（当这个小的全局环境内部嵌套一个用`声明函数方法`建立的函数时）
- 在函数中不使用`var`关键字进行赋值的变量都变成`全局变量`
- 函数中定义了形参相当于在该函数内部最前面声明了该变量，但并未赋值。

```
var a = 22
function fun(){
	console.log(a);
	a = 10;
}
fun();//22
console.log(a)//10
---------------------------------------------
//在函数中使用`var`关键字进行赋值的变量都变成`局部变量`，且在该局部函数作用域中进行变量声明提前
var a = 22
function fun(){
	console.log(a);
	 var a = 10;
}
fun();//undefined
---------------------------------------------
//在函数中不使用`var`关键字进行赋值的变量都变成`全局变量`
var a = 22
function fun(){
	console.log(a);
	a = 10;
}
fun();//22
console.log(a)// 10   
---------------------------------------------
var a = 22
function fun(){
	console.log(a);
	var a = 10;
}
fun();//undefined
console.log(a)// 22


---------------------------------------------
var a = 12
function fun(b){
	console.log(b)
}
fun();//undefined
fun(2)//2
```

`不论变量还是函数，所定义时的所在的作用域很重要!!!!`下面是一些关于作用域的面试题,`较难`

```js
var x = 10;
function fn() {
    console.log(x)
}
function show(f) {
    var x= 20;
    f();
}
show(fn);  //10
//fn函数是定义在全局作用域，当show函数调用fn函数时，并没有向fn函数传入参数，且fn函数本身也没有要传入的参数，找到fn函数最初的定义位置为全局作用域，那么就在全局作用域里找要打印的x变量
--------------------------------------
var fn = function () {
    console.log(fn)
}
fn();    //fn = function () {
           console.log(fn)
            }
=============================           
            
var obj = {
    fn2:function () {
        console.log(fn2);
    }
}
obj.fn2();//error

```





#### this

- 代码解析器每次调用函数时，都会向函数内部传入一个隐含参数`this`，
- `this`指向的是一个对象
- 这个对象是该函数执行时的`上下文对象`
- 根据函数调用的方式不同，`this`指向也不同
  1. 以函数形式调用时，`this`指向window对象
  2. 以对象的方法调用时，`this`指向调用该方法的那个对象
  3. 当以构造函函数调用时，this指向的是新创建的对象
  4. 当以call(),apply(),bind()方法调用时，this指的是调用该函数时传入的形参，因此在这里可以使用前述方法更改函数执行时的this指向

#### 对象

创建对象方法：

- 工厂方法创建对象

  - 特点该方法都是使用`object()构造函数`创建一个新的对象，所产出的obj1,obj2对象的类型都是Object类型，无法区分出类型obj1和obj2对象的类型，也即是工厂方法生产出的对象一样，没类别可分性。

  ```js
  function creatperson(name,age,gender)
  {
  	var obj = new Object(); //new一个新对象
  	obj.name = name;
  	obj.age = age;
  	obj.gender = gender;
  	obj.sayname = function(){
  		console.log(this.name);
  	}
  	return obj
  }
  
  var person1 = creatperson('lisi',13,male);
  var person2 = creatperson('wangwu',15,male);
  
  ----------------------------------------------------
  function creatdog(name,age,gender)
  {
  	var obj = new Object(); //new一个新对象
  	obj.name = name;
  	obj.age = age;
  	obj.gender = gender;
  	obj.sayname = function(){
  		console.log(this.name);
  	}
  	return obj
  }
  
  var dog1 = creatodog('xiaohu',3,male);
  var dog2 = creatodog('xiaolang',1,male);
  
  //上述两个工厂模式产生出对象(person1,person2,dog1,dog2)都是object类型,无法分类别
  ```

- 构造函数方法

  构造函数是一种函数，目的是用来创建对象的，构造函数需要首字母大写，在调用构造时需要new关键字，调用不同的构造函数所产出的对象是具有不同的类别，`一个构造函数就是对应一个类`。

  - 构造函数执行流程:
    1. 立即创建新的对象
    2. 将新建的对象设置为构造函数中的this，在构造函数中可以引用this为新的对象添加属性和方法
    3. 逐行执行构造函数中的代码 
    4. 返回创建的对象

  ```js
  function Person(name,age){
  	this.age = age;
  	this.name = name;
  	this.sayname(){
  		console.log(this.name)
  	}
  }
  var person1 = new Person('zs',13);
  var person2 = new Person('li',13);
  ---------------------------------------------------
  
  function Dog(name,age){
  	this.age = age;
  	this.name = name;
  	this.sayname(){
  		console.log(this.name)
  	}
  }
  var dog1 = Dog('wanwgang',1);
  var dog2 = Dog('xiaogou',3);
  //构造函数产出的对象person1,person2对应Person构造函数类，dog1,dog2对象对应Dog构造函数类，
  `一个构造函数就是对应一个类`
  //person1,person2独享对象属于Person类
  //dog1,dog2独享对象属于dog类
  //但Person构造函数(Person类)和Dog构造函数(Gog类),但(Person类),(Gog类)都属于Object的实例(Object相当于人类的亚当和夏娃)
  
  //`一个构造函数就是对应一个类`
  //使用instanceof 方法可以判别一个对象是否属于一个构造函数(类)实例
  // object instanceof constructor
  //对象 instanceof 构造函数（类）
  console.log(person1 instanceof Person)//true
  console.log(person2 instanceof Person)//true
  console.log(dog1 instanceof Dog)//true
  console.log(dog2 instanceof Dog)//true
  console.log(dog1 instanceof Person)//False
  console.log(dog1 instanceof Object)//true
  
  ```
  
- 构造函数存在问题
  
  在上述代码中每次调用构造函数就会开辟一个新的内存，并且构造函数内的方法都会被重新保存到新建的对象中，试想建立一万个新的对象，那么这一万个对象都包含这个相同的方法，虽然各自是各自的，但是占用很大内存。（**无法函数复用**）
  
- 解决方案：在构造函数的原型对象`prototype`属性中加入公共方法，每个实例对象通过原型链就可以对
  
- 这些公共方法访问,
  
  ```js
  //方法1，将构造函数方法进行放置到全局作用域
  function Person(name,age){
  	this.age = age;
  	this.name = name;
      this.sayname = fun; 
  	}
  }
  function fun() {
  	console.log(this.name)
  }//对Person原型添加方法
  
  var person1 = new Person('zs',13);
  var person2 = new Person('li',13);
  console.log(person1.sayname == person2.sayname)//true
  //但方法1存在外置方法fun()，会污染全局作用域，代码安全性不高，不建议随便在全局作用域设置对象的方法
  
  ============================================
  //原型
  //创建任何一个函数时，解析器都会给该函数增加一个`prototype`属性，这属性是个对象
  //不同函数创建时有各自不同的`prototype`，
  function Person(){}
  function Fun(){}
  console.log(Person.prototype == Fun.prototype)//False
  
  //当`prototype`通过普通函数调用时，没有任何作用
  //当`prototype`通过构造函数调用时，由构造函数建立的新对象实例里包含一个隐含属性`__proto__`来指向构
  //造函数的`prototype`属性

  function Person(){
}
  var person1 = new Person();
var person2 = new Person();
  console.log(person1.__proto__ == Person.prototype);//True
  console.log(person2.__proto__ == Person.prototype);//True   
  
  //构造函数的原型对象就相当于一个公共区域，这个类(构造函数)的所有实例都可以通过`__proto__`属性去访问构造函数(类)的原型，因此可以在以后将公共的属性和方法都放在原型中，方便所有的实例去访问，并且不会污染全局作用域
  
  
  
  
  
  //方法2，设置构造函数原型
  function Person(name,age){
  	this.age = age;
  	this.name = name;
  	}
  }
  Person.prototype.sayname = function () {
  	console.log(this.name)
  }//对Person原型添加方法
  
  var person1 = new Person('zs',13);
  var person2 = new Person('li',13);
  var person3= new Person('ed',13);
  
  console.log(person1.sayname === person2.sayname)//true
  console.log(person1.sayname === Person.prototype.sayname)//true
  
  //实例对象person1.__proto__指向的就是Person构造函数的原型：
  //同样实例对象person2.__proto__指向的也是Person构造函数的原型：
  //person1.__person__ == Person.prototype
  //person2.__person__ == Person.prototype
  
  //因此当使用构造函数方法创建对象时，将属性等信息放在构造函数中，方法放到构造函数的原型中，当创建大量对象实例时节省内存，通过构造函数原型即可以访问到构造函数内部共享的方法。
  
  //建立的每个实例对象在调用方法/或者属性时，先判断自身否包含该方法，若没有则去构造函数的原型中寻找，可以通过原型链一直向上查找，一直找到Object(亚当和夏娃)的原型为止，如果还是没有找到就输出undefined。
  
  //建立的每个实例对象判断自身是否包含一些属性或者方法时采用`.hasOwnproperty(属性/方法)`person1.hasOwnProperty(‘属性名’)
  //建立的每个实例对象判断自身以及原型否包含一些属性可以用 `in`:(属性名 in 对象实例)
  
  
  //当原型的方法不满足实例的需要时，可以为实例自定义方法，当这个自定义的方法与原型中的方法命名出现冲突，肯定去执行实例本身的那个方法，也所谓自个有就是用自个的，当没有时再去原型里查找是否有对应的方法。
  
  // function Person(age,name){
  	this.name = name;
  	this.age = age;
  }
  var person1 = new Person(12,'lisi');
  var result = person1.toString()// toSting()方法是Person原型中的方法，不满足实例对象person1的需求
  person1.toString = function(){
      console.log(this.name + '????');
  }//为实例对象person1设置自身的自定义方法`toString()`,只有自个才能访问到，实例对象以后都是以此方法代替原型中`toString()`方法的执行，但在原型中`toString()`方法依然存在，依然为其它实例提供服务
  ```
  
  #### 垃圾回收：
  
  只需要将不再使用的变量赋值为`null`即可
  
  
  
  ```js
  var obj = {};
  obj = null;
  ```
  
  

#### arguments

- 每次调用函数，都会传入两个隐含参数：`this`,`arguments`

- 其中`arguments`是一个类数组对象，类数组可以通过索引读取，也可以获得长度

- `arguments`包含了传入函数的实参

- `arguments.length()`可以获得真参长度

- 调用函数时可以不适用形参，调用`arguments`伪数组可以获取传入函数的实参，但是一般不这样，太麻烦了

- `arguments[0]` 是第一个传入的实参

- `arguments[1]`是第二个传入的实参

  - `arguments`中包含一个`callee`属性,还属表示当然正在执行的函数是谁？

    ```js
    function fun(){
    		console.log(arguments instanceof Array);//False
        	console.log(Array.isArray(arguments));//False
        	console.log(arguments[0]);
        	console.log(arguments.length);
        	console.log(arguments.callee == fun)//True
    
    }
    ```

#### 包装类

```js
//基本数据类型
// Undefined Null Number String Boolean
//引用数据类型
// object

//在js中提供三种包装类，可以将基本数据类型转化为对象
--String()
     -可以将基本数据类型的字符串转换为String对象
--Number()
     -可以将基本数据类型的数字转化为Number对象
--Boolean()
     -可以将基本数据类型布尔值转化为布尔对象

var a = new Number(3);
var b = new String('abc');
var c = new Boolean(true);
console.log(typeof a);// object
console.log(typeof b);// object
console.log(typeof c);// object

a.hello = hello;
console.log(a.hello)//hello
=========================================
var a = 123;  //基本数据类型
a = a.toString();//浏览器临时使用包装类，将a变量转换成对象，再调用方法和属性，那么a此时变为字符串类型，且刚刚的临时对象立即销毁
console.log(a.hello)//undefined//在对a的helo属性查找时，首先用临时包装类将a转化成临时对象，再去这个临时对象中寻找hello属性，并未发现这个属性，输出undefined


=========================================
var a = 123;  //基本数据类型
a = a.toString();//浏览器临时使用包装类，将a变量转换成对象，再调用方法和属性，那么a此时变为字符串类型，且刚刚的临时对象立即销毁
a.hello = 'nihao'//浏览器临时使用包装类，将a变量转换成字符串对象，再调用方法和属性，那么a此时变为字符串类型，且刚刚的临时对象立即销毁
console.log(a.hello)//undefined//在对a的helo属性查找时，首先用临时包装类将a转化成临时对象，再去这个临时对象中寻找hello属性(上面那个定义的a.hello = hello属性对象早就销毁了)，并未发现这个属性，输出undefined



```

#### 继承

##### 1.原型链继承

- 原理：**把父类的实例作为子类的原型**(利用原型让一个引用类型继承另一个引用类型的属性和方法)

- ```js
  //父类型
  function Person(name, age) {
      this.name = name,
          this.age = age,
          this.play = [1, 2, 3]
      this.setName = function () { }
  }
  Person.prototype.setAge = function () { }
  //子类型
  function Student(price) {
      this.price = price
      this.setScore = function () { }
  }
  Student.prototype = new Person() // 子类型的原型为父类型的一个实例对象
  var s1 = new Student(15000)
  var s2 = new Student(14000)
  console.log(s1,s2)
  ```

- 优点：简单易于实现，父类的新增方法/属性子类都能访问

- 缺点：

  - 多个实例对引用类型的操作会被篡改(父类私有属性)(继承单一，无法多继承)
  - 子类型的原型上的 constructor 属性被重写了
  - 给子类型原型添加属性和方法必须在替换原型语句之后
  - 在创建子类型的实例时，没有办法在不影响所有实例的情况下，向父类型的构造函数传递参数

##### 2.借用构造函数继承(伪造对象继承，经典继承)

- 原理：复制父类的实例属性给子类(:**在子类型构造函数中调用call()调用父类型构造函数**)

- ```js
  function Person(name, age) {
      this.name = name,
          this.age = age,
          this.setName = function () {}
  }
  Person.prototype.setAge = function () {}
  
  function Student(name, age, price) {
      Person.call(this, name, age)  // 相当于: this.Person(name, age)
      /*this.name = name
      this.age = age*/
      this.price = price
  }
  var s1 = new Student('Tom', 20, 15000)
  ```

- 优点：

  - 子类构造函数可以向向父类构造函数中传递参数
  - 可以实现多继承（call或者apply多个父类）

- 缺点：

  - 方法都在构造函数中定义，无法函数复用(**在构造函数中定义的方法都无法复用**)
  - 不能继承父类原型属性/方法，只能继承父类实例的属性/方法

##### 3.组合继承

- 原理：通过调用父类构造函数，继承父类的属性并保留传参的优点，然后通过将父类实例作为子类原型，实现函数复用

- ```js
  function Person(name, age) {
      this.name = name,
          this.age = age,
          this.setAge = function () { }
  }
  Person.prototype.setAge = function () {
      console.log("111")
  }
  
  function Student(name, age, price) {
      Person.call(this,name,age)      //借用父类的构造函数继承属性
      this.price = price
      this.setScore = function () { }
  }
  
  Student.prototype = new Person()      //继承父类实例作为子类原型实现方法(函数)复用
  Student.prototype.constructor = Student//组合继承也是需要修复构造函数指向的
  Student.prototype.sayHello = function () { }
  var s1 = new Student('Tom', 20, 15000)
  var s2 = new Student('Jack', 22, 14000)
  console.log(s1)
  console.log(s1.constructor) //Student
  console.log(p1.constructor) //Person
  ```

- 优点

  - 可以继承父类实例属性，也可以继承父类原型方法
  - 不存在引用属性共享问题
  - 可传参
  - 函数可复用

- 缺点：
  
  - 调用了两次父类构造函数，生成了两份实例

##### 4.原型式继承(浅复制继承)

- 原理：利用一个空对象作为中介，将某个被继承对象直接赋值给空对象构造函数的原型

  ```js
  function object(Person) {
    function Son() {};
   
    Son.prototype = Person;
  
    return new Son();
  }
  ```

  

- 缺点：(与原型链继承类似)

  - 原型式继承多个实例的引用类型属性指向相同，存在篡改的可能。
  - 无法传递参数

##### 5.寄生式继承

- 原理：在原型式继承的基础上，增强对象方法，返回构造函数

  ```js
  function createAnother(original){
      var clone = object(original); // 通过调用 object() 函数创建一个新对象
      clone.sayHi = function(){  // 以某种方式来增强对象，方法无法复用
          alert("hi");
      };
      return clone; // 返回这个对象
  }
  
  ```

  

- 缺点：

  - 原型链继承多个实例的引用类型属性指向相同，存在篡改的可能。
  - 无法传递参数，方法无法复用

##### 7.寄生组合式继承

- 原理：即通过借用构造函数来继承父类属性，通过原型链的混成形式来继承父类方法，其背后的基本思路是：不必为了指定子类型的原型而调用超类型的构造函数，我们所需要的无非就是超类型原型的一个副本而已。本质上，就是使用寄生式继承来继承超类型的原型，然后再将结果指定给子类型的原型

  ```js
  function inheritPrototype(subType, superType){
    var prototype = Object.create(superType.prototype); // 创建对象，创建父类原型的一个副本
    prototype.constructor = subType;                    // 增强对象，弥补因重写原型而失去的默认的constructor 属性
    subType.prototype = prototype;                      // 指定对象，将新创建的对象赋值给子类的原型
  }
  
  // 父类初始化实例属性和原型属性
  function SuperType(name){
    this.name = name;
    this.colors = ["red", "blue", "green"];
  }
  SuperType.prototype.sayName = function(){
    alert(this.name);
  };
  
  // 借用构造函数传递增强子类实例属性（支持传参和避免篡改）
  function SubType(name, age){
    SuperType.call(this, name);
    this.age = age;
  }
  
  // 将父类原型指向子类
  inheritPrototype(SubType, SuperType);
  
  // 新增子类原型属性
  SubType.prototype.sayAge = function(){
    alert(this.age);
  }
  
  var instance1 = new SubType("xyc", 23);
  var instance2 = new SubType("lxy", 23);
  
  instance1.colors.push("2"); // ["red", "blue", "green", "2"]
  instance1.colors.push("3"); // ["red", "blue", "green", "3"]
  
  ```

- 优点：这个例子的高效率体现在它只调用了一次`SuperType` 父类构造函数，并且因此避免了在`SubType.prototype` 上创建不必要的、多余的属性。于此同时，原型链还能保持不变；因此，还能够正常使用`instanceof` 和`isPrototypeOf()`，使用很多。
- 

##### 8.ES6类extends继承

- 

```js
//父类
class Person{
    constructor(skin,language){
        this.skin=skin;
        this.language=language;
    }
    say(){
        console.log('I am a Person')
    }
}
===========================================
//继承
class Chinese extends Person{
    constructor(skin,language,positon){
    	//console.log(this);//报错
         super(skin,language);
        //super();
        //console.log(this);调用super后得到了this，不报错
         this.positon=positon;
        }
        aboutMe(){
            console.log(this.skin+' '+this.language+' '+this.positon);
        }
    }
```



##### JS中三个等号区别

- 两个等号(==)和三个等号(===)的区别：


1. "=="表示：equality -> 等同  的意思，"=="使用两个等号时，如果两边值的类型不同的时候，是要先先进行`类型转换后`，`才能做比较`。

2. "==="表示：identity -> 恒等 的意思，"==="使用三个等号时，是`不需要做类型转换的`，如果两边值的类型不同，就表示一定是不等的


#### 浏览器中输入URL后的事情

#####  1.DNS域名解析

- 在浏览器DNS缓存中搜索
- 在操作系统DNS缓存中搜索
- 读取系统hosts文件，查找其中是否有对应的ip
- 向本地配置的首选DNS服务器发起域名解析请求

##### 2.建立TCP连接

- 为了准确地传输数据，TCP协议采用了三次握手策略。发送端首先发送一个带SYN（synchronize）标志的数据包给接收方，接收方收到后，回传一个带有SYN/ACK(acknowledegment)标志的数据包以示传达确认信息。最后发送方再回传一个带ACK标志的数据包，代表握手结束。在这过程中若出现问题中断，TCP会再次发送相同的数据包。
   **TCP是一个端到端的可靠的面向连接的协议，所以HTTP基于传输层TCP协议不用担心数据的传输的各种问题。**

##### 3. 发起HTTP请求

- 请求方法：
- - GET:获取资源
  - POST:传输实体主体
  - HEAD:获取报文首部
  - PUT:传输文件
  - DELETE:删除文件
  - OPTIONS:询问支持的方法
  - TRACE:追踪路径

##### 4. 接受响应结果

状态码：

- 1**：信息性状态码
- 2**：`成功状态码`
   200：OK 请求正常处理
   204：No Content请求处理成功，但没有资源可返回
   206：Partial Content对资源的某一部分的请求
- 3**：`重定向状态码`
   301：Moved Permanently 永久重定向
   302：Found 临时性重定向
   304：Not Modified 缓存中读取
- 4**：`客户端错误状态码`
   400：Bad Request 请求报文中存在语法错误
   401：Unauthorized需要有通过Http认证的认证信息
   403：Forbidden访问被拒绝
   404：Not Found无法找到请求资源
- 5**：`服务器错误状态码`
   500：Internal Server Error 服务器端在执行时发生错误
   503：Service Unavailable 服务器处于超负载或者正在进行停机维护



##### 5. 浏览器解析html

- 浏览器按**顺序解析html**文件，构建**DOM树**，在解析到外部的**css和js文件**时，向服务器发起**请求下载资源**，若是**下载css文件**，则解析器会在异步下载的同时**继续解析**后面的html来构建**DOM树**，**但在下载js文件和执行**它时，解析器会**停止对html的解析**。这便出现了**js阻塞问题**。所以在平时的代码中，
  - js是放在html文档末尾的
  - 也可以在<script>标签中设置 `defer`属性(告诉浏览器立即下载，但延迟执行)，延迟脚本运行
  - 设置<script>标签中设置`async`属性，不保证多个脚本加载顺序，起到异步加载脚本和布局页面效果

```js
###### tip:

#####  预加载器

资源预加载是另一个**性能优化技术**，我们可以使用该技术来预先告知浏览器某些资源可能在将来会被使用到。**预加载简单来说就是将所有所需的资源提前请求加载到本地，这样后面在需要用到时就直接从缓存取资源**

##### 为什么要预加载：

在网页全部加载之前，对一些主要内容进行加载，以提供给用户更好的体验，减少等待的时间。否则，如果一个页面的内容过于庞大，没有使用预加载技术的页面就会长时间的展现为一片空白，直到所有内容加载完毕。

##### 实现预加载的几种办法

- 使用html标签

  ```js
  <script src="./myPreload.js"></script>
```

- 使用img标签

  ```js
  <img src="http://pic26.nipic.com/20121213/6168183 0044449030002.jpg" style="display:none"/>
  ```

###### /tip


```



解析过程中，浏览器首先会**解析HTML文件**构建**DOM树**，然后解析CSS文件构建CSSOM**渲染树**，等到渲染树构建完成后，浏览器开始**布局渲染树并将其绘制到屏幕上**。这个过程比较复杂，涉及到两个概念: **reflow**(回流)和**repain**(重绘)。

- **回流**　　

  DOM节点中的各个元素都是以盒模型的形式存在，这些都需要浏览器去计算其位置和大小等，这个过程称为reflow;

- **重绘**

  当盒模型的位置,大小以及其他属性，如颜色,字体,等确定下来之后，浏览器便开始绘制内容，这个过程称为repain。

  页面在首次加载时必然会经历reflow和repain。reflow和repain过程是非常消耗性能的，尤其是在移动设备上，它会破坏用户体验，有时会造成页面卡顿。所以我们应该尽可能少的减少reflow和repain。

##### JS解析：

- JS的解析是由浏览器中的JS解析引擎完成的，比如谷歌的是V8。JS是单线程运行，也就是说，在同一个时间内只能做一件事，所有的任务都需要排队，前一个任务结束，后一个任务才能开始。但是又存在某些任务比较耗时，如IO读写等，所以需要一种机制可以先执行排在后面的任务，这就是：同步任务(synchronous)和异步任务(asynchronous)。

- 　　JS的执行机制就可以看做是一个**主线程**加上一个**任务队列**(task queue)。同步任务就是放在主线程上执行的任务，异步任务是放在任务队列中的任务。所有的同步任务在主线程上执行，形成一个执行栈;异步任务有了运行结果就会在任务队列中放置一个事件；脚本运行时先依次运行执行栈，然后会从任务队列里提取事件，运行任务队列中的任务，这个过程是不断重复的，所以又叫做事件循环(Event loop)

<img src="F:\前端总结\个人总结文档\JS-V8执行栈.png" style="zoom:80%;" />

####  防抖和节流

- **防抖(debounce)**
- 定义
  - 对于**短时间内连续触发**的事件（例如下面监听浏览器滚动事件），**防抖的含义就是让某个时间期限（如上面的1000毫秒）内，事件处理函数只执行一次**

- 场景：
  - 现在抽象出一个功能需求-- **监听浏览器滚动事件，返回当前滚条与顶部的距离**基于上述场景，首先提出第一种思路：**在第一次触发事件时，不立即执行函数，而是给出一个期限值比如200ms**，然后：
    - 如果在200ms内没有再次触发滚动事件，那么就执行函数
    - 如果在200ms内再次触发滚动事件，那么当前的计时取消，重新开始计时

- 效果：如果短时间内大量触发同一事件，只会执行一次函数。

- 实现：既然前面都提到了计时，那实现的关键就在于`setTimeout`这个函数，由于还需要一个变量来保存计时，考虑维护全局纯净，可以借助闭包来实现：

​```js
/*
* fn [function] 需要防抖的函数
* delay [number] 毫秒，防抖期限值
*/
function debounce(fn,delay){
    let timer = null //借助闭包
    return function() {
        if(timer){
            clearTimeout(timer) //进入该分支语句，说明当前正在一个计时过程中，并且又触发了相同事件。所以要取消当前的计时，重新开始计时
            timer = setTimeout(fn,delay) 
        }else{
            timer = setTimeout(fn,delay) // 进入该分支说明当前并没有在计时，那么就开始一个计时
        }
    }
}
/*****************************简化后的分割线 ******************************/
function debounce(fn,delay){
    let timer = null //借助闭包
    return function() {
        if(timer){
            clearTimeout(timer) 
        }
        timer = setTimeout(fn,delay) // 简化写法
    }
}
// 然后是旧代码
function showTop  () {
    var scrollTop = document.body.scrollTop || document.documentElement.scrollTop;
　　console.log('滚动条位置：' + scrollTop);
}
window.onscroll = debounce(showTop,1000) // 为了方便观察效果我们取个大点的间断值，实际使用根据需要来配置

```

- **节流(throttle)**
  - 继续思考，使用上面的防抖方案来处理问题的结果是：
    - 如果在限定时间段内，不断触发滚动事件（比如某个用户闲着无聊，按住滚动不断的拖来拖去），只要不停止触发，理论上就永远不会输出当前距离顶部的距离。
    - **但是如果产品同学的期望处理方案是：即使用户不断拖动滚动条，也能在某个时间间隔之后给出反馈呢**
    - 我们可以设计一种**类似控制阀门一样定期开放的函数，也就是让函数执行一次后，在某个时间段内暂时失效，过了这段时间后再重新激活**（类似于技能冷却时间
- 定义：让持续发生的事件一定间隔再执行对应的回调函数

- 效果：
  
- 如果短时间内大量触发同一事件，那么**在函数执行一次之后，该函数在指定的时间期限内不再工作**，直至过了这段时间才重新生效
  
- 实现：

  - 这里借助`setTimeout`来做一个简单的实现，加上一个状态位`valid`来表示当前函数是否处于工作状态：

    ```js
    function throttle(fn,delay){
        let valid = true
        return function() {
           if(!valid){
               //休息时间 暂不接客
               return false 
           }
           // 工作时间，执行函数并且在间隔期内把状态位设为无效
            valid = false
            setTimeout(() => {
                fn()
                valid = true;
            }, delay)
        }
    }
    /* 请注意，节流函数并不止上面这种实现方案,
       例如可以完全不借助setTimeout，可以把状态位换成时间戳，然后利用时间戳差值是否大于指定间隔时间来做判定。
       也可以直接将setTimeout的返回的标记当做判断条件-判断当前定时器是否存在，如果存在表示还在冷却，并且在执行fn之后消除定时器表示激活，原理都一样
        */
    
    // 以下照旧
    function showTop  () {
        var scrollTop = document.body.scrollTop || document.documentElement.scrollTop;
    　　console.log('滚动条位置：' + scrollTop);
    }
    window.onscroll = throttle(showTop,1000) 
    ```

- 结果
  
  - 如果一直拖着滚动条进行滚动，那么会以1s的时间间隔，持续输出当前位置和顶部的距离



#### 强制缓存/协商缓存

强制缓存

- 强制缓存整体流程比较简单，就是在第一次访问服务器取到数据之后，在过期时间之内不会再去重复请求。实现这个流程的核心就是如何知道当前时间是否超过了过期时间。

- 强制缓存的过期时间通过第一次访问服务器时返回的响应头获取。在 `http 1.0` ( `Expires` 响应头)和 `http 1.1` ( `Cache-Control` 响应头)版本中通过不同的响应头字段实现。

强制缓存特点：

- 强制缓存只有首次请求才会跟服务器通信，读取缓存资源时不会发出任何请求，资源的 `Status` 状态码为 `200`，资源的 `Size` 为 `from memory` 或者 `from disk` ，http 1.1 版本的实现优先级会高于 http 1.0 版本的实现。

协商缓存

- 协商缓存与强制缓存的不同之处在于，协商缓存每次读取数据时都需要跟服务器通信，并且会增加缓存标识。在第一次请求服务器时，服务器会返回资源，并且返回一个资源的缓存标识，一起存到浏览器的缓存数据库。当第二次请求资源时，浏览器会首先将缓存标识发送给服务器，服务器拿到标识后判断标识是否匹配，如果不匹配，表示资源有更新，服务器会将新数据和新的缓存标识一起返回到浏览器；如果缓存标识匹配，表示资源没有更新，并且返回 `304` 状态码，浏览器就读取本地缓存服务器中的数据

协商缓存特点：

- 协商缓存每次请求都会与服务器交互，第一次是**拿数据**和**标识**的过程，第二次开始，就是浏览器询问服务器**资源是否有更新**的过程。每次请求都会传输数据，如果命中缓存(第二次资源与本地缓存第一次缓存资源一致)，则资源的 `Status` 状态码为 `304` 而不是 `200` 。同样的，一般来讲为了兼容，两个版本的协商缓存都会被实现，`http 1.1` 版本的实现优先级会高于 `http 1.0` 版本的实现。

#### innerHTML/innerText区别

**innerHTML**指的是从对象的起始位置到终止位置的全部内容**,包括html标签**。
**innerText**  指的是从起始位置到终止位置的内容,但它**去除html标签**。

#### [WEB前端性能优化总结——如何提高网页加载速度]

网页加载顺序：1.DNS查找 > 2.下载并渲染HTML文件 > 3.下载并执行css及js组件 > 4.下载图片

- 减少**DNS**查找
  
  - 一般而言，电脑会进行DNS缓存，包括浏览器缓存、系统缓存、路由器缓存、ISP DNS缓存。所以，浏览器DNS查找顺序一般是这样的：浏览器缓存→系统缓存→路由器缓存→ISP DNS 缓存→递归搜索。而每一个DNS查找，需要耗时20-120ms
- 减少**HTTP**请求，即客户端到服务器端的请求消息，包括资源请求、数据处理等。
  - HTTP请求需从客户端发起请求，然后由服务器端进行数据处理，然后再返回数据或资源。一般而言，耗时据请求资源的大小，服务器网速，约**数ms-数百ms**之间。请求资源越大，所花费的时间越长，服务器网速越慢，所花费的时间也越长。
  - 一般而言，完成了DNS查找后，接下来便是进行HTTP请求，获取资源。首先下载HTML文件，然后解析HTML文件，根据HTML内容，获取CSS、JS及图片文件。每一个CSS链接、JS链接以及图片链接都是一个HTTP请求。
  - 每一个HTTP请求都需要花费额外的时间。因此，我们可以将一些可合并的资源进行合并，譬如将所有页面的css合并成一个style.css文件，譬如将所有页面的js合并成一个function.js文件，再譬如**将一批小图标利用ps合成一张图片（此手段效果最显著，也最常用）**
- CSS**优先加载**，JS延迟加载
  - 在解析HTML文件，构建DOM树时，一旦遇到link标记时，即遇到了CSS样式表，将之下载，便可立即构建渲染树，从而立即呈现页面效果。
  - 而一旦遇到script 标记时，即遇到了JS脚本，将立即阻塞DOM树的构建，将控制权移交给 JavaScript 引擎，等到 JavaScript 引擎运行完毕，浏览器才会从中断的地方恢复渲染树的构建。这涉及到浏览器渲染原理
  - 若将引入JS脚本的链接放到HTML页面顶部，那么在加载该页面时，一旦遇到JS，页面渲染就会停滞，出现一段时间的灰色空白，直到JS加载完成，才会出现页面内容，这对用户体验是不友好的。因此，我们需要将JS脚本放置到页面底部，或者让JS脚本异步或是延迟加载。

- **缩小文件**

- **善于利用缓存**

  　　避免在HTML文件中使用style标签插入CSS样式，及使用script标签插入JS脚本。若在HTML文件中插入CSS及JS，那么它们无法进入缓存，每次刷新页面，都要重新加载，不但浪费了浏览器资源，拖慢了页面加载速度，而且显得冗余且复用性低，不利于日后的维护。因此，将CSS样式与JS脚本分离出来，形成CSS文件及JS文件，就能进入缓存，进而提高页面加载速度。

    　　灵活使用cookie和localstorage。在使用接口时，灵活使用cookie和localstorage来缓存接口返回的信息，避免不必要的接口查询，从而提升页面加载速度。譬如：在登录页面登录时，缓存好用户信息，设置过期时间。在进入用户个人中心页面时，若数据并未过期，可以直接从缓存中取用户信息，不必再调起接口去获取用户信息。　**实例：css、js、图片都可进行缓存，从缓存中获取文件，时间为0ms。**

- HTML文件代码优化

  　　　　1. 避免使用空请求，包括空的href链接、空src链接。空链接本身无法请求成功，因此会把一个HTTP请求拖到超时，而且空链接会阻塞页面中其他资源的下载进程，会拖慢页面加载速度。譬如：<img src="" alt="">。

  　　　　2. 根据项目大小，选择主要使用class还是id。id选择器优先级最高，访问速度最快。但是在html中每声明一个id，就会在JS底层声明一个全局变量，而全局变量的增多，将会拖慢JS中变量遍历的效率，若变量遍历达到十万次以上，就会出现较显著的延迟，而且容易造成全局变量污染。对于小项目，并无影响，但是对中大型项目来说，尤其是游戏项目，影响很大。个人推荐，当项目较小时，灵活使用class和id，当项目较大时，尽量少使用id。

  　　　　3. 预先设定图片大小。在页面加载过程中，图片最后加载，若不对图片预设大小，当图片加载完成后，将会引起大量的重排，将会浪费浏览器资源及拖慢页面加载速度。

  　　　　4. 尽量减少DOM元素的数量与层级。解析HTML时，标签的数量越多，标签的层级越深，浏览器解析构建DOM树的时间就越长，应尽可能的减少DOM元素的数量和层级。

  　　　　5. 尽量避免使用table标签。浏览器对table标签的解析是全部生成后再一次性绘制的，因此会造成表格位置较长时间的空白，推荐使用ul及li标签绘制表格。

  　　　　6. 使用异步加载iframe标签。浏览器加载iframe标签时，会阻塞父页面渲染树的构建及HTTP请求，因此尽量使用异步加载iframe。

  　　　　等等…

- CSS样式代码优化

  　　　　1. 禁止使用样式表达式。CSS表达式从IE5起开始支持，但仅有IE支持。它的解析速度较慢，而且运算次数远比我们想象的要大，随意动动鼠标就能轻松达到上万次运算，会对页面性能造成影响。譬如：**"**#myDiv{width:expression(document.body.offsetWidth - 110 + "px"); }**"**

   　　　2. 优化关键选择器，去掉无效的父级选择器，尽量少在选择器末尾使用通配符。大多数人都认为，浏览器对CSS选择器的解析式从左往右进行的，譬如选择器：**"**#myDiv ul li a**"**，大多数人会认为这个选择器效率极高，毕竟第一个ID #myDiv 就已经把范围限定了，先选择 #myDiv ，再在 #myDiv 下寻找 ul ，再一级一级往下，直到找到 a 标签，效率很高。事实上这是错的，浏览器对CSS选择器的解析式从右往左进行的。在上述选择器中，浏览器会先去寻找 a 标签，范围为全局，再在 a 标签的列表中，寻找父级标签是 li 标签的 a 标签，一直向上，直到最后，找到父级标签是 #myDiv ul li 的a标签。因此，效率并不像想象中那么高。显而易见，**"**#myDi a**"**选择器比**"**#myDiv ul li a**"**选择器效率要高得多。而通配符 a 的效率远比类选择器及id选择器低，若给 a 标签添加一个class myA ，构造新选择器：**"**#myDiv .myA**"，**它的效率又远比**"**#myDi a**"**要高了。浏览器对CSS选择器的解析式从右往左进行，因此在选择器末尾最好使用类选择器，而不是通配符。CSS选择器效率问题详情请见：[CSS选择器效率问题](https://www.cnblogs.com/sherryupup/p/4780449.html)

   　　　等等…

-  JS代码优化

    　　　　1. ajax请求方法按需求选择get或是post，访问接口所花费的时间在页面加载时间中占很大的比重，而接口访问方法中，get方法远比post方法要快，因此按需选择接口访问方法很重要。

      　　　　2. 减少全局变量，尽量使用局部变量。js中，全局变量运算速率远低于局部变量，速度差异达到上百倍，且全局变量越多，全局变量的查找速率便越慢。详情请见：[减少全局变量对效率的提升](http://tieba.baidu.com/p/2094796514)

      　　　　3. 减少对DOM的操作。js操作DOM将会引起页面的重绘及重排，需要花费时间及耗费浏览器资源。

    　　　　等等…

