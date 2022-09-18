## 一、初识Node.js

### 1. 铺垫内容

#### **1.1. 为什么 JavaScript 可以在浏览器中被执行？**

因为浏览器中存在 JavaScript 解析引擎

**不同的浏览器使用不同的 JavaScript 解析引擎：**

Chrome浏览器=>V8

Firefox浏览器=>OdinMonkey (奥丁猴)

Safri 浏览器=>JSCore

IE 浏览器=>Chakra(查克拉)



#### 1.2. 为什么JavaScript可以操作DOM和BOM？

因为浏览器内置了 DOM、BOM、Ajax 的 API

![image-20220416110617638](1. 初识Node.js.assets/image-20220416110617638.png)



#### 1.3. 浏览器中的 JavaScript 运行环境

运行环境是指代码正常运行所需的必要环境

1. V8引擎负责解析和执行JavaScript代码。

2. 内置 API 是由运行环境（浏览器）提供的特殊接口，只能在所属的运行环境中被调用。

<img src="1. 初识Node.js.assets/image-20220416110849134.png" alt="image-20220416110849134" style="zoom:67%;" />



#### 1.4. JavaScript能否做后端开发

可以，只不过要借助 **Node.js 这个后端运行环境**



### 2. Node.js 简介

#### 2.1 什么是Node.js

Node.js 是一个**基于 Chrome V8 引擎**的 JavaScript **运行环境**



#### 2.2 Node.js 中的 JavaScript 运行环境

浏览器是JavaScript的前端运行环境。

Node.js 是 JavaScript的后端运行环境。

Node.js 中无法调用DOM 和 BOM 等浏览器内置API。

<img src="1. 初识Node.js.assets/image-20220416112219311.png" alt="image-20220416112219311" style="zoom:67%;" />



#### 2.3 Node.js 可以做什么

Node.js 作为一个 JavaScript 的运行环境，仅仅提供了基础的功能和API。然而，基于 Node.js 提供的这些基础能，很多强大的工具和框架如雨后春笋，层出不穷，所以学会了 Node.js，可以让前端程序员胜任更多的工作和岗位：

① 基于 Express 框架（http://www.expressjs.com.cn/），可以快速构建 Web 应用

