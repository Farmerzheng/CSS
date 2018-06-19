http://www.css88.com/doc/less/features/#features-overview-feature

http://www.bootcss.com/p/lesscss/

## 概览

Less 是一个 CSS 预编译语言,

意思指的是它可以扩展 CSS 语言,

添加功能：变量(variables) , 混合(mixins) , 函数(functions) 和 许多其他的技术，

让你的 CSS 更具维护性，主题性，扩展性。

Less 可运行在 Node 环境 , 浏览器环境

## 使用

### 浏览器中使用

+ 开发环境中使用   (引入less.js)
+ 生产环境中使用（编译成CSS）

#### 生产环境中使用less

浏览器是不能够解析less文件的(浏览器能够解析html、CSS、js)，

我们必须将less文件转换成CSS文件才能在浏览器中运行

因此项目上线的时候，我们需要将less代码转换成CSS代码

如何将less代码转换成css代码？

通过安装node包（less包），來将LESS转换成CSS

如何使用node包？

1. 创建package.json
2. 安装node包
3. 调用node包为我们提供的命令
4. 有些node包需要配置文件，例如webpack包的webpack.congfig.js文件， babel包的.babelrc文件



安装less包？

1. 在项目根目录下执行 npm init  ，生成一个 package.json 文件

2. 将less包作为项目的开发依赖安装

   > npm install --save-dev  less  

​     `项目的名称`一定不要和`包名`一样！！！！

​     如果项目的名称是less  那么在less 项目下将不能安装less包 

3. 运行安装好的less包，将 less文件转换成 CSS 文件

   方法一：  

   ​     在命令行输入

   ​     (本地安装)

   >  node_modules/.bin/lessc  style.less > style.css

      （全局安装）

   > lessc style.less > style.css	

   

   方法二：

   ​     修改 package.json 中的`scripts`字段

   > ​     scripts:{
   >
   > ​       'test-less':'lessc style.less>style.css'
   >
   > ​     }

   ​     然后在命令行执行` npm run test-less`

   ```
   注意： 只有全局安装的node包才能直接使用包内命令！！！！（注册到了系统的环境变量当中）
         本地安装的node包（安装在了node_modules文件夹下面）使用有两种方式：
         1. node_modules/.bin/ 全局命令
         2. 修改package.json中scripts字段，通过npm run ***的方式
   ```

​      如果你想输出一个压缩后的 CSS，只要加到 `-x` 选项即可。

```
   "scripts": {
        "less": "lessc style.less>style.css -x"
    }
```



#### 开发环境中使用less

开发的时候不能每次都将写好的 less 编译成 css 进行测试

需要实时看到写好的样式

1. 引入 `rel` 属性的值是 `stylesheet/less` 的 `.less` 样式表 :

```
<link rel="stylesheet/less" type="text/css" href="styles.less" />
注意： rel 的属性值 ："stylesheet/less"
```

2. 引入less.js（less.js能够将less文件转换成 CSS 文件）

```
<script src="less.js" type="text/javascript"></script>
```

less.js 的 CDN （内容分发网络）地址如下：

<script src="//cdnjs.cloudflare.com/ajax/libs/less.js/2.2.0/less.min.js"></script>

使用CDN的好处？

> 	1. 减轻了服务器负载
>
>    2.提高了资源文件的加载速度，提高了用户体验

3. 特别注意

- 确保 `.less` 样式表在 `less.js` 脚本前面

- 当你引入多个 `.less` 样式表时，它们都是独立编译的。所以，在每个文件中定义的变量、混合、命名空间都不会被其它的文件共享。

- 需要在本地服务器环境下运行（在localhost：下运行，而不是直接通过files://方式打开）

  创建本地服务器有很多种方式，以下以 browsersync为例讲解

  npm install -save-dev browser-sync （将browser-sync作为开发依赖安装）

  node_modules/.bin/browser-sync start --server --files  "**/\*.css, **/\*.html"

  解释：  `--files  "**/\*.css, **/\*.html"   `

  ​             `*.css`   扩展名是.css的所有文件

  ​            ` *.html ` 扩展名是.html的所有文件

  ​            `/ `根目录下

  ​               `--files  "**/\*.css, **/\*.html"   `  只要css文件,html文件改变，就会自动刷新浏览器

  

​      本地服务器？

​      服务器：服务器本质上就是一台计算机（常用的服务器软件appache\nginx）

​                     服务器能够对客户端的请求做出响应

​     本地服务器：将自己的电脑作为一台服务器使用

​                            本地服务器的域名为 localhost 

​     如何开启本地服务器？

​            有很多开启本地服务器的软件（包）

