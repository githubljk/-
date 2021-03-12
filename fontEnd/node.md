#### Node.js是什么

- Node.js是JavaScript运行环境
  - 简单来讲就是可以执行运行js代码
  - 以前只有浏览器才可以执行js代码

- 浏览器中的JavaScript
  - Ecmascript(基本语法)
  - BOM
  - DOM

- Node.js中的JavaScript
  - 没有BOM,DOM
  - 有Ecmascript
  - 再Node这个JavaScript运行环境中为JavaScript提供了一些服务器级别的API操作
    - 例如文档读写
    - 网络服务重建
    - 网络通信
    - http服务器

- Node.js特性
  - 事件驱动
  - 非阻塞IO模型,简单讲就是异步API
  - 轻量高效

- Node.js
  - 采用npm包管理工具，该工具基于Node.js开发

- Node.js
  - 基于chromeV8引擎(解析，执行代码的工具)

#### 1.3. Node.js能做什么

- web服务器
- 命令行工具
  - npm
  - git（C语言）



- 对前端开发工程师来说，接触最多是node的命令工具
  - gulp
  - webpack
  - npm

#### 1.4.Node.js知识块

- B/S编程模式
- 模块化编程
  - @import('文件路径')
  - 以前认知JavaScript只能通过`script`标签加载
  - 在Node.js中可以像`@import()`一样来加载JavaScript脚本文件

- 异步编程
  - 回调函数
  - Promise
  - async
  - generator
- Expresss Web开发框架
- ES6
  - 新语法
- Node打开服务器黑盒子

#### 1.5.Hello word

- 读取文件

  - 核心模块`fs`

    语法：

  - `var fs = require('fs')`

  - `fs.readFile('/路径',callback())`

  - `fs.writeFile('路径'，callback())`

- http
  - 核心模块`http`
  - 语法`var http = require('http')`

- 路径模块
  
- `path`
  
- `OS操作系统信息模块`

`凡是核心模块都语法需要引用`：`var 模块 = require('模块')`

#### 1.6. 模块作用域

- Node.js中没有全局作用域，只有模块作用域

- 每个Node.js文件就是一个单独模块，相互之间可以引用，对应的依赖之间需要导出和引用才可以相互使用

  - ```js
    module.exports.a = 123; //A文件
    
    var res = require('./A文件')//B文件
    res.a //123
    
    
    ```

  - 

##### IP小知识

![1](C:\Users\Administrator\Desktop\1.png)

- `联网运行的程序必须需要占用一个端口号`,端口号用来定位具体的应用程序
- 端口号：0-65535

##### 创建服务

```js
const http = require('http');
const url = require('url');


const app = http.createServer();

app.on('request', (req, res) => {
	// 获取用户的请求路径
	let pathname = url.parse(req.url).pathname;

	pathname = pathname == '/' ? '/default.html' : pathname;

	// 将用户的请求路径转换为实际的服务器硬盘路径
	let realPath = path.join(__dirname, 'public' + pathname);

	let type = mime.getType(realPath)

	// 读取文件
	fs.readFile(realPath, (error, result) => {
		// 如果文件读取失败
		if (error != null) {
			res.writeHead(404, {
				'content-type': 'text/html;charset=utf8'
			})
            //res.setHeader('Content-type', 'text/plain;charset=utf-8')
            

			res.end('文件读取失败');
            
			return;
		}
		
		res.writeHead(200, {
			'content-type': type
		})

		res.end(result);
	});
});

app.listen(3000);
console.log('服务器启动成功')
```

#### 1.7. Node.js服务器中的常识

1. http状态码重定向码：301,302
   - 相同点：
     - 浏览器对应两个状态响应码，都可以从响应的Location首部中获取地址
     - 301和302状态码都表示重定向
   - 不同点：
     - 301重定向/跳转表示**永久性转移**(Permanently Moved)，表示本网页永久性转移到另一个地址,会把旧页面的PR等信息转移到新页面
     - 302重定向表示**临时性转移**(Temporarily Moved )，当一个网页URL需要短期变化时使用

