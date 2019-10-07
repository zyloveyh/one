## CSS 预处理器

### 1. 为什么要有 CSS 预处理器

**CSS基本上是设计师的工具，不是程序员的工具**。在程序员的眼里，CSS是很头痛的事情，它并不像其它程序语言，比如说PHP、Javascript等等，有自己的变量、常量、条件语句以及一些编程语法，只是一行行单纯的属性描述，写起来相当的费事，而且代码难以组织和维护。

很自然的，有人就开始在想，能不能给CSS像其他程序语言一样，加入一些编程元素，让CSS能像其他程序语言一样可以做一些预定的处理。这样一来，就有了“**CSS预处器**（CSS Preprocessor）”。

### 2. 什么是 CSS 预处理器

- 是 CSS 语言的**超集**，比CSS更丰满。

CSS 预处理器定义了一种新的语言，其基本思想是：**用一种专门的编程语言，为CSS增加了一些编程的特性**，将CSS作为目标生成文件，然后开发者就只要使用这种语言进行编码工作。

通俗的说，**CSS预处理器用一种专门的编程语言，进行Web页面样式设计，然后再编译成正常的CSS文件**，以供项目使用。CSS预处理器为CSS增加一些编程的特性，无需考虑浏览器的兼容性问题，例如你可以在CSS中使用变量、简单的逻辑程序、函数等等在编程语言中的一些基本特性，可以让你的CSS更加简洁、适应性更强、可读性更佳，更易于代码的维护等诸多好处。

CSS预处理器技术已经非常成熟，而且也涌现出了很多种不同的CSS预处理器语言，比如说：**Sass（SCSS）、LESS**、Stylus、Turbine、Swithch CSS、CSS Cacheer、DT CSS等。如此之多的CSS预处理器，那么“我应该选择哪种CSS预处理器？”也相应成了最近网上的一大热门话题，在Linkedin、Twitter、CSS-Trick、知呼以及各大技术论坛上，很多人为此争论不休。相比过计我们对是否应该使用CSS预处理器的话题而言，这已经是很大的进步了。

到目前为止，在众多优秀的CSS预处理器语言中就属**Sass、LESS和Stylus最优秀**，讨论的也多，对比的也多。本文将分别从他们产生的背景、安装、使用语法、异同等几个对比之处向你介绍这三款CSS预处理器语言。相信前端开发工程师会做出自己的选择——我要选择哪款CSS预处理器。

### 3. less 的介绍

less 是一款比较流行的**预处理 CSS**，支持变量、混合、函数、嵌套、循环等特点。