​            我们这里以 browsersync 为例开启一个本地服务器

           1. npm init
    
           2. npm install --save-dev browser-sync
    
           3. node_modules/.bin/browser-sync  start  --server
    
               执行开启服务器的命令后，会自动在浏览器打开项目根目录下的index.html 
               
               访问本地服务器根目录下的index.html页面？
               
               方式一：localhost:端口号(默认)
               方式二：localhost:端口号/index.html
               
               访问本地服务器根目录下的index-02.html页面？
               
               localhost:端口号/index-02.html
               
               访问本地服务器根目录下的html文件夹下的index-02.html页面？
               
               localhost:端口号/html/index-02.html


​          通过本地直接打开index.html

![1529027901866](C:\Users\王争\AppData\Local\Temp\1529027901866.png)



​             通过本地服务器打开index.html (index.html代表网站的首页，首页默认不显示在路径当中)

![1529027858319](C:\Users\王争\AppData\Local\Temp\1529027858319.png)



如果在本地直接代开index.html文件会在浏览器控制台打印出如下错误：

`origin requests are only supported for protocol schemes: http, data, chrome, chrome-extension, https.`

此错误的含义是： 必须通过‘http, data, chrome, chrome-extension, https.`’协议去打开网页，也就是此网页需要在服务器环境下运行！！！

 如果要是生产环境用less.js可以么？

可以！ 但是不好，因为没必要（生产环境需要简洁的代码，没必要下载一个less.js文件，然后再让less.js去解析一系列的less文件，这样降低了用户体验 ）





### 在 node 中使用

> cmd 窗口如何创建文件？
>
> cd  空格  >  文件名
>
> cmd窗口如何创建文件夹？
>
> mkdir 空格 文件夹名称
>
> 删除某个文件、文件夹？
>
> del 文件名/文件夹名称
>
> 在node当中运行demo.js文件？
>
> node demo.js

你可以在 Node 中调用编译器，例如：

1. 创建less-demo.js

```
/*less-demo.js*/
var less = require('less');

less.render('.class { width: (1 + 1) }', function (e, output) {
  console.log(output.css);
});
```

2. 直接执行  node  less-demo.js 会报错，错误信息如下：

   ```
   module.js:549
       throw err;
       ^
   
   Error: Cannot find module 'less'
       at Function.Module._resolveFilename (module.js:547:15)
       at Function.Module._load (module.js:474:25)
       at Module.require (module.js:596:17)
       at require (internal/module.js:11:18)
       at Object.<anonymous> (D:\H5\CSS\Less-Demo\demo-03\less-demo.js:2:12)
       at Module._compile (module.js:652:30)
       at Object.Module._extensions..js (module.js:663:10)
       at Module.load (module.js:565:32)
       at tryModuleLoad (module.js:505:12)
       at Function.Module._load (module.js:497:3)
   ```

   通过错误信息，我们发现，项目缺少 less包

   

3. 安装less 包

   ```
   npm init
   npm install --save-dev less
   ```

   

4. 运行less-demo.js

   输入  node less-demo.js 

   将会在控制台打印出如下内容：

```
.class {
  width: 2;
}
```

5.  node 包常见用法？

   第一种用法： 直接输入包提供的命令

   > node_modules/.bin/lessc style.less>style.css

   第二种用法：每个node包都为我们提供了一个对象，既然是对象，那么肯定会有很多方法

   我们可以通过require() 方法，将node包引入相应的js文件，在文件里面也可以运用node包的方法

   例如：

   ```
   /*less-demo.js*/
   var less = require('less');
   
   less.render('.class { width: (1 + 1) }', function (e, output) {
     console.log(output.css);
   });
   ```

   运行less-demo.js

   >  node less-demo.js



## 变量

变量允许我们单独定义一系列通用的样式，然后在需要的时候去调用。所以在做全局样式调整的时候我们可能只需要修改几行代码就可以了。

```
 /* LESS */

@color: #4D926F;

#header {
  color: @color;
}

/* 生成的 CSS */

#header {
  color: #4D926F;
}
```

## 混合

混合可以将一个定义好的 classA 轻松的引入到另一个 classB 中，

从而简单实现 classB 继承 classA 中的所有属性。

我们还可以带参数地调用，就像使用函数一样。

### 不带参数的混合

```
// LESS

