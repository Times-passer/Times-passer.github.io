
## 标题标签\<h1>~\<h6>

- 块级元素

- 一般一个HTML里面只有一个\<h1>，即使样式改变，他的权重不变
- 没有h7及以后的标签，若写了h7，字体样式会变成普通文本

## 段落标签\<p>

+ 输入多个空格时只渲染一个空格，想渲染多个空格的话，用多个`&nbsp;`

+ p标签具有默认的样式——上下有一定的margin外边距：![image-20210711162113954](https://i.loli.net/2021/07/13/dGsPZcN8qFLSwVh.png)

  <img src="E:\Warehouse\conscious\【前端学习】\华为云大前端\第1阶段 前端基础篇\1 HTML\image-20210711162134749.png" alt="image-20210711162134749" style="zoom: 67%;" />

  

+ p标签中的行数，取决于浏览器窗口的长度





## 结构标签\<div>\<span>

### \<div>(division)

* **是块级元素**
* 没有特殊含义，所以常用来划分区域，是最通用的页面容器



### \<span>

- **是内联元素**
- 也是没有什么特定格式，常用来修饰部分文字的样式





## 链接标签\<a>

- **是内联元素**

- anchor（锚）的缩写，用于定义网页链接
- `href`属性表示链接的地址，可以是相对地址或者绝对地址
- `target`属性表示点击链接后打开的方式，默认值为`"_self"`,代表在当前窗口打开新的链接；也可设置为`"_blank"`，代表在新窗口中打开
- 如果不想在每个链接后面都加`target="_blank"`,可以在\<head>里使用`<base>`标签

~~~
<base target="_blank">
~~~

**当然，你可以在使用base标签之后，仍然在某些链接后面单独加target属性，优先级比base高**



## html相对路径的写法

 > ./   代表文件所在的目录（可以省略不写）如果写成image/background就相当于是在html文件下找image文件夹，当然是找不到的  
 > ../    代表文件所在的父级目录    
 > ../../ 代表文件所在的父级目录的父级目录   
 > /      代表文件所在的根目录    



### HTML 中的 href 和 src 有什么区别

href 是 Hypertext Reference 的缩写，表示超文本引用。用来建立当前元素和文档之间的链接。常用的有：link、a。例如：

`<link href="reset.css" rel=”stylesheet“/>`
浏览器会识别该文档为 css 文档，并行下载该文档，并且不会停止对当前文档的处理。这也是建议使用 link，而不采用 @import 加载 css 的原因。 src 是 source 的缩写，src 的内容是页面必不可少的一部分，是引入。src 指向的内容会嵌入到文档中当前标签所在的位置。常用的有：img、script、iframe。例如:

`<script src="script.js"></script>`
当浏览器解析到该元素时，会暂停浏览器的渲染，直到该资源加载完毕。这也是将js脚本放在底部而不是头部得原因。

***简而言之，src 用于替换当前元素；href 用于在当前文档和引用资源之间建立联系。***



## 图片标签\<img>

- 单标签
- `src`属性表示图片的地址，`alt`属性表示当图片无法显示时的替代文本，`title`属性表示鼠标光标移动到图片上时的提示





### 引入图片路径示例

1. *.html 文件跟 *.jpg 文件(f盘)在不同目录下：

   > ` <img src="file:///f:/*.jpg" width="300" height="120"/>  `

2. *.html 文件跟 *.jpg 图片在相同目录下：

   >  ` <img src="*.jpg" width="300" height="120"/> `

3. *.html 文件跟 *.jpg 图片在不同目录下：

   >a、图片 *.jpg 在 image 文件夹中，*.html 跟 image 在同一目录下：
   >
   >>`<img src="image/*.jpg/"width="300" height="120"/>`

   >b、图片 *.jpg 在 image 文件夹中，*.html 在 connage 文件夹中，image 跟 connage 在同一目录下：
   >
   >>`<img src="../image/*.jpg/"width="300" height="120"/>`

4. 如果图片来源于网络，那么写绝对路径：

   > ` <img src="http://static.runoob.com/images/runoob-logo.png" width="300" height="120"/> ` 





## 列表标签\<ul>\<ol>\<dl>

- \<ul>无序列表、\<ol>有序列表；\<li>定义列表项
- \<dl>（definition list）自定义列表（\<dt>标题、\<dd>列表项）

> <img src="https://i.loli.net/2021/07/13/DmeukoCWMaNq1Jb.png" alt="image-20210712095515695" style="zoom: 67%;" />





## 表格标签\<table>\<caption>\<tr>\<th>\<td>

- \<table>包括整个表格
- \<caption>表示表格标题
- \<tr>表示一行，\<td>表示一列
- \<th>表示表头，和td一样都是写在tr里面的；**但th相比td，有自己独特的样式：居中  字体加粗** 
- `align`属性规定单元格内容的水平对齐方式

> <img src="E:\Warehouse\conscious\【前端学习】\华为云大前端\第1阶段 前端基础篇\1 HTML\image-20210712102642249.png" alt="image-20210712102642249" style="zoom:67%;" />



### thead、tbody、tfoot标签

**\<thead>\</thead>**			***\*表格页眉标签（包裹表头的<tr>）\****

**\<tbody>\</tbody>**			***\*表格主体标签（包裹表格内容的<tr>）\****

**\<tfoot>\</tfoot>**			***\*表格页尾标签（包裹页尾的<tr>）\****

**内部也需要tr、th、td标签**

> <img src="E:\Warehouse\conscious\【前端学习】\华为云大前端\第1阶段 前端基础篇\1 HTML\image-20210712103528249.png" alt="image-20210712103528249" style="zoom:67%;" />



**特点：**

- 3个标签缺一不可，即使不写页尾，就放一个空的\<tfoot>\</tfoot>也要写。(\<thead>和tfoot各自只能有一个，但tbody可以有多个)
- 不会因为你写代码的时候把tfoot标签在tbody前面就会影响表格的显示顺序
- \<thead>和\<tfoot>**有自己的样式**，不会被table标签里面的宽高属性所限制；\<tbody>没有自己的样式

- 使用这3个标签，会先加载页眉页尾，再加载主体（在数据量大的时候，如果不用这3个标签，等全部加载完再渲染出来会显得特别慢）【加载顺序始终是thead->tfoot->tbody】

>  <img src="E:\Warehouse\conscious\【前端学习】\华为云大前端\第1阶段 前端基础篇\1 HTML\image-20210712151804020.png" alt="image-20210712151804020" style="zoom:67%;" />



### \<col>\<colgroup> 标签：规定某一列的全部样式

- \<col> 标签为表格中一个或多个列定义属性值。
- 如需对全部列应用样式，\<col> 标签很有用，这样就不需要对各个单元和各行重复应用样式了。
- 您只能在\<table>  或 \< colgroup> 元素中使用 \<col> 标签。

> ![image-20210713162120133](E:\Warehouse\conscious\【前端学习】\华为云大前端\第1阶段 前端基础篇\1 HTML\image-20210713162120133.png)
>
> ![image-20210713162235166](E:\Warehouse\conscious\【前端学习】\华为云大前端\第1阶段 前端基础篇\1 HTML\image-20210713162235166.png)



### 表格的常用属性

- `border`设定边框，属性值的数字代表边框宽度
- `border-collapse: collapse;`使表格边框变成实心
- `width`宽度、`height`高度
- `cellspacing` 单元格间距（="0" 使得边框不会镂空）
- `cellpadding `单元格内边距



### \<colspan>\< rowspan> 标签：合并单元格

\<td>有两个常用属性，**`colspan`用于相邻列（横向）合并、`rowspan`用于相邻行（纵向）合并**

- 如果使用了单元格合并，没有把多余的单元格删除，多余的单元格会被挤到表格外面去

- > 有被thead、tbody、tfoot标签包裹的单元格，不会受到没被thead、tbody、tfoot标签的合并影响；
  >
  > 同样，没有被thead、tbody、tfoot标签包裹的单元格，也不会受到有被thead、tbody、tfoot标签包裹的单元格影响。





## 表单标签\<form>[数据交互功能]

- `action`属性定义表单提交的**地址（可以是网页，可以是后端地址）**

- `method`属性定义**提交的方式**，表单提交有2种方式：**get是用来从服务器上获得数据，而post是用来向服务器上传递数据**
- 其他表单控件元素必须放在form标签的内部，最好每**部分都用\<div>分块**

> 实例：
>
> ![image-20210713170709672](E:\Warehouse\conscious\【前端学习】\华为云大前端\第1阶段 前端基础篇\1 HTML\image-20210713170709672.png)
>
> ![image-20210713170728302](E:\Warehouse\conscious\【前端学习】\华为云大前端\第1阶段 前端基础篇\1 HTML\image-20210713170728302.png)



### \<input>输入框/按钮

- **单标签**元素
- 其type属性代表了input的表单类型，通过type属性的不同取值，来定义不同的表单控件

> `<input type="text" />`				  单文本框
>
> `<input type="password" />`		  密码输入框
>
> `<input type="radio" />`				单选按钮
>
> `<input type="checkbox" />`		  多选按钮
>
> `<input type="button" />`			  普通按钮
>
> `<input type="submit" />`			  提交按钮
>
> `<input type="reset" />`				重置按钮
>
> `<input type="file" />`				  文件上传按钮



### \<select>\<option>下拉列表

- \<select>用来定义列表；\<option>用来定义列表项
- \<option>里可添加`selected`属性，规定该选项默认选中
- \<select>里可添加`size="n"`属性，规定同时展示n个选项

- \<select>里可添加`multiple`属性，使得下拉列表可以按住shift多选

> ![image-20210713204856555](E:\Warehouse\conscious\【前端学习】\华为云大前端\第1阶段 前端基础篇\1 HTML\image-20210713204856555.png)



### \<textarea>输入多行文本域

- `cols`属性设定列数，`rows`属性设定行数

> ![image-20210713204820560](E:\Warehouse\conscious\【前端学习】\华为云大前端\第1阶段 前端基础篇\1 HTML\image-20210713204820560.png)