② 基于 Electron 框架 (https://electronjs.org/)，可以构建跨平台的桌面应用

③ 基于 restify 框架 (http://restify.com/），可以快速构建 API 接口项目

④ 读写和操作数据库、创建实用的命令行工具辅助前端开发、etc...



#### 2.4 Node.js 学习路线



![image-20220416112614763](1. 初识Node.js.assets/image-20220416112614763.png)



### 3. Node.js 的使用

#### **3.1 Node.js 运行环境安装**

http://nodejs.cn/download/current/

- LTS = Long Term Support 长期支持版 稳定版

- Current 拥有最新特性 实验版



#### 3.2 在Node.js 环境中执行JavaScript代码

1. 在要执行的 js 文件的路径中打开终端（shift + 右键 打开PowerShell/ cmd）
2. `node xxx.js` 



#### 3.3 win终端中的快捷键

Windows 有2个终端，一个 cmd  一个powershell ，cmd发布时间较早，powershell 发布时间较晚，功能更强大

1. 使用 **↑** 键，可以快速定位到**上一次执行的命令**
2. 先输入某个文件的开头，然后按 **tab** 键，能够**快速补全路径**
3. 使用 **esc** 键，能够快速**清空当前已输入**的命令
4. 输入 **cls** 命令,可以**清空终端**



## 二、fs 文件系统模块

### 1.1什么是 fs 文件系统模块

f：file 文件 ，s：system 系统，文件操作系统。

fs 模块是 Node.js 官方提供的、用来操作文件的模块。它提供了一系列的方法和属性，用来满足用户对文件的操作需求。例如:

1. fs.readFile() 方法，用来读取指定文件中的内容
2. fs.writeFile0 方法，用来向指定的文件中写入内容

如果要在JavaScript 代码中，使用 fs 模块来操作文件，则需要使用如下的方式先导入它

~~~js
const fs = require('fs')
~~~



### 1.2 fs.readFile() 读取文件内容

~~~js
fs.readFile('文件路径/文件名称'[,'文件编码'], 回调函数);
~~~

- 参数1：必选参数，**字符串**，表示文件的**路径**。

- 参数2：可选参数，表示以什么编码格式来读取文件。

- 参数3：必选参数，文件读取完成后，执行的回调函数**（包含两个参数）**。

   如果文件读取**成功**：err 是 null , doc 是文件读取的结果

   如果文件读取**失败**：err 是一个包含错误信息的对象 , doc 为 undefined

~~~js
// 1.通过模块的名字fs对模块进行引用
const fs = require('fs');

// 2.通过模块内部的readFile读取文件内容
fs.readFile('./01.helloworld.js', 'utf8', (err, doc) => {
  // 如果文件读取出错 err 是一个对象 包含错误信息 , doc 为 undefined
  // 如果文件读取正确 err 是 null , doc 是文件读取的结果
  console.log(err);
  console.log(doc);
});
~~~



### 1.3 fs.writeFile() 写入文件内容

~~~js
fs.writeFile(filedata,data[,options],callback).
~~~

- 参数1：必选参数，需要指定一个文件路径的字符串， 表示文件的**存放路径**。
- 参数2：必选参数，表示要写入的内容。
- 参数3：可选参数，表示以什么格式写入文件内容，默认值是 utf-8。
- 参数4：必选参数，文件写入完成后执行的回调函数**（包含一个参数）**
  如果文件读取**成功**：err 是 null 
  如果文件读取**失败**：err 是一个包含错误信息的对象

**注意：**

1. fs.writeFile() 方法只能用来创建文件，不能用来创建路径（**在原本不存在的路径下使用会报错**）

2. 重复调用 fs.writeFile() 写入同一个文件，新写入的内容会**覆盖之前的旧内容**

~~~js
const fs = require('fs');

fs.writeFile('./demo.txt', '即将要写入的内容', (err) => {
  if (err != null) {
    console.log(err);
    return;
  }

  console.log('文件内容写入成功');
});
~~~



### 1.4 使用 __dirname + 相对路径

在使用 fs 模块操作文件时，如果提供的操作路径是以 / 或 ./ 开头的相对路径时，很容易出现路径动态拼接错误的问题。

![image-20220416194239654](2. fs文件系统模块.assets/image-20220416194239654.png)

原因：代码在运行的时候，会以执行 node 命令时所处的目录，动态拼接出被操作文件的完整路径。



解决方案：

**__dirname 表示当前文件所处的目录**

在使用 fs 模块操作文件时，**使用 __dirname  + 相对路径(不能以./开头)**

~~~js
fs.readFile(__dirname + '01.helloworld.js'), 'utf8', (err, doc) => {}
fs.readFile(path.join(__dirname, '01.helloworld.js'), 'utf8', (err, doc) => {}
~~~



## 三、path 路径模块

### 1 什么是 path 路径模块

path 模块是 Node.js 官方提供的、用来处理路径的模块。它提供了一系列的方法和属性，用来满足用户对路径的处理需求。

例如:

- path.join() 方法，用来将多个路径片段拼接成一个完整的路径字符串
- path.basename() 方法，用来从路径字符串中，将文件名解析出来



### 2 path.join() 路径拼接

~~~js
fs.readFile(path.join(__dirname, '01.helloworld.js'), 'utf8', (err, doc) => {}
~~~

为什么要进行路径拼接？

1. 不同操作系统的路径分隔符不统一

   > Windows 上是 \  /
   >
   > Linux 上是 /

2. 过滤bug

   > `__dirname + './1.txt'`会因为你多加一个点而报错
   >
   > 但是`path.join(__dirname, './1.txt'`不会



### 3 path.basename() 路径中的最后一部分

~~~js
path.basename(path[,ext])
~~~

使用 path.basename() 方法，可以**获取路径中的最后一部分**，经常通过这个方法获取路径中的文件名

- path \<string> 必选参数，表示一个路径的字符串

- ext \<string> 可选参数，表示**想移除掉的文件扩展名**

~~~js
const fpath = '/a/b/c/index.html' //文件的存放路径

var fullName = path.basename(fapath)
console.log(fullName) //输出 index.html

var nameWithoutExt = path.basename(fpath,'.html')
console.log(nameWithoutExt）// 输出 index
~~~



#### path.extname() 获取扩展名

~~~js
path.extname(path)
~~~



## 四、http 模块

## 1 什么是http模块

什么是**客户端**、什么是**服务器**？

在网络节点中，负责消费资源的电脑，叫做客户端；负责对外提供网络资源的电脑，叫做服务器。

http 模块是 Node.js 官方提供的、用来**创建 web 服务器**的模块。通过 http 模块提供的 `http.createServer()` 方法，就能方便地把一台普通的电脑，变成一台 Web 服务器，从而对外提供 Web 资源服务。

如果要希望使用 http 模块创建 Web 服务器，则需要先导入它:

~~~js
const http = require('http')
~~~

服务器和普通电脑的**区别**在于，服务器上安装了 **web 服务器软件**，例如： IIS、**Apache** 等。通过安装这些服务器软件，就能把一台普通的电脑变成一台 web 服务器。

在 Node.js 中，我们**不需要使用** IIS、Apache 等这些**第三方 web 服务器软件**。因为我们可以基于 Node.js 提供的http 模块，通过几行简单的代码，就能轻松的手写一个服务器软件，从而对外提供 web 服务。



## 2 服务器相关概念

### 2.1 IP地址

IP 地址就是互联网上每台计算机的**唯一地址**，因此 IP 地址具有唯一性。如果把“个人电脑”比作“一台电话”，那么“IP地址”就相当于“电话号码”，只有在知道对方 IP 地址的前提下，才能与对应的电脑之间进行数据通信。

IP 地址的格式：通常用“点分十进制”表示成（a.b.c.d）的形式，其中，a,b,c,d 都是 0～255 之间的十进制整数。例如：用点分十进表示的 IP地址（192.168.1.1）

**注意：**

1. 互联网中**每台 Web 服务器，都有自己的 IP 地址**，例如：大家可以在 Windows 的终端中运行 ping www.baidu.com 命令，即可查看到百度服务器的 IP 地址。
2. 在开发期间，自己的电脑既是一台服务器，也是一个客户端，为了方便测试，可以在自己的浏览器中输入 127.0.0.1 这个IP 地址，就能把自己的电脑当做一台服务器进行访问了。



### 2.2 域名和域名服务器

尽管 IP 地址能够唯一地标记网络上的计算机，但IP地址是一长串数字，不直观，而且不便于记忆，于是人们又发明了另一套**字符型的地址方案**，即所谓的**域名（Domain Name）**地址。

IP地址和域名是—-对应的关系，这份对应关系存放在一种叫做**域名服务器（DNS，Domain Name Server)** 的电脑中。使用者只需通过好记的域名访问对应的服务器即可，对应的转换工作由域名服务器实现。因此，**域名服务器就是提供 IP 地址和域名之间的转换服务的服务器。**



**注意:**

1. **单纯使用 IP 地址，互联网中的电脑也能正常工作**。但是有了域名的加持，能让互联网变得更加方便。

2. 在开发测试 **127.0.0.1 对应的域名是 localhost**，它们都代表我们自己的这台电脑，在使用效果上无区别



### 2.3 端口号

计算机中的端口号，就好像是现实生活中的门牌号一样。通过门牌号，外卖小哥可以在整栋大楼众多的房间中，准确把外卖送到你的手中。

同样的道理，在**一台电脑中，可以运行成百上千个 web 服务**。每个 web 服务都对应一个唯一的端口号。客户端发送过来的网络请求，通过端口号，可以被**准确地交给对应的 web 服务**进行处理。

<img src="4. http 模块.assets/image-20220417111003105.png" alt="image-20220417111003105" style="zoom:67%;" />

**注意：**

1. 每个端口号不能同时被多个 web 服务占用。（**一个端口号对应一个服务**）
2. 在实际应用中，URL中的 **80 端口可以省略不写:80**。（其他非80端口必须得在URL后面加上 :xxx）



## 3 创建最基本的web服务器

### ▲3.1 创建web 服务器的基本步骤

1. 导入 http 模块

~~~js
const http = require('http')
~~~

2. 创建 web 服务器实例

~~~js
const server = http.createServer()
~~~

3. 为服务器实例用 .on 绑定 request 事件，**监听客户端的请求**

~~~js
// 使用服务器实例的 .on()方法，为服务器绑定一个 request 事件
sever.on('request', (req, res) => {
// 只要有客户端来请求我们自己的服务器，就会触发request事件，从而调用这个事件处理函数
console.log('someone visit our web server')
});
~~~


4. 启动服务器，**调用服务器实例的 .listen() 方法即可启动服务器**

~~~js
// 调用 server.listen(端口号,回调函数) 即可启动服务器
srver.listen(8080,() => {
    console.log('http server running at http://127.0.0.1')
})
~~~

5. 然后使用终端运行 node 文件名，就可以在浏览器内输入URL，向该文件发送请求



### 3.2  request 事件

只要服务器**接收到了客户端的请求**，**就会调用  request** 事件处理函数。



#### 3.2.1 req 请求对象（**request**）

req 是请求对象，它**包含了与客户端相关的数据和属性**，例如：

| req.url         | 客户端请求的 URL 地址        |
| --------------- | ---------------------------- |
| **req.method**  | **客户端的 method 请求类型** |
| req**.**headers | 获取请求报文                 |



如果想在事件处理函数中，**访问与客户端相关的数据或属性**，可以使用如下的方式：

~~~js
server.on('request',(req) => {
    const str = 'Your request url is ${req.url}, and request method is ${req.method}'
    console.log(str)
})
~~~



#### 3.2.2 res 响应对象（**response**）

res 是响应对象，它**包含了与服务器相关的数据和属性**，例如：

| res.end(xxx) | 向客户端发送xxx，并结束这次请求的处理过程 |
| ------------ | ----------------------------------------- |
|              |                                           |




如果想访问与服务器相关的数据或属性，可以使用如下的方式：

~~~js
server.on('request',(req,res) => {	// req是第一个参数，res是第二个参数不能变
    const str = 'Your request url is ${req.url}, and request method is ${req.method}'
    res.end(str)
})
~~~



#### 3.2.3 res.end() 乱码问题

当调用 res.end() 方法，**向客户端发送中文内容的时候，会出现乱码问题**，

用 `res.setHeader('Content-Type','text/html;charst=utf-8')` 手动设置内容的编码格式：

【若这样做导致css和js没生效，是因为设置了res.setHeader(),写死了所有资源以 text/html 展示，那就别用这个方法，老老实实把中文改成英文吧】

~~~js
server.on('request',(req,res) => {	
    const str = '您请求的地址是 ${req.url}, 请求的 method 类型是 ${req.method}'
    res.setHeader('Content-Type','text/html;charst=utf-8')
    res.end(str)
})

~~~



## 4 根据不同的 url 响应不同的 html 内容

### 4.1 基本步骤

1. 获取**请求的 url 地址**
2. 设置**默认的响应内容**为 404 Not found
3. 判断用户请求的是否为**／或/index.html** 首页
4. 判断用户请求的是否为 **/about.html** 关于页面
5. 设置 **Content-Type 响应头**，防止中文乱码
6. 使用 **res.end()** 把内容响应给客户端



### 4.2 案例

#### 4.2.1 核心思路

把文件的**实际存放路径**，作为每个资源的请求 **url 地址**。

<img src="4. http 模块.assets/image-20220417170051687.png" alt="image-20220417170051687" style="zoom:67%;" />



#### 4.2.2 实现步骤

1. 导入需要的模块
2. 创建基本的 web 服务器
3. 将资源的请求 url 地址映射为文件的存放路径
4. 读取文件内容并响应给客户端
5. 优化资源的请求路径



####  1-导入需要的模块

~~~js
const fs = require('fs')
const path = require('path')
const http = require('http')
~~~



#### 2-创建基本的 web 服务器

~~~js
const server = http.createServer()
server.on('request',(req,res) => {
    
})

server.listen(8080,function(){
    
})
~~~



#### 3-将资源的请求 url 地址映射为文件的存放路径

~~~js
// 3.1 获取到客户端请求的url地址
const url = req.url
// 3.2 把请求的url地址，映射为本地文件的存放路径
const fpath = path.join(__dirname,url) // 第5步会优化
~~~



#### 4-读取文件内容并响应给客户端

~~~js
// 4.1 根据“映射”过来的文件路径 通过 fs.readFile 读取文件
fs.readFile(fpath,'utf8',(err,dataStr) => { // 注意是'utf8' 不是 'utf-8'
	// 4.2 若读取失败，返回错误信息
    if(err) return res.end('404 Not Found.')
	// 4.3 若读取成功，返回客户端需要的内容
    res.end(dataStr)
})
~~~



#### 5-优化资源的请求路径

1. 访问根路径 '/' 的时候，能够展示首页，不会报错
2. 访问具体路径的时候，希望能够省略中间路径依然能请求到数据

~~~js
// 修改 const fpath = path.join(__dirname,url)
// 因为万一用户直接请求'./index.html' 而不是 './clock/index.html' 会请求失败
// 5.1 预定义空白字符串为文件路径
let fpath= ''
if(url === '/'){
    // 5.2 如果请求的路径为 / 根目录，则手动指定到 索引页面
    fpath = path.join(__dirname,'./clock/index.html')
} else {
    // 5.3 如果请求的路径不为 / ，则动态拼接文件的存放路径
    fpath = path.join(__dirname,'./clock',url)
}
~~~



## 五、模块化、npm与包

## 1 Node.js 中模块的分类

### 1.1 模块分类

Node.js 中根据模块来源的不同，将模块分为了 3 大类，分别是：

1. 内置模块（内置模块是由 Node.js 官方提供的，例如 **fs、path、http** 等）
2. 自定义模块 （用户创建的每个 .js 文件，都是自定义模块）
3. 第三方模块（由**第三方开发**出来的模块，并非官方提供的内置模块，**使用前需要先下载**）



### 1.2 require() 使用

只有加载自定义模块的时候才用路径，其他2种直接用模块名：

![image-20220417213958805](5. 模块化、npm与包.assets/image-20220417202726205.png)

注意：使用`require()`方法加载其他模块时，会**执行**被加载模块中的代码



### 1.3 Node.js 中的模块作用域

什么是模块作用域？

和函数作用域类似，在自定义模块中定义的变量、方法等成员，只能在当前模块内被访问

好处就是防止变量污染（覆盖）



### ▲1.4 向外共享模块作用域中的成员

#### 1.4.1 module 对象

在每个 .js 自定义模块中都有一个 module 对象，它里面存储了和当前模块有关的信息，打印如下：

![image-20220417205222943](5. 模块化、npm与包.assets/image-20220417205222943.png)

exports 属性 存放暴露的对象



#### 1.4.2 module.exports 对象

在自定义模块中，可以使用 module.exports 对象，将模块内的成员共享出去，供外界使用。

外界用 require(）方法导入自定义模块时，**得到的就是 module.exports 所指向的对象**。

使用 require() 方法导入模块时，导入的结果，永远以 module.exports 指向的对象为准（后面的代码会覆盖）

![image-20220417214133190](5. 模块化、npm与包.assets/image-20220417214133190.png)



#### 1.4.3 exports 对象

由于 module.exports 单词写起来比较复杂，为了简化向外共享成员的代码，Node 提供了 `exports` 对象。

默认情况下，exports 和 module.exports **指向同一个对象**。

最终共享的结果，还是以 module.exports 指向的对象为准！【不嫌麻烦的话还是写 module.exports 吧】

![exports和module.exports的使用注意点](5. 模块化、npm与包.assets/exports和module.exports的使用注意点.png)

#### 1.4.4 Node.js 中的模块化规范

Node.js 遵循了 CommonJS 模块化规范，CommonJS 规定了模块的特性和各模块之间如何相互依赖。

CommonJS 规定：

1. 每个模块内部，**module 变量代表当前模块**。
2. module 变量是一个对象，它的 exports 属性即 **module.exports 是对外的接口**。
3. 加载某个模块，其实是加载该模块的 module.exports 属性。**require() 方法用于导入模块**。



---



## 2 模块化的基本概念

编程领域中的模块化，就是遵守固定的规则，把一个大文件拆成独立并且相互依赖的多个小模块。

把代码进行模块化拆分的好处:

1. 提高了代码的**复用性**

2. 提高了代码的**可维护性**
3. 实现**按需加载**



### 2.1 优先从缓存中加载

模块在**第一次加载后会被缓存**。 这也意味着**多次调用** require() **只会执行一次**。

注意：不论是内置模块、用户自定义模块、还是第三方模块，它们都会优先从缓存中加载，从而提高模块的加载效率。



### 2.2 内置模块的加载机制

内置模块是由 Node.js 官方提供的模块，**内置模块的加载优先级最高**。

例如，即使在 node_modules 目录下有名字相同的包也叫做 fs，require('fs') 始终返回 node 内置的 fs 模块。



### 2.3 自定义模块的加载机制

使用 require() **加载自定义模块**时，**必须指定以 ./ 或 ../ 开头的路径标识符**。

在加载自定义模块时，**如果没有**指定 ./ 或 ../ 这样的路径标识符，则 node 会把它**当作内置模块或第三方模块**进行加载。

同时，在使用 require() 导入自定义模块时，**如果省略了文件的扩展名**，则 Node.js 会按顺序分别尝试加载以下的文件：

1. 按照**确切的文件名**进行加载
2. 补全 **.js** 扩展名进行加载
3. 补全 **.json** 扩展名进行加载
4. 补全 **.node** 扩展名进行加载
5. 加载失败，终端报错



### 2.4 第三方模块的加载机制

如果传递给 require() 的模块标识符不是一个内置模块，也没有以 ‘./’ 或 ‘../’ 开头，则 Node.js 会**从当前模块的父目录开始**，尝试**从 /node_modules 文件夹**中加载第三方模块。

如果没有找到对应的第三方模块，则移动到再上一层父目录中，**继续寻找/node_modules**，**直到文件系统的根目录**。

例如，假设在 'C:\Users\itheima\project\foo.js' 文件里调用了 require('tools')，则 Node.js 会按以下顺序查找：

1.  **C:\Users\itheima\project\node_modules\\**tools
2.  **C:\Users\itheima\node_modules\\**tools
3.  **C:\Users\node_modules\\**tools
4.  **C:\node_modules\\**tools



### 2.5 目录作为模块

当把**目录（文件夹）作为模块标识符**，传递给 require() 进行加载的时候，有三种加载方式：

1. 在被加载的目录（文件夹）下查找 **package.json** ，并**寻找 main 属性**，作为 require() 加载的入口
2. 如果目录（文件夹）里没有 package.json 文件，或者 main 入口不存在或无法解析，则 Node.js 将会试图加载目录（文件夹）下的 **index.js** 文件。
3. 如果以上两步都失败了，则 Node.js 会在终端打印错误消息，报告模块的缺失：Error: Cannot find module 'xxx'





---



## 3 npm 与包
### 3.1 包

#### 3.1.1 什么是包

Node.js 中的第三方模块又叫做包。
就像电脑和计算机指的是相同的东西，第三方模块和包指的是同一个概念，只不过叫法不同。

#### 3.1.2 包的来源

同于 Node.js 中的内置模块与自定义模块，包是由第三方个人或团队开发出来的，免费供所有人使用。
**注意：**Node.js 中的包都是**免费且开源**的，不需要付费即可免费下载使用。

#### 3.1.3 为什么需要包

由于 Node.js 的内置模块仅提供了一些底层的 API，导致在基于内置模块进行项目开发的时，效率很低。
包是**基于内置模块封装**出来的，提供了更高级、更方便的 API，极大的**提高了开发效率**。
包和内置模块之间的关系，类似于 jQuery 和 浏览器内置 API 之间的关系。

#### 3.1.4 从哪里搜索、下载包

国外有一家 IT 公司，叫做 npm, Inc. 这家公司旗下有一个非常著名的网站： https://www.npmjs.com/ ，它是全球最大的包共享平台，你可以从这个网站上搜索到任何你需要的包，只要你有足够的耐心！
到目前位置，全球约 1100 多万的开发人员，通过这个包共享平台，开发并共享了超过 120 多万个包 供我们使用。
npm, Inc. 公司提供了一个地址为 https://registry.npmjs.org/ 的服务器，来对外共享所有的包，我们可以从这个服务器上下载自己所需要的包。

注意：

- 从 https://www.npmjs.com/ **网站**上**搜索**自己所需要的包
- 从 https://registry.npmjs.org/  **服务器**上**下载**自己需要的包

#### 3.1.5 如何下载包

npm, Inc. 公司提供了一个包管理工具，我们可以使用这个包管理工具，从 https://registry.npmjs.org/ 服务器把需要的包下载到本地使用。
这个包管理工具的名字叫做 **Node Package Manager（简称 npm 包管理工具）**，这个包管理工具随着 Node.js 的安装包一起被安装到了用户的电脑上。
大家可以在终端中执行 **npm -v** 命令，来查看自己电脑上所安装的 **npm 包管理工具的版本号**



### ▲3.2 npm

#### 3.2.1 安装包的命令【可缩写为 i 】

在终端中输入

~~~js
npm install A包名 B包名
// 上述的装包命令，可以简写成如下格式：
npm i A包名 B包名
~~~



#### 3.2.2 初次装包后多了哪些文件

初次装包完成后，在项目文件夹下多一个叫做 **node_modules 的文件夹**和 **package-lock.json 的配置文件**

其中：

- `node_modules` 文件夹用来**存放所有已安装到项目中的包**。require() 导入第三方包时，就是从这个目录中查找并加载包。
- `package-lock.json`配置文件用来**记录 node_modules 目录下的每一个包的下载信息**，例如包的名字、版本号、下载地址等。

注意：程序员不要手动修改 node_modules 或 package-lock.json 文件中的任何代码，npm 包管理工具会自动维护它们。



#### 3.2.3 安装指定版本的包

默认情况下，使用 npm install 命令安装包的时候，会自动安装最新版本的包。如果需要安装指定版本的包，可以在包名之后，通过 @ 符号指定具体的版本，例如：

~~~js
npm i moment@2.22.2
~~~



### ▲3.3 包管理配置文件 package.json

npm 规定，在项目**根目录**中，必须提供一个叫做 ``package.json`` 的包管理配置文件。用来记录与项目有关的一些配置信息【**存放在"dependencies" 节点里**】例如：
- 项目的名称、版本号、描述等
- 项目中都用到了哪些包
- 哪些包只在**开发期间**会用到
- 那些包在**开发和部署**时都需要用到



#### 3.3.1 多人开发时注意

整个项目的体积是 30.4M
第三方包的体积是 28.8M
项目源代码的体积 1.6M

遇到的问题：第三方包的体积过大，不方便团队成员之间共享项目源代码。

**解决方案：共享时剔除 node_modules ，利用 package.json 的配置文件，记录项目中安装了哪些包**

**注意：**今后在项目开发中，一定要**把 node_modules 文件夹，添加到 .gitignore 忽略文件中。**



#### 3.3.2 快速创建package.json 【不可缩写为 i 】

在项目新建的时候（开发之前），运行以下命令：

~~~js
npm init -y  【注意是 init 不是 install ,且不可缩写为 i】
~~~

**注意：**

- 上述命令只能在**英文目录**下成功运行！所以，项目文件夹的名称一定要使用英文命名，不要使用中文，**不能出现空格（用下划线代替）**
- 运行 npm install 命令安装包的时候，npm 包管理工具会**自动**把包的名称和版本号，记录到 package.json 中



#### 3.3.3 一次性安装所有的包

当我们拿到一个剔除了 node_modules 的项目之后，需要先把所有的包下载到项目中，才能将项目运行起来。

一次性安装所有的依赖包：

~~~js
npm install 或 npm i
~~~



#### 3.3.4 卸载包

npm uninstall (不能用uni) 命令执行成功后，会把卸载的包，自动**从 package.json 的 dependencies 中移除**

~~~js
npm uninstall 包名
~~~



#### 3.3.5 devDependencies 节点

如果某些包只在项目**开发阶段会用到**，在项目**上线之后不会用到**，这些包会记录到 **devDependencies 节点**中。

与之对应的，如果某些包在**开发和项目上线之后都需要用到**，则建议把这些包记录到 **dependencies 节点**中。

您可以使用如下的命令，将包记录到 devDependencies 节点中：

~~~js
npm i 包名 -D
~~~



### 3.4 解决下包速度慢的问题

#### 3.4.1 为什么下包速度慢

在使用 npm 下包的时候，默认从国外的 https://registry.npmjs.org/ 服务器进行下载，此时，网络数据的传输需要经过漫长的海底光缆，因此下包速度会很慢。

扩展阅读 - 海底光缆：
https://baike.baidu.com/item/%E6%B5%B7%E5%BA%95%E5%85%89%E7%BC%86/4107830
https://baike.baidu.com/item/%E4%B8%AD%E7%BE%8E%E6%B5%B7%E5%BA%95%E5%85%89%E7%BC%86/10520363
https://baike.baidu.com/item/APG/23647721?fr=aladdin



#### 3.4.2 淘宝 NPM 镜像服务器

淘宝在国内搭建了一个服务器，专门把国外官方服务器上的包**同步**到国内的服务器，然后在国内提供下包的服务。从而极大的提高了下包的速度。

扩展：

**镜像**（Mirroring）是一种文件存储形式，一个磁盘上的数据在另一个磁盘上存在一个完全相同的副本即为镜像。

<img src="5. 模块化、npm与包.assets/image-20220419232159407.png" alt="image-20220419232159407" style="zoom:50%;" />



#### 3.4.3 切换镜像源

法一：

~~~js
npm config get registry  查看当前下包的镜像源
npm config set registry=http://registry.npm.taobao.org/  切换为淘宝镜像源
~~~

法二：

为了更方便的切换下包的镜像源，我们可以安装 nrm 这个包，利用 nrm 提供的终端命令，可以快速查看和切换下包的镜像源。

~~~js
npm i nrm -g
nrm ls   查看所有可用的镜像源
nrm use taobao  切换为淘宝镜像
~~~



### 3.5 包的分类

#### 3.5.1 项目包

那些被安装到项目的 **node_modules 目录中的包**，都是**项目包**。

项目包又分为两类，分别是：

- 开发依赖包（被记录到 devDependencies 节点中的包，只在开发期间会用到）
- 核心依赖包（被记录到 dependencies 节点中的包，在开发期间和项目上线之后都会用到）



#### 3.5.2 全局包

在执行 npm install 命令时，如果提供了 -g 参数，则会把包安装为全局包。
全局包会被安装到 **C:\Users\用户目录\AppData\Roaming\npm\node_modules** 目录下。

~~~js
npm i 包名 -g				全局安装
npm uninstall 包名 -g		卸载全局安装的包
~~~

**注意：**

1. 只有**工具性质的包**，才有全局安装的必要性。因为它们提供了好用的终端命令。
2. 判断某个包是否需要全局安装后才能使用，可以参考**官方提供的使用说明**即可。



##### 例如 i5ting_toc

i5ting_toc 是一个可以把 md 文档转为 html 页面的小工具，使用步骤如下：

~~~js
npm instal -g i5ting_toc
i5ting_toc -f 要转化的md文件路径 -o
~~~



### 3.5.3 规范的包结构

一个规范的包，它的组成结构，必须符合以下 3 点要求：

1. 包必须以单独的目录而存在
2. 包的**顶级目录**下要**必须包含 package.json** 这个包管理配置文件
3. package.json 中**必须包含 name，version，main 这三个属性**，
   分别代表包的**名字**、**版本号**、**包的入口**（其他包 **require 导入时执行的文件**）。



注意：以上 3 点要求是一个规范的包结构必须遵守的格式，关于更多的约束，可以参考如下网址：
https://yarnpkg.com/zh-Hans/docs/package-json



## 六、Express

## 1 Express 基本使用

### 1.1 Express 简介

#### 1.1.1 什么是 Express

官方给出的概念：Express 是基于 Node.js 平台，快速、开放、极简的 Web 开发框架。

通俗的理解：Express 的作用和 Node.js 内置的 http 模块类似，是专门用来**创建 Web 服务器**的。

Express 的本质：就是一个 npm 上的**第三方包**，提供了快速创建 Web 服务器的便捷方法。

Express 的中文官网： http://www.expressjs.com.cn/



#### 1.1.2 进一步理解 Express

思考：不使用 Express 能否创建 Web 服务器？
答案：能，使用 Node.js 提供的原生 http 模块即可。

思考：既然有了 http 内置模块，为什么还要用 Express？
答案：http 内置模块用起来很复杂，开发效率低；Express 是基于内置的 http 模块进一步封装出来的，能够极大的**提高开发效率**。

思考：http 内置模块与 Express 是什么关系？
答案：类似于浏览器中 Web API 和 jQuery 的关系。**Express是基于 node 的 http 内置模块 进一步封装出来的**。



#### 1.1.3 Express 能做什么

对于前端程序员来说，最常见的两种服务器，分别是：

- **Web 网站服务器**：专门对外提供 Web 网页资源的服务器。
- **API 接口服务器**：专门对外提供  API 接口的服务器。

使用 Express，我们可以方便、快速的创建 Web 网站的服务器或 API 接口的服务器。



### ▲1.2 Express 的基本使用

#### 1.2.1 安装

~~~js
npm i express@4.17.1
~~~



#### ▲1.2.2 创建基本的 Web 服务器

~~~js
// 1. 导入express
const express = require('express')

// 2. 创建web服务器    express()是无参构造函数，创建一个express实例
const app = express()


/* 中间写各种get、post 请求 */


// 3. 最后再调用 app.listen(端口号，启动成功后的回调函数) 来启动服务器
app.listen(8080,()=>{
    console.log('express server running at http://127.0.0.1')
})
~~~



#### 1.2.3 监听 GET 请求

通过 app.get() 方法，可以监听客户端的 GET 请求，具体的语法格式如下：

~~~js
app.get('请求的URL',function(req,res){
    /* 处理函数 */
})
参数1：客户端请求的 URL 地址
参数2：请求对应的处理函数
	req：请求对象（包含与请求相关的属性和方法）
	res：响应对象（包含与相应相关的属性和方法）
~~~



#### 1.2.4 监听 POST 请求

通过 app.post() 方法，可以监听客户端的 POST 请求，具体的语法格式如下：

~~~js
app.post('请求的URL',function(req,res){
    /* 处理函数 */
})
参数1：客户端请求的 URL 地址
参数2：请求对应的处理函数
	req：请求对象（包含与请求相关的属性和方法）
	res：响应对象（包含与相应相关的属性和方法）
~~~



#### ▲1.2.5 把内容响应给客户端 res.send()

通过 res.send() 方法，可以把处理好的内容，发送给客户端：

~~~js
app.get('/user',(req,res) => {
    // 当客户端 get 请求 /user 时
    
    res.send({name:'zs', age:20, gender:'男'})
    // 向客户端发送JSON对象
})

app.post('/user',(req,res) => {
    // 当客户端 post 请求 /user 时
    
    res.send('请求成功')
    // 向客户端发送文本内容
})
~~~



#### ▲1.2.6 获取 URL 中携带的查询参数 req.query

通过 req.query 对象，可以访问到  **客户端发送到服务器的参数（查询字符串的形式）**：

req.query 默认是一个空对象

“查询字符串的形式” 类似于 ?name=zs&age=20 

~~~js
app.get('/',(req,res) => {
    console.log(req.query)
	res.send(req.query)
    // 客户端使用 ?name=zs&age=20 这种查询字符串形式,发送到服务器的参类，可以通过 req.query 对象访问到，例如:
    // req.query.name   req.query.age
})
~~~



#### ▲1.2.7 获取 URL 中的动态参数 req.params

通过 req.params 对象，可以访问到 URL 中，通过 : 匹配到的动态参数：

req.params 默认是一个空对象，里面存放着通过 ：动态匹配到的参数值

~~~js
// URL 地址中，可以通过 ：参数名 的形式，匹配动态参数值
app.get('/user/:xxx/:xxxx', (req,res)=>{
    // 这里的:xxx 是需要动态匹配的属性名，可以添加多个
    // 当客户端把请求发过来后，就会往 req.params 对象里添加 xxx:(传过来的值)
    console.log(req.params)
    res.send(req.params)
    })
~~~

![image-20220420132900224](6. Express.assets/image-20220420132900224.png)

![image-20220420133408239](6. Express.assets/image-20220420133408239.png)



### 1.3 托管静态资源

#### 1.3.1 app.use 和 express.static()

通过 `express.static()` ，我们可以非常方便地创建一个**静态资源服务器**

例如，通过如下代码就可以将 public 目录下的图片、CSS 文件、JavaScript 文件对外开放访问了：

~~~js
const express = require('express')
const app = express()

// express.static() 括号里面填写你要静态部署的文件夹
app.use(express.static('./clock'))

app.listen(80, () => {
  console.log('express server running at http://127.0.0.1')
})
~~~



**注意：**Express 在指定的静态目录中查找文件，并对外提供资源的访问路径。

因此，**存放静态文件的目录名（比如上面例子中的 'clock'）不会出现在 URL 中**。

~~~js
URL里应该填写(显示)的是
http://localhost:8080/images/bg.jpg 
而不是
http://localhost:8080/clock/images/bg.jpg 
~~~

如果你想挂载上路径前缀，则可以**在 .use 方法中的第一个参数里添加第路径字符串**：

~~~js
app.use('/clock', express.static('./clock'));
/*
现在，你就可以通过带有 /clock 前缀地址来访问 clock 目录中的文件了：
http://localhost:8080/clock/images/bg.jpg
*/
~~~



#### 1.3.2 托管多个静态资源目录

如果要托管多个静态资源目录，就多次调用 express.static() 函数：

**当多个目录下都有同样的文件名时**，express.static() 函数会**根据代码的添加顺序查找所需的文件**。

~~~js
const express = require('express');
const app = express();

// 在这里，优先查找 files 文件夹下面的文件
app.use(express.static('./files'));
app.use(express.static('./clock'));

app.listen(80, () => {
  console.log('express server running at http://127.0.0.1');
});
~~~



如果希望在托管的静态资源访问路径之前，挂载路径前缀，则可以通过 `.use` 添加前缀：

~~~js
const express = require('express');
const app = express();


// 当你在files 之前挂载路径前缀，那除非客户端访问的URL带/files，不然还是加载/clock的index文件
app.use('/files', express.static('./files'));
// 现在，你就可以通过带有 /files 前缀地址来访问 files 目录中的文件了：
app.use(express.static('./clock'));

app.listen(80, () => {
  console.log('express server running at http://127.0.0.1');
});

~~~



### ▲1.4 nodemon 方便调试

#### 1.4.1  nodemon 第三方包的作用

在调试 Node.js 项目的时候，如果修改了项目的代码，则需要频繁的手动 ctrl+c 掉，然后再 node xxx.js，非常繁琐。

现在，我们可以使用 nodemon（https://www.npmjs.com/package/nodemon） 这个工具，它能够**监听项目文件的变动**，当代码被修改后，nodemon 会**自动帮我们重启项目**，极大方便了开发和调试。

#### 1.4.2  安装nodemon

~~~js
npm i -g nodemon
~~~

#### 1.4.3  使用nodemon

在终端输入：

~~~js
nodemon xxx.js
~~~



## 2 Express 路由

### 2.1 路由的概念



#### 2.1.1 Express 中的路由

广义上来讲，路由就是**映射关系**。

在 Express 中，路由指的是**客户端的请求**与**服务器处理函数之间**的映射关系。



Express 中的路由分 3 部分组成，分别是**HTTP请求的类型(get、post...)**、**请求的 URL 地址**、**处理函数**，格式如下：

~~~js
app.HTTP请求的类型(请求的 URL 地址,处理函数)

// 例如：
app.get('/user', (req, res) => {
  res.send({ name: 'zs', age: 20, gender: '男' })
})

app.post('/user', (req, res) => {
  res.send('请求成功')
})
~~~



#### 2.1.2 路由的匹配过程

每当一个**请求到达服务器之后**，需要**先经过路由的匹配**，只有**匹配成功之后，才会调用对应的处理函数**。

在匹配时，会**按照路由的定义顺序进行匹配**，如果请求类型和请求的 URL 同时匹配成功，则 Express 会将这次请求，转交给对应的 function 函数进行处理。

路由匹配的注意点：
1. 按照**定义的先后顺序**进行匹配
2. **请求类型**和**请求的URL**同时匹配成功，才会调用对应的处理函数

![image-20220420155223801](6. Express.assets/image-20220420155223801.png)

### ▲2.2 模块化路由的使用

为了方便对路由进行**模块化的管理**，Express 不建议将路由直接挂载到 app 上，而是推荐将**路由抽离为单独的模块**。

将路由抽离为单独模块的步骤如下：

1. **创建**路由模块**对应的 router.js 文件**
2. `require('express')` 调用 `express.Router()` 函数**创建路由对象 router**
3. 向路由对象上挂载具体的路由`router.get`、`router.post`
4. 使用 `module.exports = router` **向外导出**路由对象
5. 主文件使用 `require('./router.js')` **导入**路由模块
6. 主文件使用 `app.use('/api', router)` **注册路由模块**【/api 类似于托管静态资源，添加(挂载)访问前缀】

> app.use() 函数的作用：注册全局中间件
> 托管静态资源 和 注册路由模块时 需要用到 .use()

#### 2.2.1 router.js

~~~js
// 这是路由模块
// 1. 导入 express
const express = require('express')
// 2. 创建路由对象
const router = express.Router()

// 3. 挂载具体的路由
router.get('/user/list', (req, res) => {
  res.send('Get user list.')
})
router.post('/user/add', (req, res) => {
  res.send('Add new user.')
})

// 4. 向外导出路由对象
module.exports = router
~~~

#### 2.2.2 index.js

~~~js
// 这是主要模块
const express = require('express')
const app = express()

// 1. 导入路由模块
const router = require('./03.router')

// 2. 注册路由模块
app.use('/api', router)
// 直接 app.use(router) 也行,
// 添加'/api'前缀，就得通过 /api/user/list 来访问，而不是/user/list

app.listen(80, () => {
  console.log('http://127.0.0.1')
})
~~~



## 3 Express 中间件

### 3.1 中间件的概念、作用

中间件（Middleware ），特指业务流程的中间处理环节。

**中间件的作用：**

多个中间件之间，**共享同一份 req 和 res**。

基于这样的特性，我们可以在上游的中间件中，统一**为 req 或 res 对象添加自定义的属性或方法**，**供下游**的中间件或路由进行使用。



### 3.2 Express 中间件的调用流程

当一个请求到达 Express 的服务器之后，可以**连续调用多个**中间件，从而对这次请求进行预处理。

<img src="6. Express.assets/image-20220421223258125.png" alt="image-20220421223258125" style="zoom: 80%;" />



### 3.3 Express 中间件的格式

Express 的中间件，本质上就是一个 function 处理函数，

**只不过多了第三个形参 ——> 回调参数，按照约定称为“next”**

注意：中间件函数的形参列表中，**必须包含 next 参数**。而路由处理函数中**只包含** req 和 res。

![image-20220421224036385](6. Express.assets/image-20220421224036385.png)



### ▲3.4 全局中间件

客户端发起的**任何请求**，到达服务器之后，**都会触发的中间件**，叫做全局生效的中间件。

通过调用 **app**.use(中间件函数)，即可定义一个全局生效的中间件，示例代码如下：

~~~js
// 定义一个最简单的中间件函数
const mw = function (req, res, next) {
  console.log('这是最简单的中间件函数')
  next() 	// next()一定要写！！！ 否则就不能把流转关系，转交给下一个中间件或路由
}

// 将 mw 注册为全局生效的中间件
app.use(mw)
~~~

这是定义全局中间件的简化形式：把函数写到 use() 里

~~~js
// 这是定义全局中间件的简化形式
app.use((req, res, next) => {
  console.log('这是最简单的中间件函数');
  next();
});
~~~

#### 定义多个全局中间件

可以使用 app.use() 连续定义多个全局中间件。

客户端请求到达服务器之后，会按照中间件**定义的先后顺序**依次进行调用，示例代码如下：

~~~js
const express = require('express')
const app = express()

// 定义第一个全局中间件
app.use((req, res, next) => {
  console.log('调用了第1个全局中间件')
  next()
})
// 定义第二个全局中间件
app.use((req, res, next) => {
  console.log('调用了第2个全局中间件')
  next()
})

// 定义一个路由
app.get('/user', (req, res) => {
  res.send('User page.')
})

app.listen(80, () => {
  console.log('http://127.0.0.1')
})
~~~



### ▲3.5 局部中间件

**不使用 app.**use() 定义的中间件，叫做**局部生效**的中间件

局部中间件添加到路由的 **URL 和处理函数之间**，才会被调用

~~~js
// 导入 express 模块
const express = require('express')
// 创建 express 的服务器实例
const app = express()

// 1. 定义中间件函数
const mw1 = (req, res, next) => {
  console.log('调用了局部生效的中间件')
  next()
}

// 2. 创建路由
app.get('/', mw1, (req, res) => {	// 请求根目录的时候才会调用mw1中间件函数
  res.send('Home page.')
})
app.get('/user', (req, res) => {	// 请求/user的时候不会调用
  res.send('User page.')
})

// 调用 app.listen 方法，指定端口号并启动web服务器
app.listen(80, function () {
  console.log('Express server running at http://127.0.0.1')
})
~~~

#### 定义-调用多个局部中间件

~~~js
// 以下两种写法是"完全等价"的，可根据自己的喜好，选择任意一种方式进行使用
app.get('/', mw1, mw2, (req, res) => { res.send('Home page.') })
app.get('/', [mw1, mw2], (req, res) => { res.send('Home page.')})
~~~



### ▲3.6 中间件的5个使用注意事项

1. 一定要在**路由之前注册**中间件
2. 客户端发送过来的请求，**可以连续调用多个**中间件进行处理
3. 执行完中间件的业务代码之后，**不要忘记调用 next()** 函数
4. 为了防止代码逻辑混乱，调用 **next() 函数后不要再写额外的代码** 
   【如果你在 next() 后面写了额外的代码，那等路由结束后，它会**按照出栈顺序依次执行！**】
5. 连续调用多个中间件时，多个中间件之间，**共享** req 和 res 对象



### ▲3.7 错误中间件、内置中间件

为了方便大家理解和记忆中间件的使用，Express 官方把常见的中间件用法，分成了 5 大类，分别是：

1.  **应用**级别的中间件
2.  **路由**级别的中间件
3.  **错误**级别的中间件
4.  Express **内置**的中间件
5.  **第三方**的中间件



#### 3.7.1 **应用**级别的中间件

**绑定到 app = express() 实例上的**中间件，叫做应用级别的中间件

通过 app.use() 或 app.get() 或 app.post() ，**绑定到 app 实例上的中间件**，叫做应用级别的中间件

**全局中间件和局部中间件** 就是应用级别的中间件



#### 3.7.2 路由级别的中间件

**绑定到 express.Router() 实例上的**中间件，叫做路由级别的中间件。

它的用法和应用级别中间件没有任何区别。

只不过，应用级别中间件是绑定到 app 实例上，路由级别中间件**绑定到 router 实例**上



#### ▲3.7.3 错误级别的中间件

错误级别中间件的作用：专门用来**捕获整个项目中发生的异常错误**，从而防止项目异常崩溃的问题。

格式：错误级别中间件的 function 处理函数中，

必须有 **4 个形参**，形参顺序从前到后，分别是 (**err**, req, res, next)。



**注意：**只有错误级别的中间件，必须**注册在所有路由之后！app.listen() 之前**

~~~js
// 导入 express 模块
const express = require('express');
// 创建 express 的服务器实例
const app = express();

// 1. 定义路由
app.get('/', (req, res) => {
  // 1.1 人为的制造错误
  throw new Error('服务器内部发生了错误！');
  res.send('Home page.'); //这行代码因为上一行抛出错误，所以不会执行
});

// 2. 定义错误级别的中间件，捕获整个项目的异常错误，从而防止程序的崩溃
app.use((err, req, res, next) => {
  console.log('发生了错误！' + err.message);
  res.send('Error：' + err.message);
});

// 调用 app.listen 方法，指定端口号并启动web服务器
app.listen(80, function () {
  console.log('Express server running at http://127.0.0.1');
});
~~~



#### ▲3.7.4 Express内置的中间件

自 Express 4.16.0 版本开始，Express 内置了 **3 个常用的中间件**，极大的提高了 Express 项目的开发效率和体验：

1. `express.static()` 快速托管静态资源的内置中间件，例如： HTML 文件、图片、CSS 样式等（无兼容性）
2. ▲`express.json()` **解析 JSON 格式**的请求体数据，**解析后挂载（赋值）到 req.body**（有兼容性，仅在 4.16.0+ 版本中可用）
3. ▲`express.urlencoded({ extended: false })` **解析 `application/x-www-form-urlencoded` 格式**的请求体数据，**解析后挂载（赋值）到 req.body**（有兼容性，仅在 4.16.0+ 版本中可用）



【 提前配置过 `express.json` / `express.urlencoded` 后，**才可以使用 `req.body` 这个属性**，来**接收客户端发送过来的请求体**数据。

如果不配置解析表单数据的中间件，则 req.body 默认等于 undefined】

~~~~~js
// 导入 express 模块
const express = require('express');
// 创建 express 的服务器实例
const app = express();

// 注意：除了错误级别的中间件，其他的中间件，必须在路由之前进行配置

// 通过 express.json() 这个中间件，解析表单中的 JSON 格式的数据
app.use(express.json());

// 通过 express.urlencoded() 这个中间件，来解析表单中的application/x-www-form-urlencoded格式的数据
app.use(express.urlencoded({ extended: false }));

app.post('/user', (req, res) => {
  // 配置过 express.json() 后，才可以使用 req.body 这个属性，来接收客户端发送过来的请求体数据
  // 默认情况下，如果不配置解析表单数据的中间件，则 req.body 默认等于 undefined
  console.log(req.body);
  res.send('ok');
});

app.post('/book', (req, res) => {
  // 配置过 express.urlencoded() 后，才可以通过 req.body 来获取 JSON 格式的表单数据和 url-encoded 格式的数据
  console.log(req.body);
  res.send('ok');
});

// 调用 app.listen 方法，指定端口号并启动web服务器
app.listen(80, function () {
  console.log('Express server running at http://127.0.0.1');
});
~~~~~



#### 3.7.5 第三方的中间件

非 Express 官方内置的，而是由第三方开发出来的中间件，叫做第三方中间件。在项目中，大家可以按需下载并配置第三方中间件，从而提高项目的开发效率。

例如：在 express@4.16.0 之前的版本中，经常使用 body-parser 这个第三方中间件，来解析请求体数据。使用步骤如下：

1. 运行 npm install body-parser **安装**中间件
2. 使用 require **导入**中间件
3. 调用 app.use() **注册并使用**中间件

**注意：**Express 内置的 express.urlencoded 中间件，就是基于 body-parser 这个第三方中间件进一步封装出来的。



### 3.8 自定义一个中间件

#### 3.8.1 需求描述

自己手动模拟一个类似于 express.urlencoded 这样的中间件，来**解析并返回 POST 提交到服务器的表单数据**。

#### 3.8.2 实现步骤

1. 定义中间件
2. 监听 req 的 **data 事件**
   【只要**有数据到达服务器**就会触发 `req.on('data',()=>{})` 事件】
   如果数据量比较大，无法一次性发送完毕，则**客户端会把数据切割后，分批发送到服务器**。
   所以 **data 事件可能会触发多次**，每一次触发 data 事件时，获取到数据只是完整数据的一部分，**需要手动对接收到的数据进行拼接**。
3. 监听 req 的 **end 事件**
   【当请求体**数据接收完毕**之后，会自动触发 `req.on('end',()=>{})` 事件】
   因此，我们可以在 end 事件中，拿到并**处理完整的请求体数据**。
4. 使用 **querystring** 内置模块解析请求体数据
5. 将解析出来的数据对象挂载为 `req.body`
6. 用 module.exports 将自定义中间件封装为模块 

封装：

~~~js
// 导入 Node.js 内置的 querystring 模块
const qs = require('node:querystring');

const bodyParser = (req, res, next) => {
  // 1. 定义一个 str 字符串，专门用来存储客户端发送过来的请求体数据
  let str = '';
  // 2. 监听 req 的 data 事件
  req.on('data', (chunk) => {
    str += chunk;
  });
  // 3. 监听 req 的 end 事件
  req.on('end', () => {
    const body = qs.parse(str); // 4.使用 querystring 内置模块把字符串格式的请求体数据，解析成对象格式
    req.body = body; // 5.将解析出来的数据对象挂载为 req.body
    next();
  });
};
// 6.用module.exports将自定义中间件封装为模块
module.exports = bodyParser;
~~~

使用：

~~~js
// 导入 express 模块
const express = require('express')
// 创建 express 的服务器实例
const app = express()

// 1. 导入自己封装的中间件模块
const customBodyParser = require('./14.custom-body-parser')
// 2. 将自定义的中间件函数，注册为全局可用的中间件
app.use(customBodyParser)

app.post('/user', (req, res) => {
  res.send(req.body)
})

// 调用 app.listen 方法，指定端口号并启动web服务器
app.listen(80, function () {
  console.log('Express server running at http://127.0.0.1')
})
~~~



## 4 跨域

### 4.1 跨域报错格式

只要出现跨域问题，浏览器就会出现一个固定格式的报错信息

```
Access to XMLHttpRequest at '服务器url地址' from origin 'null' has been blocked by CORS policy: No 'Access-Control-Allow-Origin' header is present on the requested resource.
```

### 4.2 跨域报错原因

**不满足同源策略:**

同源策略是一种约定，它是浏览器最核心也最基本的安全功能，如果缺少了同源策略，浏览器很容易受到XSS、CSRF等攻击。所谓同源是指"协议+域名+端口"三者相同，即便两个不同的域名指向同一个ip地址，也非同源。

**同源策略限制内容有：**

- Cookie、LocalStorage、IndexedDB 等存储性内容
- DOM 节点
- AJAX 请求发送后，结果被浏览器拦截了

但是有三个标签是允许跨域加载资源：(凡是带有“src”这个属性的标签都拥有跨域的能力，比如\<img>、\<iframe>、\<script>)

- `<img src=XXX>`
- `<link href=XXX>`
- `<script src=XXX>`



### 4.3 跨域解决方案

https://juejin.cn/post/6844903767226351623#heading-4

- JSONP (不推荐)

**利用 `<script>` 标签没有跨域限制的漏洞，网页可以得到从其他来源动态产生的 JSON 数据。JSONP请求一定需要对方的服务器做支持才可以。**

JSONP优点是简单兼容性好，可用于解决主流浏览器的跨域数据访问的问题。**缺点是仅支持get方法具有局限性,不安全可能会遭受XSS攻击。**

- cors

- nginx反向代理



### ▲4.4 CORS 跨域资源共享

cors 是 Express 的一个**第三方中间件**。通过安装和配置 cors 中间件，可以很方便地解决跨域问题。

CORS （Cross-Origin Resource Sharing，跨域资源共享）**由一系列 HTTP 响应头组成**，这些 HTTP 响应头决定浏览器是否阻止前端 JS 代码跨域获取资源。

浏览器的同源安全策略默认会阻止网页“跨域”获取资源。但如果**接口服务器配置了 CORS 相关的 HTTP 响应头，就可以解除浏览器端的跨域访问限制。**

<img src="6. Express.assets/image-20220424164304518.png" alt="image-20220424164304518" style="zoom:80%;" />



1. CORS 主要**在服务器端进行配置**。客户端浏览器无须做任何额外的配置，即可请求开启了 CORS 的接口。
2. CORS 在浏览器中有兼容性。只有支持 XMLHttpRequest Level2 的浏览器，才能正常访问开启了 CORS 的服务端接口（例如：IE10+、Chrome4+、FireFox3.5+）。



#### 4.4.1 使用步骤

使用步骤分为如下 3 步：

1. 运行 `npm install cors` **安装**中间件

2. 使用 `const cors = require('cors')`**导入**中间件

3. 在路由之前调用 `app.use(cors())` **配置**中间件



主服务器文件

~~~js
// 导入 express
const express = require('express');
// 创建服务器实例
const app = express();

// 提前注册解析表单数据的中间件
app.use(express.urlencoded({ extended: false }));

// 必须在配置 cors 中间件之前，配置 JSONP 的接口
app.get('/api/jsonp', (req, res) => {
  // TODO: 定义 JSONP 接口具体的实现过程
  // 1. 得到函数的名称
  const funcName = req.query.callback;
  // 2. 定义要发送到客户端的数据对象
  const data = { name: 'zs', age: 22 };
  // 3. 拼接出一个函数的调用
  const scriptStr = `${funcName}(${JSON.stringify(data)})`;
  // 4. 把拼接的字符串，响应给客户端
  res.send(scriptStr);
});

// 一定要在路由之前，配置 cors 这个中间件，从而解决接口跨域的问题
const cors = require('cors');
app.use(cors());

// 导入路由模块
const router = require('./16.apiRouter');
// 把路由模块，注册到 app 上
app.use('/api', router);

// 启动服务器
app.listen(80, () => {
  console.log('express server running at http://127.0.0.1');
});

~~~

路由文件 16.apiRouter.js

~~~js
const express = require('express')
const router = express.Router()

// 在这里挂载对应的路由
router.get('/get', (req, res) => {
  // 通过 req.query 获取客户端通过查询字符串，发送到服务器的数据
  const query = req.query
  // 调用 res.send() 方法，向客户端响应处理的结果
  res.send({
    status: 0, // 0 表示处理成功，1 表示处理失败
    msg: 'GET 请求成功！', // 状态的描述
    data: query, // 需要响应给客户端的数据
  })
})

// 定义 POST 接口
router.post('/post', (req, res) => {
  // 通过 req.body 获取请求体中包含的 url-encoded 格式的数据
  const body = req.body
  // 调用 res.send() 方法，向客户端响应结果
  res.send({
    status: 0,
    msg: 'POST 请求成功！',
    data: body,
  })
})

// 定义 DELETE 接口
router.delete('/delete', (req, res) => {
  res.send({
    status: 0,
    msg: 'DELETE请求成功',
  })
})

module.exports = router
~~~



#### 4.4.2 CORS 响应头部

- ##### Access-Control-Allow-**Origin**  限制请求来源

其中，origin 参数的值指定了**允许访问该资源的外域 URL**。

例如，下面的字段值将**只允许**来自 http://itcast.cn 的请求：

~~~js
res.setHeader('Access-Control-Allow-Origin', 'http://itcast.cn')
~~~

如果指定了 Access-Control-Allow-Origin 字段的值为通配符 *，表示**允许来自任何域的请求**，示例代码如下：
~~~js
res.setHeader('Access-Control-Allow-Origin', '*')
~~~



- ##### Access-Control-Allow-**Headers**  接收额外请求头

默认情况下，CORS 仅支持客户端向服务器发送如下的 9 个请求头：

Accept、Accept-Language、Content-Language、DPR、Downlink、Save-Data、Viewport-Width、Width 、Content-Type （值仅限于 text/plain、multipart/form-data、application/x-www-form-urlencoded 三者之一）



如果客户端向服务器**发送了额外的请求头信息**，则需要在服务器端，通过 Access-Control-Allow-Headers **对额外的请求头进行声明**，否则这次请求会失败！

~~~js
// 允许客户端额外向服务器发送 Content-Type 请求头和 X-Custom-Header 请求头
// 注意：多个请求头之间使用英文逗号进行分隔！！
res.setHeader('Access-Control-Allow-Headers', 'Content-Type, X-Custom-Header')
~~~



- ##### Access-Control-Allow-Methods  限制允许使用的 HTTP 方法

默认情况下，CORS 仅支持客户端发起 GET、POST、HEAD 请求。

如果客户端希望通过 PUT、DELETE 等方式请求服务器的资源，则需要在服务器端，通过 Access-Control-Alow-Methods来指明实际请求

所允许使用的 HTTP 方法。

~~~js
// 只允许 POST GET DELETE HEAD 请求方法
res.setHeader('Access-Control-Allow-Methods', 'POST, GET, DELETE, HEAD')
// 允许所有的 HTTP 请求方法
res.setHeader('Access-Control-Allow-Methods', '*')
~~~



#### 4.4.3 CORS请求的分类（预检请求）

客户端在请求 CORS 接口时，根据请求方式和请求头的不同，可以将 CORS 的请求分为两大类，分别是：

-  **简单请求**

同时满足以下两大条件的请求，就属于简单请求：

1.  请求方式：**GET、POST、HEAD** 三者之一
2.  HTTP 头部信息无自定义头部字段、且不超过以下几种字段：、Accept、Accept-Language、Content-Language、DPR、Downlink、Save-Data、Viewport-Width、Width 、Content-Type（只有三个值application/x-www-form-urlencoded、multipart/form-data、text/plain）



- **预检请求**

只要符合以下任何一个条件的请求，都需要进行预检请求：

1. 请求方式为 GET、POST、HEAD **之外**的请求 Method 类型
2.  请求头中包含**自定义头部字段**
3.  向服务器发送了 `application/json` 格式的数据

在浏览器与服务器正式通信之前，浏览器会**先发送 OPTION 请求进行预检**，以获知服务器是否允许该实际请求，所以这一次的 OPTION 请求称为“预检请求”。

服务器成功响应预检请求后，才会发送真正的请求，并且携带真实数据。



**简单请求和预检请求的区别**

简单请求的特点：客户端与服务器之间只会发生**一次请求**。

预检请求的特点：客户端与服务器之间会**发生两次请求**，**OPTION 预检请求成功之后，才会发起真正的请求。**（防止恶意DELETE）







### 4.5 JSONP 解决跨域

#### 4.5.1 JSONP 概念

概念：浏览器端通过 <script> 标签的 src 属性，请求服务器上的数据，同时，服务器返回一个函数的调用。这种请求数据的方式叫做 JSONP。
特点：
JSONP 不属于真正的 Ajax 请求，因为它没有使用 XMLHttpRequest 这个对象。
JSONP 仅支持 GET 请求，不支持 POST、PUT、DELETE 等请求。



#### 4.5.2 实现 JSONP 接口的步骤

1. **获取客户端**发送过来的**回调函数的名字**
2. 得到要通过 JSONP 形式发送给客户端的**数据**
3. 根据前两步得到的数据，**拼接出一个函数调用的字符串**
4. 把上一步拼接得到的字符串，**响应**给客户端的 <script> 标签进行解析执行



#### 4.5.3 创建 JSONP 接口的注意事项

如果**项目中已经配置了 CORS** 跨域资源共享，为了防止冲突，必须在配置 **CORS 之前声明 JSONP** 的接口。

否则 JSONP 接口会被处理成开启了 CORS 的接口。示例代码如下：

~~~js
// 导入 express
const express = require('express');
// 创建服务器实例
const app = express();
// 提前注册解析表单数据的中间件
app.use(express.urlencoded({ extended: false }));

// 必须在配置 cors 中间件之前，配置 JSONP 的接口
// jsonp 只支持 get 请求，所以绑定在 app.get
// 因为在路由模块之前，所以要自己挂载一个 /api
app.get('/api/jsonp', (req, res) => {
  // 1. 得到函数的名称
  const funcName = req.query.callback;
  // 2. 定义要发送到客户端的数据对象
  const data = { name: 'zs', age: 22 };
  // 3. 拼接出一个函数的调用
  const scriptStr = `${funcName}(${JSON.stringify(data)})`;
  // 4. 把拼接的字符串，响应给客户端
  res.send(scriptStr);
});

// 在路由之前，配置 cors 这个中间件，从而解决接口跨域的问题
const cors = require('cors');
app.use(cors());

// 导入路由模块
const router = require('./16.apiRouter');
// 把路由模块，注册到 app 上
app.use('/api', router);

// 启动服务器
app.listen(80, () => {
  console.log('express server running at http://127.0.0.1');
});

~~~



## 七、数据库、身份认证

## 1 数据库的基本概念

### 1.1 什么是数据库

数据库（database）是用来组织、存储和管理数据的仓库。

当今世界是一个充满着数据的互联网世界，充斥着大量的数据。数据的来源有很多，比如出行记录、消费记录、浏览的网页、发送的消息等等。除了文本类型的数据，图像、音乐、声音都是数据。

为了方便管理互联网世界中的数据，就有了**数据库管理系统**的概念（简称：数据库）。用户可以对数据库中的数据进行**新增、查询、更新、删除**等操作。



### 1.2 常见的数据库及分类

市面上的数据库有很多种，最常见的数据库有如下几个：

-  **MySQL** 数据库（目前使用最广泛、流行度最高的开源免费数据库；Community【社区免费版，企业可用】 + Enterprise【企业收费版】）
-  Oracle 数据库（收费）
-  SQL Server 数据库（收费；微软出品）
-  **Mongodb** 数据库（Community【社区免费版，企业可用】+ Enterprise【企业收费版】）



其中，MySQL、Oracle、SQL Server 属于**传统型数据库**（又叫做：关系型数据库 或 SQL 数据库），这三者的设计理念相同，用法比较类似。【学会其中一个，就能轻易上手另外的】

而 Mongodb 属于新型数据库（又叫做：**非关系型数据库 或 NoSQL 数据库**），它在一定程度上弥补了传统型数据库的缺陷。【和传统型数据库是相辅相成的关系，在企业开发中可能既用传统数据库，又用 Mongodb 】



### 1.3 传统型数据库的数据组织结构

#### 1.3.1 Excel 的数据组织结构

每个 Excel 中，数据的组织结构分别为**工作簿**、**工作表**、**数据行**、**列**这 4 大部分组成。

1. 整个 Excel 叫做**工作簿**
2. users 和 books 是**工作表**
3. users 工作表中有 3 **行**数据
4. 每行数据由 6 **列**信息组成
5. 每列信息都有对应的数据类型

<img src="7. 数据库、身份认证.assets/image-20220425124723588.png" alt="image-20220425124723588"  />

#### 1.3.2 传统型数据库的数据组织结构

在传统型数据库中，数据的组织结构分为 **数据库(database)**、**数据表(table)**、**数据行(row)**、**字段(field)** 这 4 大部分组成。

- **数据库**类似于 Excel 的**工作簿**
- **数据表**类似于 Excel 的**工作表**
- **数据行**类似于 Excel 的每一**行**数据
- **字段**类似于 Excel 的**列**
- 每个**字段**都有对应的**数据类型**

#### 1.3.3 实际开发中库、表、行、字段的关系

1. 在实际项目开发中，一般情况下，**每个项目都对应独立的数据库**。
2. 不同的数据，要存储到数据库的不同表中，例如：**用户数据存储到 users 表**中，**图书数据存储到 books 表**中。
3. 每个表中具体存储哪些信息，由字段来决定，例如：我们可以为 users 表设计 id、username、password 这3 个字段。
4. 表中的行，代表每一条具体的数据。



## 2 安装并配置 MySQL

MySQL下载页 https://dev.mysql.com/downloads/

[Mac安装教程](./MySQL for Mac)

[Windows安装教程](./MySQL for Windows)





## 3 MySQL的基本使用

### 3.1 使用 MySQL Workbench 管理数据库

#### 3.1.1 连接数据库

<img src="7. 数据库、身份认证.assets/image-20220426104227205.png" alt="image-20220426104227205" style="zoom: 80%;" />

#### 3.1.2 了解主界面的组成部分

<img src="7. 数据库、身份认证.assets/image-20220426104621537.png" alt="image-20220426104621537"  />

#### 3.1.3 创建数据库

![image-20220426104724241](7. 数据库、身份认证.assets/image-20220426104724241.png)

#### 3.1.4 创建数据表

![image-20220426104752665](7. 数据库、身份认证.assets/image-20220426104752665.png)

**DataType 数据类型：**

-  int 整数
-  varchar(len) 字符串
-  tinyint(1) 布尔值

**字段的特殊标识：**

- **PK（Primary Key）主键、唯一标识**

- **NN（Not Null）值不允许为空**【不传入值时，就取默认值】

- **UQ（Unique）值唯一**

- BIN：binary 二进制数据(比text更大的二进制数据)

- UN：unsigned 无符号   整数（非负数）

- ZF：zero fill 填充0 例如字段内容是1 int(4), 则内容显示为0001

- **AI（Auto Increment）值自动增长**

- G：generated column 生成列

- 在mysql查询语句中加\g、\G的意思：

  \g 的作用是分号和在sql语句中写“；”是等效的
  \G 的作用是将查到的结构旋转90度变成纵向（换行打印）

#### 3.1.5 向表中写入数据

![image-20220426105545005](7. 数据库、身份认证.assets/image-20220426105545005.png)



| 菜单                     | 翻译              |
| ------------------------ | ----------------- |
| Select Rows Limit 1000   | 选择行数限制 1000 |
| Table Inspector          | 表检查器          |
| Copy to Clipboard        | 复制到剪贴板      |
| Table Data Export Wizard | 表数据导出向导    |
| Table Data Import Wizard | 表数据导入向导    |
| Send to SQL Editor       | 发送到 SQL 编辑器 |
| Create Table.            | 创建表。          |
| Create Table Like.       | 创建表喜欢。      |
| Alter Table.             | 更改表。          |
| Table Maintenance.       | 表维护。          |
| Drop Table.              | 丢弃表。          |
| Truncate Table.          | 截断表。          |
| Search Table Data.       | 搜索表数据。      |
| Refresh All              | 全部刷新          |



### 3.2.1 什么是 SQL

SQL（英文全称：Structured Query Language）是**结构化查询语言**，专门用来访问和处理数据库的编程语言。能够让我们以编程的形式，操作数据库里面的数据。

三个关键点：

1. SQL 是一门**数据库编程语言**
2. 使用 SQL 语言编写出来的代码，叫做 SQL 语句
3. SQL 语言**只能在关系型数据库中使用**（例如 MySQL、Oracle、SQL Server）。非关系型数据库（例如 Mongodb）不支持 SQL 语言



### ▲3.2.2 SQL 使用注意点

#### 1 执行 SQL 之前

- 想要执行 SQL 语句，**在此之前**你必须选择你要操作的数据库，**数据库名字加粗就代表当前操作的数据库**，有2种方法:

1. **双击**你想操作的数据库，使之数据库名字加粗
2. 在所有语句之前执行 `USE xxx`



#### 2 执行 SQL 语句

1.  点击闪电图标
2.  Ctrl + Enter  执行光标处的一条语句（Windows）
2.  **Ctrl + Shift + Enter  执行所有语句**（Windows）



#### 3 SQL 的**注释**方法

1. 在语句前面加上 -- 
2. 选中、Ctrl + / 

~~~sql
-- USE my_db_01;	// 每句话最后记得要加分号
SELECT * FROM users
~~~



#### 4 每句 SQL 最后记得要加分号

#### 5 每个字句最好分行写（FROM、SET、WHERE）



### ▲3.3 查 SELECT ... FROM ...

SELECT 语句用于**从表中查询数据**。执行的结果被存储在一个**结果表**中（称为**结果集**）

~~~sql
-- 从 FROM 指定的【表中】，查询出指定 【列名称（字段）】的数据
SELECT 列名称,列名称,列名称 FROM 表名称

-- 从 FROM 指定的【表中】,查询出【所有】的数据。*表示【所有列】
SELECT * FROM 表名称
~~~



换行、tab、大间隔 在SQL 语句里都没有作用

随着你的查询越来越复杂，最好**把每条子句放在新建行**里

~~~sql
SELECT 列名称,列名称,列名称 
FROM 表名称
~~~



### ▲3.4 增

不论用以下哪种方法，当你要插入一行数据时，都得给够**没有默认值（要求非空的列，只要有默认值，你还是可以不给的）的列值**

【你可以不给id、status，但不能不给username和password】



#### 法一：INSERT INTO ...() VALUES()

INSERT INTO 语句用于向数据表中**插入新的数据行**，语法格式如下：

~~~sql
INSERT INTO 表名(列1, 列2)
VALUES(值1, 值2)
~~~

~~~sql
-- 如果 098123 没有加单引号，那就会当做数字，最后新增的结果是98123
INSERT INTO users(username, password) 
VALUES('tony stark', '098123');

-- 如果没有指定要插入数据的列名，则需要列出插入行的每一列数据【连id都要！】
INSERT INTO users 
VALUES(8, 't', '111', 0) ;
~~~



#### 法二：INSERT INTO ... SET ...

~~~sql
INSERT INTO 表名
SET 列1 = 值1, 列2 = 值2
~~~

~~~sql
INSERT INTO users SET username= 'Spider-Man', password= 'pcc123' ;
~~~







### ▲3.5 改 UPDATE ... SET ... WHERE ...

UPDATE 语句用于**修改**表中的数据。

~~~sql
-- 1. 用 UPDATE 指定要更新哪个表中的数据
-- 2. 用 SET    指定你想更新的 列和新值
-- 3. 用 WHERE  指定更新的条件 【如果省略了 WHERE 子句，所有的记录都将被更新!!!】
UPDATE users 
SET 列名 = 新值, 列名 = 新值 
WHERE 列名 = 原值;
~~~



### ▲3.6 删 DELETE FROM ... WHERE ...

DELETE 语句用于**删除表中的行**

~~~sql
DELETE FROM 表名
WHERE 列名 = 原值;
-- 【如果省略了 WHERE 子句，所有的记录都将被删除!!!】
~~~

~~~sql
-- 例子
DELETE FROM users
WHERE id = 6;
~~~



### 3.7 WHERE 子句

WHERE 子句用于**限定选择的条件**。

在 SELECT（查）、UPDATE（改）、DELETE（删） 语句中，皆可使用 WHERE 子句来限定条件。

~~~sql
-- 查询语句中的 WHERE 条件
SELECT 列名称 FROM 表名称 WHERE 列 运算符 值

-- 更新语句中的 WHERE 条件
UPDATE 表名称 SET 列=新值 WHERE 列 运算符 值

-- 删除语句中的 WHERE 条件
DELETE FROM 表名称 WHERE 列 运算符 值
~~~



可在 WHERE 子句中使用的**运算符：**

| 操作符  | 描述         |
| ------- | ------------ |
| =       | 等于         |
| <>  !=  | 不等于       |
| >       | 大于         |
| <       | 小于         |
| >=      | 大于等于     |
| <=      | 小于等于     |
| BETWEEN | 在某个范围内 |
| LIKE    | 搜索某种模式 |



#### BETWEEN

~~~sql
选取 alexa 介于 1 和 20 之间的所有网站：
SELECT * FROM Websites
WHERE alexa BETWEEN 1 AND 20;

选取 alexa 不介于 1 和 20 之间的所有网站：
SELECT * FROM Websites
WHERE alexa NOT BETWEEN 1 AND 20;

选取 name 以介于 'A' 和 'H' 之间字母开始的所有网站：
SELECT * FROM Websites
WHERE name BETWEEN 'A' AND 'H';

选取 date 介于 '2016-05-10' 和 '2016-05-14' 之间的所有访问记录：
SELECT * FROM access_log
WHERE date BETWEEN '2016-05-10' AND '2016-05-14';
~~~



#### LIKE

~~~sql
选取 name 以字母 "G" 开始的所有客户：
SELECT * FROM Websites
WHERE name LIKE 'G%';

选取 name 以字母 "k" 结尾的所有客户：
SELECT * FROM Websites
WHERE name LIKE '%k';

选取 name 包含模式 "oo" 的所有客户：
SELECT * FROM Websites
WHERE name LIKE '%oo%';
~~~



### 3.8 AND 和 OR 运算符

AND 和 OR 可**在 WHERE 子语句中**把两个或多个条件结合起来。

**AND** 表示必须同时满足多个条件，相当于 JavaScript 中的 **&&** 运算符，例如 if (a !== 10 && a !== 20) 

**OR** 表示只要满足任意一个条件即可，相当于 JavaScript 中的 **||** 运算符，例如 if(a !== 10 || a !== 20)



### 3.9 ORDER BY 子句

ORDER BY 语句用于根据指定的列对结果集进行**排序**。

ORDER BY 语句**默认按照升序**对记录进行排序。

- 如果您希望按照**降序**对记录进行排序，后面添加 **DESC 关键字**。
- 升序的话其实也可以在后面加 **ASC 关键字**

~~~sql
选自 "Websites" 表的数据：
+----+--------------+---------------------------+-------+---------+
| id | name         | url                       | alexa | country |
+----+--------------+---------------------------+-------+---------+
| 1  | Google       | https://www.google.cm/    | 1     | USA     |
| 2  | 淘宝          | https://www.taobao.com/   | 13    | CN      |
| 3  | 菜鸟教程      | http://www.runoob.com/    | 4689  | CN      |
| 4  | 微博          | http://weibo.com/         | 20    | CN      |
| 5  | Facebook     | https://www.facebook.com/ | 3     | USA     |
+----+--------------+---------------------------+-------+---------+

按照 "alexa" 列排序：
SELECT * FROM Websites
ORDER BY alexa;

按照 "alexa" 列降序排序：
SELECT * FROM Websites
ORDER BY alexa DESC;

先按"country"排，同名的再按"alexa"排
SELECT * FROM Websites
ORDER BY country,alexa;

先按"country"倒序排，同名的再按"alexa"正序排
SELECT * FROM Websites
ORDER BY country DESC, alexa ASC;
~~~



### 3.10 COUNT(*) 函数

COUNT(*) 函数用于返回查询符合条件的总**数据条数**

如果希望给查询出来的**列名称设置别名**，可以使用 **AS** 关键字

~~~sql
+-----+---------+-------+------------+
| aid | site_id | count | date       |
+-----+---------+-------+------------+
|   1 |       1 |    45 | 2016-05-10 |
|   2 |       3 |   100 | 2016-05-13 |
|   3 |       1 |   230 | 2016-05-14 |
|   4 |       2 |    10 | 2016-05-14 |
|   5 |       5 |   205 | 2016-05-14 |
|   6 |       4 |    13 | 2016-05-15 |
|   7 |       3 |   220 | 2016-05-15 |
|   8 |       5 |   545 | 2016-05-16 |
|   9 |       3 |   201 | 2016-05-17 |
+-----+---------+-------+------------+

计算 "access_log" 表中总记录数：
SELECT COUNT(*) AS nums FROM access_log;
结果：
+------+
| nums | 
+------+
|   9  |
+------+

计算 "access_log" 表中不同 site_id 的记录数：
SELECT COUNT(DISTINCT site_id) AS nums FROM access_log;
+------+
| nums | 
+------+
|   5  |
+------+
~~~





## 4 后端连接 MySQL

### 4.1 在项目中操作数据库的步骤

1. **安装**操作 MySQL 数据库的第三方模块 `mysql` （注意这个包名都是小写）
2. 通过 mysql 模块**连接**到 MySQL 数据库
3. 通过 mysql 模块**执行** SQL 语句

![image-20220428095817235](7. 数据库、身份认证.assets/image-20220428095817235.png)



### ▲4.2 安装与配置 mysql 模块

#### 4.2.1 安装 mysql 模块

~~~js
npm install mysql
~~~

#### ▲4.2.2 配置 mysql 模块

~~~js
// 1. 导入 mysql 模块
const mysql = require('mysql');

// 2. 建立与 MySQL 数据库的连接关系
const db = mysql.createPool({ // 传入一个对象{}
  host: '127.0.0.1', 	// 数据库的 IP 地址 (因为数据库在本地，所以用本地的IP地址)
  user: 'root', 		// 登录数据库的账号
  password: 'root', 	// 登录数据库的密码
  database: 'my_db_01', // 指定要操作哪个数据库
});
~~~

#### 4.2.3 测试 mysql 模块能否正常工作

~~~js
// 测试 mysql 模块能否正常工作
db.query('select 1', (err, results) => {
  if (err) return console.log(err.message);
  console.log(results);
});
// select 1 不需要返回任何字段，只是判断是否连接成功
// 成功的话会打印 [ RowDataPacket { '1': 1 } ]
~~~



### ▲4.3 在js文件中操作 MySQL 数据库

#### 4.3.1 查询数据

如果执行的是 **SELECT 查询语句**，则返回的 results 是**数组**(其他返回的都是对象)

~~~js
// 查询 users 表中所有的数据
const sqlStr = 'SELECT * FROM users'; //'select * from users'也可以

db.query(sqlStr, (err, results) => {
  // 如果查询数据失败，就打印错误信息
  if (err) return console.log(err.message);
  // 注意：如果执行的是 select 查询语句，则执行的结果是[数组]
  console.log(results);
});
~~~

<img src="7. 数据库、身份认证.assets/image-20220428184726239.png" alt="image-20220428184726239" style="zoom:50%;" />

#### 4.3.2 插入数据

##### 法一：INSERT INTO CALUES

执行 **INSERT INTO 语句**，返回的 results 是一个**对象**，可以通过 **affectedRows** 属性，判断是否插入数据成功



  ▲  待执行的 SQL 语句里，使用**英文的 ? 表示占位符**

- 如果 SQL 语句里有**多个占位符**，则必须使用**数组**为每个占位符指定具体的值

- 如果 SQL 语句里只有**一个**占位符，则**可以省略**数组

> ? 占位符的**作用：防止SQL注入**
>
> 参数化查询目前被视作是预防 SQL 注入攻击最有效的方法。参数化查询是指在设计与数据库连接并访问数据时，在需要填入数值或数据的地方，使用参数（Parameter）来给值。
>
> 在使用参数化查询的情况下，**数据库服务器不会将参数的内容视为 SQL 语句的一部分来进行处理**，而是在数据库**完成 SQL 语句的编译之后，才套用参数运行**。因此就算参数中含有破坏性的指令，也不会被数据库所运行。

~~~js
const user = { username: 'Spider-Man', password: 'pcc123' }

// 待执行的 SQL 语句，其中英文的 ? 表示占位符
const sqlStr = 'INSERT INTO users (username, password) VALUES (?, ?)'

// 使用数组的形式，依次为 ? 占位符指定具体的值
db.query(sqlStr, [user.username, user.password], (err, results) => {
  if (err) return console.log(err.message)
  // 注意：如果执行的是 insert into 插入语句，则 results 是一个对象
  // 可以通过 affectedRows 属性，来判断是否插入数据成功
  if (results.affectedRows === 1) {
    console.log('插入数据成功!')
  }
})
~~~



##### 法二：INSERT INTO SET

向表中新增数据时，如果**数据对象的每个属性和数据表的字段一一对应**，则可以通过如下方式快速插入数据：

~~~js
const user = { username: 'Spider-Man2', password: 'pcc4321' }
const sqlStr = 'INSERT INTO users SET ?'

db.query(sqlStr, user, (err, results) => {
  if (err) return console.log(err.message)
  if (results.affectedRows === 1) {
    console.log('插入数据成功')
  }
})
~~~

~~~js
const sql = 'INSERT INTO ev_users S ?'

// 也可以在 db.query 里面自己建一个对象
db.query(sql, { username: userinfo.username, password: userinfo.password }, (err, results) => {
    if (err) return res.cc(err)
    if (results.affectedRows !== 1) return res.cc('注册用户失败，请稍后再试！')
    res.cc('注册成功！', 0)
})
~~~





#### 4.3.3 更新数据

执行了 **UPDATE 语句**之后，返回的 results 也是一个**对象**，可以通过 **affectedRows** 判断是否更新成功

~~~js
const user = { id: 6, username: 'aaa', password: '000' }

// 待执行的 SQL 语句，其中英文的 ? 表示占位符
const sqlStr = 'UPDATE users SET username=?, password=? WHERE id=?'

// 使用数组的形式，依次为 ? 占位符指定具体的值
db.query(sqlStr, [user.username, user.password, user.id], (err, results) => {
  if (err) return console.log(err.message)
	// 注意：执行了 update 语句之后，执行的结果，也是一个对象.
    // 可以通过 affectedRows 判断是否更新成功
  if (results.affectedRows === 1) {
    console.log('更新成功')
  }
})
~~~

更新表数据时，如果数据对象的**每个属性和数据表的字段一一对应**，则可以通过如下方式快速更新表数据：

~~~js
const user = { id: 6, username: 'aaaa', password: '0000' }

const sqlStr = 'UPDATE users SET ? WHERE id=?'

db.query(sqlStr, [user, user.id], (err, results) => {
  if (err) return console.log(err.message)
  if (results.affectedRows === 1) {
    console.log('更新数据成功')
  }
})
~~~



#### 4.3.4 删除数据（慎用）

执行 **DELETE 语句**之后，返回的 results 也是一个**对象**，可以通过 **affectedRows** 判断是否更新成功

~~~js
// 删除 id 为 5 的用户
const sqlStr = 'DELETE FROM users WHERE id=?'
db.query(sqlStr, 5, (err, results) => {
  if (err) return console.log(err.message)
  // 注意：执行 delete 语句之后，结果也是一个对象，也会包含 affectedRows 属性
  if (results.affectedRows === 1) {
    console.log('删除数据成功')
  }
})
~~~



#### 4.3.5 标记删除（推荐）

使用 DELETE 语句，会把真正的把数据从表中删除掉。为了保险起见，推荐使用标记删除的形式，来**模拟删除的动作**。

所谓的标记删除，就是在表中**设置类似于 status 这样的状态字段**，来标记当前这条数据是否被删除。

当用户执行了删除的动作时，我们并没有执行 DELETE 语句把数据删除掉，而是**执行了 UPDATE 语句**，将这条数据**对应的 status 字段标记为删除**即可。

~~~js
// 标记删除：使用 UPDATE 语句替代 DELETE 语句；只更新数据的状态，并没有真正删除
const sqlStr = 'UPDATE users SET status=? WHERE id=?';
db.query(sqlStr, [1, 6], (err, results) => {
  if (err) return console.log(err.message);
  if (results.affectedRows === 1) {
    console.log('标记删除成功');
  }
});
~~~





## 5 前后端的身份认证

### 5.1 Web 开发模式

目前主流的 Web 开发模式有两种，分别是：

1. 基于**服务端渲染**的传统 Web 开发模式
2. 基于**前后端分离**的新型 Web 开发模式



#### 5.1.1 服务端渲染的 Web 开发模式

服务端渲染的概念：

服务器发送给客户端的 HTML 页面，是在服务器通过字符串的拼接，动态生成的。

（已经将数据一次性整合在 HTML 页面里了）

因此，**客户端不需要使用 Ajax** 这样的技术额外请求页面的数据。代码示例如下：

~~~js
app.get('index.html', (req, res)) => {
    // 1.要渲染的数据
    cosnet user = { name: 'zs', age: 20 }
    // 2.服务端通过字符串的拼接，动态生成 HTML 内容
    cosnet html = `<h1>姓名：${user.name}，年龄：${user.age}</h1>`
    // 3.把生成好的页面内容响应给客户端。
    // 因此客户端拿到的是带真实数据的 HTML 页面 （加载好所有数据的静态页面）
    res.send(html)
}
~~~

##### **优点：**

1. **前端耗时少**。因为服务器端负责动态生成 HTML 内容，浏览器只需要直接渲染页面即可。尤其是移动端，更省电。
2. **有利于SEO**。因为服务器端响应的是完整的 HTML 页面内容，所以爬虫更容易爬取获得信息，更有利于 SEO。

SEO是英文Search Engine Optimization的缩写，中文译为“**搜索引擎优化**”。简单地说，SEO是指从自然搜索结果获得网站流量的技术和过程。复杂但更严谨些的定义如下:

>  SEO是指在了解搜索引擎自然排名机关的基础上，**对网站进行内部及外部的调整优化，改进网站在搜索引擎中的关键词自然排名，获得更多流量**，从而达成网站销售及品牌建设的目标。



##### **缺点：**

1. **占用服务器端资源**。即服务器端完成 HTML 页面内容的拼接，如果请求较多，会对服务器造成一定的访问压力。
2. 不利于前后端分离，**开发效率低**。使用服务器端渲染，则无法进行分工合作，尤其对于前端复杂度高的项目，不利于项目高效开发。



#### 5.1.2 前后端分离的 Web 开发模式

前后端分离的概念：

前后端分离的开发模式，依赖于 Ajax 技术的广泛应用。

简而言之，就是**后端只负责提供 API 接口**，**前端使用 Ajax 调用接口**的开发模式。

（完整的 HTML 页面需要在客户端动态拼接完成）



##### **优点：**

1. **开发体验好**。前端专注于 UI 页面的开发，后端专注于api 的开发，且前端有更多的选择性。
2. **用户体验好**。Ajax 技术的广泛应用，极大的提高了用户的体验，可以轻松实现页面的局部刷新。
3. **减轻了服务器端的渲染压力**。因为页面最终是在每个用户的浏览器中生成的。



##### **缺点：**

1. **不利于 SEO**。因为完整的 HTML 页面需要在客户端动态拼接完成，所以爬虫对无法爬取页面的有效信息。

（解决方案：利用 Vue、React 等前端框架的 **SSR （server side render 服务端渲染）**技术能够很好的解决 SEO 问题！）

[面试官：SSR解决了什么问题？有做过SSR吗？你是怎么做的？ | web前端面试 - 面试官系列 (vue3js.cn)](https://vue3js.cn/interview/vue/ssr.html)



#### 5.1.3 如何选择 Web 开发模式

不谈**业务场景**而盲目选择使用何种开发模式都是耍流氓。

- 比如企业级网站，**主要功能是展示而没有复杂的交互**，并且需要良好的 SEO，则这时我们就需要使用服务器端渲染；

- 而类似后台管理项目，**交互性比较强**，不需要考虑 SEO，那么就可以使用前后端分离的开发模式。



另外，具体使用何种开发模式并不是绝对的，为了同时**兼顾了首页的渲染速度和前后端分离的开发效率**，一些网站采用了 **首屏服务器端渲染 + 其他页面前后端分离** 的开发模式。



### 5.2 身份认证

#### 5.2.1 什么是身份认证

身份认证（Authentication）又称“**身份验证”**、**“鉴权”**，是指通过一定的手段，完成对用户身份的确认。

日常生活中的身份认证随处可见，例如：高铁的验票乘车，手机的密码或指纹解锁，支付宝或微信的支付密码等。

在 Web 开发中，也涉及到用户身份的认证，例如：各大网站的手机验证码登录、邮箱密码登录、二维码登录等。

#### 5.2.2 为什么需要身份认证

身份认证的目的，是为了确认**当前所声称为某种身份的用户**，**确实是所声称的用户**。例如，你去找快递员取快递，你要怎么证明这份快递是你的。

在互联网项目开发中，如何对用户的身份进行认证，是一个值得深入探讨的问题。例如，如何才能保证网站不会错误的将“马云的存款数额”显示到“马化腾的账户”上。

#### 5.2.3 不同开发模式下的身份认证

对于 服务端渲染 和 前后端分离 这两种开发模式来说，分别有着不同的身份认证方案：

1. **服务端渲染** 推荐使用 **Session 认证机制**
2. **前后端分离** 推荐使用 **JWT 认证机制**



### 5.3 Session 认证机制

#### 5.3.1 HTTP 协议的无状态性

了解 HTTP 协议的无状态性是进一步学习 Session 认证机制的必要前提。

HTTP 协议的**无状态性**，指的是客户端的**每次 HTTP 请求都是独立的**，连续多个请求之间没有直接的关系，**服务器不会主动保留每次 HTTP 请求的状态**。



#### 5.3.2 突破 HTTP 无状态的限制

对于超市来说，为了方便收银员在进行结算时给 VIP 用户打折，超市可以为每个 VIP 用户发放会员卡。

<img src="7. 数据库、身份认证.assets/image-20220429165004817.png" alt="image-20220429165004817"  />

注意：现实生活中的会员卡身份认证方式，在 Web 开发中的专业术语叫做 **Cookie**。



#### ▲5.3.3 什么是 Cookie

Cookie 是存储在用户浏览器中的一段**不超过 4 KB 的字符串**。它由一个**名称**（Name）、一个**值**（Value）和其它几个用于控制 Cookie 有效期、安全性、使用范围的**可选属性**组成。

不同域名下的 Cookie 各自独立，每当客户端发起请求时，会**自动把当前域名下所有未过期的 Cookie 一同发送到服务器**。

Cookie的几大特性：

1. **自动**发送
2. 域名**独立**
3. **过期**时限（cookie是有有效期的）
4. 4KB **限制**



#### ▲5.3.4 Cookie 在身份认证中的作用

客户端**第一次请求**服务器的时候，服务器**通过响应头**的形式，向客户端发送一个身份认证的 Cookie，客户端会自动将 Cookie 保存在浏览器中。

随后，当客户端浏览器每次请求服务器的时候，浏览器会**自动**将身份认证相关的 Cookie，**通过请求头**的形式发送给服务器，服务器即可验明客户端的身份。

![image-20220429181438669](7. 数据库、身份认证.assets/image-20220429181438669.png)



#### 5.3.5 Cookie 不具有安全性

由于 Cookie 是存储在浏览器中的（存储在客户端），而且浏览器也提供了读写 Cookie 的 API，

因此 Cookie 很容易被伪造，不具有安全性。因此**不建议服务器将重要的隐私数据**，通过 Cookie 的形式发送给浏览器。比如用户的身份信息、密码等。

<img src="7. 数据库、身份认证.assets/image-20220429181619155.png" alt="image-20220429181619155"  />



#### 5.3.6 提高身份认证的安全性

为了防止客户伪造会员卡，收银员在拿到客户出示的会员卡之后，可以在收银机上进行**刷卡认证（cookie认证）**。只有收银机确认存在的会员卡，才能被正常使用。

这种**“会员卡 + 刷卡认证”**的设计理念，就是 **Session 认证机制**的精髓。

<img src="7. 数据库、身份认证.assets/image-20220429181944657.png" alt="image-20220429181944657"  />



#### ▲5.3.7 Session 的工作原理

Session 是存储在服务器端的，Cookie 是存储在客户端的。

![image-20220429182056664](7. 数据库、身份认证.assets/image-20220429182056664.png)



### 5.4 在 Express 中使用 Session 认证

#### 5.4.1 安装 express-session 中间件

~~~bash
npm install express-session
~~~

#### 5.4.2 配置 express-session 中间件

~~~js
// 1. 导入 express-session 中间件
var session = require('express-session')

// 2. 配置 session 中间件
app.use(
    session({
        secret: 'itheima', // secret属性可以为任意字符串
    	resave: false, // resave 强制保存 session 即使它并没有变化,默认为 true。
    	saveUninitialized: true, // 强制将未初始化的 session 存储,默认为 true。
    })
)
~~~

#### 5.4.3 向 session 中存数据（post）

配置 express-session 中间件后，**才可以通过 `req.session`** 来访问和使用 session 对象，

**`req.session.xxx` 可以自定义属性名**，存储用户信息：

~~~js
app.post('/api/login', (req, res) => {
  // 判断用户提交的登录信息是否正确
  if (req.body.username !== 'admin' || req.body.password !== '000000') {
    return res.send({ status: 1, msg: '登录失败' });
  }

  // TODO_02：请将登录成功后的用户信息，保存到 Session 中
  // 注意：只有成功配置了 express-session 这个中间件之后，才能有 req.session 这个属性
  req.session.user = req.body; // req.session.xxx 这个可以自定义
  req.session.islogin = true; // 用户的登录状态

  res.send({ status: 0, msg: '登录成功' });
});
~~~

#### 5.4.4 从 session 中取数据（get）

~~~js
// 获取用户姓名的接口
app.get('/api/username', (req, res) => {
  // TODO_03：请从 Session 中获取用户的名称，响应给客户端
  if (!req.session.islogin) {
    return res.send({ status: 1, msg: 'fail' });
  }
  res.send({
    status: 0,
    msg: 'success',
    username: req.session.user.username,
  });
});
~~~

#### 5.4.5 清空 session （post）

 `req.session.destroy() `函数的作用是：清空**当前**用户的 session 信息（不会清空其他用户的）。

~~~js
// 退出登录的接口
app.post('/api/logout', (req, res) => {
  // TODO_04：清空当前用户的 session 信息
  req.session.destroy();
  res.send({
    status: 0,
    msg: '退出登录成功',
  });
});
~~~



### 5.5 JWT 认证机制

#### 5.5.1 了解 Session 认证的局限性

Session 认证机制需要配合 Cookie 才能实现。由于 **Cookie 默认不支持跨域**访问，

所以，当涉及到前端跨域请求后端接口的时候，需要做很多额外的配置，才能实现跨域 Session 认证。

**注意：**

1. 当前端请求后端接口不存在跨域问题的时候，推荐使用 Session 身份认证机制。
2. 当前端**需要跨域请求后端接口**的时候，不推荐使用 Session 身份认证机制，推荐**使用 JWT** 认证机制。



#### 5.5.2 什么是 JWT

JWT（英文全称：JSON Web Token）是目前最流行的跨域认证解决方案。

Cookie、Session、Token、JWT 详解：https://juejin.cn/post/6844904034181070861



#### 5.5.3 JWT 的工作原理

用户的信息通过 Token 字符串的形式，**保存在客户端浏览器**中。服务器通过还原 Token 字符串的形式来认证用户的身份。

<img src="7. 数据库、身份认证.assets/image-20220429234721196.png" alt="image-20220429234721196" style="zoom: 80%;" />



#### 5.5.4  JWT 的组成部分

JWT 通常由三部分组成，分别是 Header（头部）、**Payload**（有效荷载）、Signature（签名）。

其中：

- **Payload 部分才是真正的用户信息**，它是用户信息经过**加密之后生成的字符串**。
- Header 和 Signature 是**安全性相关**的部分，只是为了保证 Token 的安全性。

<img src="7. 数据库、身份认证.assets/image-20220429235225858.png" alt="image-20220429235225858"  />



三者之间使用英文的“.”分隔，格式如下：

~~~js
<Header>.<Payload>.<Signature>

// token字符串示例（.将其分隔成三部分）
"token":"eyJhbGciOiJIUzI6IkpXVCJ9.eyJp5MSW101bmlbWUiOiLms6Xlt7Tlt7QiLCJlbWFpbCI6Im5pYmFiYUBpduY24iLCJ1c2VyX3BpYyI6IiIsImlhdCI6MTU3ODAzNjY4MiwiZXhwIjoxNTc4MDcyNjgyfQ.Mwq7GqCxJPK-EA8LNrtMG04llKdZ33S9KBL3XeuBxuI"

~~~



#### 5.5.5 JWT 的使用方式

客户端收到服务器返回的 JWT 之后，通常会将它**储存在浏览器的 localStorage 或 sessionStorage 中。**



在此之后，从客户端**第二次开始与服务器通信，都要带上这个 JWT 的字符串**，从而进行身份认证。推荐的做法是**把 JWT 放在 HTTP 请求头的 Authorization 字段**中，格式如下：

~~~js
Authorization: Bearer <token> // 'Bearer '后面的空格不能丢！！！
~~~



### ▲5.6 在 Express 中使用 JWT

#### 5.6.1 安装 JWT 相关的包

运行如下命令，安装如下两个 JWT 相关的包：

~~~bash
npm install jsonwebtoken express-jwt
~~~

其中：

- jsonwebtoken 用于**根据 JSON 对象生成 JWT 字符串**
- express-jwt 用于**将 JWT 字符串解析还原成 JSON 对象**



#### 5.6.2 导入 JWT 相关的包

~~~js
// TODO_01：安装并导入 JWT 相关的两个包，分别是 jsonwebtoken 和 express-jwt
const jwt = require('jsonwebtoken')
const expressJWT = require('express-jwt')
~~~



#### 5.6.3 定义 secret 密钥

为了保证 JWT 字符串的安全性，防止 JWT 字符串在网络传输过程中被别人破解，我们需要专门定义一个用于加密和解密的 secret 密钥：（**secret 密钥的本质就是一个自定义的字符串**）

1. 当生成 JWT 字符串的时候，需要使用 secret 密钥对用户的信息进行**加密**，最终得到加密好的 JWT 字符串
2. 当把 JWT 字符串解析还原成 JSON 对象的时候，需要使用 secret 密钥进行**解密**

~~~js
// TODO_02：定义 secret 密钥，建议将密钥命名为 secretKey
const secretKey = 'itheima No1 ^_^'
~~~



#### 5.6.4 在登录成功后生成 JWT 字符串

调用 jsonwebtoken 包提供的 `sign()` 方法，将用户的信息加密成 JWT 字符串，响应给客户端：

  // 参数1：用户的信息对象【记住：千万不要把密码加密到 token 字符中】
  // 参数2：加密的秘钥【上一步定义的常量】
  // 参数3：配置对象，可以 通过 `expiresIn:` 属性 配置当前 token 的有效期【属性值是字符串！】



jsonwebtoken中文文档： https://segmentfault.com/a/1190000009494020

~~~js
// 登录接口
app.post('/api/login', function (req, res) {
  // 将 req.body 请求体中的数据，转存为 userinfo 常量
  const userinfo = req.body
  // 登录失败
  if (userinfo.username !== 'admin' || userinfo.password !== '000000') {
    return res.send({
      status: 400,
      message: '登录失败！',
    })
  }
    
  // 登录成功
  // TODO_03：在登录成功之后，调用 jwt.sign() 方法生成 JWT 字符串。并通过 token 属性发送给客户端
  // 参数1：用户的信息对象
  // 参数2：加密的秘钥
  // 参数3：配置对象，可以 通过expiresIn:属性 配置当前 token 的有效期
  // 记住：千万不要把密码加密到 token 字符中
  const tokenStr = jwt.sign({ username: userinfo.username }, secretKey, {
    expiresIn: '30s', // 注意这是字符串！！！'30s''30h'
  });
  res.send({
    status: 200,
    message: '登录成功！',
    token: 'Bearer ' + tokenStr, 
    // 为了方便客户端使用 Token，在服务器端直接拼接上 'Bearer '的前缀【空格不能少！！】
  });
})
~~~



#### 5.6.5 将 JWT 字符串还原为 JSON 对象

客户端每次在访问那些有权限接口的时候，都需要主动通过请求头中的 Authorization 字段，将 Token 字符串发送到服务器进行身份认证。【所以要配置全局中间件，对每次请求都检查一次】

此时，服务器可以通过 `express-jwt` 这个中间件，自动将客户端发送过来的 Token 解析还原成 JSON 对象：

~~~js
// TODO_04：注册将 JWT 字符串解析还原成 JSON 对象的中间件
// 注意：只有配置成功了 express-jwt 这个中间件，才会把解析出来的用户信息，挂载到 req.user 属性上
// .unless() 指定哪些接口不需要访问权限。此处，登录、注册接口以api开头的这些都不需要访问权限
app.use(expressJWT({ secret: secretKey }).unless({ path: [/^\/api\//] }));
~~~



#### ▲5.6.6 使用 req.user 获取用户信息

**注意：**只有配置成功了 `express-jwt` 这个**中间件才会有**`req.user`，来访问从 JWT 字符串中解析出来的用户信息

【express-jwt 7 以上的版本，会挂载到`req.auth`而不是`req.user`】

~~~js
// 这是一个有权限的 API 接口（登录成功后才能拿到数据的接口）
app.get('/admin/getinfo', function (req, res) {
  // TODO_05：使用 req.user 获取用户信息，并使用 data 属性将用户信息发送给客户端
  console.log(req.user);
  res.send({
    status: 200,
    message: '获取用户信息成功！',
    data: req.user, // 要发送给客户端的用户信息
  });
});
~~~



前端发送请求示例：

![image-20220502114822053](7. 数据库、身份认证.assets/image-20220502114822053.png)



#### 5.6.7 捕获解析 JWT 失败后产生的错误

当使用 express-jwt 解析 Token 字符串时，如果客户端发送过来的 Token 字符串**过期或不合法**，会产生一个解析失败的错误，影响项目的正常运行。

我们可以通过 **Express 的错误中间件**，捕获这个错误并进行相关的处理，示例代码如下：

【**注意：**错误级别的中间件，必须**注册在所有路由之后！app.listen() 之前】**

~~~js
// TODO_06：使用全局错误处理中间件，捕获解析 JWT 失败后产生的错误
app.use((err, req, res, next) => {
  //'UnauthorizedError' 表示这次错误是由 token 解析失败导致的
  if (err.name === 'UnauthorizedError') {
    // 这里的return 是为了不执行下面那个500，不然就会执行2次res.send【res.send 无需return就能发到客户端】
    return res.send({ 
      status: 401,
      message: '无效的token',
    });
  }
  res.send({
    status: 500,
    message: '未知的错误',
  });
});

~~~



### ▲5.7 JWT 总结版 .js文件：

~~~js
// 导入 express 模块
const express = require('express');
// 创建 express 的服务器实例
const app = express();

// TODO_01：安装并导入 JWT 相关的两个包，分别是 jsonwebtoken 和 express-jwt
const jwt = require('jsonwebtoken');
const expressJWT = require('express-jwt');

// 允许跨域资源共享
const cors = require('cors');
app.use(cors());

// 解析 post 表单数据的中间件
const bodyParser = require('body-parser');
app.use(bodyParser.urlencoded({ extended: false }));

// TODO_02：定义 secret 密钥，建议将密钥命名为 secretKey
const secretKey = 'itheima No1 ^_^';

// TODO_04：注册将 JWT 字符串解析还原成 JSON 对象的中间件
// 注意：只有配置成功了 express-jwt 这个中间件，才会把解析出来的用户信息，挂载到 req.user 属性上
// .unless() 指定哪些接口不需要访问权限。登录、注册接口以api开头的这些都不需要访问权限
app.use(expressJWT({ secret: secretKey }).unless({ path: [/^\/api\//] }));

// 登录接口
app.post('/api/login', function (req, res) {
  // 将 req.body 请求体中的数据，转存为 userinfo 常量
  const userinfo = req.body;
  // 登录失败
  if (userinfo.username !== 'admin' || userinfo.password !== '000000') {
    return res.send({
      status: 400,
      message: '登录失败！',
    });
  }
  // 登录成功
  // TODO_03：在登录成功之后，调用 jwt.sign() 方法生成 JWT 字符串。并通过 token 属性发送给客户端
  // 参数1：用户的信息对象
  // 参数2：加密的秘钥
  // 参数3：配置对象，可以配置当前 token 的有效期
  // 记住：千万不要把密码加密到 token 字符中
  const tokenStr = jwt.sign({ username: userinfo.username }, secretKey, {
    expiresIn: '30s',
  });
  res.send({
    status: 200,
    message: '登录成功！',
    token: tokenStr, // 要发送给客户端的 token 字符串
  });
});

// 这是一个有权限的 API 接口（登录成功后才能拿到数据的接口）
app.get('/admin/getinfo', function (req, res) {
  // TODO_05：使用 req.user 获取用户信息，并使用 data 属性将用户信息发送给客户端
  console.log(req.user);
  res.send({
    status: 200,
    message: '获取用户信息成功！',
    data: req.user, // 要发送给客户端的用户信息
  });
});

// TODO_06：使用全局错误处理中间件，捕获解析 JWT 失败后产生的错误
app.use((err, req, res, next) => {
  // 'UnauthorizedError' 表示这次错误是由 token 解析失败导致的
  if (err.name === 'UnauthorizedError') {
    return res.send({
      // 这里的return 是为了不执行下面那个500，不然就会执行2次res.send【res.send 无需return就能发到客户端】
      status: 401,
      message: '无效的token',
    });
  }
  res.send({
    status: 500,
    message: '未知的错误',
  });
});

// 调用 app.listen 方法，指定端口号并启动web服务器
app.listen(8888, function () {
  console.log('Express server running at http://127.0.0.1:8888');
});

~~~









