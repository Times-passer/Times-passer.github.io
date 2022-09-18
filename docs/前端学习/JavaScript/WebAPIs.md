## 一、事件三要素：获取元素、绑定事件、操作元素

## 1.1. Web API介绍

### 1.1.1 API的概念

API（Application Programming Interface，应用程序编程接口）是一些预先定义的函数，目的是提供应用程序与开发人员基于某软件或硬件得以访问一组例程的能力，而又无需访问源码，无需理解其内部工作机制细节，只需直接调用使用即可。

![1550719355829](7 Web APIs.assets/1550719355829.png)

> 举例解释什么是API。
>
> 例如，
>
> ​	C语言中有一个函数 fopen()可以打开硬盘上的文件，这个函数对于我们来说，就是一个C语言提供的打开文件的工具。
>
> ​	javascript中有一个函数alert()可以在页面弹一个提示框，这个函数就是js提供的一个弹框工具。
>
> 这些工具（函数）由编程语言提供，内部的实现已经封装好了，我们只要学会灵活的使用这些工具即可。

### 1.1.2 Web  API的概念

​	Web API 是浏览器提供的一套操作**浏览器功能**和**页面元素**的 API ( BOM 和 DOM )。

​	现阶段我们主要针对于浏览器讲解常用的 API , 主要针对浏览器做交互效果。比如我们想要浏览器弹出一个警示框， 直接使用 alert(‘弹出’)

​	MDN 详细 API : https://developer.mozilla.org/zh-CN/docs/Web/API

​	因为 Web API 很多，所以我们将这个阶段称为 Web APIs。

​	此处的 Web API 特指浏览器提供的一系列API(很多函数或对象方法)，即操作网页的一系列工具。例如：操作html标签、操作页面地址的方法。

### 1.1.3 API 和 Web  API 总结

1. API 是为我们程序员提供的一个接口，帮助我们实现某种功能，我们会使用就可以了，不必纠结内部如何实现

2. Web API 主要是针对于浏览器提供的接口，主要针对于浏览器做交互效果。

3. Web API 一般都有输入和输出（函数的传参和返回值），Web API 很多都是方法（函数）

4. 学习 Web API 可以结合前面学习内置对象方法的思路学习



##  1.2. DOM 介绍

### 1.2.1 什么是DOM