.bordered {
  border-top: dotted 1px black;
  border-bottom: solid 2px black;
}
.post a {
  color: red;
  .bordered;
}
/* 生成的 CSS */
.post a {
  color: red;
  border-top: dotted 1px black;
  border-bottom: solid 2px black;
}
```

### 带参数的混合

在 LESS 中，你还可以像函数一样定义一个带参数的属性集合:

```
.border-radius (@radius) {//类似函数声明
  border-radius: @radius;
  -moz-border-radius: @radius;
  -webkit-border-radius: @radius;
}
```

然后在其他 class 中像这样调用它:

```
.button {
  .border-radius(6px);  //类似函数调用
}
```

我们还可以像这样给参数设置默认值:

```
.border-radius (@radius: 5px) {
  border-radius: @radius;
  -moz-border-radius: @radius;
  -webkit-border-radius: @radius;
}
```

所以现在如果我们像这样调用它的话:

```
#header {
  .border-radius;  
}
```

radius 的值就会是 5px.

## 媒体查询

媒体查询同样可以嵌套在选择器中。选择器将被复制到媒体查询体内：

```
.screencolor{
    @media (min-width:768px) {
      color: red;
    }  
    @media (min-width:992px) {
      color: yellow;
    }
}
```

输出:

```
@media screen and (min-width: 768px) {
  .screencolor {
    color: red;
  }
}
@media screen and (min-width: 992px) {
  .screencolor {
    color: yellow;
  }
}
```

## 嵌套规则

我们可以在一个选择器中嵌套另一个选择器来实现继承，

这样很大程度减少了代码量，

并且代码看起来更加的清晰。

让我们先看下下面这段 CSS:

```
#header { color: black; }
#header .navigation {
  font-size: 12px;
}
#header .logo {
  width: 300px;
}
#header .logo:hover {
  text-decoration: none;
}
```

在 LESS 中, 我们就可以这样写:

```
#header {
  color: black;

  .navigation {
    font-size: 12px;
  }
  .logo {
    width: 300px;
    &:hover { text-decoration: none }
  }
}
```

注意  `&` 伪类如  `:hover`  和  `:focus`.

## 函数 & 运算

### 运算

任何数字、颜色或者变量都可以参与运算. 来看一组例子:

```
@base: 5%;
@filler: @base * 2;
@other: @base + @filler;
@color: #888 / 4;
@background-color: @color + #111;
```

LESS 的运算已经超出了我们的期望，它能够分辨出颜色和单位。如果像下面这样单位运算的话:

```
@var: 1px + 5;
```

LESS 会输出 `6px`.

括号也同样允许使用:

```
width: (@var + 5) * 2;
```

并且可以在复合属性中进行运算:

```
border: (@width * 2) solid black;
```

### 函数

#### Color 函数

LESS 提供了一系列的`颜色运算函数`. 颜色会先被转化成 _HSL_ 色彩空间, 然后在通道级别操作:

```
lighten(@color, 10%);     // return a color which is 10% *lighter* than @color
darken(@color, 10%);      // return a color which is 10% *darker* than @color

saturate(@color, 10%);    // return a color 10% *more* saturated than @color
desaturate(@color, 10%);  // return a color 10% *less* saturated than @color

fadein(@color, 10%);      // return a color 10% *less* transparent than @color
fadeout(@color, 10%);     // return a color 10% *more* transparent than @color
fade(@color, 50%);        // return @color with 50% transparency

spin(@color, 10);         // return a color with a 10 degree larger in hue than @color
spin(@color, -10);        // return a color with a 10 degree smaller hue than @color

mix(@color1, @color2);    // return a mix of @color1 and @color2
```

使用起来相当简单:

```
@base: #f04615;
.class {
  color: saturate(@base, 5%);
  background-color: lighten(spin(@base, 8), 25%);
}
```

你还可以提取颜色信息:

```
hue(@color);        // returns the `hue` channel of @color
saturation(@color); // returns the `saturation` channel of @color
lightness(@color);  // returns the 'lightness' channel of @color
```

如果你想在一种颜色的通道上创建另一种颜色，这些函数就显得那么的好用，例如:

```
@new: hsl(hue(@old), 45%, 90%);
```

`@new` 将会保持 `@old`的 _色调_, 但是具有不同的饱和度和亮度.

#### Math 函数

LESS 提供了一组方便的数学函数，你可以使用它们处理一些数字类型的值:

```
round(1.67); // returns `2`
ceil(2.4);   // returns `3`
floor(2.6);  // returns `2`
```

如果你想将一个值转化为百分比，你可以使用`percentage` 函数:

```
percentage(0.5); // returns `50%`
```

## 命名空间

有时候，你可能为了更好组织 CSS 或者单纯是为了更好的封装，

将一些变量或者混合模块打包起来,

你可以像下面这样在`#bundle`中定义一些属性集后重复使用:

```
#bundle {
  .button () {
    display: block;
    border: 1px solid black;
    background-color: grey;
    &:hover {
        background-color: white
    }
  }
  .tab {  }
  .citation { }
}
```

你只需要在 `#header a`中像这样引入 `.button`:

```
#header a {
  color: orange;
  #bundle > .button;
}
```

## 作用域

LESS 中的作用域跟其他编程语言非常类似，

首先会从本地查找变量或者混合模块，

如果没找到的话会去父级作用域中查找，直到找到为止.

```
@var: red;

#page {
  @var: white;
  #header {
    color: @var; //white
  }
}

#footer {
  color: @var; //red
}
```

## Import

样式模块化！！！