#### 1.8. export ,module.export区别

- **exports** 是 **module.exports** 的一个引用
- 对于**export**只能增加属性，方法，不要重新赋值
  - `export.name = 'lisi'`
  - `export.age = 12`
  - `export = {.......}`**重新赋值错误**，此时**exports** 与 **module.exports**脱离联系，但对于`export.name = 'lisi'``export.age = 12`两个属性已经被保存至**module.exports**中，这点没问题，导出时仍在导出内容中
- **module.exports** 此时赋值的对象就是最终要导出的内容
  - `module.export = {.......}`

- 最终文件内容的导出具体内容由**module.exports**定
- 在其它文件引用时**require(./a.js)**，也是以引用文件的**module.exports**内容为准

```js
export.name = 'lisi';
export.age = 12;
module.export = {
    fun: function (){},
    add: function(){}
}
// 最终导出
{
    fun: function (){},
    add: function(){}     
}
=====================================   
export.name = 'lisi';
export.age = 12;
module.export.add = function(){};

// 最终导出
{
    name:'lisi',
	age = 12,
    add: function(){}     
}
=====================================   
export.name = 'lisi';
export.age = 12;
export = {
    fun: function (){},
    add: function(){}
}
module.export.add = function(){};
// 最终导出
{
    name:'lisi',
	age = 12,
    add: function(){}     
}
```



#### 1.9.模块加载机制

**鉴于速度要求，Node.js在加载模块时优从缓存中加载，（模块已经加载过）提高加载速度**

#### 2.0.Node.js非阻塞原理：**事件+回调**

- 基本概念：

  1. 什么是IO

     - 网络上的传输全部是在传字符串，i/o在服务器上可以理解为读写操作

  2. **进程**

     - 进程是为运行当中的应用程序提供运行环境的 

     - 一个运行当中的应用程序就会有一个进程与之相对应

  3. 什么是并发

     - 一个时间段中有几个程序都处于已启动运行到运行完毕之间。

  4. 什么是线程

     - 线程是用来运行应用程序中代码的， 
     - 一个线程在一个时间只能做一件事件。 
     - 多线程，调度起来很麻烦。
     -  node是单线程执行，用异步替代了多线程

  5. 同步异步

     - 异步不会阻塞后面的代码，
     - 同步会阻塞后面的代码 
     - 一条线程先执行同步的代码后执行异步的代码。

- **Node.js基本介绍：**
  - **nodejs的运行机制**: 
    - nodejs**主线程**主要起一个**任务调度**的作用。
    - nodejs**用一个主线程处理所有的请求**, 将**I/O操作**(异步操作)交由底下的**线程池处理**;
    - 在所有**主线程任务执行完成后**,主线程再去处理**事件队列**(回调函数队列)。 
    - 所以在**同步初始化代码执行完成后**,nodejs会基于**事件队列**不停的做**事件循环**。
    - 事实上，nodejs运行环境 = 主线程(单线程,包括事件队列) + 线程池(工作线程池,执行其他工作-多线程)

1. **特点：**
   - Node.js 是**单进程单线程**应用程序，但是通过**事件和回调支持并发**，所以性能非常高
   - Node.js 的每一个 API 都是异步的，并作为一个独立线程运行，使用异步函数调用，并处理并发。
   - Node.js 基本上所有的事件机制都是用设计模式中**观察者模式**实现。
   - Node.js 单线程类似进入一个while(true)的事件循环，每个异步事件都生成一个事件观察者，如果有事件发生就调用该回调函数

