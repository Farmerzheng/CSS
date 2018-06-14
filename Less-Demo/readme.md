http://www.css88.com/doc/less/features/#features-overview-feature

http://www.bootcss.com/p/lesscss/

## 概览

Less 是一个Css 预编译器,

意思指的是它可以扩展Css语言,

添加功能如允许变量(variables),混合(mixins),函数(functions) 和许多其他的技术，

让你的Css更具维护性，主题性，扩展性。

Less 可运行在 Node 环境,浏览器环境和Rhino环境.

同时也有3种可选工具供你编译文件和监视任何改变。



## 使用



### 在node中使用

你可以在Node中调用编译器，例如：

```
var less = require('less');

less.render('.class { width: (1 + 1) }', function (e, output) {
  console.log(output.css);
});
```

将会输出

```
.class {
  width: 2;
}
```

### 客户端使用

浏览器端使用是在使用LESS开发时最直观的一种方式。如果是在生产环境中，尤其是对性能要求比较高的场合， *建议使用node或者其它第三方工具先编译成CSS再上线使用* 。

#### 编译成CSS(项目上线时需要编译成css)

一旦安装完成，就可以在命令行中调用，例如:

```
$ lessc styles.less
```

这样的话编译后的CSS将会输出到 'stdout' 中，你可以选择将这个输出重定向到文件中:

```
$ lessc styles.less > styles.css
```

如果你想输出一个压缩后的CSS，只要加到 `-x` 选项即可。

#### 开发环境（引入less.js）

开发的时候不能每次都将 写好的 less 编译成css进行测试

需要实时看到写好的样式

首先，引入 `rel` 属性的值是 `stylesheet/less` 的 `.less` 样式表 :

```
<link rel="stylesheet/less" type="text/css" href="styles.less" />
```

接下来，[下载 less.js](https://github.com/less/less.js/archive/master.zip) 并将其包涵在您的页面 `<head>` 元素的 `<script></script>` 标记中：

```
<script src="less.js" type="text/javascript"></script>
```

less CDN

<script src="//cdnjs.cloudflare.com/ajax/libs/less.js/2.2.0/less.min.js"></script> 

##### Tips 特别注意

- 确保包涵 `.less` 样式表在 `less.js` 脚本前面

- 当你引入多个 `.less` 样式表时，它们都是独立编译的。所以，在每个文件中定义的变量、混合、命名空间都不会被其它的文件共享。

- 需要在本地服务器环境下运行

    创建本地服务器环境 (browsersync)？

    npm install -save-dev browser-sync

    browser-sync start --server --files  "**/*.css,  **/*.html"



## 变量

变量允许我们单独定义一系列通用的样式，然后在需要的时候去调用。所以在做全局样式调整的时候我们可能只需要修改几行代码就可以了。

```
 /* LESS */

@color: #4D926F;

#header {
  color: @color;
}
h2 {
  color: @color;
}

/* 生成的 CSS */

#header {
  color: #4D926F;
}
h2 {
  color: #4D926F;
}
```

## 混合

混合可以将一个定义好的classA轻松的引入到另一个classB中，

从而简单实现classB继承classA中的所有属性。

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
.border-radius (@radius) {
  border-radius: @radius;
  -moz-border-radius: @radius;
  -webkit-border-radius: @radius;
}
```

然后在其他class中像这样调用它:

```

.button {
  .border-radius(6px);  
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

radius的值就会是5px.

## 媒体查询

媒体查询同样可以嵌套在选择器中。选择器将被复制到媒体查询体内：

```
.screencolor{
    @media (min-width:768px) {
      color: red;
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

注意 `&` 符号的使用—如果你想写串联选择器，而不是写后代选择器，

就可以用到`&`了. 这点对伪类尤其有用如 `:hover` 和 `:focus`. 



## 函数 & 运算

### 运算

任何数字、颜色或者变量都可以参与运算. 来看一组例子:

```
@base: 5%;
@filler: @base * 2;
@other: @base + @filler;

color: #888 / 4;
background-color: @base-color + #111;
height: 100% / 2 + @filler;
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

LESS 提供了一系列的颜色运算函数. 颜色会先被转化成 *HSL* 色彩空间, 然后在通道级别操作:

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

`@new` 将会保持 `@old`的 *色调*, 但是具有不同的饱和度和亮度.

#### Math 函数

LESS提供了一组方便的数学函数，你可以使用它们处理一些数字类型的值:

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

有时候，你可能为了更好组织CSS或者单纯是为了更好的封装，

将一些变量或者混合模块打包起来, 

你可以像下面这样在`#bundle`中定义一些属性集后重复使用:

```
#bundle {
  .button () {
    display: block;
    border: 1px solid black;
    background-color: grey;
    &:hover { background-color: white }
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
    color: @var; // white
  }
}

#footer {
  color: @var; // red  
}
```

## Import

你可以在main文件中通过下面的形势引入 `.less` 文件, `.less` 后缀可带可不带:

```
@import "lib.less";
@import "lib";
```

如果你想导入一个CSS文件而且不想LESS对它进行处理，只需要使用`.css`后缀就可以:

```
@import "lib.css";
```

这样LESS就会跳过它不去处理它

## 字符串插值

变量可以用类似ruby和php的方式嵌入到字符串中，像`@{name}`这样的结构:

```
@base-url: "http://assets.fnord.com";
background-image: url("@{base-url}/images/bg.png");
```

## 许可证 FAQs

Less.js 基于 Apache 2 许可证发布。版权所有 2009-2015，Alexis Sellier 和 Less 核心小组（见上面）。总结如下：

#### 赋予你的权力：

- 任意下载并使用 Less.js 的全部或部分代码，可以用于个人、公司内部或商业目的
- 将 Less.js 包含到你的产品中

#### 严禁：

- 在没有声明版权归属的情况下使用 Less.js 中的任何代码片段

#### 你的义务：

- 如果你的产品中包含 Less.js，必须包含一份 Less.js 的版权协议
- 在你包含了 Less.js 的产品中明确声明 Less.js 的版权归 Less 核心小组

#### 不需要：

- 在你的产品中包含 Less。js 自身或你所修改的源码
- 提交你对 Less.js 所做的修改到 Less.js 项目（我们还是鼓励提交对 Less.js 的改进）

完整的 Less.js 版权信息位于 [项目仓库内](https://github.com/less/less.js/blob/master/LICENSE)，请参考。



## 什么时候用less?

不要盲目的在项目中使用LESS

**它更适用于皮肤、模板等整体框架固定死的网站制作，比如论坛、空间**。

**项目比较大的情况**

**页面有很多可以复用的组件，比如输入框，按钮等等 **

项目足够大，起码几十张页面，有公共的UI组件，

组件或者页面上有相似的拼装属性的方法(可以写成mixin)，

组件或者样式拼装上存在继承关系，

或者有theme的需求

在使用LESS 时请先考虑下这个工具是否适用，

别盲目的使用，

不但效率没提高，

还增加了不必要的工作量。 