引入 `.less` 文件, `.less` 后缀可带可不带:

```
@import "lib.less";
@import "lib";
```

如果你想导入一个 CSS 文件而且不想 LESS 对它进行处理，只需要使用`.css`后缀就可以:

```
@import "lib.css";
```

这样 LESS 就会跳过它不去处理它

## 字符串拼接

变量可以用类似 ruby 和 php 的方式嵌入到字符串中，像`@{name}`这样的结构:

```
@base-url: "http://assets.fnord.com";
background-image: url("@{base-url}/images/bg.png");
```

## 许可证 FAQs

Less.js 基于 Apache 2 许可证发布。版权所有 2009-2015，Alexis Sellier 和 Less 核心小组（见上面）。总结如下：

#### 赋予你的权力：

-   任意下载并使用 Less.js 的全部或部分代码，可以用于个人、公司内部或商业目的
-   将 Less.js 包含到你的产品中

#### 严禁：

-   在没有声明版权归属的情况下使用 Less.js 中的任何代码片段

#### 你的义务：

-   如果你的产品中包含 Less.js，必须包含一份 Less.js 的版权协议
-   在你包含了 Less.js 的产品中明确声明 Less.js 的版权归 Less 核心小组

#### 不需要：

-   在你的产品中包含 Less.js 自身或你所修改的源码
-   提交你对 Less.js 所做的修改到 Less.js 项目（我们还是鼓励提交对 Less.js 的改进）

完整的 Less.js 版权信息位于 [项目仓库内](https://github.com/less/less.js/blob/master/LICENSE)，请参考。

## 什么时候用 less?

不要盲目的在项目中使用 LESS

**它更适用于皮肤、模板等整体框架固定死的网站制作，比如论坛、空间**。

**项目比较大的情况**

**页面有很多可以复用的组件，比如输入框，按钮等等 **

项目足够大，起码几十张页面，有公共的 UI 组件，

组件或者页面上有相似的拼装属性的方法(可以写成 mixin)，

组件或者样式拼装上存在继承关系，

或者有 theme 的需求

在使用 LESS 时请先考虑下这个工具是否适用，

别盲目的使用，

不但效率没提高，

还增加了不必要的工作量。

## bootstrap 中如何用less

1. 高度模块化

```
/*bootstrap.less*/

// Core variables and mixins
@import "variables.less";
@import "mixins.less";

// Reset and dependencies
@import "normalize.less";
@import "print.less";
@import "glyphicons.less";

// Core CSS
@import "scaffolding.less";
@import "type.less";
@import "code.less";
@import "grid.less";
@import "tables.less";
@import "forms.less";
@import "buttons.less";

// Components
@import "component-animations.less";
@import "dropdowns.less";
@import "button-groups.less";
@import "input-groups.less";
@import "navs.less";
@import "navbar.less";
@import "breadcrumbs.less";
@import "pagination.less";
@import "pager.less";
@import "labels.less";
@import "badges.less";
@import "jumbotron.less";
@import "thumbnails.less";
@import "alerts.less";
@import "progress-bars.less";
@import "media.less";
@import "list-group.less";
@import "panels.less";
@import "responsive-embed.less";
@import "wells.less";
@import "close.less";

// Components w/ JavaScript
@import "modals.less";
@import "tooltip.less";
@import "popovers.less";
@import "carousel.less";

// Utility classes
@import "utilities.less";
@import "responsive-utilities.less";

```

2. 将所有的变量都放在了`variable.less`

```
//## Gray and brand colors for use across Bootstrap.

@gray-base:              #000;
@gray-darker:            lighten(@gray-base, 13.5%); // #222
@gray-dark:              lighten(@gray-base, 20%);   // #333
@gray:                   lighten(@gray-base, 33.5%); // #555
@gray-light:             lighten(@gray-base, 46.7%); // #777
@gray-lighter:           lighten(@gray-base, 93.5%); // #eee

@brand-primary:         darken(#428bca, 6.5%); // #337ab7
@brand-success:         #5cb85c;
@brand-info:            #5bc0de;
@brand-warning:         #f0ad4e;
@brand-danger:          #d9534f;
```

3. 将所有的混合放入了 mixins 文件夹

![1529395941979](C:\Users\王争\AppData\Local\Temp\1529395941979.png)

`混合`本质上是一个类，类本质上是样式，

less的`混合`当中类的特点：可以传参，参数之间用分号链接

说白了，bootstrap当中，基础的样式都放在了 mixins 文件夹中

![1529396182351](C:\Users\王争\AppData\Local\Temp\1529396182351.png)



4. 如何将所有的bootstrap中的less文件编译成css文件

1. npm init

2. npm install --save-dev less

3. node_modules/.bin/lessc  boostrap.less>css/bootstrap.css 

   

## 其他CSS预处理语言

sass、stylus 这些都和less很类似