2. **事件驱动机理**

   - Node通过事件驱动的方式**处理请求时无需为**每一个请求创建**额外的线程**。在事件驱动的模型当中，每一个IO工作被添加到**事件队列**中，线程循环地处理队列上的工作任务，当执行过程中遇到来堵塞(读取文件、查询数据库)时，主线程(主任务)不会停下来等待结果，而是留下一个处理结果的回调函数给事件队列，转而继续执行主线程中的下一个任务。这个传递到事件队列中的回调函数在当**堵塞任务运行(主线程任务)**结束后才被线程调用。

   **事件+回调**：

   - 这一套实现开始于Node开始启动的进程，在这个进程中Node会创建一个循环，每次循环运行就是一个Tick周期，每个Tick周期中会从**事件队列**查看是否有事件需要处理，如果有就取出事件并执行相关的回调函数。**事件队列事件全部执行完毕**，**node应用就会终止**。Node对于**堵塞IO**的处理在幕后使用**线程池**来确保工作的执行。Node从池中取得一个线程来执行复杂任务，而不占用主循环线程。这样就**防止堵塞IO占**用**空闲资源**。当堵塞任务执行完毕通过添加到事件队列中的回调函数来处理接下来的工作。

   ![](F:\前端总结\个人总结文档\img\1.webp)

   

   



#### 2.1. 跨域请求

- 概念：跨域是指一个域下的文档或脚本试图去请求另一个域下的资源

- 广义的跨域

- ```js
  1.) 资源跳转： A链接、重定向、表单提交
  2.) 资源嵌入： <link>、<script>、<img>、<frame>等dom标签，还有样式中background:url()、@font-face()等文件外链
  3.) 脚本请求： js发起的ajax请求、dom和js对象的跨域操作等
  ```

  其实：

  我们通常所说的跨域是狭义的，是由浏览器同源策略限制的一类请求场景

- 同源政策：协议+域名+端口"三者相同

  ```js
  举例来说，http://www.example.com/dir/page.html这个网址，
  协议是http://，域名是www.example.com，端口是80（默认端口可以省略）。它的同源情况如下。
  
  http://www.example.com/dir2/other.html：同源
  http://example.com/dir/other.html：不同源（域名不同）
  http://v2.www.example.com/dir/other.html：不同源（域名不同）
  http://www.example.com:81/dir/other.html：不同源（端口不同）
  ```

  

- 同源策略目的：是为了保证用户信息的安全，防止恶意的网站窃取数据

- 跨域解决方案：

  1、 通过jsonp跨域
  2、 document.domain + iframe跨域
  3、 location.hash + iframe
  4、 window.name + iframe跨域
  5、 postMessage跨域
  6、 **跨域资源共享（CORS）**
  7、 nginx代理跨域
  8、 nodejs中间件代理跨域
  9、 WebSocket协议跨域

  - 通过jsonp跨域

    ```js
    通常为了减轻web服务器的负载，我们把js、css，img等静态资源分离到另一台独立域名的服务器上，在html页面中再通过相应的标签从不同域名下加载静态资源，而被浏览器允许，基于此原理，我们可以通过动态创建script，再请求一个带参网址实现跨域通信
    
    
     <script>
        var script = document.createElement('script');
        script.type = 'text/javascript';
    
        // 传参一个回调函数名给后端，方便后端返回时执行这个在前端定义的回调函数
        script.src = 'http://www.domain2.com:8080/login?user=admin&callback=handleCallback';
        document.head.appendChild(script);
    
        // 回调执行函数
        function handleCallback(res) {
            alert(JSON.stringify(res));
        }
     </script>
    ```

    - jsonp跨域缺点:**只能实现get一种请求**

  -  document.domain + iframe跨域

    ```js
    此方案仅限主域相同，子域不同的跨域应用场景。
    
    实现原理：两个页面都通过js强制设置document.domain为基础主域，就实现了同域
    
    父窗口：(http://www.domain.com/a.html)
         <iframe id="iframe" src="http://child.domain.com/b.html"></iframe>
         <script>
         document.domain = 'domain.com';
         var user = 'admin';
         </script>
     ==============================================  
    
    子窗口：(http://child.domain.com/b.html)
         <script>
         document.domain = 'domain.com';
         // 获取父窗口中变量
         alert('get js data from parent ---> ' + window.parent.user);
    	</script>
    ```

  - **跨域资源共享**CORS

    ```js
    普通跨域请求：只服务端设置Access-Control-Allow-Origin即可，前端无须设置，若要带cookie请求：前后端都需要设置。
    
    
    ```

  - #### **nginx代理跨域**

    ```js
    跨域原理： 同源策略是浏览器的安全策略，不是HTTP协议的一部分。服务器端调用HTTP接口只是使用HTTP协议，不会执行JS脚本，不需要同源策略，也就不存在跨越问题。
    
    实现思路：通过nginx配置一个代理服务器（域名与domain1相同，端口不同）做跳板机，反向代理访问domain2接口，并且可以顺便修改cookie中domain信息，方便当前域cookie写入，实现跨域登录。
    ```

  - ####  Nodejs中间件代理跨域**

    ```js
    node中间件实现跨域代理，原理大致与nginx相同，都是通过启一个代理服务器，实现数据的转发，也可以通过设置cookieDomainRewrite参数修改响应头中cookie中域名，实现当前域的cookie写入，方便接口登录认证。
    ```

    

  - **WebSocket protocol**

    ```js
    是HTML5一种新的协议。它实现了浏览器与服务器全双工通信，同时允许跨域通讯，是server push技术的一种很好的实现。
    原生WebSocket API使用起来不太方便，我们使用Socket.io，它很好地封装了webSocket接口，提供了更简单、灵活的接口，也对不支持webSocket的浏览器提供了向下兼容
    ```