- [官网](http://lesscss.org/)
- [中文网（less 文档）](http://lesscss.cn/)
- [Bootstrap网站的 less 文档](https://less.bootcss.com/)
- 推荐文章：<http://www.w3cplus.com/css/less>

### 4. less使用 在 demo.html中直接引用 less.js

- 做法一：写完 less文件后，将其编译为 css 文件，然后在代码中引用css文件。
- 做法二：在代码中直接用引用 less 文件。

产品上线后，当然是使用做法一，因为做法二会多出编译的时间。

平时开发或演示demo的时候可以用做法二。

这一段，我们讲一下做法二，其实是浏览器在本地在线地把 less 文件转换为 css 文件。

1.  在 less 官网下载 less.js 文件：

![](http://img.smyhvae.com/20180226_2131.png)

把下载好的文件放在工程文件的lib文件夹里：

![](http://img.smyhvae.com/20180226_2143.png)

2. 在 index.html 中引入 less.js 和我们自己写的  main.less。位置如下：

    ```
    	<!-- 1. 创建和引入less文件 页面中可以直接引入 但是不会像CSS一样执行 强调rel="stylesheet/less" -->
    	<link rel="stylesheet/less" href="demo.less">
    	<!-- 2. 引入一个less.js文件 编译器文件 用来编译less -->
    	<!-- 因为less虽然引入了但是代码不能被浏览器解析成样式 通过less.js 吧less代码 编译(在js代码里面临时去编译)成css代码浏览器才可以执行 -->
    	<script src="jd/lib/less/less.js"></script>
    	<!-- 3. 使用服务器打开页面 less.js里面会发送ajax 请求demo.less 吧代码编译成css代码 通过style标签嵌入到页面中 完成了less的编译 所以要注意引入顺序 因为less.js是用来编译demo.less的 所以先引入demo.less 再引入less.js -->
    ```

    



3. 使用服务器访问页面

    1. sublimeserver

       ​  ![2](img\2.png)

       

       

    2. vscode live server

       ![3](img\3.png)

       ![4](img\4.png)



我们可以在打开的网页中，通过控制台看到效果：

![](img\5.png)

注意，我们要在服务器中打开 html 文件，否则，看不到效果。

less的编译原理

​	![less的编译原理](img\less的编译原理.png)

这里也告诉了我们：

> 不提倡将 less 引入页面，因为 less 需要编译，因此你就需要再引入一个less.js, 多了一个HTTP 请求，同时当浏览器禁用了 js 你的样式就不起作用了，less 编译应该在服务端或使用 一些自动化工具自动编译。

参考链接：

- [知乎 | less文件如何引入页面](https://www.zhihu.com/question/26075208)


### 5. less 的语法

#### 1. 注释

less 的注释可以有两种。

第一种注释：模板注释

```less
  // 模板注释 这里的注释转换成CSS后将会删除
```

因为 less 要转换为 css才能在浏览器中使用。转换成 css 之后，这种注释会被删除（毕竟 css 不识别这种注释）。

第二种注释：CSS 注释语法

```less
/* CSS 注释语法 转换为CSS后让然保留 */
```

总结：如果在less中写注释，我们推荐写第一种注释。除非是类似于版权等内容，就采用第二种注释。

#### 2. 定义变量

我们可以把**重复使用或经常修改的值**定义为变量，在需要使用的地方引用这个变量即可。这样可以避免很多重复的工作量。

（1）在less文件中，定义一个变量的格式：

```less
/* 1. 定义变量
在less里面可以写高级代码 
语法使用@符号开头
变量名的命名规范和JS一样  中间可以有-
值可以是任意CSS里面能够写的值 px 颜色 单词等等 但是写值的时候和CSS一样带单位
@变量名:值; */
/* 变量都是全局变量  变量名不能冲突 */
/* 把全局变量单独提取到一个文件里面 */
@bgc: #ccc;
@w-100:200px;
@h-100:200px;
@border-color:hotpink;
```

（2）同时，在 less 文件中引用这个变量。

最终，less文件的完整版代码如下：

demo.less：

```less
.box1 {
    background-color: @bgc;
    width: @w-100;
    height: @h-100;
    margin-top: 10px;
    float: left;
}

```

我们将上面的less文件编译为 css 文件后（下一段讲less文件的编译），自动生成的代码如下：

demo.css：

```css
.box1 {
  background-color: #ccc;
  width: 200px;
  height: 200px;
  margin-top: 10px;
  float: left;
}
```

#### 3. 使用嵌套

在 css 中经常会用到子代选择器，效果可能是这样的：

```css
.container{
	width: 1170px;
	margin: 0px auto;	
	padding: 0 15px;
	height: 100px;	
}

.container .row{
	margin: 0px -15px;	
	height: 100px;	
}

.container .row .col{
	width: 33.33%;
	float: left;
}


.container .row .col a{
	color:red;
	text-decoration: none;
} 
```

上面的代码嵌套了很多层，写起来很繁琐。可如果用 less 的嵌套语法来写这段代码，就比较简洁。

嵌套的举例如下：

demo.less:

```less
.container{
	width: 1170px;
	margin: 0px auto;	
	padding: 0 15px;
	height: 100px;	
   >.row{
		margin: 0px -15px;	
		height: 100px;	
		>.col{
			width: 33.33%;
			float: left;
			>a{
				color:red;
				text-decoration: none;
				/* &在哪里面就表示谁 和JS this */
				/* 表示当前的a的hover */
				&:hover{
					color:green;
				}
				&::before{
					content:'伪元素';
				}
				&::after{
					content:'伪元素';
				}
				/* 交集选择器 */
				&.active{
					color:yellow;
				}
			}
		}
	}
}
```

将上面的less文件编译为 css 文件后，自动生成的代码如下：

demo.css

```css
/* less嵌套 可以像标签一样写嵌套 */
.container {
  width: 1170px;
  margin: 0px auto;
  padding: 0 15px;
  height: 100px;
}
.container > .row {
  margin: 0px -15px;
  height: 100px;
}
.container > .row > .col {
  width: 33.33%;
  float: left;
}
.container > .row > .col > a {
  color: red;
  text-decoration: none;
  /* &在哪里面就表示谁 和JS this */
  /* 表示当前的a的hover */
  /* 交集选择器 */
}
.container > .row > .col > a:hover {
  color: green;
}
.container > .row > .col > a:before {
  content: '伪元素';
}
.container > .row > .col > a:after {
  content: '伪元素';
}
.container > .row > .col > a.active {
  color: yellow;
}
```



#### 4. Mixin(自定义函数)

Mixin 的作用是把**重复的代码**放到一个类当中，每次只要引用类名，就可以引用到里面的代码了，非常方便。

（1）在 less 文件中定义一个类：（将重复的代码放到自定义的类中）

```less
/* 给自定义函数添加参数
变量在函数里面 表示一个形参 参数名称也是@符号
可以把一些重复使用样式封装成一个函数 还可以带参数 参数还可以设置默认值
参数可以有多个 多个使用特殊符号隔开 一般是逗号
 */
/* 把所有全局的函数 单独提取到了一个公共的文件 */
.bordertb(@size,@style){
	border-top: @size @style @border-color;
	border-bottom: @size @style @border-color;	
}
.bordertb(@size:5px,@style:solid){
	border-top: @size @style @border-color;
	border-bottom: @size @style @border-color;
}
```

上方代码中，括号里的内容@size是参数：这个5px参数的**默认值**。

（2）在 less 文件中引用上面这个类：

```less
.box1 {
    background-color: @bgc;
    width: @w-100;
    height: @h-100;
    margin-top: 10px;
    .bordertb();
    float: left;
}

.box2 {
    background-color: @bgc;
    width: @w-100;
    height: @h-100+100;
    margin-top: 10px;
    .bordertb(20px,dashed);
    float: left;
}

```



上方代码中，header 中的引用没有带参数，表示参数为缺省值； footer 中的引用带了参数，那就用这个参数。



#### 5. Import(引包)

在开发阶段，我们可以将不同的样式放到多个文件中，最后通过@import 的方式合并。意思就是，当出现多个 less 文件时，怎么引用它们。

这个很好理解， css 文件可以有很多个，less文件也可以有很多个。

（1）定义一个被引用的less文件，名为variables.less：

`variables.less:`

```less
/* 1. 定义变量
在less里面可以写高级代码 
语法使用@符号开头
变量名的命名规范和JS一样  中间可以有-
值可以是任意CSS里面能够写的值 px 颜色 单词等等 但是写值的时候和CSS一样带单位
@变量名:值; */
/* 变量都是全局变量  变量名不能冲突 */
/* 把全局变量单独提取到一个文件里面 */
@bgc: #ccc;
@w-100:200px;
@h-100:200px;
@border-color:hotpink;
```

（2）在 `demo.less` 中引用上面的 `variables.less`

`demo.less`：

```less
/* 4. 引包 一般在最前面 把别的less文件的代码引入到当前less文件里面执行
把一些公共的样式 变量放到公共的文件里面 */
/* 引入定义变量的less文件 */
@import 'variables.less';
/* 引入定义函数的less文件 */
@import 'mixins.less';
.box1 {
    background-color: @bgc;
    width: @w-100;
    height: @h-100;
    margin-top: 10px;
    .bordertb();
    float: left;
}
```

将 上面的demo.less编译为 demo.css之后，自动生成的代码如下：

```css
.box1 {
  background-color: #ccc;
  width: 200px;
  height: 200px;
  margin-top: 10px;
  border-top: 5px solid hotpink;
  border-bottom: 5px solid hotpink;
  border-top: 10px solid hotpink;
  border-bottom: 10px solid hotpink;
  float: left;
}
```

​	`demo.less`会自动使用 `variables.less`里面定义好的变量直接

#### 6. 内置函数

less 里有一些内置的函数，这里讲一下 lighten 和 darken 这两个内置函数。

demo.less:

```less
body {
  background-color: lighten(#000, 90%);   // 让黑色变亮 10%
  color: darken(#fff, 10%);               // 让白色变暗 10%
}
```

将 上面的 demo.less 编译为 demo.css 之后，自动生成的代码如下：

demo.css：

```css
body {
  background-color: #e6e6e6;
  color: #e6e6e6;
}


```

  ​    

### 6. less 的编译

less 的编译指的是将写好的 less 文件 生成为 css 文件。

less 的编译，依赖于 NodeJS 环境。因此，我们需要先安装 NodeJS。

#### 1.安装 Node.js

去 [Node.js](https://nodejs.org/zh-cn/)的官网下载安装包：

​	![6](img\6.png)

使用本地下载好的nodejs


​	![7](img\7.png)

双击一路 next 进行安装不要修改目录。

​	

在 cmd 命令行，输入`node -v`，可以查看 node.js 的版本。

![8](img\8.png)

#### 2. 安装 less 的编译环境



可以输入下面的命令安装less包：

```bash
    npm默认为国外的话不翻墙可能安装包很慢甚至安装不了推荐使用国内的 执行分别下面2段命令
    npm config set registry http://registry.npm.taobao.org/
    npm install -g less
```

#### 3. 将 less 文件编译为 css 文件

在 less 所在的路径下，输入 `lessc xxx.less`，即可编译成功。或者，如果输入 `lessc xxx.less > ..\xx.css`，表示输出到指定路径。

​      

#### 4. 使用vscode的Easy less插件

![9](img\9.png)

写完less代码保存自动会编译生成css文件

![10](img\10.png)

## flex布局 

参考文档 http://www.runoob.com/w3cnote/flex-grammar.html

### flex布局介绍
* 绝对布局有什么问题
    * 宽高固定
    * 不能适应各种尺寸的屏幕
    * 需要大量的坐标的计算
* flex布局可以做什么？
    * 按比例分配父盒子空间，并且跟随父盒子缩放自动按比例排布
    * 自动换行与排列方向
    * 各种对齐方式

### flex布局容器和子元素

  1. flex布局 分为子元素父元素 属性分为父元素(父容器)和子元素(子项目)
  2. flex 还分主轴 和 侧轴  围绕主轴侧轴来开展的布局
## 父容器属性
    1. display:flex; 只要要使用flex布局必须给父元素设置属性 才能让里面子元素按照伸缩布局方式显示
    2. flex布局方向分为2种 水平和垂直 flex-direction改变主轴方向
        row 水平   默认值
        row-reverse 水平反方向
        column 垂直
        column-reverse 垂直反方向
        改了主轴后 侧轴也会跟着变 跟主轴相反的
    3. 主轴对齐方式 justify-content  
        flex-start 主轴起点  默认
        flex-end 主轴终点
        center 主轴中间
        space-between 主轴2端
        space-around 主轴的四周环绕
        主轴根据 flex-direction 来控制的 默认值水平 默认 justify-content  水平对齐
        如果修改了主轴方向 justify-content  控制的对齐也会修改
    4. align-items 侧轴对齐方式(单行)
            flex-start 侧轴起点
            flex-end 侧轴终点
            center 侧轴居中
            baseline 侧轴第一行文字基线 (子元素文字第一行文字大小不一样才能看出来)
            stretch 默认 拉伸
    5. flex-wrap 换行
        nowrap 不换行 默认值
        wrap 换行
        如果需要换行子元素要有宽度当放不下就换行
    6. algin-content 多行情况下的侧轴的对齐方式
        多行情况下 主轴是水平 设置align-content 控制垂直的多行对齐方式
        flex-start 侧轴起点 
        flex-end 侧轴终点
        center 侧轴中间
        space-between 侧轴2端
        space-around 侧轴的四周环绕
        stretch 拉伸 默认值