​	文档对象模型（Document Object Model，简称DOM），是 [W3C](https://baike.baidu.com/item/W3C) 组织推荐的处理[可扩展标记语言](https://baike.baidu.com/item/%E5%8F%AF%E6%89%A9%E5%B1%95%E7%BD%AE%E6%A0%87%E8%AF%AD%E8%A8%80)（html或者xhtml）的标准[编程接口](https://baike.baidu.com/item/%E7%BC%96%E7%A8%8B%E6%8E%A5%E5%8F%A3)。

​	W3C 已经定义了一系列的 DOM 接口，通过这些 DOM 接口可以改变网页的内容、结构和样式。

> DOM是W3C组织制定的一套处理 html和xml文档的规范，所有的浏览器都遵循了这套标准。

### 1.2.2. DOM树

![1550731974575](https://i.loli.net/2021/07/28/GPwxlz6HSQjDcpX.png)

DOM树 又称为文档树模型，把文档映射成树形结构，通过节点对象对其处理，处理的结果可以加入到当前的页面。

- 文档：一个页面就是一个文档，DOM中使用document表示
- 节点：网页中的所有内容，在文档树中都是节点（标签、属性、文本、注释等），使用node表示
- 标签节点：网页中的所有标签，通常称为元素节点，又简称为“元素”，使用element表示

![1550732362134](7 Web APIs.assets/1550732362134.png)



## 1.3. ▲获取元素

为什么要获取页面元素？

例如：我们想要操作页面上的某部分(显示/隐藏，动画)，需要先获取到该部分对应的元素，再对其进行操作。

### 1.3.1. 根据ID获取

语法：`document.getElementById(id)`
作用：根据ID获取元素对象
参数：id值，区分大小写的字符串
返回值：**元素对象** 或 null



**案例代码**

```js
<body>
    <div id="time">2019-9-9</div>
    <script>
        // 因为我们文档页面从上往下加载，所以先得有标签 所以我们script写到标签的下面
        var timer = document.getElementById('time');
        console.log(timer);
        console.log(typeof timer);
        // console.dir 打印我们返回的元素对象 更好的查看里面的属性和方法
        console.dir(timer);
    </script>
</body>
```

### 1.3.2. 根据标签名获取元素

语法：`document.getElementsByTagName('标签名')` 【注意是element**s多了个s**】

或者 element.getElementsByTagName('标签名') 【**父元素element必须是单个对象**】

作用：根据标签名获取元素对象
参数：标签名
返回值：元素对象集合（不管有没有元素，返回的都是**伪数组**，数组元素是元素对象）



**案例代码**

```javascript
<body>
    <ul>
        <li>知否知否，应是等你好久11</li>
        <li>知否知否，应是等你好久22</li>
        <li>知否知否，应是等你好久33</li>
        <li>知否知否，应是等你好久44</li>
        <li>知否知否，应是等你好久55</li>
    </ul>
    <ol id="nav">
        <li>生僻字1</li>
        <li>生僻字2</li>
        <li>生僻字3</li>
        <li>生僻字4</li>
        <li>生僻字5</li>
    </ol>
    <script>
        // 1.返回的是 获取过来元素对象的集合 以伪数组的形式存储的
        var lis = document.getElementsByTagName('li');
        console.log(lis);
        console.log(lis[0]);
        // 2. 我们想要依次打印里面的元素对象我们可以采取遍历的方式
        for (var i = 0; i < lis.length; i++) {
            console.log(lis[i]);
        }

// 3. element.getElementsByTagName()  可以得到这个元素里面的某些标签
/*	var ol = document.getElementsByTagName('ol'); 
	console.log(ol[0].getElementsByTagName('li')); // ol要带[0]，是因为ByTagName返回的是伪数组
	
	等价于：
*/
        var nav = document.getElementById('nav'); // 通过id获得 nav 元素
        var navLis = nav.getElementsByTagName('li'); // 可以直接用nav作父元素，是因为ById返回的是元素
        console.log(navLis);
    </script>
</body>
```

![1550733441663](7 Web APIs.assets/1550733441663.png)

注意：getElementsByTagName()获取到是动态集合，即：当页面增加了标签，这个集合中也就增加了元素。

### ▲1.3.3. H5新增获取元素方式

![1550733518278](7 Web APIs.assets/1550733518278.png)

![1550733734425](7 Web APIs.assets/1550733734425.png)



**▲前面的document不是必须写死的，你可以改成某一个元素**：

~~~js
// 比如你先获取了一个元素叫focus
var focus = document.querySelector('.focus');

// 然后你可以获取focus的某一个子元素（防止整个文档里面有很多个ul会取错）
 var ul = focus.querySelector('ul');
~~~



**案例代码**

```html
<body>
    <div class="box">盒子1</div>
    <div class="box">盒子2</div>
    <div id="nav">
        <ul>
            <li>首页</li>
            <li>产品</li>
        </ul>
    </div>
    <script>
        // 1. getElementsByClassName 根据类名获得某些元素集合
        var boxs = document.getElementsByClassName('box');
        console.log(boxs);
        // 2. querySelector 返回指定选择器的第一个元素对象  切记 里面的选择器需要加符号 .box  #nav
        var firstBox = document.querySelector('.box');
        console.log(firstBox);
        var nav = document.querySelector('#nav');
        console.log(nav);
        var li = document.querySelector('li');
        console.log(li);
        // 3. querySelectorAll()返回指定选择器的所有元素对象集合
        var allBox = document.querySelectorAll('.box');
        console.log(allBox);
        var lis = document.querySelectorAll('li');
        console.log(lis);
    </script>
</body>
```

### 1.3.4 获取特殊元素（body，html）

![1550733794816](7 Web APIs.assets/1550733794816.png)



## 1.4. 事件基础

### 1.4.1. 事件概述

JavaScript 使我们有能力创建动态页面，而事件是可以被 JavaScript 侦测到的行为。

简单理解： **触发--- 响应机制**。

​	网页中的每个元素都可以产生某些可以触发 JavaScript 的事件，例如，我们可以在用户点击某按钮时产生一个 事件，然后去执行某些操作。

### 1.4.2. 事件三要素

- 事件源（谁）：触发事件的元素
- 事件类型（什么事件）： 例如 click 点击事件
- 事件处理程序（做啥）：事件触发后要执行的代码(函数形式)，事件处理函数

**案例代码**

```html
<body>
    <button id="btn">唐伯虎</button>
    <script>
        // 点击一个按钮，弹出对话框
        // 1. 事件是有三部分组成  事件源  事件类型  事件处理程序   我们也称为事件三要素
        //(1) 事件源 事件被触发的对象   谁  按钮
        var btn = document.getElementById('btn');
        //(2) 事件类型  如何触发 什么事件 比如鼠标点击(onclick) 还是鼠标经过 还是键盘按下
        //(3) 事件处理程序  通过一个函数赋值的方式 完成
        btn.onclick = function() {
            alert('点秋香');
        }
    </script>
</body>
```

### 1.4.3. 执行事件的步骤

1. 获取事件源
2. 注册事件（绑定事件）
3. 添加事件处理程序（采取函数赋值形式）



**案例代码**

```js
<body>
    <div>123</div>
    <script>
        // 执行事件步骤
        // 点击div 控制台输出 我被选中了
        // 1. 获取事件源
        var div = document.querySelector('div');
        // 2.绑定事件 注册事件
        // div.onclick 
        // 3.添加事件处理程序 
        div.onclick = function() {
            console.log('我被选中了');
        }
    </script>
</body>
```

### ▲1.4.4. 常见的鼠标事件

注意，这些是全局事件，只能 xxx.onclick 来使用，而不能写到 addEventListener 里

全局事件：https://developer.mozilla.org/zh-CN/docs/Web/HTML/Global_attributes



![1550734506084](7 Web APIs.assets/1550734506084.png)

### 1.4.5. 分析事件三要素

- 下拉菜单三要素
- 关闭广告三要素



## 1.5. 操作元素

​	JavaScript的 **DOM 操作**可以改变网页内容、结构和样式，我们可以利用 DOM 操作元素来改变元素里面的内容、属性等。（注意：这些操作都是**通过元素对象的属性**实现的）

### 1.5.1. 改变元素内容（获取或设置）

![1550735016756](7 Web APIs.assets/1550735016756.png)

**innerText改变元素内容**

```js
<body>
    <button>显示当前系统时间</button>
    <div>某个时间</div>
    <p>1123</p>
    <script>
        // 当我们点击了按钮，  div里面的文字会发生变化
        // 1. 获取元素 
        var btn = document.querySelector('button');
        var div = document.querySelector('div');
        // 2.注册事件
        btn.onclick = function() {
            // div.innerText = '2019-6-6';
            div.innerHTML = getDate();
        }
        function getDate() {
            var date = new Date();
            // 我们写一个 2019年 5月 1日 星期三
            var year = date.getFullYear();
            var month = date.getMonth() + 1;
            var dates = date.getDate();
            var arr = ['星期日', '星期一', '星期二', '星期三', '星期四', '星期五', '星期六'];
            var day = date.getDay();
            return '今天是：' + year + '年' + month + '月' + dates + '日 ' + arr[day];
        }
    </script>
</body>
```

**innerText和innerHTML的区别**

- 获取内容时的区别：

​	innerText会去除空格和换行，而innerHTML会保**留空格和换行**

- 设置内容时的区别：

​	innerText不会识别html，只显示文字；而innerHTML不仅显示文字，还**会识别html标签**

**案例代码**

```js
<body>
    <div>今天是：2019</div>
    <p>
        我是文字
        <span>123</span>
    </p>
    <script>
        // innerText 和 innerHTML的区别 
        // 1. innerText 不识别html标签 非标准  去除空格和换行
        var div = document.querySelector('div');
        // div.innerText = '<strong>今天是：</strong> 2019';
        // 2. innerHTML 识别html标签 W3C标准 保留空格和换行的
        div.innerHTML = '<strong>今天是：</strong> 2019';
        // 3. 这两个属性是可读写的  可以获取元素里面的内容
        var p = document.querySelector('p');
        console.log(p.innerText);
        console.log(p.innerHTML);
    </script>
</body>
```



### 1.5.2. 常用元素的属性操作

![1550735556297](7 Web APIs.assets/1550735556297.png)

**获取属性的值**

> 元素对象.属性名

**设置属性的值**

> 元素对象.属性名 = 值

**案例代码**

```js
<body>
    <button id="ldh">刘德华</button>
    <button id="zxy">张学友</button> <br>
    <img src="images/ldh.jpg" alt="" title="刘德华">
    <script>
        // 修改元素属性  src
        // 1. 获取元素
        var ldh = document.getElementById('ldh');
        var zxy = document.getElementById('zxy');
        var img = document.querySelector('img');
        // 2. 注册事件  处理程序
        zxy.onclick = function() {
            img.src = 'images/zxy.jpg';
            img.title = '张学友';
        }
        ldh.onclick = function() {
            img.src = 'images/ldh.jpg';
            img.title = '刘德华';
        }
    </script>
</body>
```



### 1.5.3. 案例：分时问候

![1550735858049](7 Web APIs.assets/1550735858049.png)

![1550735877145](7 Web APIs.assets/1550735877145.png)

### 1.5.4. 表单元素的属性操作

![1550736039005](7 Web APIs.assets/1550736039005.png)

**获取属性的值**

> 元素对象.属性名

**设置属性的值**

> 元素对象.属性名 = 值
>
> 表单元素中有一些属性如：disabled、checked、selected，元素对象的这些属性的值是布尔型。

**案例代码**

```js
<body>
    <button>按钮</button>
    <input type="text" value="输入内容">
    <script>
        // 1. 获取元素
        var btn = document.querySelector('button');
        var input = document.querySelector('input');
        // 2. 注册事件 处理程序
        btn.onclick = function() {
            // 表单里面的文字内容是通过 value 来修改的；而不是innerHTML
            input.value = '被点击了';
            // 如果想要某个表单被禁用 不能再点击 disabled  我们想要这个按钮 button禁用
            // btn.disabled = true;
            this.disabled = true;
            // this 指向的是事件函数的调用者 btn
        }
    </script>
</body>
```

### 1.5.5. 案例：仿京东显示密码

![1550736330331](7 Web APIs.assets/1550736330331.png)

![1550736346822](7 Web APIs.assets/1550736346822.png)

### 1.5.6. CSS属性操作

我们可以通过 JS 修改元素的大小、颜色、位置等样式。

**常用方式**

![1550736488634](7 Web APIs.assets/1550736488634.png)



#### 方式1：通过操作style属性

> 元素对象的style属性也是一个对象！
>
> 元素对象.style.样式属性 = 值;

![1550736620181](7 Web APIs.assets/1550736620181.png)

**案例代码**

```js
<head>
    div {
        width:100px;
        height:100px;
        background-color:pink;
    }

</head>
<body>
    <div></div>
    <script>
        // 1. 获取元素
        var div = document.querySelector('div');
        // 2. 注册事件 处理程序
        div.onclick = function() {
            // div.style里面的属性 采取驼峰命名法 
            this.style.backgroundColor = 'purple';
            this.style.width = '250px';
        }
    </script>
</body>
```

#### 案例：淘宝点击关闭二维码

![1550736843659](7 Web APIs.assets/1550736843659.png)

![1550736881832](7 Web APIs.assets/1550736881832.png)

#### 案例：循环精灵图背景

![1550736940082](7 Web APIs.assets/1550736940082.png)

![1550736956754](7 Web APIs.assets/1550736956754.png)

#### 案例：显示隐藏文本框内容

![1550737006593](7 Web APIs.assets/1550737006593.png)

![1550737019729](7 Web APIs.assets/1550737019729.png)

#### ▲方式2：通过操作className属性

> 元素对象.className = 值;
>
> 因为class是关键字，所有使用className。

![1550737214510](7 Web APIs.assets/1550737214510.png)

**案例代码**

```js
<body>
    <div class="first">文本</div>
    <script>
        // 1. 使用 element.style 获得修改元素样式  如果样式比较少 或者 功能简单的情况下使用
        var test = document.querySelector('div');
        test.onclick = function() {
            // this.style.backgroundColor = 'purple';
            // this.style.color = '#fff';
            // this.style.fontSize = '25px';
            // this.style.marginTop = '100px';

            // 2. 我们可以通过 修改元素的className更改元素的样式 适合于样式较多或者功能复杂的情况
            // 3. 如果想要保留原先的类名，我们可以用： 多类名选择器（原本类名+空格+新类名）
            // this.className = 'change';
            this.className = 'first change';
        }
    </script>
</body>
```

#### 案例：密码框格式提示错误信息

![1550737269546](7 Web APIs.assets/1550737269546.png)

![1550737284218](7 Web APIs.assets/1550737284218.png)





## 二、排他思想(页签)、CSS属性操作、节点操作

## 2.1. 排他操作

### 2.1.1 排他思想

![1550914482628](images/1550914482628.png)

如果有同一组元素，我们想要某一个元素实现某种样式， 需要用到循环的排他思想算法：

1. 所有元素全部清除样式（干掉其他人）

2. 给当前元素设置样式 （留下我自己）

3. 注意顺序不能颠倒，首先干掉其他人，再设置自己

```js
    <button>按钮1</button>
    <button>按钮2</button>
    <button>按钮3</button>
    <button>按钮4</button>
    <button>按钮5</button>
    <script>
        // 1. 获取所有按钮元素
        var btns = document.getElementsByTagName('button');
        // btns得到的是伪数组  里面的每一个元素 btns[i]
        for (var i = 0; i < btns.length; i++) {
            btns[i].onclick = function() {
                // (1) 我们先把所有的按钮背景颜色去掉  干掉所有人
                for (var i = 0; i < btns.length; i++) {
                    btns[i].style.backgroundColor = '';
                }
                // (2) 然后才让当前的元素背景颜色为pink 留下我自己
                this.style.backgroundColor = 'pink';

            }
        }
    </script>
```



## 2.2 案例：百度换肤

![1550914640677](images/1550914640677.png)

![1550914663042](images/1550914663042.png)

```js
<body>
    <ul class="baidu">
        <li><img src="images/1.jpg"></li>
        <li><img src="images/2.jpg"></li>
        <li><img src="images/3.jpg"></li>
        <li><img src="images/4.jpg"></li>
    </ul>
    <script>
        // 1. 获取元素 
        var imgs = document.querySelector('.baidu').querySelectorAll('img');
        // console.log(imgs);
        // 2. 循环注册事件 
        for (var i = 0; i < imgs.length; i++) {
            imgs[i].onclick = function() {
                // this.src 就是我们点击图片的路径   images/2.jpg
                // console.log(this.src);
                // 把这个路径 this.src 给body 就可以了
                document.body.style.backgroundImage = 'url(' + this.src + ')';
            }
        }
    </script>
</body>
```

## 2.3 案例：表格隔行变色

![1550914791881](images/1550914791881.png)

![1550914812202](images/1550914812202.png)

```js
    <script>
        // 1.获取元素 获取的是 tbody 里面所有的行
        var trs = document.querySelector('tbody').querySelectorAll('tr');
        // 2. 利用循环绑定注册事件
        for (var i = 0; i < trs.length; i++) {
            // 3. 鼠标经过事件 onmouseover
            trs[i].onmouseover = function() {
                    // console.log(11);
                    this.className = 'bg';
                }
                // 4. 鼠标离开事件 onmouseout
            trs[i].onmouseout = function() {
                this.className = '';
            }
        }
    </script>
```

## 2.4 案例：全选

![1550914980274](images/1550914980274.png)

![1550915005393](images/1550915005393.png)

```js
    <script>
        // 1. 全选和取消全选做法：  让下面所有复选框的checked属性（选中状态） 跟随 全选按钮即可
        // 获取元素
        
        var j_cbAll = document.getElementById('j_cbAll'); 
        var j_tbs = document.getElementById('j_tb').getElementsByTagName('input'); 
        // 全选按钮注册事件
        j_cbAll.onclick = function() {
                // this.checked 当前复选框的选中状态
                // console.log(this.checked);
                for (var i = 0; i < j_tbs.length; i++) {
                    j_tbs[i].checked = this.checked;
                }
         }
         // 2. 给所有的子复选框注册单击事件
        for (var i = 0; i < j_tbs.length; i++) {
            j_tbs[i].onclick = function() {
                // flag 控制全选按钮是否选中
                var flag = true;
                // 每次点击下面的复选框都要循环检查者4个小按钮是否全被选中
                for (var i = 0; i < j_tbs.length; i++) {
                    if (!j_tbs[i].checked) {
                        flag = false;
                        break; 
                    }
                }
                // 设置全选按钮的状态
                j_cbAll.checked = flag;
            }
        }
    </script>
```



## 2.5. 自定义属性操作

### 2.5.1 获取属性值

![1550915376339](images/1550915376339.png)

```js
    <div id="demo" index="1" class="nav"></div>
    <script>
        var div = document.querySelector('div');
        // 1. 获取元素的属性值
        // (1) element.属性
        console.log(div.id);
        //(2) element.getAttribute('属性')  get得到获取 attribute 属性的意思 我们程序员自己添加的属性我们称为自定义属性 index
        console.log(div.getAttribute('id'));
        console.log(div.getAttribute('index'));
	</script>
```



### 2.5.2. 设置属性值

![1550915445026](images/1550915445026.png)

```js
        // 2. 设置元素属性值
        // (1) element.属性= '值'
        div.id = 'test';
        div.className = 'navs';
        // (2) element.setAttribute('属性', '值');  主要针对于自定义属性
        div.setAttribute('index', 2);
        div.setAttribute('class', 'footer'); // class 特殊  这里面写的就是
```



### 2.5.3. 移除属性

![1550915513137](images/1550915513137.png)

```js
		// class 不是className
        // 3. 移除属性 removeAttribute(属性)    
        div.removeAttribute('index');
```



### 2.5.4. 案例：tab栏 ▲

![1550915567627](images/1550915567627.png)

![1550915590707](images/1550915590707.png)

```js
    <script>
        // 获取元素
        var tab_list = document.querySelector('.tab_list');
        var lis = tab_list.querySelectorAll('li');
        var items = document.querySelectorAll('.item'); // 通过伪数组让每块内容都有序号
        // for循环，给选项卡绑定点击事件
        for (var i = 0; i < lis.length; i++) {
            lis[i].setAttribute('index', i);	// 先给5个小li 设置索引号 
            lis[i].onclick = function() {
                // 1. 上面的模块选项卡，当前这一个底色会是红色，其余不变（排他思想）
                // 先把其他li元素的class清除
                for (var i = 0; i < lis.length; i++) {
                    lis[i].className = '';
                }
                // 再给自己添加class
                this.className = 'current';
                // 2. 下面的显示内容模块
                var index = this.getAttribute('index');
                console.log(index);
                // 干掉所有人 让其余的item 这些div 隐藏
                for (var i = 0; i < items.length; i++) {
                    items[i].style.display = 'none';
                }
                // 留下我自己 让对应的item 显示出来
                items[index].style.display = 'block';
            }
        }
    </script>
```



### 2.5.5. H5获取自定义属性的方法

自定义属性目的：是为了保存并使用数据。有些数据可以保存到页面中而不用保存到数据库中。

自定义属性**获取**是通过**getAttribute(‘属性’)** 获取。

但是有些自定义属性很容易引起歧义，不容易判断是元素的内置属性还是自定义属性。

H5给我们新增了自定义属性：

![1550915798516](images/1550915798516.png)

![1550915815571](images/1550915815571.png)

```js
    <div getTime="20" data-index="2" data-list-name="andy"></div>
    <script>
        var div = document.querySelector('div');
        // console.log(div.getTime);
        console.log(div.getAttribute('getTime'));
        div.setAttribute('data-time', 20);
        console.log(div.getAttribute('data-index'));
        console.log(div.getAttribute('data-list-name'));

        // h5新增的获取自定义属性的方法 它只能获取data-开头的
        // dataset 是一个集合里面存放了所有以data开头的自定义属性
        console.log(div.dataset);
        console.log(div.dataset.index);
        console.log(div.dataset['index']);
        // 如果自定义属性里面有多个-链接的单词，我们获取的时候采取 驼峰命名法
        console.log(div.dataset.listName);
        console.log(div.dataset['listName']);
    </script>
```



## 2.6. 节点操作

### 2.6.1. 节点概述

	网页中的所有内容都是节点（标签、属性、文本、注释等），在DOM 中，节点使用 node 来表示。
	
	HTML DOM 树中的所有节点均可通过 JavaScript 进行访问，所有 HTML 元素（节点）均可被修改，也可以创建或删除。

![1550970944363](images/1550970944363.png)

	一般地，节点至少拥有nodeType（节点类型）、nodeName（节点名称）和nodeValue（节点值）这三个基本属性。

![1550970986988](images/1550970986988.png)

### 2.6.2. 节点层级

	利用 DOM 树可以把节点划分为不同的层级关系，常见的是**父子兄层级关系**。
	
	![1550971058781](images/1550971058781.png)

### 2.6.3. 父级节点

![1550971196686](images/1550971196686.png)

```js
    <div class="demo">
        <div class="box">
            <span class="erweima">×</span>
        </div>
    </div>
    <script>
        // 1. 父节点 parentNode
        var erweima = document.querySelector('.erweima');
        // var box = document.querySelector('.box');
        // 得到的是离元素最近的父级节点(亲爸爸) 如果找不到父节点就返回为 null
        console.log(erweima.parentNode);
    </script>
```

### 2.6.4. 子节点

**所有子节点**

![1550971263925](images/1550971263925.png)

**子元素节点**

![1550971325828](images/1550971325828.png)

```js
    <ul>
        <li>我是li</li>
        <li>我是li</li>
        <li>我是li</li>
        <li>我是li</li>
    </ul>
    <script>
        // DOM 提供的方法（API）获取
        var ul = document.querySelector('ul');
        var lis = ul.querySelectorAll('li');
        // 1. 子节点  childNodes 所有的子节点 包含 元素节点 文本节点等等
        console.log(ul.childNodes);
        console.log(ul.childNodes[0].nodeType);
        console.log(ul.childNodes[1].nodeType);
        // 2. children 获取所有的子元素节点 也是我们实际开发常用的
        console.log(ul.children);
    </script>
```

**第1个子节点**

![1550971774758](images/1550971774758.png)

**最后1个子节点**

![1550971825493](images/1550971825493.png)

**第1个子元素节点**

![1550972014509](images/1550972014509.png)

**最后1个子元素节点**

![1550972106485](images/1550972106485.png)

	实际开发中，firstChild 和 lastChild 包含其他节点，操作不方便，而 firstElementChild 和 lastElementChild 又有兼容性问题，那么我们如何获取第一个子元素节点或最后一个子元素节点呢？

![1550972648014](images/1550972648014.png)

```js
    <ol>
        <li>我是li1</li>
        <li>我是li2</li>
        <li>我是li3</li>
        <li>我是li4</li>
        <li>我是li5</li>
    </ol>
    <script>
        var ol = document.querySelector('ol');
        // 1. firstChild 第一个子节点 不管是文本节点还是元素节点
        console.log(ol.firstChild);
        console.log(ol.lastChild);
        // 2. firstElementChild 返回第一个子元素节点 ie9才支持
        console.log(ol.firstElementChild);
        console.log(ol.lastElementChild);
        // 3. 实际开发的写法  既没有兼容性问题又返回第一个子元素
        console.log(ol.children[0]);
        console.log(ol.children[ol.children.length - 1]);
    </script>
```

### 2.6.5. 案例：新浪下拉菜单



![1550974934894](images/1550974934894.png)

![1550975025608](images/1550975025608.png)

![1550975049176](images/1550975049176.png)

```js
    <script>
        // 1. 获取元素
        var nav = document.querySelector('.nav');
        var lis = nav.children; // 得到4个小li
        // 2.循环注册事件
        for (var i = 0; i < lis.length; i++) {
            lis[i].onmouseover = function() {
                this.children[1].style.display = 'block';
            }
            lis[i].onmouseout = function() {
                this.children[1].style.display = 'none';
            }
        }
    </script>
```

### 2.6.6. 兄弟节点

**下一个兄弟节点**

![1550973538696](images/1550973538696.png)

**上一个兄弟节点**

![1550973558511](images/1550973558511.png)

```js
    <div>我是div</div>
    <span>我是span</span>
    <script>	
        var div = document.querySelector('div');
        // 1.nextSibling 下一个兄弟节点 【包含元素节点或者 文本节点】等等
        console.log(div.nextSibling);
        console.log(div.previousSibling);
        // 2. nextElementSibling 得到下一个兄弟元素节点
        console.log(div.nextElementSibling);
        console.log(div.previousElementSibling);
    </script>
```

**下一个兄弟元素节点（有兼容性问题）**

![1550973610223](images/1550973610223.png)

**上一个兄弟元素节点（有兼容性问题）**

![1550973630150](images/1550973630150.png)

![1550973722805](images/1550973722805.png)

![1550973799759](images/1550973799759.png)

```js
   function getNextElementSibling(element) {
      var el = element;
      while (el = el.nextSibling) {
        if (el.nodeType === 1) {
            return el;
        }
      }
      return null;
    }  
```

### 2.6.7. 创建节点

![1550975514321](images/1550975514321.png)

### 2.6.8. 添加子节点

![1550975640170](images/1550975640170.png)



* 注意都是添加到**子节点**里面，只是一个在前一个在后

```js
    <ul>
        <li>123</li>
    </ul>
    <script>
        // 1. 创建节点元素节点
        var li = document.createElement('li');

        // 2. 添加节点 node.appendChild(child)  node 父级  child 是子级 后面追加元素
        var ul = document.querySelector('ul');
        ul.appendChild(li);

	// 3. 添加节点 node.insertBefore(child, 指定元素);
        var lili = document.createElement('li');
        ul.insertBefore(lili, ul.children[0]);
        // 4. 我们想要页面添加一个新的元素 ： 1. 创建元素 2. 添加元素
    </script>
```

### 2.6.9. 案例：简单版发布留言

![1550975849302](images/1550975849302.png)

![1550975887017](images/1550975887017.png)

```js
<body>
    <textarea name="" id=""></textarea>
    <button>发布</button>
    <ul>

    </ul>
    <script>
        // 1. 获取元素
        var btn = document.querySelector('button');
        var text = document.querySelector('textarea');
        var ul = document.querySelector('ul');
        // 2. 注册事件
        btn.onclick = function() {
            if (text.value == '') {
                alert('您没有输入内容');
                return false;
            } else {
                // console.log(text.value);
                // (1) 创建元素
                var li = document.createElement('li');
                // 先有li 才能赋值
                li.innerHTML = text.value;
                // (2) 添加元素
                // ul.appendChild(li);
                ul.insertBefore(li, ul.children[0]);
            }
        }
    </script>
</body>
```



## 三、节点操作、增删改查总结、事件监听、事件流(捕获、冒泡)、鼠标事件

## 1.1. 节点操作

### 1.1.1 删除子节点

![1551163384254](images/1551163384254.png)

node.removeChild() 方法从 node节点中删除一个**子节点**，返回删除的节点。

```js
    <button>删除</button>
    <ul>
        <li>熊大</li>
        <li>熊二</li>
        <li>光头强</li>
    </ul>
    <script>
        // 1.获取元素
        var ul = document.querySelector('ul');
        var btn = document.querySelector('button');
        // 2. 删除元素  node.removeChild(child)
        // ul.removeChild(ul.children[0]);
        // 3. 点击按钮依次删除里面的孩子
        btn.onclick = function() {
            if (ul.children.length == 0) {
                this.disabled = true;
            } else {
                ul.removeChild(ul.children[0]);
            }
        }
    </script>
```



### 1.1.2 案例：删除留言

![1551163586475](images/1551163586475.png)

![1551163635501](images/1551163635501.png)

用a标签作为删除按钮：

```js
    <textarea name="" id=""></textarea>
    <button>发布</button>
    <ul>

    </ul>
    <script>
        // 1. 获取元素
        var btn = document.querySelector('button');
        var text = document.querySelector('textarea');
        var ul = document.querySelector('ul');
        // 2. 注册事件
        btn.onclick = function() {
            if (text.value == '') {
                alert('您没有输入内容');
                return false;
            } else {
                var li = document.createElement('li');
                // innerHTML的好处，添加删除标签：
                li.innerHTML = text.value + "<a href='javascript:;'>删除</a>";
                ul.insertBefore(li, ul.children[0]);
                // 删除元素：删除的是当前链接的li  它的父亲
                var as = document.querySelectorAll('a');
                as[0].onclick = function() {// querySelectorAll返回的是伪数组，所以要[0]
                // querySelector('a') 就可以不用[0]
                        // 删除的是 li 当前a所在的li  this.parentNode;
                        ul.removeChild(this.parentNode);
                    }
            }
        }
    </script>
```

用button标签作为删除按钮：

~~~js

<body>
    <textarea name="" id=""></textarea>
    <button>发布</button>
    <ul>

    </ul>
    <script>
        // 1. 获取元素
        var btn = document.querySelector('button');
        var text = document.querySelector('textarea');
        var ul = document.querySelector('ul');
        // 2. 注册事件
        btn.onclick = function() {
            if (text.value == '') {
                alert('您没有输入内容');
                return false;
            } else {
                var li = document.createElement('li');
                li.innerHTML = text.value + "<button >删除</button>";
                ul.insertBefore(li, ul.children[0]);
                var as = document.querySelector('li button'); // 注意！这个HTML里面还有“发布”按钮；如果只写button，会给“发布”按钮添加点击事件，所以要给 li 里面的 button 加事件
                    as.onclick = function() {
                        ul.removeChild(this.parentNode);
                    }
            }
        }
    </script>
</body>

~~~





### 1.1.3 复制（克隆）节点

![1551163763825](images/1551163763825.png)

```js
    <ul>
        <li>1111</li>
        <li>2</li>
        <li>3</li>
    </ul>
    <script>
        var ul = document.querySelector('ul');
        // 1. node.cloneNode(); 括号为空或者里面是false 浅拷贝 只复制标签不复制里面的内容
        // 2. node.cloneNode(true); 括号为true 深拷贝 复制标签并且复制里面的内容
        var lili = ul.children[0].cloneNode(true);
        ul.appendChild(lili);
    </script>
```

### 1.1.4 案例：动态生成表格

![1551163900675](images/1551163900675.png)

![1551163924396](images/1551163924396.png)

```js
    <script>
        // 1.先去准备好学生的数据
        var datas = [{
            name: '魏璎珞',
            subject: 'JavaScript',
            score: 100
        }, {
            name: '弘历',
            subject: 'JavaScript',
            score: 98
        }, {
            name: '傅恒',
            subject: 'JavaScript',
            score: 99
        }, {
            name: '明玉',
            subject: 'JavaScript',
            score: 88
        }, {
            name: '大猪蹄子',
            subject: 'JavaScript',
            score: 0
        }];
        // 2. 往tbody 里面创建行： 有几个人（通过数组的长度）我们就创建几行
        var tbody = document.querySelector('tbody');
		// 遍历数组
        for (var i = 0; i < datas.length; i++) { 
            // 1. 创建 tr行
            var tr = document.createElement('tr');
            tbody.appendChild(tr);
            // 2. 行里面创建单元格td 单元格的数量取决于每个对象里面的属性个数  
            // 使用for in遍历学生对象
            for (var k in datas[i]) { 
                // 创建单元格 
                var td = document.createElement('td');
                // 把对象里面的属性值 datas[i][k] 给 td  
                td.innerHTML = datas[i][k];
                tr.appendChild(td);
            }
            // 3. 创建有删除2个字的单元格 
            var td = document.createElement('td');
            td.innerHTML = '<a href="javascript:;">删除 </a>';
            tr.appendChild(td);

        }
        // 4. 删除操作 开始 
        var as = document.querySelectorAll('a');
        for (var i = 0; i < as.length; i++) {
            as[i].onclick = function() {
                // 点击a 删除 当前a 所在的行(链接的爸爸的爸爸)  node.removeChild(child)  
                tbody.removeChild(this.parentNode.parentNode)
            }
        }
    </script>
```



### 1.1.5 ▲创建元素的三种方式

![1551164214925](images/1551164214925.png)

```js
    <script>
        // 三种创建元素方式区别 
        // 1. document.write() 创建元素  如果页面文档流加载完毕，再调用这句话会导致页面重绘
         var btn = document.querySelector('button');
         btn.onclick = function() {
             document.write('<div>123</div>');
         }

        // 2. innerHTML 创建元素
        var inner = document.querySelector('.inner');
         for (var i = 0; i <= 100; i++) {
             inner.innerHTML += '<a href="#">百度</a>'
         }
        var arr = [];
        for (var i = 0; i <= 100; i++) {
            arr.push('<a href="#">百度</a>');
        }
        inner.innerHTML = arr.join('');
        // 3. document.createElement() 创建元素
        var create = document.querySelector('.create');
        for (var i = 0; i <= 100; i++) {
            var a = document.createElement('a');
            create.appendChild(a);
        }
    </script>
```



### 1.1.6 innerTHML和createElement效率对比

**innerHTML字符串拼接方式（效率低）**

```js
<script>
    function fn() {
        var d1 = +new Date();
        var str = '';
        for (var i = 0; i < 1000; i++) {
            document.body.innerHTML += '<div style="width:100px; height:2px; border:1px solid blue;"></div>';
        }
        var d2 = +new Date();
        console.log(d2 - d1);
    }
    fn();
</script>
```

**createElement方式（效率一般）**

```js
<script>
    function fn() {
        var d1 = +new Date();

        for (var i = 0; i < 1000; i++) {
            var div = document.createElement('div');	// 先创建节点
            div.style.width = '100px';
            div.style.height = '2px';
            div.style.border = '1px solid red';
            document.body.appendChild(div);				// 再添加子节点
        }
        var d2 = +new Date();
        console.log(d2 - d1);
    }
    fn();
</script>
```

**innerHTML数组方式（效率高）**

```js
<script>
    function fn() {
        var d1 = +new Date();
        var array = [];
        for (var i = 0; i < 1000; i++) {
            array.push('<div style="width:100px; height:2px; border:1px solid blue;"></div>');
        }
        document.body.innerHTML = array.join('');
        var d2 = +new Date();
        console.log(d2 - d1);
    }
    fn();
</script>
```



## 1.2. DOM的核心总结

![1551164669434](images/1551164669434.png)

![1551164715018](images/1551164715018.png)



关于dom操作，我们主要针对于元素的操作。主要有创建、增、删、改、查、属性操作、事件操作。

### 1.2.1. 创建

![1551164797164](images/1551164797164.png)

### 1.2.2. ▲增

![1551164829832](images/1551164829832.png)

### 1.2.3. 删

![1551164872533](images/1551164872533.png)

### 1.2.4. 改

![1551164907830](images/1551164907830.png)

### 1.2.5. 查

![1551164936214](images/1551164936214.png)

### 1.2.6. ▲属性操作

![1551164985383](images/1551164985383.png)

### 1.2.7. ▲事件操作

**事件源.事件类型 = 事件处理程序**

![image-20220306145746101](images/image-20220306145746101.png)

![image-20210803135028178](https://i.loli.net/2021/08/03/w8EVPasNXCGAD2x.png)



## 1.3. 事件高级 

### 1.3.1. 注册事件（2种方式）

![1551165252019](images/1551165252019.png)



### ▲1.3.2 事件监听

#### addEventListener()事件监听（IE9以后支持）

![1551165364122](images/1551165364122.png)

`eventTarget.addEventListener( type , listener , useCapture )`

方法将指定的监听器注册到 eventTarget（目标对象）上，当该对象触发指定的事件时，就会执行事件处理函数。

![1551165604792](images/1551165604792.png)



**type参数可选事件：https://developer.mozilla.org/zh-CN/docs/Web/Events**



`addEventListener()` 是 W3C DOM 规范中提供的注册事件监听器的方法。它的优点包括：

- 它允许给一个事件**注册多个监听器**。 特别是在使用[AJAX](https://developer.mozilla.org/zh-CN/docs/Glossary/AJAX)库，JavaScript模块，或其他需要第三方库/插件的代码。
- 它提供了一种更精细的手段控制 `listener` 的触发阶段。（即**可以选择捕获或者冒泡**）。
- 它**对任何 DOM 元素都是有效**的，而不仅仅只对 HTML 元素有效。





#### attacheEvent()事件监听（IE678支持   了解即可）

![1551165781836](images/1551165781836.png)

	eventTarget.attachEvent()方法将指定的监听器注册到 eventTarget（目标对象） 上，当该对象触发指定的事件时，指定的回调函数就会被执行。

![1551165843912](images/1551165843912.png)

```html
<button>传统注册事件</button>
<button>方法监听注册事件</button>
<button>ie9 attachEvent</button>
<script>
    var btns = document.querySelectorAll('button');
    // 1. 传统方式注册事件
    btns[0].onclick = function() {
        alert('hi');
    }
    btns[0].onclick = function() {
            alert('hao a u');
        }
   // 2. 事件侦听注册事件 addEventListener 
   // (1) 里面的事件类型是字符串 必定加引号 而且不带on
   // (2) 同一个元素 同一个事件可以添加多个侦听器（事件处理程序）
    btns[1].addEventListener('click', function() {
        alert(22);
    })
    btns[1].addEventListener('click', function() {
            alert(33);
    })
    // 3. attachEvent ie9以前的版本支持
    btns[2].attachEvent('onclick', function() {
        alert(11);
    })
</script>
```
#### 事件监听兼容性解决方案（封装函数）

封装一个函数，函数中判断浏览器的类型：

![1551166023885](images/1551166023885.png)

### 1.3.3. 删除事件（解绑事件）

![1551166185410](images/1551166185410.png)

```html
    <div>1</div>
    <div>2</div>
    <div>3</div>
    <script>
        var divs = document.querySelectorAll('div');
        divs[0].onclick = function() {
            alert(11);
            // 1. 传统方式删除事件
            divs[0].onclick = null;
        }
        // 2. removeEventListener 删除事件
        divs[1].addEventListener('click', fn) // 里面的fn 不需要调用加小括号
        function fn() {
            alert(22);
            divs[1].removeEventListener('click', fn);
        }
        // 3. detachEvent
        divs[2].attachEvent('onclick', fn1);

        function fn1() {
            alert(33);
            divs[2].detachEvent('onclick', fn1);
        }
    </script>
```

**删除事件兼容性解决方案 **

![1551166332453](images/1551166332453.png)

### ▲1.3.4. DOM事件流（捕获、冒泡）

> ```
> html中的标签都是相互嵌套的，我们可以将元素想象成一个盒子装一个盒子，document是最外面的大盒子。
> 当你单击一个div时，同时你也单击了div的父元素，甚至整个页面。
> 
> 那么是先执行父元素的单击事件，还是先执行div的单击事件 ？？？
> ```

![1551166423144](images/1551166423144.png)

> 比如：我们给页面中的一个div注册了单击事件，当你单击了div时，也就单击了body，单击了html，单击了document。

![1551166555833](images/1551166555833.png)

![1551166581552](images/1551166581552.png)

> ```
> 当时的2大浏览器霸主谁也不服谁！
> IE 提出从目标元素开始，然后一层一层向外接收事件并响应，也就是冒泡型事件流。
> Netscape（网景公司）提出从最外层开始，然后一层一层向内接收事件并响应，也就是捕获型事件流。
> 
> 江湖纷争，武林盟主也脑壳疼！！！
> 
> 最终，w3c 采用折中的方式，平息了战火，制定了统一的标准 —--— 先捕获再冒泡。
> 现代浏览器都遵循了此标准，所以当事件发生时，会经历3个阶段。
> ```

DOM 事件流会经历3个阶段： 

1. 捕获阶段

2. 当前目标阶段

3. 冒泡阶段 



	我们向水里面扔一块石头，首先它会有一个下降的过程，这个过程就可以理解为从最顶层向事件发生的最具体元素（目标点）的捕获过程；之后会产生泡泡，会在最低点（ 最具体元素）之后漂浮到水面上，这个过程相当于事件冒泡。 

![1551169007768](images/1551169007768.png)

![1551169042295](images/1551169042295.png)

**事件冒泡**

```html
    <div class="father">
        <div class="son">son盒子</div>
    </div>
    <script>
        // onclick 和 attachEvent（ie） 在冒泡阶段触发
        // 冒泡阶段 如果addEventListener 第三个参数是 false 或者 省略 
        // son -> father ->body -> html -> document
        var son = document.querySelector('.son');
		// 给son注册单击事件
        son.addEventListener('click', function() {
            alert('son');
        }, false);
		// 给father注册单击事件
        var father = document.querySelector('.father');
        father.addEventListener('click', function() {
            alert('father');
        }, false);
		// 给document注册单击事件，省略第3个参数
        document.addEventListener('click', function() {
            alert('document');
        })
    </script>
```

**事件捕获**

```html
    <div class="father">
        <div class="son">son盒子</div>
    </div>
    <script>
        // 如果addEventListener() 第三个参数是 true 那么在捕获阶段触发
        // document -> html -> body -> father -> son
         var son = document.querySelector('.son');
		// 给son注册单击事件，第3个参数为true
         son.addEventListener('click', function() {
             alert('son');
         }, true);
         var father = document.querySelector('.father');
		// 给father注册单击事件，第3个参数为true
         father.addEventListener('click', function() {
             alert('father');
         }, true);
		// 给document注册单击事件，第3个参数为true
        document.addEventListener('click', function() {
            alert('document');
        }, true)
    </script>
```

### ▲1.3.5. 事件对象 function(e)

#### 什么是事件对象

事件发生后，跟事件相关的一系列信息数据的集合都放到这个对象里面，这个对象就是事件对象。

比如：  

1. 谁绑定了这个事件。

2. 鼠标触发事件的话，会得到鼠标的相关信息，如鼠标位置。

3. 键盘触发事件的话，会得到键盘的相关信息，如按了哪个键。

#### 事件对象的使用

事件触发发生时就会产生事件对象，并且系统会以实参的形式传给事件处理函数。

所以，在事件处理函数中声明1个形参用来接收事件对象。

![1551169537789](images/1551169537789.png)

#### 事件对象的兼容性处理

事件对象本身的获取存在兼容问题：

1. 标准浏览器中是浏览器给方法传递的参数，只需要定义形参 e 就可以获取到。

2. 在 IE6~8 中，浏览器不会给方法传递参数，如果需要的话，需要到 window.event 中获取查找。

![1551169680823](images/1551169680823.png)

```
只要“||”前面为false, 不管“||”后面是true 还是 false，都返回 “||” 后面的值。
只要“||”前面为true, 不管“||”后面是true 还是 false，都返回 “||” 前面的值。
```

```js
    <div>123</div>
    <script>
        var div = document.querySelector('div');
        div.onclick = function(e) {
                // 事件对象
                e = e || window.event;
                console.log(e);
        }
    </script>
```

#### ▲事件对象的属性和方法

![1551169931778](images/1551169931778.png)

#### ▲e.target 和 this 的区别

-  this 是事件**绑定的元素**（绑定这个事件处理函数的元素） 。

-  e.target 是事件**触发的元素**。

> ```
> 常情况下terget 和 this是一致的，
> 但有一种情况不同，那就是在事件冒泡时（父子元素有相同事件，单击子元素，父元素的事件处理函数也会被触发执行），
> 	这时候this指向的是父元素，因为它是绑定事件的元素对象，
> 	而target指向的是子元素，因为他是触发事件的那个具体元素对象。
> ```

```js
    <div>123</div>
    <script>
        var div = document.querySelector('div');
        div.addEventListener('click', function(e) {
            // e.target 和 this指向的都是div
            console.log(e.target);
            console.log(this);

        });
    </script>
```

冒泡事件下的e.target和this

```js
    <ul>
        <li>abc</li>
        <li>abc</li>
        <li>abc</li>
    </ul>
    <script>
        var ul = document.querySelector('ul');
        ul.addEventListener('click', function(e) {
              // 我们给ul 绑定了事件  那么this 就指向ul  
              console.log(this); // ul

              // e.target 触发了事件的对象 我们点击的是li e.target 指向的就是li
              console.log(e.target); // li
        });
    </script>
```

### 1.3.6 阻止默认行为

> html中一些标签有默认行为，例如a标签被单击后，默认会进行页面跳转。

```js
    <a href="http://www.baidu.com">百度</a>
    <script>
        // 2. 阻止默认行为 让链接不跳转 
        var a = document.querySelector('a');
        a.addEventListener('click', function(e) {
             e.preventDefault(); //  dom 标准写法
        });
        // 3. 传统的注册方式
        a.onclick = function(e) {
            // 普通浏览器 e.preventDefault();  方法
            e.preventDefault();
            // 低版本浏览器 ie678  returnValue  属性
            e.returnValue = false;
            // 我们可以利用return false 也能阻止默认行为 没有兼容性问题
            return false;
        }
    </script>
```

### ▲1.3.7 阻止事件冒泡

事件冒泡本身的特性，会带来的坏处，也会带来的好处。

![1551171467194](images/1551171467194.png)

```js
    <div class="father">
        <div class="son">son儿子</div>
    </div>
    <script>
        var son = document.querySelector('.son');
		// 给son注册单击事件
        son.addEventListener('click', function(e) {
            alert('son');
            e.stopPropagation(); // stop 停止  Propagation 传播
            window.event.cancelBubble = true; // 非标准 cancel 取消 bubble 泡泡
        }, false);

        var father = document.querySelector('.father');
		// 给father注册单击事件
        father.addEventListener('click', function() {
            alert('father');
        }, false);
		// 给document注册单击事件
        document.addEventListener('click', function() {
            alert('document');
        })
    </script>
```

**阻止事件冒泡的兼容性处理**

![1551171657513](images/1551171657513.png)

### 1.3.8 事件委托

事件冒泡本身的特性，会带来的坏处，也会带来的好处。

#### 什么是事件委托

```
把事情委托给别人，代为处理。
```

事件委托也称为事件代理，在 jQuery 里面称为事件委派。

> 说白了就是，不给子元素注册事件，给父元素注册事件，把处理代码在父元素的事件中执行。



**生活中的代理：**

![1551172082624](images/1551172082624.png)

**js事件中的代理：**

![1551172159273](images/1551172159273.png)

#### 事件委托的原理

	给父元素注册事件，利用事件冒泡，当子元素的事件触发，会冒泡到父元素，然后去控制相应的子元素。

#### 事件委托的作用

- 我们只操作了一次 DOM ，提高了程序的性能。

- 动态新创建的子元素，也拥有事件。

```js
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
            // e.target 这个可以得到我们点击的对象
            e.target.style.backgroundColor = 'pink';
        })
    </script>
```

## 1.4. 常用鼠标事件

![1551172699854](images/1551172699854.png)

**点击鼠标时的事件顺序：**

**onmousedown 按下 --> onmouseup 弹起 --> onclick 点击**

（和键盘不同，键盘点击事件顺序：

keydown 按下 --> keypress 按下时 --> keyup 弹起）



**mouseenter 和mouseover的区别：**

- 当鼠标移动到元素上时就会触发mouseenter 事件

- 类似 mouseover，它们两者之间的差别是mouse**over** 鼠标经过自身盒子会触发，**经过子元素盒子还会触发**。mouseenter  只会经过自身盒子触发；

  之所以这样，是因为mouseenter不会冒泡

- **鼠标离开事件： mouseleave  同样不会冒泡**





### 1.4.1 案例：禁止选中文字和禁止右键菜单

![1551172755484](images/1551172755484.png)

```js
<body>
    我是一段不愿意分享的文字
    <script>
        // 1. contextmenu 我们可以禁用右键菜单
        document.addEventListener('contextmenu', function(e) {
                e.preventDefault();
        })
        // 2. 禁止选中文字 selectstart
        document.addEventListener('selectstart', function(e) {
            e.preventDefault();
        })
    </script>
</body>
```

### 1.4.2 鼠标事件对象

![1551173103741](images/1551173103741.png)

### 1.4.3 获取鼠标在页面的坐标

```js
    <script>
        // 鼠标事件对象 MouseEvent
        document.addEventListener('click', function(e) {
            // 1. client 鼠标在可视区的x和y坐标
            console.log(e.clientX);
            console.log(e.clientY);
            console.log('---------------------');

            // 2. page 鼠标在页面文档的x和y坐标
            console.log(e.pageX);
            console.log(e.pageY);
            console.log('---------------------');

            // 3. screen 鼠标在电脑屏幕的x和y坐标
            console.log(e.screenX);
            console.log(e.screenY);

        })
    </script>
```

### 1.4.4 案例：跟随鼠标的天使

![1551173172613](images/1551173172613.png)

![1551173186812](images/1551173186812.png)

```js
    <img src="images/angel.gif" alt="">
    <script>
        var pic = document.querySelector('img');
        document.addEventListener('mousemove', function(e) {
        	// 1. mousemove只要我们鼠标移动1px 就会触发这个事件
        	// 2.核心原理： 每次鼠标移动，我们都会获得最新的鼠标坐标， 
            // 把这个x和y坐标做为图片的top和left 值就可以移动图片
        	var x = e.pageX;
        	var y = e.pageY;
        	console.log('x坐标是' + x, 'y坐标是' + y);
        	//3 . 千万不要忘记给left 和top 添加 px 单位！！！！！！！！！
        	pic.style.left = x - 50 + 'px';
        	pic.style.top = y - 40 + 'px';
    	});
    </script>
```



## 四、键盘事件、BOM(定时器,location)、JS执行机制：事件循环



## 1.1. 常用的键盘事件

### 1.1.1 键盘事件

![1551318122855](images/1551318122855.png)

![1551318160371](images/1551318160371.png)

```js
    <script>
        // 常用的键盘事件
        //1. keyup 按键弹起的时候触发 
        document.addEventListener('keyup', function() { // 直接用document.代表按哪个键都会触发
            console.log('我弹起了');
        })

        //3. keypress 按键按下的时候触发  不能识别功能键 比如 ctrl shift 左右箭头啊
        document.addEventListener('keypress', function() {
                console.log('我按下了press');
        })
        //2. keydown 按键按下的时候触发  能识别功能键 比如 ctrl shift 左右箭头啊
        document.addEventListener('keydown', function() {
                console.log('我按下了down');
        })
        // 4. 三个事件的执行顺序  keydown -- keypress -- keyup
    </script>
```

### 1.1.2 键盘事件对象

![1551318355505](images/1551318355505.png)

![1551318404238](images/1551318404238.png)

**使用keyCode属性判断用户按下哪个键**

```js
    <script>
        // 键盘事件对象中的keyCode属性可以得到相应键的ASCII码值
        document.addEventListener('keyup', function(e) {
            console.log('up:' + e.keyCode);
            // 我们可以利用keycode返回的ASCII码值来判断用户按下了那个键
            if (e.keyCode === 65) {
                alert('您按下的a键');
            } else {
                alert('您没有按下a键')
            }
        })
        document.addEventListener('keypress', function(e) {
            // console.log(e);
            console.log('press:' + e.keyCode);
        })
    </script>
```

### 1.1.3 案例：模拟京东按键输入内容

当我们按下 s 键， 光标就定位到搜索框（文本框获得焦点）。

![1551318669520](images/1551318669520.png)

> 注意：触发获得焦点事件，可以使用 元素对象.focus()

```js
    <input type="text">
    <script>
        // 获取输入框
        var search = document.querySelector('input');
		// 给document注册keyup事件
        document.addEventListener('keyup', function(e) {
            // 判断keyCode的值
            if (e.keyCode === 83) {
                // 触发输入框的获得焦点事件
                search.focus();
            }
        })
    </script>
```

### 1.1.4 案例：模拟京东快递单号查询

要求：当我们在文本框中输入内容时，文本框上面自动显示大字号的内容。

![1551318882189](images/1551318882189.png)

![1551318909264](images/1551318909264.png)

```js
    <div class="search">
        <div class="con">123</div>
        <input type="text" placeholder="请输入您的快递单号" class="jd">
    </div>
    <script>
        // 获取要操作的元素
        var con = document.querySelector('.con');
        var jd_input = document.querySelector('.jd');
		// 给输入框注册keyup事件
        jd_input.addEventListener('keyup', function() {
				// 判断输入框内容是否为空
                if (this.value == '') {
                    // 为空，隐藏放大提示盒子
                    con.style.display = 'none';
                } else {
                    // 不为空，显示放大提示盒子，设置盒子的内容
                    con.style.display = 'block';
                    con.innerText = this.value;
                }
            })
        // 给输入框注册失去焦点事件，隐藏放大提示盒子
        jd_input.addEventListener('blur', function() {
                con.style.display = 'none';
            })
        // 给输入框注册获得焦点事件
        jd_input.addEventListener('focus', function() {
            // 判断输入框内容是否为空
            if (this.value !== '') {
                // 不为空则显示提示盒子
                con.style.display = 'block';
            }
        })
    </script>
```

## 1.2. BOM

### 1.2.1. 什么是BOM

	BOM（Browser Object Model）即浏览器对象模型，它提供了独立于内容而与浏览器窗口进行交互的对象，其核心对象是 window。
	
	BOM 由一系列相关的对象构成，并且每个对象都提供了很多方法与属性。
	
	BOM 缺乏标准，JavaScript 语法的标准化组织是 ECMA，DOM 的标准化组织是 W3C，BOM 最初是Netscape 浏览器标准的一部分。

![1551319264407](images/1551319264407.png)

### 1.2.2. BOM的构成

BOM 比 DOM 更大，它包含 DOM。

![1551319344183](images/1551319344183.png)

### 1.2.3. 顶级对象window

![1551319372909](images/1551319372909.png)

### 1.2.4. window对象的常见事件

#### 页面（窗口）加载事件（2种）

**第1种**

![1551319525109](images/1551319525109.png)

![1551319600263](images/1551319600263.png)

**第2种**

![1551319620299](images/1551319620299.png)

* window.onload 是窗口 (页面）加载事件，**当文档内容完全加载完成**后，才会触发该事件(包括图像、脚本文件、CSS 文件等)调用的处理函数。

* DOMContentLoaded 事件触发时，**仅当DOM加载完成**，不包括样式表，图片，flash等等。

  （如果页面的图片很多的话, 从用户访问到onload触发可能需要较长的时间, 交互效果就不能实现，必然影响用户的体验，此时用 DOMContentLoaded 事件比较合适。）【IE9以上支持】

  

```js
    <script>
        window.addEventListener('load', function() {
            var btn = document.querySelector('button');
            btn.addEventListener('click', function() {
                alert('点击我');
            })
        })
        window.addEventListener('load', function() {
            alert(22);
        })
        document.addEventListener('DOMContentLoaded', function() {
            alert(33);
        })
    </script>
```

#### 调整窗口大小事件

![1551319803117](images/1551319803117.png)

	window.onresize 是调整窗口大小加载事件,  当触发时就调用的处理函数。

注意：

1. 只要窗口大小发生像素变化，就会触发这个事件。

2. 我们经常利用这个事件完成响应式布局。 window.innerWidth 当前**浏览器内部的宽度（会受到ctrl+滚轮的影响）**

```js
    <script>
        // 注册页面加载事件
        window.addEventListener('load', function() {
            var div = document.querySelector('div');
        	// 注册调整窗口大小事件
            window.addEventListener('resize', function() {
                // window.innerWidth 获取窗口大小
                console.log('变化了');
                if (window.innerWidth <= 800) {
                    div.style.display = 'none';
                } else {
                    div.style.display = 'block';
                }
            })
        })
    </script>
    <div></div>
```



### ▲1.2.5. 定时器（注意this指向问题！！！）

#### ▲setTimeout() / setInterval() 若想处理外部的变量，一定要【使用不带形参的匿名函数/箭头函数】



#### 错误做法：

如果像下面这样把传入 setInterval()  的函数 flag 写在外面，

那么传入外部变量n的时候，相当于**只是传了一下当前n的值，并没有把n的地址传进去！！！**

~~~js
var timer = null;
let n = 10;
timer = setInterval(flag, 200, n);

function flag(x) {
    x -= 1;
    console.log(x); // 一直打印9
    console.log(n); // 一直打印10
    if (x == 0) clearInterval(timer);
}
~~~



#### 问题原因

因为 setTimeout 中函数内的 **this 是指向了window对象**

这是由于 setTimeout() 调用的代码**运行在与当前函数完全分离的执行环境上**。

这会导致 setTimeout() 中包含的 `this` 关键字会指向 `window` (或`全局`)对象。详细可参考[MDN setTimeout](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/setTimeout)



#### 正确做法：（注意，箭头函数/匿名函数不能写任何形参！！！）：

~~~js
法1 箭头函数：
var timer = null;
let n = 10;
timer = setInterval(
    () => {	// 注意！这里不能写任何形参！！！
        n -= 1;
        console.log(n);
        if (n == 0) clearInterval(timer);
    },
    200,
    n // 这里已经把n传进去了
);
------------------------------------------------------------------------------------
法2 匿名函数：
var timer = null;
let n = 10;
timer = setInterval(
    function () {	// 注意！这里不能写任何形参！！！
        n -= 1;
        console.log(n);
        if (n == 0) clearInterval(timer);
    },
    200,
    n // 这里已经把n传进去了
);
~~~

如果你写了形参，那还是会出错（一直打印9）

~~~js
var timer = null;
let n = 10;
timer = setInterval(
    (x) => {
        x -= 1;
        console.log(x); // 一直打印9
        if (x == 0) clearInterval(timer);
    },
    200,
    n
);
------------------------------------------------------------------------------------
var timer = null;
let n = 10;
timer = setInterval(
    function (x) {	
        x -= 1;
        console.log(x); // 一直打印9
        if (x == 0) clearInterval(timer);
    },
    200,
    n
);
~~~





window 对象给我们提供了 2 个非常好用的方法-定时器。

- setTimeout() 

- setInterval()  

#### setTimeout() 炸弹定时器【1次】

##### 开启定时器

![1551320279307](images/1551320279307.png)

![1551320408854](images/1551320408854.png)

![1551320298981](images/1551320298981.png)

> ```
> 普通函数是按照代码顺序直接调用。
> 
> 简单理解： 回调，就是回头调用的意思。上一件事干完，再回头再调用这个函数。
> 例如：定时器中的调用函数，事件处理函数，也是回调函数。
> 
> 以前我们讲的   element.onclick = function(){}   或者  element.addEventListener(“click”, fn);   里面的函数是回调函数。
> 
> ```



```js
    <script>
        //1. 回调函数是一个匿名函数
        // 在setTimeout里面写函数
         setTimeout(function() {
             console.log('时间到了');

         }, 2000);

		// 在setTimeout外部写函数
        function callback() {
            console.log('爆炸了');
        }
		setTimeout(callback, 2000);// 函数名不带()

		// 回调函数是一个有名函数
        var timer1 = setTimeout(callback, 3000);
        var timer2 = setTimeout(callback, 5000);
    </script>
```

##### 案例：5秒后关闭广告

![1551320924828](images/1551320924828.png)



![1551320959756](images/1551320959756.png)

```js
<body>
    <img src="images/ad.jpg" alt="" class="ad">
    <script>
        // 获取要操作的元素
        var ad = document.querySelector('.ad');
		// 开启定时器
        setTimeout(function() {
            ad.style.display = 'none';
        }, 5000);
    </script>
</body>
```

##### 停止定时器

![1551321051001](images/1551321051001.png)

![1551321064154](images/1551321064154.png)

```js
    <button>点击停止定时器</button>
    <script>
        var btn = document.querySelector('button');
		// 开启定时器
        var timer = setTimeout(function() {
            console.log('爆炸了');
        }, 5000);
		// 给按钮注册单击事件
        btn.addEventListener('click', function() {
            // 停止定时器
            clearTimeout(timer);
        })
    </script>
```



#### setInterval() 闹钟定时器【多次】

##### 开启定时器

![1551321162158](images/1551321162158.png)

```js
    <script>
        // 1. setInterval 
        setInterval(function() {
            console.log('继续输出');
        }, 1000);
    </script>
```

##### 案例：倒计时

![1551321298787](images/1551321298787.png)

![1551321322188](images/1551321322188.png)

```js
    <div>
        <span class="hour">1</span>
        <span class="minute">2</span>
        <span class="second">3</span>
    </div>
    <script>
        // 1. 获取元素（时分秒盒子） 
        var hour = document.querySelector('.hour'); // 小时的黑色盒子
        var minute = document.querySelector('.minute'); // 分钟的黑色盒子
        var second = document.querySelector('.second'); // 秒数的黑色盒子
        var inputTime = +new Date('2019-5-1 18:00:00'); // 返回的是用户输入时间总的毫秒数

        countDown(); // 我们先调用一次这个函数，防止第一次刷新页面有空白 

        // 2. 开启定时器
        setInterval(countDown, 1000);
		
        function countDown() {
            var nowTime = +new Date(); // 返回的是当前时间总的毫秒数
            var times = (inputTime - nowTime) / 1000; // times是剩余时间总的秒数 
            var h = parseInt(times / 60 / 60 % 24); // 当前距离目标时间的时
            h = h < 10 ? '0' + h : h;
            hour.innerHTML = h; // 把剩余的小时给 小时黑色盒子
            var m = parseInt(times / 60 % 60); // 当前距离目标时间的分
            m = m < 10 ? '0' + m : m;
            minute.innerHTML = m;// 把剩余的分钟给 分钟黑色盒子
            var s = parseInt(times % 60); // 当前距离目标时间的秒
            s = s < 10 ? '0' + s : s;
            second.innerHTML = s;// 把剩余的秒给 秒黑色盒子
        }
    </script>
```



#### clearInterval() 停止定时器

![1551321444559](images/1551321444559.png)

**案例**

~~~html
<body>
    <button class="begin">开启定时器</button>
    <button class="stop">停止定时器</button>
    <script>
        var begin = document.querySelector('.begin');
        var stop = document.querySelector('.stop');
        var timer = null; // 先给定时器命名为全局变量，后面停止定时器才能使用
// 定义的时候不要 var timer 这样会生成undefined；null是一个空对象（至少null还算一个对象数据类型，而undefined啥也不是）
        begin.addEventListener('click', function() {
            timer = setInterval(function() {
                console.log('ni hao ma');

            }, 1000);
        })
        stop.addEventListener('click', function() {
            clearInterval(timer);
        })
    </script>
</body>
~~~







#### 案例：发送短信倒计时

	点击按钮后，该按钮60秒之内不能再次点击，防止重复发送短信。

![1551321540676](images/1551321540676.png)

![1551321564247](images/1551321564247.png)

```html
<body>
手机号码： <input type="number"> <button>发送</button>

    <script>
        var btn = document.querySelector('button');
		// 全局变量，定义剩下的秒数
        var time = 3; 
		// 注册单击事件
        btn.addEventListener('click', function() {
            // 禁用按钮
            btn.disabled = true;
            // 开启定时器
            var timer = setInterval(function() {
                // 判断剩余秒数
                if (time == 0) {
                    // 清除定时器和复原按钮
                    clearInterval(timer);
                    btn.disabled = false;
                    btn.innerHTML = '发送';
                } else {
                    btn.innerHTML = '还剩下' + time + '秒';
                    time--;
                }
            }, 1000);
        });
    </script>
</body>
```



### 1.2.6. this指向问题

	this的指向在函数定义的时候是确定不了的，**只有函数执行的时候才能确定this到底指向谁**，一般情况下this的最终指向的是那个调用它的对象。

现阶段，我们先了解一下几个this指向

1. 全局作用域或者普通函数中this指向全局对象window（注意定时器里面的this指向window）

2. 方法调用中谁调用this指向谁
3. 构造函数中this指向构造函数的实例

```js
    <button>点击</button>
    <script>
        // this 指向问题 一般情况下this的最终指向的是那个调用它的对象
        
        // 1. 全局作用域或者普通函数中this指向全局对象window（ 注意定时器里面的this指向window）
        console.log(this);
        function fn() {
            console.log(this);
        }
        window.fn();
        window.setTimeout(function() {
            console.log(this);
        }, 1000);

        // 2. 方法调用中谁调用this指向谁
        var o = {
            sayHi: function() {
                console.log(this); // this指向的是 o 这个对象
            }
        }
        o.sayHi();
        var btn = document.querySelector('button');
        btn.addEventListener('click', function() {
                console.log(this); // 事件处理函数中的this指向的是btn这个按钮对象
            })

        // 3. 构造函数中this指向构造函数的实例
        function Fun() {
            console.log(this); // this 指向的是 xxx 实例对象
        }
        var xxx = new Fun();
    </script>
```



### 1.2.7. location对象

#### 什么是 location 对象

![1551322091638](images/1551322091638.png)

#### URL

![1551322373704](images/1551322373704.png)

![1551322387201](images/1551322387201.png)

#### location 对象的属性

![1551322416716](images/1551322416716.png)

![1551322438200](images/1551322438200.png)

#### 案例：5分钟自动跳转页面

![1551322496871](images/1551322496871.png)

![1551322517605](images/1551322517605.png)

```js
    <button>点击</button>
    <div></div>
    <script>
        var btn = document.querySelector('button');
        var div = document.querySelector('div');
        btn.addEventListener('click', function() {
            // console.log(location.href);
            location.href = 'http://www.itcast.cn';
        })
        var timer = 5;
        setInterval(function() {
            if (timer == 0) {
                location.href = 'http://www.itcast.cn';
            } else {
                div.innerHTML = '您将在' + timer + '秒钟之后跳转到首页';
                timer--;
            }
        }, 1000);
    </script>
```

#### 案例：获取URL参数

![1551322622640](images/1551322622640.png)

![1551322639241](images/1551322639241.png)

```js
    <div></div>
	<script>
        console.log(location.search); // ?uname=andy
        // 1.先去掉？  substr('起始的位置'，截取几个字符);
        var params = location.search.substr(1); // uname=andy
        console.log(params);
        // 2. 利用=把字符串分割为数组 split('=');
        var arr = params.split('=');
        console.log(arr); // ["uname", "ANDY"]
        var div = document.querySelector('div');
        // 3.把数据写入div中
        div.innerHTML = arr[1] + '欢迎您';
    </script>
```

#### location对象的常见方法

![1551322750241](images/1551322750241.png)

```js
    <button>点击</button>
    <script>
        var btn = document.querySelector('button');
        btn.addEventListener('click', function() {
            // 记录浏览历史，所以可以实现后退功能
            location.assign('http://www.itcast.cn');
            
            // 不记录浏览历史，所以不可以实现后退功能
            location.replace('http://www.itcast.cn');
            
            // 不加参数也能刷新（读取缓存），加了true就是强制刷新（不读取缓存）；可后退
            location.reload(true); 
        })
    </script>
```

### 1.2.8. navigator对象

	navigator 对象包含有关浏览器的信息，它有很多属性，我们最常用的是 userAgent，该属性可以返回由客户机发送服务器的 user-agent 头部的值。

下面前端代码可以判断用户那个终端打开页面，实现跳转

```js
if((navigator.userAgent.match(/(phone|pad|pod|iPhone|iPod|ios|iPad|Android|Mobile|BlackBerry|IEMobile|MQQBrowser|JUC|Fennec|wOSBrowser|BrowserNG|WebOS|Symbian|Windows Phone)/i))) {
    window.location.href = "";     //手机
 } else {
    window.location.href = "";     //电脑
 }
```

### 1.2.9 history对象

	window对象给我们提供了一个 history对象，与浏览器历史记录进行交互。该对象包含用户（在浏览器窗口中）访问过的URL。

![1551322885216](images/1551322885216.png)

history对象一般在实际开发中比较少用，但是会在一些 OA 办公系统中见到。

![1551322959148](images/1551322959148.png)

## 1.3. JS执行机制

以下代码执行的结果是什么？

```js
 console.log(1);
 
 setTimeout(function () {
     console.log(3);
 }, 1000);
 
 console.log(2);
```

以下代码执行的结果是什么？

```js
 console.log(1);
 
 setTimeout(function () {
     console.log(3);
 }, 0);
 
 console.log(2);
```



### 1.3.1 JS 是单线程

![1551415019322](images/1551415019322.png)

```js
	单线程就意味着，所有任务需要排队，前一个任务结束，才会执行后一个任务。如果前一个任务耗时很长，后一个任务就不得不一直等着。
	这样所导致的问题是： 如果 JS 执行的时间过长，这样就会造成页面的渲染不连贯，导致页面渲染加载阻塞的感觉。
```

### 1.3.2 同步任务和异步任务

	单线程导致的问题就是后面的任务等待前面任务完成，如果前面任务很耗时（比如读取网络数据），后面任务不得不一直等待！！
	
	为了解决这个问题，利用多核 CPU 的计算能力，HTML5 提出 Web Worker 标准，允许 JavaScript 脚本创建多个线程，但是子线程完全受主线程控制。于是，JS 中出现了**同步任务**和**异步任务**。

#### 同步

	前一个任务结束后再执行后一个任务，程序的执行顺序与任务的排列顺序是一致的、同步的。比如做饭的同步做法：我们要烧水煮饭，等水开了（10分钟之后），再去切菜，炒菜。

#### 异步

	你在做一件事情时，因为这件事情会花费很长时间，在做这件事的同时，你还可以去处理其他事情。比如做饭的异步做法，我们在烧水的同时，利用这10分钟，去切菜，炒菜。

![1551434295074](images/1551434295074.png)

> ```js
> JS中所有任务可以分成两种，一种是同步任务（synchronous），另一种是异步任务（asynchronous）。
> 
> 同步任务指的是：
> 	在主线程上排队执行的任务，只有前一个任务执行完毕，才能执行后一个任务；
> 异步任务指的是：
> 	不进入主线程、而进入”任务队列”的任务，当主线程中的任务运行完了，才会从”任务队列”取出异步任务放入主线程执行。
> ```

![1551434972778](images/1551434972778.png)

### 1.3.3 JS执行机制（事件循环）

![1551435335464](images/1551435335464.png)

![1551435398306](images/1551435398306.png)

![1551435449634](images/1551435449634.png)

### 1.3.4 代码思考题

```js
 console.log(1);
 document.onclick = function() {
   console.log('click');
 }

 setTimeout(function() {
   console.log(3)
 }, 3000)
 console.log(2);
```

先打印1和2

然后再过3秒后打印3；如果3秒前有点击鼠标，就是1 --> 2 --> click --> 3

如果3秒后才点击鼠标，就是1 --> 2 --> 3 --> click



## 五、offset、client、scroll属性

## 1.1. 元素偏移量 offset 系列

### 1.1.1 offset 概述

offset 翻译过来就是偏移量， 我们使用 offset系列相关属性可以动态的得到该元素的位置（偏移）、大小等。

1. 获得元素距离带有定位父元素的位置
2. 获得元素自身的大小（宽度高度）
3. 注意：返回的数值都**不带单位**

**offset系列使得固定参数可被动态参数替代**

![图片1](images/图片1.png)

![图片2](./images/图片2.png)



### 1.1.2 offset 与 style 区别

#### offset

- offset 可以得到任意样式表中的样式值

- offset 系列获得的数值是的

- offsetWidth 包含padding+border+width

- offsetWidth 等属性是**只读**属性，只能获取不能赋值

- **所以，我们想要获取元素大小位置，用offset更合适**

#### style

- style 只能得到行内样式表中的样式值
- style.width 获得的是带有单位的字符串
- style.width 获得不包含padding和border 的值
- style.width 是**可读写**属性，可以获取也可以赋值
- **所以，我们想要给元素更改值，则需要用style改变**

|        | 适用于？ | 有无单位？ | 包含padding+border+width吗？ | 读写？   |
| ------ | -------- | ---------- | ---------------------------- | -------- |
| offset | 任意样式 | 没有单位   | 包含                         | 只读     |
| style  | 行内样式 | 有单位     | 不包含                       | 可读可写 |

> **因为平时我们都是给元素注册触摸事件，所以重点记住 targetTocuhes**



### 1.1.3  案例：获取鼠标在盒子内的坐标

1. 我们在盒子内点击，想要得到鼠标距离盒子左右的距离。
2. 首先得到鼠标在页面中的坐标（e.pageX, e.pageY）
3. 其次得到盒子在页面中的距离 ( box.offsetLeft, box.offsetTop)
4. 用鼠标距离页面的坐标减去盒子在页面中的距离，得到 鼠标在盒子内的坐标
5. 如果想要移动一下鼠标，就要获取最新的坐标，使用鼠标移动

```javascript
var box = document.querySelector('.box');
box.addEventListener('mousemove', function(e) {
var x = e.pageX - this.offsetLeft;
var y = e.pageY - this.offsetTop;
this.innerHTML = 'x坐标是' + x + ' y坐标是' + y;
})
```



### 1.1.4  案例：模态框拖拽

弹出框，我们也称为模态框。

	1.点击弹出层，会弹出模态框， 并且显示灰色半透明的遮挡层。
	
	2.点击关闭按钮，可以关闭模态框，并且同时关闭灰色半透明遮挡层。
	
	3.鼠标放到模态框最上面一行，可以按住鼠标拖拽模态框在页面中移动。
	
	4.鼠标松开，可以停止拖动模态框移动

#### 案例分析:

1. 点击弹出层， 模态框和遮挡层就会显示出来 display:block;
2. 点击关闭按钮，模态框和遮挡层就会隐藏起来 display:none;
3. 在页面中拖拽的原理：鼠标按下并且移动， 之后松开鼠标
4. 触发事件是鼠标按下mousedown，鼠标移动mousemove 鼠标松开 mouseup
5. 拖拽过程:  鼠标移动过程中，获得最新的值赋值给模态框的left和top值，这样模态框可以跟着鼠标走了
6. 鼠标按下触发的事件源是最上面一行，就是  id 为 title 
7. 鼠标的坐标减去 鼠标在盒子内的坐标， 才是模态框真正的位置。
8. 鼠标按下，我们要得到鼠标在盒子的坐标。
9. 鼠标移动，就让模态框的坐标  设置为  ：鼠标坐标 减去盒子坐标即可，注意移动事件写到按下事件里面。
10. 鼠标松开，就停止拖拽，就是可以让鼠标移动事件解除  

```javascript
 // 1. 获取元素
        var login = document.querySelector('.login');
        var mask = document.querySelector('.login-bg');
        var link = document.querySelector('#link');
        var closeBtn = document.querySelector('#closeBtn');
        var title = document.querySelector('#title');
        // 2. 点击弹出层这个链接 link  让mask 和login 显示出来
        link.addEventListener('click', function() {
                mask.style.display = 'block';
                login.style.display = 'block';
            })
            // 3. 点击 closeBtn 就隐藏 mask 和 login 
        closeBtn.addEventListener('click', function() {
                mask.style.display = 'none';
                login.style.display = 'none';
            })
            // 4. 开始拖拽
            // (1) 当我们鼠标按下， 就获得鼠标在盒子内的坐标
        title.addEventListener('mousedown', function(e) {
            var x = e.pageX - login.offsetLeft;
            var y = e.pageY - login.offsetTop;
            // (2) 鼠标移动的时候，把鼠标在页面中的坐标，减去 鼠标在盒子内的坐标就是模态框的left和top值
            document.addEventListener('mousemove', move)

            function move(e) {
                login.style.left = e.pageX - x + 'px';
                login.style.top = e.pageY - y + 'px';
            }
            // (3) 鼠标弹起，就让鼠标移动事件移除
            document.addEventListener('mouseup', function() {
                document.removeEventListener('mousemove', move);
            })
        })

```



### 1.1.5  案例：仿京东放大镜

1. 整个案例可以分为三个功能模块
2. 鼠标经过小图片盒子， 黄色的遮挡层 和 大图片盒子显示，离开隐藏2个盒子功能
3. 黄色的遮挡层跟随鼠标功能。 
4. 移动黄色遮挡层，大图片跟随移动功能。

#### 案例分析:

1. 黄色的遮挡层跟随鼠标功能。
2. 把鼠标坐标给遮挡层不合适。因为遮挡层坐标以父盒子为准。
3. **首先是获得鼠标在盒子的坐标。** 
4. 之后把数值给遮挡层做为left 和top值。
5. 此时用到鼠标移动事件，但是还是在小图片盒子内移动。
6. 发现，遮挡层位置不对，**需要再减去盒子自身高度和宽度的一半。**
7. 遮挡层不能超出小图片盒子范围。
8. **如果小于零，就把坐标设置为0**
9. **如果大于遮挡层最大的移动距离，就把坐标设置为最大的移动距离**
10. 遮挡层的最大移动距离：小图片盒子宽度 减去 遮挡层盒子宽度

![1551881487(1)](images\1551881487(1).png)



![1551881563(1)](images\1551881563(1).jpg)

```javascript
window.addEventListener('load', function() {
    var preview_img = document.querySelector('.preview_img');
    var mask = document.querySelector('.mask');
    var big = document.querySelector('.big');
    // 1. 当我们鼠标经过 preview_img 就显示和隐藏 mask 遮挡层 和 big 大盒子
    preview_img.addEventListener('mouseover', function() {
        mask.style.display = 'block';
        big.style.display = 'block';
    })
    preview_img.addEventListener('mouseout', function() {
            mask.style.display = 'none';
            big.style.display = 'none';
        })
        // 2. 鼠标移动的时候，让黄色的盒子跟着鼠标来走
    preview_img.addEventListener('mousemove', function(e) {
        // (1). 先计算出鼠标在盒子内的坐标
        var x = e.pageX - this.offsetLeft;
        var y = e.pageY - this.offsetTop;
        // console.log(x, y);
        // (2) 减去盒子高度 300的一半 是 150 就是我们mask 的最终 left 和top值了
        // (3) 我们mask 移动的距离
        var maskX = x - mask.offsetWidth / 2;
        var maskY = y - mask.offsetHeight / 2;
        // (4) 如果x 坐标小于了0 就让他停在0 的位置
        // 遮挡层的最大移动距离
        var maskMax = preview_img.offsetWidth - mask.offsetWidth;
        if (maskX <= 0) {
            maskX = 0;
        } else if (maskX >= maskMax) {
            maskX = maskMax;
        }
        if (maskY <= 0) {
            maskY = 0;
        } else if (maskY >= maskMax) {
            maskY = maskMax;
        }
        mask.style.left = maskX + 'px';
        mask.style.top = maskY + 'px';
        // 3. 大图片的移动距离 = 遮挡层移动距离 * 大图片最大移动距离 / 遮挡层的最大移动距离
        // 大图
        var bigIMg = document.querySelector('.bigImg');
        // 大图片最大移动距离
        var bigMax = bigIMg.offsetWidth - big.offsetWidth;
        // 大图片的移动距离 X Y
        var bigX = maskX * bigMax / maskMax;
        var bigY = maskY * bigMax / maskMax;
        bigIMg.style.left = -bigX + 'px'; //记住这里要添加负号，因为大图片是要反着移动的
        bigIMg.style.top = -bigY + 'px';

    })

})
```



## 1.2. 元素可视区 client 系列



### 1.2.1 client概述

client 翻译过来就是客户端，我们使用 client 系列的相关属性来获取元素可视区的相关信息。通过 client
系列的相关属性可以动态的得到该元素的边框大小、元素大小等。



**client和offset最大的区别就是：client不包含边框**

![图片3](images\图片3.png)

![图片4](images\图片4.png)



### 1.2.2. 淘宝 flexible.js 源码分析

flexible.js手淘框架，是一个淘宝用来适配移动端的js框架。
手淘框架的核心原理就是根据不同的width给网页中html跟节点设置不同的font-size，然后所有的距离大小都用rem来代替，这样就实现了不同大小的屏幕都适应相同的样式了。

~~~js
(function flexible(window, document) {
    // 获取的html 的根元素
    var docEl = document.documentElement
        // dpr 物理像素比
    var dpr = window.devicePixelRatio || 1

    // adjust body font size  设置我们body 的字体大小
    function setBodyFontSize() {
        // 如果页面中有body 这个元素 就设置body的字体大小
        if (document.body) {
            document.body.style.fontSize = (12 * dpr) + 'px'
        } else {
            // 如果页面中没有body 这个元素，则等着 我们页面主要的DOM元素加载完毕再去设置body
            // 的字体大小
            document.addEventListener('DOMContentLoaded', setBodyFontSize)
        }
    }
    setBodyFontSize();

    // set 1rem = viewWidth / 10    设置我们html 元素的文字大小
    function setRemUnit() {
        var rem = docEl.clientWidth / 10
        docEl.style.fontSize = rem + 'px'
    }

    setRemUnit()

    // reset rem unit on page resize  当我们页面尺寸大小发生变化的时候，要重新设置下rem 的大小
    window.addEventListener('resize', setRemUnit)
        // pageshow 是我们重新加载页面触发的事件
    window.addEventListener('pageshow', function(e) {
        // e.persisted 返回的是true 就是说如果这个页面是从缓存取过来的页面，也需要从新计算一下rem 的大小
        if (e.persisted) {
            setRemUnit()
        }
    })

    // detect 0.5px supports  有些移动端的浏览器不支持0.5像素的写法
    if (dpr >= 2) {
        var fakeBody = document.createElement('body')
        var testElement = document.createElement('div')
        testElement.style.border = '.5px solid transparent'
        fakeBody.appendChild(testElement)
        docEl.appendChild(fakeBody)
        if (testElement.offsetHeight === 1) {
            docEl.classList.add('hairlines')
        }
        docEl.removeChild(fakeBody)
    }
}(window, document))
~~~



#### 立即执行函数 (function(){})()  或者 (function(){}())

主要作用： **创建一个独立的作用域。 避免了命名冲突问题**



#### pageshow相比load更兼容各种浏览器

下面三种情况都会刷新页面都会触发 **load 事件**。

1.a标签的超链接

2.F5或者刷新按钮（强制刷新）

3.前进后退按钮

 但是 火狐中，有个特点，有个“往返缓存”，这个缓存中不仅保存着页面数据，还保存了DOM和JavaScript的状态；实际上是将整个页面都保存在了内存里。所以此时后退按钮不能刷新页面。

此时可以使用 **pageshow **事件来触发。这个事件在页面显示时触发，无论页面是否来自缓存。在重新加载页面中，**pageshow会在load事件触发后触发**；

同时，根据 pageshow事件对象中的**persisted属性（来自于缓存返回true，不是为false）**来判断是否是缓存中的页面触发的pageshow事件

* 注意这个事件给window添加。



## 1.3.元素滚动 scroll 系列



### 1.3.1. scroll 概述

scroll 翻译过来就是滚动的，我们使用 scroll 系列的相关属性可以动态的得到该元素的大小、滚动距离等。

element常用于window（浏览器窗口）

![图片5](images\图片5.png)

![图片6](images\图片6.png)



### 1.3.2. 页面被卷去的头部

如果浏览器的高（或宽）度不足以显示整个页面时，会自动出现滚动条。当滚动条向下滚动时，页面上面被隐藏掉的高度，我们就称为页面被卷去的头部。滚动条在滚动时会触发 **onscroll事件**。

~~~js
xxx.addEventListener('scroll',function(){}) // 当滑动滚动条时触发该事件
~~~



### 1.3.3.案例：仿淘宝固定右侧侧边栏

1. 原先侧边栏是绝对定位
2. 当页面滚动到一定位置，侧边栏改为固定定位
3. 页面继续滚动，会让 返回顶部显示出来

#### 案例分析:

1. 需要用到页面滚动事件 scroll  因为是页面滚动，所以事件源是document
2. 滚动到某个位置，就是判断页面被卷去的上部值。
3. 页面被卷去的头部：可以通过window.pageYOffset 获得  如果是被卷去的左侧window.pageXOffset
4. 注意，**元素**被卷去的头部是**element.scrollTop**  , 如果是**页面**被卷去的头部 则是 **window.pageYOffset**
5. 其实这个值 可以通过盒子的 offsetTop可以得到，如果大于等于这个值，就可以让盒子固定定位了

```javascript
  //1. 获取元素
        var sliderbar = document.querySelector('.slider-bar');
        var banner = document.querySelector('.banner');
        // banner.offestTop 就是被卷去头部的大小，一定要在滚动函数之前先封装到一个变量里
        var bannerTop = banner.offsetTop
        // 当我们侧边栏变成fixed定位之后应该相距顶部的数值
        var sliderbarTop = sliderbar.offsetTop - bannerTop;
        // 获取main 主体元素
        var main = document.querySelector('.main');
        var goBack = document.querySelector('.goBack');
        var mainTop = main.offsetTop;
        // 2. 页面滚动事件 scroll
        document.addEventListener('scroll', function() {
            // console.log(11);
            // window.pageYOffset 页面被卷去的头部
            // console.log(window.pageYOffset);
            // 3 .当我们页面被卷去的头部大于等于头部区域高度 此时 侧边栏就要改为固定定位
            if (window.pageYOffset >= bannerTop) {
                sliderbar.style.position = 'fixed';
                sliderbar.style.top = sliderbarTop + 'px';
            } else {
                sliderbar.style.position = 'absolute';
                sliderbar.style.top = '300px';
            }
            // 4. 当我们页面滚动到main盒子，就显示 goback模块
            if (window.pageYOffset >= mainTop) {
                goBack.style.display = 'block';
            } else {
                goBack.style.display = 'none';
            }

        })
```

### 1.3.4. 页面被卷去的头部兼容性解决方案

需要注意的是，页面被卷去的头部，有兼容性问题，因此被卷去的头部通常有如下几种写法：

1. 声明了 DTD，使用 document.documentElement.scrollTop
2. 未声明 DTD，使用  document.body.scrollTop
3. 新方法 window.pageYOffset和 window.pageXOffset，IE9 开始支持

```javascript
function getScroll() {
    return {
      left: window.pageXOffset || document.documentElement.scrollLeft || document.body.scrollLeft||0,
      top: window.pageYOffset || document.documentElement.scrollTop || document.body.scrollTop || 0
    };
 } 
使用的时候  getScroll().left

```



## 1.4. 三大长度系列总结

![图片7](images\图片7.png)

element.offsetWidth 包括边框，client和scroll不包括边框；

scroll包含超出盒子内容的长度，client不包括。

**主要用法：**

1. **offset**系列 经常用于获得**元素位置**    offsetLeft  offsetTop

2. **client**经常用于获取**元素大小**  clientWidth clientHeight

3. **scroll** 经常用于获取**滚动距离** scrollTop  scrollLeft  

* 注意**页面**滚动的距离通过 **window.**pageXOffset  获得
* 以上三种距离属性，都是**只能获得、不能赋值**的



## 六、动画函数封装、网页特效案例



## 1.1. 动画函数封装



### 1.1.1 动画实现原理

> 核心原理：通过定时器 setInterval() 不断移动盒子位置。

实现步骤：

1. 获得盒子当前位置
2. 让盒子在当前位置加上1个移动距离
3. 利用定时器不断重复这个操作
4. 加一个结束定时器的条件
5. 注意**此元素需要添加定位（position:absolute），才能使用element.style.left**



### 1.1.2 动画函数给不同元素记录不同定时器

如果多个元素都使用这个动画函数，每次都要新var 声明一个定时器。我们可以给不同的**元素对象添加对应的定时器方法**（自己专门用自己的定时器）好处是：

1. 避免每次 var timer 每次都要在内存中开辟新的空间
2. 给不同的元素指定了不同的定时器

> 核心原理：利用 JS 是一门动态语言，可以很方便的给当前对象添加属性。

```javascript
 function animate(obj, target) {
            // 当我们不断地点击按钮，这个元素的速度会越来越快，因为开启了太多的定时器
            // 解决方案就是 让我们元素只有一个定时器执行
            // 先清除以前的定时器，只保留当前的一个定时器执行
            clearInterval(obj.timer);
     
            obj.timer = setInterval(function() { // 不要写var timer  理由如上
                if (obj.offsetLeft >= target) {
                    clearInterval(obj.timer);	// 停止动画（本质是停止定时器）
                }
                obj.style.left = obj.offsetLeft + 1 + 'px';

            }, 30); // 每30ms执行一次
        }

```



### 1.1.3 缓动效果原理

缓动动画就是让元素运动速度有所变化，最常见的是让速度慢慢停下来

思路：

1. 让盒子每次移动的距离慢慢变小，速度就会慢慢落下来。
2. 核心算法： **(目标值 - 现在的位置)   /  10**    做为每次移动的距离步长
3. 停止的条件是： 让当前盒子位置等于目标位置就停止定时器  
4. 注意步长值需要取整  



### 1.1.4 动画函数多个目标值之间移动

可以让动画函数从 800 移动到 500。

当我们点击按钮时候，判断步长是正值还是负值

​	1.如果是**正值，则步长往大取整**

​	2.如果是**负值，则步长往小取整**



### 1.1.5  动函数添加回调函数

回调函数就是**一个被作为参数传递的函数**

回调函数原理：函数可以作为一个参数。将这个函数作为参数传到另一个函数里面，**当那个函数执行完之后，再执行传进去的这个函数，这个过程就叫做回调**。

回调函数写的位置：定时器结束的位置。



### 1.1.6  动画完整版代码:

将该代码专门放到一个.js文件里，以后需要用到动画效果，直接引入\<script src="xxx.js">\</script>即可

```javascript
function animate(obj, target, callback) { // 动画对象、目标位置、回调函数
    // console.log(callback);  callback = function() {}  调用的时候 callback()

    // 先清除以前的定时器，只保留当前的一个定时器执行，否则会越点越快
    clearInterval(obj.timer);
    
    obj.timer = setInterval(function() {
        //  步长值写到定时器的里面
        var step = (target - obj.offsetLeft) / 10;
        
        // 把步长值改为整数，不要出现小数的问题，否则最后不能到我们想要的距离
        // var step = Math.ceil((target - obj.offsetLeft) / 10);
        // 正值，则步长往大取整；负值，则步长往小取整
        step = step > 0 ? Math.ceil(step) : Math.floor(step);
        
        if (obj.offsetLeft == target) {
            // 停止动画 本质是停止定时器
            clearInterval(obj.timer);
            
            // 回调函数写到定时器结束里面
            // 如果有回调函数才执行，否则不执行
         /* if (callback) {
               调用函数
               callback();
             } */
            
            // 上面代码等价于：
            callback && callback();
        }

        obj.style.left = obj.offsetLeft + step + 'px';

    }, 15); // 每15ms执行一次
}
```



## 1.2. 常见网页特效案例



### 1.2.1 案例：网页轮播图

轮播图也称为焦点图，是网页中比较常见的网页特效。

~~~js
功能需求：

1.鼠标经过轮播图模块，左右按钮显示，离开隐藏左右按钮。

2.点击右侧按钮一次，图片往左播放一张，以此类推，左侧按钮同理。

3.图片播放的同时，下面小圆圈模块跟随一起变化。

4.点击小圆圈，可以播放相应图片。

5.鼠标不经过轮播图，轮播图也会自动播放图片。

6.鼠标经过，轮播图模块， 自动播放停止。
~~~



#### 1. 鼠标经过轮播图模块，左右按钮显示

- 因为js较多，我们**单独新建js文件夹，再新建js文件， 引入页面中**。

- 此时需要添加 load 事件。（页面加载完再加载JS）

- 鼠标经过轮播图模块，左右按钮显示，离开隐藏左右按钮。

- 显示隐藏 display 按钮。



#### **2. 动态生成小圆圈**

- 核心思路：小圆圈的个数要跟图片张数一致

- 所以首先先得到ul里面图片的张数（图片放入li里面，所以就是li的个数 **ul.children.length**）

- 利用循环动态生成小圆圈（这个小圆圈要放入ol里面）

- 创建节点 createElement(‘li’)

- 插入节点 ol. appendChild(li)

- 第一个小圆圈需要**添加 current 类**（点击之后变色的效果）



#### 3.**点击小圆圈滚动图片**

- 此时用到animate动画函数，将js文件引入（注意，因为index.js 依赖 animate.js ，所以**animate.js 要写到 index.js 上面**）

- 使用动画函数的**前提，该元素必须有定位**

- 注意是ul 移动，而不是小li 

- 滚动图片的核心算法： 点击某个小圆圈，就让图片滚动：小圆圈的索引号**乘以**图片的宽度；

  以此作为ul移动距离。

- 此时需要知道小圆圈的索引号， 我们可以在生成小圆圈的时候，给它**设置一个自定义属性当做索引号**，点击的时候获取这个自定义属性即可。



#### 4. 点击右侧按钮滚动一张

- 如果按钮是a标签做的，先去把按钮标签里面的 href="javascript:;"
- 声明一个变量num， 点击一次，自增1， 让这个变量乘以图片宽度，就是 ul 的滚动距离。

图片无缝滚动原理：

- 5. 把ul 第一个li 复制一份，放到ul 的最后面

- 当图片滚动到克隆的最后一张图片时，让 ul 快速的、不做动画的跳到最左侧：即直接把 left 赋值为0
- 同时num 赋值为0，可以从头开始滚动图片了

> 考虑到先点圆圈再点左/右按钮的情况,当我们点击了某个小圆圈，就要把这个li的索引号给 num（控制移动）
>
> 在小圆圈的点击事件末尾处添加以下代码：
>
> ​            num = index;
> ​            



#### 5.**克隆第一张图片**

- 利用 var first = ul.children[0].cloneNode(true); 克隆ul 的第一个li 并赋值给一个变量（加true 深克隆，复制里面的子节点；不加或者 false 浅克隆）

- 利用 ul.appendChild(first); 将该变量添加到 ul 最后面 



#### 6. **点击右侧按钮， 小圆圈跟着变化**

- 最简单的做法是再声明一个变量circle，每次点击自增1。（注意，左侧按钮也需要这个变量，因此**要声明全局变量**）
- 但是图片有5张，我们小圆圈只有4个少一个，必须加一个判断条件：如果circle == 4 则复原为 0

> 考虑到先点圆圈再点左/右按钮的情况，当我们点击了某个小圆圈，就要把这个li 的索引号给 circle（控制小圆圈变色）
>
> 在小圆圈的点击事件末尾处添加以下代码：
>
> ​            circle = index;



#### 7.点击右侧按钮， 小圆圈跟着变化

- 复制右侧按钮的代码，然后将++改成--
- 特殊情况的距离也对应修改



#### 8. **自动播放功能**

- 添加一个定时器
- 自动播放轮播图，实际就类似于点击了右侧按钮
- 此时我们使用**手动调用**右侧按钮点击事件 arrow_r**.click()**
- 鼠标经过focus 就停止定时器
- 鼠标离开focus 就开启定时器

 



```js
window.addEventListener('load', function() {
    // 获取元素
    var arrow_l = document.querySelector('.arrow-l');
    var arrow_r = document.querySelector('.arrow-r');
    var focus = document.querySelector('.focus');
    var focusWidth = focusoffsetWidth;
    // 1. 鼠标经过focus 就显示左右按钮
    focus.addEventListener('mouseenter', function() {
        arrow_l.style.display = 'block';
        arrow_r.style.display = 'block';
        
        // 清除定时器变量
        clearInterval(timer);
        timer = null; 
    });
    // 1. 鼠标离开leave 就隐藏左右按钮
    focus.addEventListener('mouseleave', function() {
        arrow_l.style.display = 'none';
        arrow_r.style.display = 'none';
        
        //手动调用点击事件
        timer = setInterval(function() {
            arrow_r.click();
        }, 2000);
    });
    
    // 2. 动态生成小圆圈  有几张图片，我就生成几个小圆圈
    var ul = focus.querySelector('ul');
    var ol = focus.querySelector('.circle');

    for (var i = 0; i < ul.children.length; i++) {
        // 创建一个小li 
        var li = document.createElement('li');
        
        // 记录当前小圆圈的索引号 通过自定义属性来做
        li.setAttribute('index', i);
        
        // 把小li插入到ol 里面
        ol.appendChild(li);
        
        // 3. 直接在生成小圆圈的同时绑定点击事件
        li.addEventListener('click', function() {
            // 干掉所有人：把所有的小li 清除 current 类名
            for (var i = 0; i < ol.children.length; i++) {
                ol.children[i].className = '';
            }
            // 留下我自己：当前的小li 设置current 类名
            this.className = 'current';
            
            // 点击小圆圈，移动图片 注意移动的是 ul ，不是li
// ul的移动距离 = 小圆圈的索引号 * 图片的宽度 注意是负值【所以我们要给li加自定义属性做索引号】
            // 当我们点击了某个小li 就拿到当前小li 的索引号
            var index = this.getAttribute('index');
            
// 考虑到先点圆圈再点左/右按钮的情况，当我们点击了某个小圆圈，就要把这个li的索引号给 num（控制移动）
            num = index;
            
// 考虑到先点圆圈再点左/右按钮的情况，当我们点击了某个小圆圈，就要把这个li 的索引号给 circle（控制小圆圈变色）
            circle = index;
            
            // 以上2步可以统一写成：num = circle = index;

            // 动画移动距离记得加负号
            animate(ul, -index * focusWidth);
        })
    }
    
    // 把ol里面的第一个小li设置类名为 current （默认第一个圆圈亮）
    ol.children[0].className = 'current';
    
    // 5. 克隆第一张图片(li)放到ul最后面【克隆语句要放在生成小圆圈的后面，否则会多一个圆圈】
    var first = ul.children[0].cloneNode(true);
    ul.appendChild(first);
    
    // 4. 点击右侧按钮
    // 定义 num 让图片滚动一张
    var num = 0;
    
    // 定义 circle 控制小圆圈的变色
    var circle = 0;
    
    // flag 节流阀
    var flag = true;
    
    arrow_r.addEventListener('click', function() {
        if (flag) {	// 将所有代码放置到节流阀里面
            flag = false; // 关闭节流阀
            // 如果走到了最后复制的一张图片，此时 我们的ul 要快速复原 left 改为 0
            if (num == ul.children.length - 1) {
                ul.style.left = 0;
                num = 0;
            }
            
            // 点击右侧按钮，通过num控制图片的滚动
            num++;
            animate(ul, -num * focusWidth, function() { // 回调函数打开节流阀
                flag = true; 
            });
            
            // 点击右侧按钮，通过circle控制小圆圈随着变色
            circle++;
            // 如果circle == 4 说明走到最后我们克隆的这张图片了 我们就复原为0
         /* if (circle == ol.children.length) {
                circle = 0;
            } */
         // 可简写为：circle = 三元表达式
            circle == ol.children.length ? 0 : circle;
            
            // 调用函数使得对应圆圈亮起来
            circleChange();
        }
    });

    // 9. 左侧按钮做法
    arrow_l.addEventListener('click', function() {
        if (flag) {
            flag = false;
            if (num == 0) {
                num = ul.children.length - 1;
                ul.style.left = -num * focusWidth + 'px';

            }
            
            num--;
            animate(ul, -num * focusWidth, function() {
                flag = true;
            });
            
            // 点击左侧按钮，小圆圈跟随一起变化 可以再声明一个变量控制小圆圈的播放
            circle--;
            // 如果circle < 0  说明第一张图片，则小圆圈要改为第4个小圆圈（3）
            // if (circle < 0) {
            //     circle = ol.children.length - 1;
            // }
            // 可简写为：circle = 三元表达式
            circle = circle < 0 ? ol.children.length - 1 : circle;
            
            // 调用函数使得对应圆圈亮起来
            circleChange();
        }
    });

    // 点击左/右按钮后的圆圈变色函数：
    function circleChange() {
        // 先清除其余小圆圈的current类名
        for (var i = 0; i < ol.children.length; i++) {
            ol.children[i].className = '';
        }
        // 留下当前的小圆圈的current类名
        ol.children[circle].className = 'current';
    }
    
    // 10. 自动播放轮播图
    var timer = setInterval(function() {
        //手动调用点击事件
        arrow_r.click();
    }, 2000);

})
```



### 1.2.2. 节流阀

#### **目的**

防止轮播图按钮连续点击造成播放过快

#### 要求

做法当上一个函数动画内容执行完毕，再去执行下一个函数动画，让事件无法连续触发。

#### 思路

- 利用回调函数，添加一个变量来控制，锁住函数和解锁函数

  开始设置一个变量var flag= true;

- **If(flag){flag = false; do something}**       关闭水龙头

  **利用回调函数动画执行完毕， flag = true**     打开水龙头



### 1.2.3. 案例：返回顶部

1. 带有动画的返回顶部
2. 此时可以继续使用我们封装的动画函数
3. 只需要把所有的left 相关的值改为 跟 页面垂直滚动距离相关就可以了
4. 页面滚动了多少，可以通过 **window.pageYOffset** 得到
5. 页面滚动，使用 **window.scroll(x,y)** 的话会**直接跳转，没有动画**

```javascript
  //1. 获取元素
        var sliderbar = document.querySelector('.slider-bar');
        var banner = document.querySelector('.banner');
        // banner.offestTop 就是被卷去头部的大小 一定要写到滚动的外面
        var bannerTop = banner.offsetTop
            // 当我们侧边栏固定定位之后应该变化的数值
        var sliderbarTop = sliderbar.offsetTop - bannerTop;
        // 获取main 主体元素
        var main = document.querySelector('.main');
        var goBack = document.querySelector('.goBack');
        var mainTop = main.offsetTop;
        // 2. 页面滚动事件 scroll
        document.addEventListener('scroll', function() {
                // console.log(11);
                // window.pageYOffset 页面被卷去的头部
                // console.log(window.pageYOffset);
                // 3 .当我们页面被卷去的头部大于等于了 172 此时 侧边栏就要改为固定定位
                if (window.pageYOffset >= bannerTop) {
                    sliderbar.style.position = 'fixed';
                    sliderbar.style.top = sliderbarTop + 'px';
                } else {
                    sliderbar.style.position = 'absolute';
                    sliderbar.style.top = '300px';
                }
                // 4. 当我们页面滚动到main盒子，就显示 goback模块
                if (window.pageYOffset >= mainTop) {
                    goBack.style.display = 'block';
                } else {
                    goBack.style.display = 'none';
                }

            })
            // 3. 当我们点击了返回顶部模块，就让窗口滚动的页面的最上方
        goBack.addEventListener('click', function() {
            // 里面的x和y 不跟单位的 直接写数字即可
            // window.scroll(0, 0); 直接跳转，没有动画
            // 因为是窗口滚动 所以对象是window
            animate(window, 0);
        });

```



### 1.2.4. 案例：筋斗云案例

1. 利用动画函数做动画效果
2. 原先筋斗云的起始位置是0
3. 鼠标经过某个小li，把当前小li的offsetLeft 位置做为目标值即可
4. 鼠标离开某个小li，就把目标值设为 0
5. 如果点击了某个小li， 就把li当前的位置存储起来，做为筋斗云的起始位置

```javascript
 window.addEventListener('load', function() {
            // 1. 获取元素
            var cloud = document.querySelector('.cloud');
            var c_nav = document.querySelector('.c-nav');
            var lis = c_nav.querySelectorAll('li');
            // 2. 给所有的小li绑定事件 
            // 这个current 做为筋斗云的起始位置
            var current = 0;
            for (var i = 0; i < lis.length; i++) {
                // (1) 鼠标经过把当前小li 的位置做为目标值
                lis[i].addEventListener('mouseenter', function() {
                    animate(cloud, this.offsetLeft);
                });
                // (2) 鼠标离开就回到起始的位置 
                lis[i].addEventListener('mouseleave', function() {
                    animate(cloud, current);
                });
                // (3) 当我们鼠标点击，就把当前位置做为目标值
                lis[i].addEventListener('click', function() {
                    current = this.offsetLeft;
                });
            }
        })

```





## 七、移动端特效



## 1.1. 触屏事件

### 1.1.1 触屏事件概述

移动端浏览器兼容性较好，我们不需要考虑以前 JS 的兼容性问题，可以放心的使用原生 JS 书写效果，但是移动端也有自己独特的地方。比如触屏事件 touch（也称触摸事件），Android 和 IOS 都有。touch 对象代表一个触摸点。触摸点可能是一根手指，也可能是一根触摸笔。触屏事件可响应用户手指（或触控笔）对屏幕或者触控板操作。

常见的触屏事件如下：

![图片1](images\图片1.png)

### 1.1.2 触摸事件对象（TouchEvent）

TouchEvent 是一类描述手指在触摸平面（触摸屏、触摸板等）的状态变化的事件。这类事件用于描述一个或多个触点，使开发者可以检测触点的移动，触点的增加和减少，等等

touchstart、touchmove、touchend 三个事件都会各自有事件对象。

触摸事件对象重点我们看三个常见对象列表：

![图片2](images\图片2.png)

> **因为平时我们都是给元素注册触摸事件，所以重点记住 targetTocuhes**

### 1.1.3  移动端拖动元素

1.  touchstart、touchmove、touchend 可以实现拖动元素
2.  但是拖动元素需要当前手指的坐标值 我们可以使用  targetTouches[0] 里面的pageX 和 pageY 
3.  移动端拖动的原理：    手指移动中，计算出手指移动的距离。然后用盒子原来的位置 + 手指移动的距离
4.  手指移动的距离：  手指滑动中的位置 减去  手指刚开始触摸的位置

拖动元素三步曲：

（1） 触摸元素 touchstart： 获取手指初始坐标，同时获得盒子原来的位置

（2） 移动手指 touchmove： 计算手指的滑动距离，并且移动盒子

（3） 离开手指 touchend:



> **注意： 手指移动也会触发滚动屏幕所以这里要阻止默认的屏幕滚动 e.preventDefault();**

## 1.2. 移动端常见特效

### 1.2.1 案例: 移动轮播图

`移动端轮播图功能和基本PC端一致。`

1. 可以自动播放图片
2. 手指可以拖动播放轮播图

### 1.2.2. 案例分析:

1. 自动播放功能
2. 开启定时器
3. 移动端移动，可以使用translate 移动
4. 想要图片优雅的移动，请添加过渡效果![1551795152(1)](images\1551795152(1).jpg)


1. 自动播放功能-无缝滚动

2. 注意，我们判断条件是要等到图片滚动完毕再去判断，就是过渡完成后判断

3. 此时需要添加检测过渡完成事件  transitionend 

4. 判断条件：如果索引号等于 3 说明走到最后一张图片，此时 索引号要复原为 0

5. 此时图片，去掉过渡效果，然后移动

6. 如果索引号小于0， 说明是倒着走， 索引号等于2 

7. 此时图片，去掉过渡效果，然后移动

   ![1551795483(1)](images\1551795483(1).jpg)

## 1.2.3 classList 属性

classList属性是HTML5新增的一个属性，返回元素的类名。但是ie10以上版本支持。

该属性用于在元素中添加，移除及切换 CSS 类。有以下方法

**添加类：**

element.classList.add（’类名’）；

```javascript
focus.classList.add('current');
```

**移除类：**

element.classList.remove（’类名’）;

```javascript
focus.classList.remove('current');
```

**切换类：**

element.classList.toggle（’类名’）;

```javascript
focus.classList.toggle('current');
```

`注意:以上方法里面，所有类名都不带点`

### 1.2.4. 案例分析

1. 小圆点跟随变化效果

2. 把ol里面li带有current类名的选出来去掉类名 remove

3. 让当前索引号的小li 加上 current   add

4. 但是，是等着过渡结束之后变化，所以这个写到 transitionend 事件里面

   ![1551796072(1)](images\1551796072(1).jpg)


1. 手指滑动轮播图
2. 本质就是ul跟随手指移动，简单说就是移动端拖动元素
3. 触摸元素touchstart：  获取手指初始坐标
4. 移动手指touchmove：  计算手指的滑动距离，并且移动盒子
5. 离开手指touchend:   根据滑动的距离分不同的情况
6. 如果移动距离小于某个像素  就回弹原来位置
7. 如果移动距离大于某个像素就上一张下一张滑动。
8. 滑动也分为左滑动和右滑动判断的标准是 移动距离正负 如果是负值就是左滑 反之右滑 
9. 如果是左滑就播放下一张 （index++）
10. 如果是右滑就播放上一张  (index--)

![1551796363(1)](images\1551796363(1).jpg)

![1551796502(1)](images\1551796502(1).jpg)





### 1.3.1. 案例：返回顶部

当页面滚动某个地方，就显示，否则隐藏

点击可以返回顶部

### 1.3.2.案例分析

1. 滚动某个地方显示
2. 事件：scroll页面滚动事件  
3. 如果被卷去的头部（window.pageYOffset ）大于某个数值
4. 点击，window.scroll(0,0) 返回顶部

![1551797003(1)](images\1551797003(1).jpg)



## 1.4. click 延时解决方案

移动端 click 事件会有 300ms 的延时，原因是移动端屏幕双击会缩放(double tap to zoom) 页面。

解决方案：

	1. 禁用缩放。 浏览器禁用默认的双击缩放行为并且去掉300ms 的点击延迟。

```html
  <meta name="viewport" content="user-scalable=no">
```

	2.利用touch事件自己封装这个事件解决300ms 延迟。 
	
	原理就是：

1.  当我们手指触摸屏幕，记录当前触摸时间
2.  当我们手指离开屏幕， 用离开的时间减去触摸的时间
3.  如果时间小于150ms，并且没有滑动过屏幕， 那么我们就定义为点击

代码如下:

```javascript
//封装tap，解决click 300ms 延时
function tap (obj, callback) {
        var isMove = false;
        var startTime = 0; // 记录触摸时候的时间变量
        obj.addEventListener('touchstart', function (e) {
            startTime = Date.now(); // 记录触摸时间
        });
        obj.addEventListener('touchmove', function (e) {
            isMove = true;  // 看看是否有滑动，有滑动算拖拽，不算点击
        });
        obj.addEventListener('touchend', function (e) {
            if (!isMove && (Date.now() - startTime) < 150) {  // 如果手指触摸和离开时间小于150ms 算点击
                callback && callback(); // 执行回调函数
            }
            isMove = false;  //  取反 重置
            startTime = 0;
        });
}
//调用  
  tap(div, function(){   // 执行代码  });

```

3. 使用插件。fastclick 插件解决300ms 延迟。 

   ![1551797533(1)](images\1551797533(1).jpg)

## 1.5. 移动端常用开发插件

### 1.5.1. 什么是插件

移动端要求的是快速开发，所以我们经常会借助于一些插件来帮我完成操作，那么什么是插件呢？

JS 插件是 js 文件，它遵循一定规范编写，方便程序展示效果，拥有特定功能且方便调用。如轮播图和瀑布流插件。

特点：它一般是为了解决某个问题而专门存在，其功能单一，并且比较小。

我们以前写的animate.js 也算一个最简单的插件

fastclick 插件解决 300ms 延迟。 使用延时

GitHub官网地址： [https://](https://github.com/ftlabs/fastclick)[github.com/ftlabs/fastclick](https://github.com/ftlabs/fastclick)

### 1.5.2. 插件的使用

1.  引入 js 插件文件。

2.  按照规定语法使用。

3.  fastclick 插件解决 300ms 延迟。 使用延时

4.  GitHub官网地址： https://github.com/ftlabs/fastclick

    ```javascript
    if ('addEventListener' in document) {
                document.addEventListener('DOMContentLoaded', function() {
                           FastClick.attach(document.body);
                }, false);
    }
    ```

### 1.5.3. Swiper 插件的使用

中文官网地址： https://www.swiper.com.cn/ 

1.  引入插件相关文件。
2.  按照规定语法使用

### 1.5.4. 其他移动端常见插件

lsuperslide： http://www.superslide2.com/

l iscroll： https://github.com/cubiq/iscroll

### 1.5.5. 插件的使用总结

1.确认插件实现的功能

2.去官网查看使用说明

3.下载插件

4.打开demo实例文件，查看需要引入的相关文件，并且引入

5.复制demo实例文件中的结构html，样式css以及js代码

### 1.5.6. 移动端视频插件 zy.media.js

H5 给我们提供了 video 标签，但是浏览器的支持情况不同。

不同的视频格式文件，我们可以通过source解决。

但是外观样式，还有暂停，播放，全屏等功能我们只能自己写代码解决。

这个时候我们可以使用插件方式来制作。

我们可以通过 JS 修改元素的大小、颜色、位置等样式。



## 1.6. 移动端常用开发框架

### 1.6.1. 移动端视频插件 zy.media.js

框架，顾名思义就是一套架构，它会基于自身的特点向用户提供一套较为完整的解决方案。框架的控制权在框架本身，使用者要按照框架所规定的某种规范进行开发。

插件一般是为了解决某个问题而专门存在，其功能单一，并且比较小。

前端常用的框架有 Bootstrap、Vue、Angular、React 等。既能开发PC端，也能开发移动端

前端常用的移动端插件有 swiper、superslide、iscroll等。

框架： 大而全，一整套解决方案

插件： 小而专一，某个功能的解决方案

### 1.6.2. Bootstrap

Bootstrap 是一个简洁、直观、强悍的前端开发框架，它让 web 开发更迅速、简单。

它能开发PC端，也能开发移动端 

Bootstrap JS插件使用步骤：

1.引入相关js 文件

2.复制HTML 结构

3.修改对应样式

4.修改相应JS 参数

## 1.7. 本地存储

随着互联网的快速发展，基于网页的应用越来越普遍，同时也变的越来越复杂，为了满足各种各样的需求，会经常性在本地存储大量的数据，HTML5规范提出了相关解决方案。

### 1.7.1.本地存储特性

1、数据存储在用户浏览器中

2、设置、读取方便、甚至页面刷新不丢失数据

3、容量较大，sessionStorage约5M、localStorage约20M

4、只能存储字符串，可以将对象JSON.stringify() 编码后存储

### 1.7.2.window.sessionStorage

1、生命周期为关闭浏览器窗口

2、在同一个窗口(页面)下数据可以共享

3、以键值对的形式存储使用

存储数据：

```javascript
sessionStorage.setItem(key, value)
```

获取数据：

```javascript
sessionStorage.getItem(key)
```

删除数据：

```javascript
sessionStorage.removeItem(key)
```

清空数据：(所有都清除掉)

```javascript
sessionStorage.clear()
```

### 1.7.3.window.localStorage

1、声明周期永久生效，除非手动删除 否则关闭页面也会存在

2、可以多窗口（页面）共享（同一浏览器可以共享）

3.  以键值对的形式存储使用

存储数据：

```javascript
localStorage.setItem(key, value)
```

获取数据：

```javascript
localStorage.getItem(key)
```

删除数据：

```javascript
localStorage.removeItem(key)
```

清空数据：(所有都清除掉)

```javascript
localStorage.clear()
```

### 1.7.4.案例：记住用户名

如果勾选记住用户名， 下次用户打开浏览器，就在文本框里面自动显示上次登录的用户名

#### 案例分析

1. 把数据存起来，用到本地存储

2. 关闭页面，也可以显示用户名，所以用到localStorage

3. 打开页面，先判断是否有这个用户名，如果有，就在表单里面显示用户名，并且勾选复选框

4. 当复选框发生改变的时候change事件

5. 如果勾选，就存储，否则就移除

   ![1551800263(1)](images\1551800263(1).jpg)