2.2. **cookie与session的区别**

- cookie 是一种发送到客户浏览器的文本串句柄，并保存在客户机硬盘上，可以用来在某个WEB站点会话间持久的保持数据。

- session其实指的就是访问者从到达某个特定主页到离开为止的那段时间。 Session其实是利用Cookie进行信息处理的，当用户首先进行了请求后，服务端就在用户浏览器上创建了一个Cookie，当这个Session结束时，其实就是意味着这个Cookie就过期了。
  注：为这个用户创建的Cookie的名称是aspsessionid。这个Cookie的唯一目的就是为每一个用户提供不同的身份认证。

- cookie和session的共同之处在于：cookie和session都是用来跟踪浏览器用户身份的会话方式。

- cookie 和session的区别是：cookie数据保存在客户端，session数据保存在服务器端。
  简单的说，当你登录一个网站的时候，

  - 如果web服务器端使用的是session，那么所有的数据都保存在服务器上，客户端每次请求服务器的时候会发送当前会话的sessionid，服务器根据当前sessionid判断相应的用户数据标志，以确定用户是否登录或具有某种权限。由于数据是存储在服务器上面，所以你不能伪造，但是如果你能够获取某个登录用户的 sessionid，用特殊的浏览器伪造该用户的请求也是能够成功的。sessionid是服务器和客户端链接时候随机分配的，一般来说是不会有重复，但如果有大量的并发请求，也不是没有重复的可能性.

  - 如果浏览器使用的是cookie，那么所有的数据都保存在浏览器端，比如你登录以后，服务器设置了cookie用户名，那么当你再次请求服务器的时候，浏览器会将用户名一块发送给服务器，这些变量有一定的特殊标记。服务器会解释为cookie变量，所以只要不关闭浏览器，那么cookie变量一直是有效的，所以能够保证长时间不掉线。

- 两个都可以用来存私密的东西，同样也都有有效期的说法,区别在于session是放在服务器上的，过期与否取决于服务期的设定，cookie是存在客户端的，过去与否可以在cookie生成的时候设置进去。

  ```js
  1，session 在服务器端，cookie 在客户端（浏览器）
  2，session 默认被存在在服务器的一个文件里（不是内存）
  3，session 的运行依赖 session id，而 session id 是存在 cookie 中的，也就是说，如果浏览器禁用了 cookie ，同时 session 也会失效（但是可以通过其它方式实现，比如在 url 中传递 session_id）
  4，session 可以放在 文件、数据库、或内存中都可以。
  5，用户验证这种场合一般会用 session
  ```

  











。



