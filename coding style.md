# Web Front-End Engineer Coding Style Conventions and Standards

`Author: ` GreenMelon Chinn-San-Ken @吾南蛮野人 陈灿坚
`Github: `
`Date: ` 2015-10-03

[TOC]
## 其他
## 开发环境
- 系统平台：windows ，os x ，liunx
- 编辑器：sublime ，Hbuilder
- 编译器：koala
- 软件环境：*
### 文件编码
统一使用UTF-8
### 目录结构 
不同资源文件夹需要分开以便统一管理
```css
── project
 ├─ css
 ├─ font
 ├─ images
 ├─ js
 ├─ less/sass
 ├─ lib 库
 └─ template 模板
```
### 框架
- MVC 框架：Angular.js
- CSS 框架：LESS/SASS
- DOM 类框架：jQuery, zepto

## 前言
目的：使开发流程更加规范化
## 通用规范 General Conventions
### 文件名规范
- 文件名用英文单词
- 多个单词用 `Camel` 命名法
- 避免使用以下词汇，因为部分浏览器会将含有这些词汇的文件作为广告拦截
```
ad、ads、adv、banner、sponsor、guanggao、guang、gg
```
### 文件编码 charset
统一使用不带 BOM 的 `UTF-8` 编码。BOM 在使用程序或工具处理文件时可能造成不必要的干扰。
- 在 HTML 中的第一个 meta 标签指定编码 `<meta charset="UTF-8">`
- 样式表默认编码为 UTF-8，因此无需使用 `@charset`
- CSS 与 JavaScript 中的非注释类中文字符须转换成 unicode 编码使用，以避免编码错误时乱码显示
### 分号断句
CSS 样式属性或者 JavaScript 代码后加 `分号;` ，方便压缩工具“断句”
### 结构-样式-行为相分离
尽量让这三者之间的交互保持最低限度
尽量确保文档和模板只包含 HTML 结构，样式都放到 CSS 样式表里，行为都放到 JS 脚本里。

#### Class 与 ID

- class 与 id 使用小写字母的英文单词，多个单词组成时，采用 `破折号dash'-' `分隔
- `不要驼峰命名法和下划线`
- class 必须代表相应模块或部件的内容或功能，尽量语义化
- 使用有意义的名称。使用有组织的或目的明确的名称，不要使用表现形式（presentational）的名称
- 避免冲突并描述清楚的前提下尽可能短。
- 避免过度任意的简写。 .btn 代表 button ，但是 .s 不能表达任何意思。
- 基于最近的父 class 或基本（base） class 作为新 class 的前缀
- 元素 `id` 必须保证页面唯一，特别注意模板的 id 重复问题。同一个页面中，不同的元素包含相同的 id，不符合 id 的属性含义。也会出现问题
```css
/* bad */
.t {}
.left {}
.header {}
<div id="navigation"></div>
<p class="com"></p>
/* good */
.tweet {}
.sidebar {}
.tweet-header {}
<div id="nav"></div>
<p class="comment"></p>
```
JavaScript 钩子

切勿将标记 CSS 样式的 class 用作 JavaScript 钩子。把 JS 行为与样式混在一起将无法对其分别处理。

如果你要把 JS 和某些标记绑定起来的话，写一个 JS 专用的 class。简单地说就是划定一个前缀 .js- 的命名空间，例如 .js-toggle，.js-drag-and-drop。这意味着我们可以通过 class 同时绑定 JS 和 CSS 而不会因为冲突而引发麻烦。
```css
<th class="is-sortable  js-is-sortable">
</th>
```
上面的这个标记有两个 class，你可以用其中一个来给这个可排序的表格栏添加样式，用另一个添加排序功能。
- 使用 .js-* class 来标识行为（与样式相对），并且不要将这些 class 包含到 CSS 文件中。
- 使用唯一的 id 作为 Javascript hook, 同时 `避免创建无样式信息的 class`
```html
<!-- Recommended -->
<div id="js-hook" class="sidebar content-wrapper"></div>

<!-- Not Recommended -->
<div class="js-hook sidebar content-wrapper"></div>
```
## id name
- 当  JavaScript 获取单个元素时，通常使用 document.getElementById() 来获取 DOM 元素，该方法兼容所有浏览器
- 但 IE 会混淆元素的 id 和 name 属性，所以要区分 id 和 name 的命名
```html
<input name="melon" type="text">
<div id="melon"></div>
```
``` JavaScript 
document.getElementById('melon');  // IE6下为input
```
### 缩进 indent
统一 `2个空格` 缩进，禁止使用 Tab 键，禁止使用 Tab 键与空格混搭。

### 一律使用小写字母 lowercase
```html
<!-- good -->
<img src="images/img.jpg" alt="images">

<!-- bad -->
<A HREF="JAVASCRIPT:VOID(0);"></a>
```
```CSS
/* Recommended */	
color: #c3c3c3;

/* Not Recommended */	
color: #C3C3C3;
```
### 省略外链资源 URL 协议部分
 移动环境或只针对现代浏览器设计的 Web 应用，如果引用外部资源的 `URL` 协议部分与页面相同，建议省略协议前缀。
省略外链资源（图片及其它媒体资源）URL 中的 `http/https` 协议，使 URL 成为相对地址，避免 [Mixed Content](https://developer.mozilla.org/en-US/docs/Security/MixedContent) 问题，减小文件字节数，防止小文件重复下载。
```html
<!-- Recommended -->
<script src="//www.google.com/js/gweb/analytics/autotrack.js"></script>

<!-- Not Recommended -->
<script src="http://www.google.com/js/gweb/analytics/autotrack.js"></script>
```
```css
/* Recommended */
background-image: url(//www.google.com/images/example);

/* Not Recommended */
background: url(http://www.google.com/images/example);
```
其它协议（FTP 等）的 URL 不省略
### 统一注释
确保你的代码能够自描述，注释良好并且易于他人理解。通过配置编辑器，可以使用快捷键来输出一致认可的注释模式。





#### JavaScript 注释
- 单行注释
必须独占一行。`//` 后跟一个空格，缩进与下一行被注释说明的代码一致。
- 多行注释
避免使用 /*...*/ 这样的多行注释。有多行注释内容时，使用多个单行注释。
- 函数/方法注释
```javascript
/**
 * [sliceArray description] 函数说明
 * @param  {[type]} array [description] 参数类型和说明
 * @param  {[type]} star  [description] 参数类型和说明
 * @param  {[type]} end   [description] 参数类型和说明
 * @return {[type]}       [description] 返回值类型和说明
 */
function sliceArray(array, star, end) {
  var initialArray = array,
           starPos = star,
            endPos = end;
  var sliceArray = initialArray.slice(starPos, endPos);
  return sliceArray;
}
```
#### 文件注释
文件注释用于告诉不熟悉这段代码的读者这个文件中包含哪些东西。 应该提供文件的大体内容, 它的作者, 依赖关系和兼容性信息。
```javascript
/**
 *      @function:
 *  @fileoverview: 
 *  @dependencies:
 * @compatibility:
 *        @author:
 */
```
### 代码验证
- 使用 [W3C HTML Validator](http://validator.w3.org/) 验证 HTML 代码有效性
- 使用 [W3C CSS Validator](http://jigsaw.w3.org/css-validator/validator.html.zh-cn) 验证 CSS 代码有效性

目的在于让开发者在经过多次的这种验证过程后，能够深刻理解到怎样的语法或写法是非标准和不推荐的



## 2 HTML
### 代码格式
#### 缩进 indent
- 统一 `2个空格` 缩进
- 禁止使用制表符 Tab
- 禁止使用制表符 Tab 与空格混搭
- 嵌套元素应当缩进一次
#### 换行 line break
- 每个块元素、列表元素或表格元素都独占一行
- 尽量使父元素独占一行
#### 行长度
- 每行不得超过 `120个字符`。过长的代码不容易阅读与维护

### HTML注释
#### 模块注释
```html
<!-- 侧边栏模块 -->
<div class="sidebar">
  ...
</div>
```
#### 区块注释
```html
<!--
@description: slideToggle Menu
     @author: GreenMelon(GreenMelon@126.com)
       @date: 2015-10-03
-->
```
### HEAD
#### 文档类型声明 DTD
为每个 HTML 页面的第一行添加标准模式 `standard mode` 的声明， 这样能够确保在每个浏览器中拥有一致的表现。
```html
<!DOCTYPE html>
```
不要用 XHTML 文档格式，即 `application/xhtml+xml` 。原因：
- 有 2 个浏览器完全不支持
- 比 HTML 占用更多的存储空间
#### 语言属性 lang
> 根据 [HTML5规范](http://www.w3.org/html/wg/drafts/html/master/semantics.html#the-html-element)：
> 强烈建议为 html 根元素指定 lang 属性，从而为文档设置正确的语言。这将有助于语音合成工具确定其所应该采用的发音，有助于翻译工具确定其翻译时所应遵守的规则等等。

因此，虽然语言和字符编码的定义是可选的，但还是推荐在文档级别声明它们，即使它们已经在 HTTP 请求的头部指定。

为什么使用 `lang="zh-cmn-Hans"` 而不是我们通常写的 `lang="zh-CN"` 呢? 请参考知乎 [网页的语言声明](http://www.zhihu.com/question/20797118) 的讨论
```html
<!-- 中文 -->
<html lang="zh-Hans">

<!-- 简体中文 -->
<html lang="zh-cmn-Hans">

<!-- 繁体中文 -->
<html lang="zh-cmn-Hant">

<!-- English -->
<html lang="en">
```
更多的语言属性值，请参考 [语言代码表](http://www.sitepoint.com/web-foundations/iso-2-letter-language-codes/)
#### 字符编码 charset
通过明确的字符编码声明，能够确保浏览器快速简捷地判断页面内容的渲染方式。这样可以避免在 HTML 中使用字符实体标记（character entity），从而全部与文档编码保持一致（统一采用 UTF-8 编码）。
指定字符编码的 meta 必须是 head 的第一个直接子元素。
```html
<meta charset="utf-8">
```
参考 [HTML5 Charset](http://www.qianduan.net/html5-charset-can-it.html) 
#### 标题 title
页面必须包含 title 标签声明标题。其必须紧跟在设置字符编码的 meta 标签之后。因为 title 中如果包含 ASCII 之外的字符，浏览器需要知道字符编码类型才能进行解码，否则可能导致乱码。
```html
<head>
  <meta charset="utf-8">
  <title>Style Guide</title>
</head>
```
#### IE 兼容模式
IE 支持通过特定 meta 标签来确定绘制当前页面所应该采用的 IE 版本。除非有特殊需求，否则设置为 `edge mode`，从而通知 IE 采用其所支持的最新的模式。
```html
<!-- 优先使用最新版本的 IE 和 Chrome 内核 -->
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
```
有兴趣的话可以阅读 [X-UA-Compatible](http://stackoverflow.com/questions/6771258/whats-the-difference-if-meta-http-equiv-x-ua-compatible-content-ie-edge-e) 这篇文档
#### 搜索引擎 SE
```html
<head>
  <!-- SE -->
  <meta name="description" content="your description">
  <meta name="keywords" content="your keywords">
  <meta name="author" content="author,email">
  <!-- 实际上并没有什么卵用 -->
</head>
```
#### viewport
若页面欲对移动设备友好，需指定页面的 viewport。viewport 可以设置可视区域的宽度和初始缩放大小，避免在移动设备上页面显示不正常。

比如，在页面宽度小于 980px 时，若需 iOS 设备友好，应当设置 viewport 的 width 值来适应页面宽度。同时因为不同移动设备分辨率不同，在设置时应当使用 device-width 和 device-height 变量。

另外，为了使 viewport 正常工作，在页面内容的样式布局设计上也要做相应调整，如避免绝对定位等。

- viewport: 一般指的是浏览器窗口内容区的大小，不包含工具条、选项卡等内容
- width: 浏览器宽度，输出设备中的页面可见区域宽度
- `device-width`: 设备分辨率宽度，输出设备的屏幕可见宽度
- `initial-scale`: 初始缩放比例
- maximum-scale: 最大缩放比例
- user-scalable: 用户调节缩放比例
```html
<!-- 优化移动端设备，设置可见区域的宽度和初始缩放比例 -->
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0">
```
参考 [Safari Web Content Guide](https://developer.apple.com/library/mac/documentation/AppleApplications/Reference/SafariWebContent/UsingtheViewport/UsingtheViewport.html#//apple_ref/doc/uid/TP40006509-SW26)

#### 指定微链接资源的 MIME 类型
```html
<!-- BAD -->
<link href="/pdf" rel="alternate">
<link href="/feed" rel="alternate">
<link href="/css/screen.css" rel="stylesheet">

<!-- GOOD -->
<link href="/pdf" rel="alternate" type="application/pdf">
<link href="/feed" rel="alternate" type="application/rss+xml">
<link href="/css/screen.css" rel="stylesheet">
```

#### iOS 图标
- apple-touch-icon 图片自动处理成圆角和高光等效果
- apple-touch-icon-precomposed 禁止系统自动添加效果，直接显示设计原图
```html
<!-- iPhone 和 iTouch，默认 57x57 像素，必须有 -->
<link rel="apple-touch-icon-precomposed" href="/apple-touch-icon-57x57-precomposed.png">

<!-- iPad，72x72 像素，可以没有，但推荐有 -->
<link rel="apple-touch-icon-precomposed" href="/apple-touch-icon-72x72-precomposed.png" sizes="72x72">

<!-- Retina iPhone 和 Retina iTouch，114x114 像素，可以没有，但推荐有 -->
<link rel="apple-touch-icon-precomposed" href="/apple-touch-icon-114x114-precomposed.png" sizes="114x114">

<!-- Retina iPad，144x144 像素，可以没有，但推荐有 -->
<link rel="apple-touch-icon-precomposed" href="/apple-touch-icon-144x144-precomposed.png" sizes="144x144">
```
#### favicon
在未指定 favicon 时，大多数浏览器会请求 Web Server 根目录下的 favicon.ico 。为了保证 favicon 可访问，避免404，必须遵循以下两种方法之一：
- 在 Web Server 根目录放置 favicon.ico 文件
- 使用 link 指定 favicon
```html
<link rel="shortcut icon" href="path/to/favicon.ico">
```
#### 其他
```html
<head>
  <!-- 禁止浏览器从本地的缓存中调阅页面内容 -->
  <meta http-equiv="Pragma" content="no-cache">
  <!-- 网页的过期时间。一旦过期，必须到服务器上重新调阅 -->
  <meta http-equiv="expires" content="expire-date">	
  <!-- 禁止页面被别的框架调用 -->
  <meta http-equiv="Window-target" content="_top">
  <!-- 网页缓存 -->
  <meta http-equiv="Cache-Control" content="no-cache, must-revalidate">
  <!-- 跳转页面。包括停留时间和目标地址 -->
  <meta http-equiv="Refresh" content="yourSeconds;URL=yourURL">
  <!-- 网页搜索机器人向导。 -->
  <meta name="robots" content="all/none/index/noindex/follow/nofollow">
</head>
```
#### HEAD模板
忘记旧的 XHTML 习惯，保持代码简洁。
```html
<!DOCTYPE html>
<!-- 简体中文 -->
<html lang="zh-cmn-Hans">
<head>
  <!-- 字符编码 -->
  <meta charset="utf-8">
  <!-- 标题 -->
  <title>Style Guide</title>
  <!-- 使用最新版本的 IE 和 Chrome 内核 -->
  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
  <!-- 搜索引擎 -->
  <meta name="description" content="不超过150个字符">
  <meta name="keywords" content="your keywords">
  <meta name="author" content="author,email">
  <!-- 为移动设备添加 viewport -->
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0">
  <!-- 禁止浏览器从本地的缓存中调阅页面内容 -->
  <meta http-equiv="Pragma" content="no-cache">
  <!-- 网页的过期时间。一旦过期，必须到服务器上重新调阅 -->
  <meta http-equiv="expires" content="expire-date"> 
  <!-- 禁止页面被别的框架调用 -->
  <meta http-equiv="Window-target" content="_top">
  <!-- 网页缓存 -->
  <meta http-equiv="Cache-Control" content="no-cache, must-revalidate">
  <!-- 跳转页面。包括停留时间和目标地址 -->
  <meta http-equiv="Refresh" content="yourSeconds;URL=yourURL">
  <!-- 网页搜索机器人向导。 -->
  <meta name="robots" content="all/none/index/noindex/follow/nofollow">
  <!-- 文档的替代版本 -->
  <link rel="alternate" type="application/rss+xml" href="/rss.xml" title="RSS">     
  <!-- iOS 图标 -->
  <link rel="apple-touch-icon-precomposed" href="/apple-touch-icon-57x57-precomposed.png">
  <!-- favicon -->
  <link rel="shortcut icon" href="path/to/favicon.ico"> 
</head>
</html>
```
#### 引入 CSS 和 JS
##### CSS
- 非特殊情况，在 head 之间外链 CSS 样式文件
- 引入 CSS 时必须指明 `rel="stylesheet"`
- 根据 HTML5 规范，在引入 CSS 文件时一般不需要指定 type 属性，因为 text/css 是默认值
- 如果你的样式表很大，分离出初始化时必须的样式，并在一个独立样式表中延迟加载其它部分。两次 HTTP 请求显然低于一次，但用户体验速度是最重要的因素
- 在 head 中引入页面需要的所有 CSS 文件。在页面渲染的过程中，新的 CSS 可能导致元素的样式重新计算和绘制，页面闪烁
##### JS
- 除非有特殊的需求在内容之前加载脚本，否则请不要把脚本放在内容之前阻碍页面的渲染
- 非特殊情况，在 body 底部外链 JavaScript 文件或采用异步加载
- 根据 HTML5 规范，在引入 JavaScript 文件时一般不需要指定 type 属性，因为 text/javascript 是默认值
```html
<head>
  <link rel="stylesheet" href="path/to/your.css">
</head>
<body>
  <!-- 逻辑代码 -->
  <script src="path/to/your.js"></script>
</body>
```
参考 HTML5 规范
- [link element](http://www.w3.org/TR/2011/WD-html5-20110525/semantics.html#the-link-element)
- [style element](http://www.w3.org/TR/2011/WD-html5-20110525/semantics.html#the-style-element)
- [script element](http://www.w3.org/TR/2011/WD-html5-20110525/scripting-1.html#the-script-element)
#### 引入库
引入 JavaScript 库文件，文件名格式：``库名称 + 版本号 + 是否压缩版`
```html
<head>
  <script src="path/to/jQuery-1.11.1.min.js"></script
</head>
```
#### 引入插件
引入  JavaScript 插件, 文件名格式：`库名称 + '.' + 插件名称`
```html
<head>
  <script src="path/to/jQuery.cookie.js"></script>
</head>
```

### 标签
#### 标签名小写
标签名必须使用小写字母
```html
<!-- good -->
<img src="images/img.jpg" alt="images">

<!-- bad -->
<A HREF="JAVASCRIPT:VOID(0);"></A>
```
#### 自闭合标签 self-closing
对于无需自闭合的标签，不允许自闭合。例如：br、hr、img、input
```html
<!-- bad -->
<input type="text" />
<br />
<img src="path/to/image.png" />

<!-- good -->
<input type="text">
<br>
<img src="path/to/image.png">
```
#### 可选的闭合标签
HTML5 中规定允许省略的闭合标签，不允许省略。例如：body、li
```html
<!-- bad -->
<body>
<ul>
    <li>
    <li>
    <li>
</ul>

<!-- good -->
<body>
<ul>
    <li></li>
    <li></li>
    <li></li>
</ul>
</body>
```
#### 标签嵌套
标签使用必须符合标签嵌套规则。

嵌套约束：
- 语义嵌套约束：a 不允许嵌套 div。语义嵌套约束，浏览器大多会容错处理，生成的文档树可能相互不太一样
- 严格嵌套约束：`a 不允许嵌套 a`。严格嵌套约束在所有的浏览器下都不被允许

##### 语义嵌套约束
- ul / ol > li
- dl > dt > dd
- table > thead/tbody/tfoot > tr > th/td

##### 严格嵌套约束
- inline-level 元素，仅可以包含文本或其它 inline-Level 元素
- a 里不可以嵌套交互式元素 a/button/select 等
- p 里不可以嵌套块级元素 div / dl>dt>dd / form / h1~h6 / p / ul/ol>li 等

参考 [web 标准系列之 HTML 元素嵌套](http://www.smallni.com/element-nesting/)

#### 精简标签
标签的使用应尽量简洁，减少不必要的标签
```html
<!-- bad -->
<span class="avatar">
  <img src="path/to/image.png">
</span>

<!-- good -->
<img class="avatar" src="path/to/image.png">
```
参考 [HTML5规范](http://dev.w3.org/html5/spec-author-view/syntax.html#syntax-start-tag)


#### table
在 CSS 可以实现相同需求的情况下`不得使用表格布局`

### 语义化 semantic
> 没有 CSS 的 HTML 是一个语义系统而不是 UI 系统

- 通常情况下，每个标签都是有语义的，各自有对应的功能和含义
- 语义化的 HTML 结构，有助于机器（搜索引擎）理解，同时在多人协作时，能迅速了解开发者意图
- 尽量遵循 HTML 标准和语义，但是不要以牺牲实用性为代价。任何时候都要尽量 `用最少的标签保持最小的复杂度`

更多语义化的内容，参考 [这样去写你的 HTML](http://wenku.baidu.com/view/0a8d3774f242336c1eb95ea9.html)

HTML5 为我们提供了大量的语义元素，使我们能够更加精准地描述内容，尽量在开发中使用它们
```html
<!-- Not Recommended -->
<div id="main">
  <div class="article">
    <div class="header">
      <h1>Green Melon</h1>
      <p>Borned: <span>17th June, 1992</span></p>
    </div>
  </div>
</div>

<!-- Recommended -->
<main>
  <article>
    <header>
      <h1>Green Melon</h1>
      <p>Borned: <time datetime="1992-06-17">17th June, 1992</time></p>
    </header>
  </article>
</main>
```
确保自己理解正在使用的语义元素。以错误的方式使用语义元素比不使用更加糟糕
```html
<!-- bad -->
<h1>
  <figure>
    <img src="" alt="">
  </figure>
</h1>

<!-- good -->
<h1>
  <img src="" alt="">
</h1>
```

### 属性
#### 属性名小写
属性名必须使用小写字母
```html
<!-- good -->
<a href="javascript:void(0);"></a>

<!-- bad -->
<a HREF="javascript:void(0);"></a>
```
#### 属性值双引号
统一使用双引号包裹属性值，不允许使用单引号，不允许不使用引号
```html
<!-- Recommended -->
<span id="js-hook" class="demo">Google</span>

<!-- Not recommended -->
<span id='js-hook' class='demo'>Google</span>
<span id=js-hook class=demo>Google</span>
```
#### 属性顺序
HTML 属性应该按照特定的顺序出现以保证易读性
> - class 标识高度可复用组件，放在首位
> - id 标识特定组件，页面唯一
> - name
> - data-* 自定义属性
> - for, href, src, type 
> - title, alt
> - aria-*, role
#### 简写布尔型属性
布尔型属性可以在声明时不赋值。XHTML 规范要求为其赋值，但是 HTML5 规范不需要。元素的布尔型属性如果有值，就是 true，如果没有值，就是 false。

HTML5 规范中 disabled、checked、selected 等属性不用设置值
```html
<!-- Recommended -->
<input type="text" disabled>
<input type="checkbox" value="1" checked>
<select>
  <option value="1" selected>1</option>
</select>

<!-- Not recommended -->
<input type="text" disabled="disabled">
<input type="checkbox" value="1" checked="checked">
```
参考 [boolean-attributes](https://html.spec.whatwg.org/multipage/common-microsyntaxes.html#boolean-attributes)
#### 自定义属性
自定义属性建议以 **xxx-** 为前缀，推荐使用 `data-`，避免使用其他命名方式。使用前缀有助于区分自定义属性和标准属性。
```html
<ol data-ui-type="Select"></ol>
```
### 表单 Form
#### 控件标题 label
有文本标题的控件必须使用 `label` 标签将其与其标题相关联

有两种方式：
```html
<!-- 将控件置于 label 内 -->
<label>
  <input name="confirm" type="checkbox"> 我已确认上述条款
</label>

<!-- label 的 for 属性指向控件的 id -->
<label for="user-name">用户名：</label>
<input id="user-name" name="user-name" type="text">
```
推荐使用第一种，减少不必要的 id。如果 DOM 结构不允许直接嵌套，则应使用第二种。
#### 按钮 button
使用 button 元素时`必须指明 type 属性值`。button 元素的默认 type 为 submit，如果被置于 form 元素中，点击后将导致表单提交。为显示区分其作用，方便理解，必须指明 type 属性。
```html
<button type="submit">提交</button>
<button type="button">取消</button>
```
尽量`不要使用按钮类元素的 name 属性`。由于浏览器兼容性问题，使用按钮的 name 属性会带来许多难以发现的问题。

参考 [带有 name 属性的 BUTTON](http://w3help.org/zh-cn/causes/CM2001)

#### 可访问性

负责主要功能的按钮在 DOM 中的顺序应靠前，以提高可访问性。如果在 CSS 中指定了 **float: right** 则可能导致视觉上主按钮在前，而 DOM 中主按钮靠后的情况。
```css
.btn-group button {
   float: right;
}
```
```html
<!-- good -->
<div class="btn-group">
  <button type="submit">提交</button>
  <button type="button">取消</button>
</div>

<!-- bad -->
<div class="btn-group">
  <button type="button">取消</button>
  <button type="submit">提交</button>
</div>
```
#### 原生提交
当使用 JavaScript 进行表单提交时，如果条件允许，应使原生提交功能正常工作。否则，当浏览器 JS 运行错误或关闭 JS 时，提交功能将无法工作。

如果正确指定了 form 元素的 `action 属性`和表单控件的 `name 属性`时，提交仍可继续进行。
```html
<form action="" method="post">
  <input name="username" type="text">
  <input name="password" type="password">
</form>
```
#### 输入框的 type 属性
在针对移动设备开发的页面时，根据内容类型指定输入框的 `type` 属性，能使用户获得更友好的输入体验。
```html
<input type="color">
<input type="date">
<input type="datetime-local">
<input type="email">
<input type="image">
<input type="tel">
<input type="url">
```
### 多媒体
#### 用下载属性下载一个资源
```HTML
<!-- BAD -->
<a href="/downloads/offline.zip">offline version</a>

<!-- GOOD -->
<a href="/downloads/offline.zip" download>offline version</a>
```
#### 如果需要的话就使用 rel,hreflang 等类型属性
```HTML
<!-- BAD -->
<a href="/ja/pdf">Japanese PDF version</a>

<!-- GOOD -->
<a href="/ja/pdf" hreflang="ja" rel="alternate" type="application/pdf">Japanese PDF version</a>
```
#### 图片
##### 图片格式
- 图片格式仅限于 gif、jpg、png 等
- 使用 png 时，要求图片格式为 `png-8` 格式，若 png-8 实在影响图片质量或其中有半透明效果，请为  IE6 单独定义背景，并尽量避免使用半透明的 png 图片
- 背景图片尽可能使用 sprite 技术，减小 http 请求
- 图片命名应用小写英文、数字、_组合，便于团队其他成员理解
##### 图片src
`禁止 img 的 src 取值为空`。延迟加载的图片也要增加默认的 src。src 取值为空，会导致部分浏览器重新加载一次当前页面，参考 [empty-src](https://developer.yahoo.com/performance/rules.html#emptysrc)
##### 图片title
 避免为 img 添加不必要的 title 属性。多余的 title 影响看图体验，并且增加了页面尺寸。
##### 图片width
为图片添加 width 和 height 属性，以避免页面抖动。
##### 背景图
- 有潜在下载需求的图片采用 **img** 标签实现，方便用户下载
- 无下载需求的图片采用 CSS 背景图 **background-image** 实现

#### 视音频
##### 格式
当在现代浏览器中使用 audio 以及 video 标签来播放音频、视频时，应当注意格式。

音频格式：
* MP3
* WAV
* Ogg

视频格式：
* MP4
* WebM
* Ogg
##### 优先使用HTML5
在支持 HTML5 的浏览器中优先使用 audio 和 video 标签来定义视音频元素。
```html
<audio controls>
  <source src="audio.mp3" type="audio/mpeg">
  <source src="audio.ogg" type="audio/ogg">
  <object width="100" height="50" data="audio.mp3">
    <embed width="100" height="50" src="audio.swf">
  </object>
</audio>

<video width="100" height="50" controls>
  <source src="video.mp4" type="video/mp4">
  <source src="video.ogg" type="video/ogg">
  <object width="100" height="50" data="video.mp4">
    <embed width="100" height="50" src="video.swf">
  </object>
</video>
```
##### 自动播放
只在必要的时候开启视音频的自动播放
##### object说明
在 object 标签内部提供指示浏览器不支持该标签的说明
```html
<object width="100" height="50" data="something.swf">DO NOT SUPPORT THIS TAG</object>
```
### 模板 template

#### 代码缩进
模板代码的缩进优先保证 HTML 代码的缩进规则。
```html
<!-- good -->
{if $display == true}
<div>
  <ul>
    {foreach $item_list as $item}
    <li>{$item.name}<li>
    {/foreach}
  </ul>
</div>
{/if}

<!-- bad -->
{if $display == true}
    <div>
        <ul>
    {foreach $item_list as $item}
        <li>{$item.name}<li>
    {/foreach}
        </ul>
    </div>
{/if}
```

#### 语法正确性
模板代码应以保证 HTML 单个标签语法的正确性为基本原则。
```html
<!-- good -->
<li class="{if $item.type_id == $current_type}focus{/if}">{ $item.type_name }</li>

<!-- bad -->
<li {if $item.type_id == $current_type} class="focus"{/if}>{ $item.type_name }</li>
```

#### 模板数据分组
在循环处理模板数据构造表格时，若要求每行输出固定的个数，建议先将数据分组，之后再循环输出。
```html
<!-- good -->
<table>
  {foreach $item_list as $item_group}
  <tr>
    {foreach $item_group as $item}
    <td>{ $item.name }</td>
    {/foreach}
  <tr>
  {/foreach}
</table>
```
### 可访问性 Accessibility
在开发中要时刻考虑可访问性，而不是在开发后才去改善。你不必像一位 WCAG 专家那样去提升你的网站，但你可以立即开始修复一些将产生巨大的改善作用的小问题。如:

- 确保你的链接和按钮等都很好地标记
```html
<!-- bad -->
<div class="button"></div>

<!-- good -->
<button></button>
```
- 显式地给表单控件加 **label** 标签
```html
<label for="melon"></label>
<input id="melon" type="text">
```
- 学会正确使用 **alt** 属性
  - 为多媒体（如图像、视频、通过 canvas 读取的动画元素）提供备选内容
  - 对图像使用有意义的替代文本（alt）
  - 对视频和音频使用有效的副本和文案说明
```html
<!-- bad -->
<img src="logo.png" alt="Logo">

<!-- good -->
<img src="logo.png" alt="My Company, Inc.">
```
提供备选内容是很重要的，原因：
- 用 alt 给盲人用户一些图像的提示性文字
- 用文案说明帮助用户理解视频或音频的内容
- 图像的 alt 属性会产生冗余，可不写，alt=""

## CSS

### CSS文件

#### 单文件与多文件

有人喜欢在一份文件中编写所有的内容，也有人喜欢将样式表拆分成多个小文件（特别是使用 LESS 和 SASS）。这都是很好的做法。

#### 不要使用 @import

与 link 相比，@import 的加载速度要慢很多，不光增加额外的请求数，还会导致不可预料的问题。
```css
/*  Not Recommended  */
@import url(path/to/reset.css);
@import url(path/to/base.css);
```
建议：

- 使用多个 link 元素
```html
<!-- Recommended -->
<link rel="stylesheet" href="path/to/reset.css">
<link rel="stylesheet" href="path/to/base.css">
<link rel="stylesheet" href="path/to/common.css">
```
- 通过 Sass / Less 或类似的 CSS 预处理器将多个 CSS 文件编译为一个文件
```less
/*  Recommended  */
@import url(path/to/reset.less);
@import url(path/to/base.less);

/* 在 common.less 中 导入 reset.less 和 base.less，使用 LESS 编译 */
```
```html
<link rel="stylesheet" href="path/to/common.css">
```
- 其他 CSS 文件合并工具（Rails / Jekyll）

`reference: ` [Don't Use @import](http://www.stevesouders.com/blog/2009/04/09/dont-use-import/)

### 目录与注释
```css
/*--------------------------------*\
  0. CONTENTS
\*--------------------------------*/

/**
 *  0. Contents
 *  1. Reset & Clearfix
 *  2. Document Setup
 *  3. Header
 *  4. Section
 *  5. Footer
 *  6. Mending
 */


/*--------------------------------*\
  1. RESET & CLEARFIX
\*--------------------------------*/
.meyer {}


/*--------------------------------*\
  2. DOCUMENT SETUP
\*--------------------------------*/
html {
  font-size: 62.5%;
}


/*--------------------------------*\
  2. DOCUMENT SETUP
\*--------------------------------*/
.selector {}

  .selector-child {}

      .selector-grandchild {}

.selector-siblings {}


/*--------------------------------*\
  3. HEADER
\*--------------------------------*/
.wrapper {}

   /**
    * navigation
    */
  .nav {}

```
#### 目录

这份目录可以告诉其他开发者这个文件中具体包含哪些内容。这份目录中的每一项都与其对应的区块标题相同。
```css
/*--------------------------------*\
  0. CONTENTS
\*--------------------------------*/

/**
 *  0. Contents
 *  1. Reset & Clearfix
 *  2. Document Setup
 *  3. Header
 *  4. Section
 *  5. Footer
 */
```
#### 区块顺序
尽量按照特定的顺序声明样式，这将确保你充分发挥 CSS 中 C 的意义：Cascading 层叠。

一份规划良好的 CSS 应当按照如下顺序排列：

> - Reset
> - 元素类型
> - 对象以及抽象内容  (最基础的设计模式)
> - 子元素  (对象拓展及其子元素)  
> - 修补

如此一来，当你依次编写 CSS 时，每个区块都可以自动继承在它之前的区块的属性。这样就可以减少重复代码，减少某些特殊的问题，组成更理想的 CSS 结构。

`reference: ` [SMACSS By Jonathan Snook](https://smacss.com/)

#### 组件单位
> 以组件为单位组织代码段

如果使用了多个 CSS 文件，将其按照组件而非页面的形式分拆，因为页面会被重组，而组件只会被移动。
```css
/* -------------------------------------
/*   组件块
/* -------------------------------------

/*   子组件块1
/* ------------------------------------- */
.selector-1st {}

/*   子组件块2
/* ------------------------------------- */
.selector-2nd {}

.selector-3rd {}
```

#### 注释

良好的注释是非常重要的。请留出时间来描述代码的工作方式、局限性和构建它们的方法。不要让团队其它成员来猜测一段不通用或不明显的代码的目的。
```css
/**
 * 这是一个文档块（DocBlock）风格的注释。
 *
 * 这里开始是描述更详细、篇幅更长的注释正文。当然，我们要把行宽控制在 80 字节以内。
 *
 * 我们可以在注释中嵌入 HTML 标记，而且这也是个不错的办法：
 *
  <div class=foo>
    <p>Lorem</p>
  </div>
 *
 * 如果是注释内嵌的标记的话，在它前面不加星号，以免被复制进去。
 */
```

注释有很多高级的拓展用法：

- 准修饰选择器 Quasi-qualified-selectors
- 代码标签
- 继承标记

##### `准修饰选择器`
我们应当避免过分修饰选择器。如果能写 .nav{} 就尽量不要写 ul.nav{}。过分修饰选择器将增加选择器私有度，影响 class 复用性，影响性能。

不过有时我们可能希望告诉其他开发者 class 的使用范围。以 .product-page 为例，这个 class 看起来像是一个根容器，可能是 html 或者 body 元素，但是仅凭 .product-page 则无法判断。我们可以在选择器前加上准修饰来描述 class 的作用范围：
```css
/* 将前面的类型选择器注释掉 */

/*html*/.product-page {}
```
这样我们就能明确该 class 的作用范围而不增加选择器私有度，不影响复用性。

##### 代码标签

如果你写了一组新样式的话，可以在它上面加上标签，例如：
```css
/**
 * ^navigation ^lists
 */
.nav {}

/**
 * ^grids ^lists ^tables
 */
.matrix {}
```
这些标签可以使得其他开发者快速找到相关代码。如果一个开发者需要查找和列表相关的部分，他只要搜索 ^lists 就能快速定位到 .nav / .matrix 以及其它相关部分。

##### 继承标记

将面向对象的思路用于 CSS 编写的话，你经常能找到两部分 CSS 密切相关（其一为基础，其一为拓展）却分列两处。我们可以用继承标记来在原元素和继承元素之间建立紧密联系。这些在注释中的写法如下：

在元素的基本样式中：
```css
/**
 * Extend `.foo` in theme.css
 */
 .foo {}
```
在元素的拓展样式中：
```css
/**
 * Extends `.foo` in base.css
 */
 .bar {}
```
 
这样一来，我们就能在两块相隔很远的代码间建立紧密联系。

### 选择器

#### `禁止使用id选择器`

在 HTML 里 id 可以用于 js-hooks 以及锚点定位，但是在 CSS 里只用 class，一个 id 也不要用。

class 的优势在于复用性，而且私有度也不高。在项目中私有度非常容易导致问题，所以将其降低就显得尤为重要。`id 的私有度是 class 的 255 倍`，所以在 CSS 中坚决不要使用。
```html
<section class="segs js-segs" id="segment"></section>
```
```css
/* Not Recommended */
#segment {}
.js-segs {}

/* Recommended */
.segs {}
```

#### 多使用class选择器

对于通用元素多使用 class 选择器，有利于渲染性能的优化。

#### BEM 命名法
> BEM : Block_Element-Modifier

BEM 命名法可以使得选择器更规范，更清晰，更具语义。该命名法按照如下格式：
```css
.block {} 代表某个基本的抽象元素
.block_element {} 代表构成 .block 的某个子元素
.block-modifier {} 代表 .block 的某个不同的状态或版本
```
i.e.
```css
.person {}
.person-woman {}
.person_hand {}
.person_hand-left {}
.person_hand-right {}
```
BEM 命名法虽然不太好看，而且相当冗长，但是它使得我们可以通过名称快速获知元素的功能和元素之间的关系。与此同时，BEM 语法中的重复部分非常有利于 gzip 的压缩算法。无论你是否使用 BEM 命名法，你都应当确保 class 命名得当，力保一字不多、一字不少。

#### 避免为class选择器添加类型限定

如无必要，不得为class选择器添加类型限定。其弊在于：
- 影响性能
- 违反结构与表现相分离原则。如果修改了 HTML 标签，则 CSS 选择器也必须发生变化，不利于后期维护
```css
/* Not Recommended */
p.msg-danger {}

/* Recommended */
.msg-danger {}
```

#### 避免使用类型选择器

确保你的核心选择器不是类型选择器，也不是高级对象或抽象选择器。
```css
/* Not Recommended */
.form input {}

/* Recommended */
.form .user-name {}
```

#### 避免选择器的嵌套层级过高

选择器的嵌套层级应不大于 3 级，位置靠后的限定条件应尽可能精确，务必保持选择器简短高效。
```css
/* Not Recommended */
.page .header .login .username .avatar {}

/* Recommended */
#username .avatar {}
```
结构复杂的选择器将会影响性能。选择器的结构越复杂，浏览器的开销就越大。尽量使得样式不依赖于其定位，尽量保持选择器简洁清晰。

#### 明确使用选择器的目的

比起努力运用选择器定位到某元素，更好的办法是给你想要添加样式的元素直接添加一个 class。力保表达清晰：`直接找到你要添加样式的元素，而非其父元素`。不要想当然地认为 HTML 不会改变。用 CSS 直接命中你需要的元素，而非投机取巧。

你的选择器必须符合你要给这个元素添加样式的原因。例如：
```html
<header>
  <ul class="main-nav"></ul>
</header>
```
```css
header ul {
	/* 我定位到这个元素是因为它是 header 下的 ul */
}

.main-nav {
	/* 我定位到这个元素是因为它是网站导航 */
}
```
这将决定你应当如何使用选择器。

参考 [Shoot to kill; CSS selector intent](http://csswizardry.com/2012/07/shoot-to-kill-css-selector-intent/)   

### 声明块格式

- 缩进样式集从而反映 DOM

在编写规则时，根据选择器之间的关系适当缩进代码，提高易读性
```css
/*  Recommended  */
.widget {}

  .widget-heading {}

/*  Not Recommended  */ 
.widget {}

.widget-heading {}
```
我们可以发现，.widget-heading 是 .widget 的子元素，因为前者的样式集比后者多缩进了一级。这样就可以通过缩进让开发者在阅读代码时快速获取这样的重要信息。

- 选择器分组时，独立的选择器占用一行
```css
/*  Recommended  */
.post,
.page,
.comment {
  line-height: 1.5;
}

/*  Not Recommended  */
.post, .page, .comment {
  line-height: 1.5;
}
```

- 动态伪类的样式顺序
```css
a:link {}
a:visited {}
a:hover {}
a:active {}
```

- `>`、`+`、`~` 选择器的两边各保留一个空格。
```css
/*  Recommended  */
main > nav {}

label + input {}

input:checked ~ button {}

/*  Not Recommended  */
main>nav {}

label+input {}

input:checked~button {}
```

- 属性选择器中的值必须用双引号包围

不允许使用单引号，不允许不使用引号。这里是一些 [例外情况](https://mathiasbynens.be/notes/unquoted-attribute-values#css)。为了代码的一致性，建议都加上双引号。
```css
/* Recommended */
input[type="text"] {}

/*  Not Recommended  */
input[type='text'] {}
input[type=text] {}
```

- 声明块的 `{` 前添加一个空格，保持代码的易读性
```css
/*  Recommended  */
.selector {
  
}

/*  Not Recommended  */
.selector{
  
}
```

- 声明块的 `}` 应单独成行
```css
/*  Recommended  */
.selector {
  margin: 0;
}

/*  Not Recommended  */
.selector {
  margin: 0;}
```

- 声明语句的 `:` 前无空格，后有一个空格
```css
/*  Recommended  */
.selector {
  padding: 0;
  margin: 0;
}

/*  Not Recommended  */
.selector {
  padding : 0;
  margin:0;
}
```

- 声明语句以 `;` 结尾（即使是最后一条语句）
```css
/*  Recommended  */
.selector {
  margin: 0 auto;
}

/*  Not Recommended  */
.selector {
  margin: 0 auto
}
```

- 每条声明语句独占一行，可以获得更准确的错误报告
```css
/*  Recommended  */
.selector {
  padding: 0;
  margin: 0;
}

/*  Not Recommended  */
.selector { padding: 0; margin: 0; }
```
- 不拆分多行的情况
```css
.t10 { width:10% }
.t20 { width:20% }
.t25 { width:25% }  /* 1/4 */
.t30 { width:30% }
.t33 { width:33% }  /* 1/3 */
.t40 { width:40% }
.t50 { width:50% }  /* 1/2 */
.t60 { width:60% }
.t66 { width:66% }  /* 2/3 */
.t70 { width:70% }
.t75 { width:75% }  /* 3/4 */
.t80 { width:80% }
.t90 { width:90% }
```
这种情况下，将声明语句放在一行内可以使得代码更紧凑和美观

- 列表型属性值，每个逗号后应添加一个空格
```css
/*  Recommended  */
.selector {
  font-family: Arial, sans-serif;
}

/*  Not Recommended  */
.selector {
  font-family: Arial,sans-serif;
}
```

- 样式分组

对于超长的样式，在样式值的空格处或 `,` 后换行，建议按逻辑分组。
```css
/*  Recommended  */
.selector {
  /* 不同属性值按逻辑分组 */
  background:
    transparent url("aVeryVeryVeryLongUrlIsPlacedHere")
    no-repeat 0 0;

  /* 可重复多次的属性，每次重复一行 */
  background-image:
    url("aVeryVeryVeryLongUrlIsPlacedHere")
    url("aVeryVeryVeryLongUrlIsPlacedHere");

  /* 类似函数的属性值可以根据函数调用的缩进进行 */
  background-image: -webkit-gradient(
    linear,
    left bottom,
    left top,
    color-stop(0.04, rgb(88,94,124)),
    color-stop(0.52, rgb(115,123,162))
  );
}
```

- rgb()、rgba()、hsl()、hsla() 或 rect() 括号内以逗号分隔的值后面，不添加空格
```css
/*  Recommended  */
.selector {
  color: rgba(255,255,255,0.5);
}

/*  Not Recommended  */
.selector {
  color: rgba(255, 255, 255, 0.5);
}
```
- 将行宽控制在 80 字节以下

渐变相关的语法以及注释中的 URL 等可以算作例外，毕竟这部分我们也无能为力。

`reference: ` [Cascading_Style_Sheets#Syntax](https://en.wikipedia.org/wiki/Cascading_Style_Sheets#Syntax)

### 属性

#### 属性编写顺序

##### 按功能分组

同一声明块内下的属性在书写时按功能进行分组，可以提高代码的易读性
> 1. `Positioning 布局方式`
>   - **position**
>   - offsets: top / right / bottom / left
>   - z-index
> 2. `Box model 盒模型`
>   - **display**
>   - box-sizing
>   - size: width / height / padding / border / margin / (border-radius / outline)
>   - **float**
>   - clear
>   - overflow
> 3. `Typographic 文本排版`
>   - font
>   - line-height
>   - text-align
>   - vertical-align
>   - text-overflow
> 4. `Visual 视觉效果`
>   - visibility
>   - color
>   - background
>   - opacity
>   - transition

`WHY: `
- 由于定位可以从正常的文档流中移除元素，并且还能覆盖盒模型相关的样式，因此排在首位
- 盒模型决定了组件的尺寸和位置，因此排在第二位
- 其他属性只是影响组件的内部，不影响前两组属性，因此排在后面
- 各分组内的属性也是有序可循的
- 根据实际需要，一些属性可以跨组书写，如 border-radius 在 border 之后
```css
.declaration-order {
  /* Positioning: positioning schemes / offsets / z-index / ...  */
  position: absolute;
  top: 50%;
  left: 50%;
  z-index: 9999;

  /* Box model: display / box-size / float / overflow / ... */
  display: block;
  box-sizing: border-box;
  width: 100px;
  height: 100px;
  padding: 10px;
  border: 1px solid #eee;
  border-radius: 5px;
  outline: 1px double #ddd;
  margin: 0 auto;
  float: right;
  clear: both;
  overflow: hidden;

  /* Typographic: font / text style / align / ... */
  font: normal 16px "Helvetica Neue", sans-serif;
  line-height: 1.5;
  text-align: center;
  vertical-align: middle;
  text-overflow: ellipsis;
  white-space: nowrap;
  
  /* Visual: fore-color / background-color / shadows / gradients / ... */
  visibility: hidden;
  color: #fff;
  background-color: #ccc;
  opacity: .8;
  clip: rect(10px, 10px, 10px, 10px);

  /* Other */
  cursor: pointer;
  -webkit-transition: all 1s ease .5s infinite;;
       -o-transition: all 1s ease .5s infinite;;
          transition: all 1s ease .5s infinite;;    
} 
```

##### 按字母排序

另一种常用的方法是按字母表对属性进行排序，使用这种方法的公司如 WordPress 团队。
```css
/* Method 1st */
.function-order {
  position: absolute;
  top: 50%;
  left: 50%;
  z-index: 1;
  width: 80px;
  height: 60px;
  overflow: hidden;
  background-color: #ccc;
}

/* Method 2nd */
.alphabet-order {
  background-color: #ccc;
  height: 60px;
  left: 50%;
  overflow: hidden;
  position: absolute;
  top: 50%;
  width: 80px;
  z-index: 1;
}
```


#### 属性简写 shorthand 
有些 CSS 属性是可以简写的，比如 padding / margin / font 等。使用简写属性可以精简代码，同时又能提高阅读体验。在允许的情况下，尽量使用简写属性，避免书写不必要的多个属性。
```css
/* Not Recommended */
.selector {
  top: 50%;
  margin-top: -10px;
  padding-top: 5px;
  padding-right: 10px;
  padding-bottom: 15px;
  padding-left: 10px;
  font-family: arial, sans-serif;
  font-size: 12px;
  line-height: 1.5;
  background-color: #ccc; 
  background-image: url("path/to/your.jpg"); 
}

/* Recommended */
.selector {
  top: calc(50% - 10px);
  padding: 5px 10px 15px;
  font: 12px/1.5 arial, sans-serif;
  background: #ccc url("path/to/your.jpg") no-repeat fixed top;
}
```

##### 慎重使用简写属性
通常，我们不需要为简写属性声明指定所有值。因此在使用时要注意默认的隐含值对实际数值的影响。默认的隐含值极有可能会覆盖实际值而导致意外的副作用。
在使用 margin / font / background 等简写属性时，应明确是否需要设置多个属性值。在不需要显式地设置所有值的情况下，应当尽量限制使用简写属性。
```css
/* bad */
.selector {
  background: #ccc;
  /* equals to code below */
  background-color: #ccc;
  background-image: none;
  background-repeat: repeat;  
  background-position: top left;
}

/* good */
.selector {
  background-color: #ccc;
}
```
过度使用简写属性会导致代码混乱，不要贪图方便就使用简写属性。

`reference: ` [Shorthand Properties](https://developer.mozilla.org/en-US/docs/Web/CSS/Shorthand_properties)


### 属性值

#### 文本型

文本型属性值必须用双引号包围，包括选择器中的属性值。不允许使用单引号，不允许不使用引号。
```css
/* Recommended */
.selector[class~="user"] {
  font-family: "Microsoft YaHei", sans-serif;
  background-image: url("path/to/your.img");
}

/* Not Recommended */
.selector[class~='user'] {
  font-family: 'Microsoft YaHei', sans-serif;
  background-image: url(path/to/your.img);
}
```

`reference: ` [Is Quoting The Value Necessary](http://stackoverflow.com/questions/2168855/is-quoting-the-value-of-url-really-necessary)

#### 数值型

- 对于属性值或颜色参数，当数值为 [0,1] 之间的小数时，省略整数部分的 0
```css
/* Recommended */
panel {
  margin-top: -.5px; 
  opacity: .8;
}

/* Not Recommended */
panel {
  margin-top: -0.5px; 
  opacity: 0.8;
}
```

##### 魔数

魔数（Magic Number）是指那些「凑巧有效果」的数字，使用魔数非常不好，因为它们只是治标不治本而且缺乏拓展性。例如：
```css
.dropdown-nav li:hover ul {
  top: 37px;
}

```
使用上述样式把下拉菜单移动下来远非良策，因为这里的 37px 就是个魔数。37px 会生效的原因是因为这时 .dropbox-nav 碰巧高 37px 而已。这时你应该这么设置：
```css
.dropdown-nav li:hover ul {
  top: 100%;
}
```
即无论 .dropbox-nav 多高，这个下拉菜单都会往下移动 100%


每当你要在代码中放入数字的时候，请三思而行。如果你能用一个关键字替换之或者有更好的解决方法的话，就`尽量避免直接出现数字`。


#### 颜色

- 颜色值不允许使用关键字色值
```css
/* Recommended */
.btn-success {
  color: #90ee90;
}

/* Not Recommended */
.btn-success {
  color: lightgreen;
}
```
- 颜色值可以缩写时必须使用缩写形式
```css
/* Recommended */
.btn-info {
  color: #fff;
}

/* Not Recommended */
.btn-info {
  color: #ffffff;
}
```
- 十六进制值应该全部小写或者保持项目内大小写统一
```css
/* Recommended */
.btn-warning {
  color: #90ee90;
  background-color: #aca;
}

/* Not Recommended */
.btn-warning {
  color: #90ee90;
  background-color: #aaccaa;
}

/* Recommended */
.btn-danger {
  color: #90EE90;
  background-color: #ACA;
}

/* Not Recommended */
.btn-danger {
  color: #90EE90;
  background-color: #aca;
}
```
- RGB颜色值统一使用十六进制形式「#RRGGBB」，不允许使用「rgb()」。带有 alpha 的颜色可以使用「rgba()」
```css
/* Recommended */
.btn-primary {
  color: #ccc;
  background-color: #008000;
  box-shadow: 0 0 2px rgba(0,128,0,.3);
}
/* Not Recommended */
.btn-primary {
  color: hsl(360,100%,100%);
  background-color: rgb(0,128,0);
  box-shadow: 0 0 2px rgba(0,128,0,.3);
}
```

#### 2D位置
必须同时给出水平方向和垂直方向的位置。2D位置初始值为「0% 0%」，但当只有一个方向值时，另一个方向值会被解析为「center」。为避免理解上的困扰，应同时给出两个方向的值。
```css
/* Recommended */
body {
  background-position: center top; /* 50% 0% */
}

/* Not Recommended */
body {
  background-position: center; /* 50% 50% */
}
```

`reference: ` [background-position属性值的定义](http://www.w3.org/TR/CSS21/colors.html#propdef-background-position)

#### 单位

- 长度为 0 时须省略单位
```css
/* Recommended */
body {
  padding: 0 5px;
}

/* Not Recommended */
body {
  padding: 0px 5px;
}
```
- 在允许的情况下使用无单位的值
```css
/* Recommended */
.selector {
  line-height: 1.5;
}

/* Not Recommended */
.selector {
  line-height: 16px;
}
```
- 当使用相对单位时优先使用 `rem`
```css
/* Recommended */
html {
  font-size: 62.5%;
}
.selector {
  font-size: 1.6rem;
}

/* Not Recommended */
.selector {
  font-size: 1em;
}
```
- 优先使用秒而不是毫秒
```css
/* Recommended */
.selector {
  transition: all .5s;
}

/* Not Recommended */
.selector {
  transition: all 500ms;
}
```

### CSS重要概念
#### 定位

在 CSS 中定位元素有很多的方式，但尽量限制自己按如下的参考顺序使用属性/值

> - display: block;
> - display: flex;
> - position: relative;
> - position: sticky;
> - position: absolute;
> - position: fixed;

#### 布局

- 所有组件都不要声明宽度，而由其父元素或格栅系统来决定
- 坚决不要声明高度。高度应当仅仅用于尺寸已经固定的东西，例如图片和雪碧图

应当把格栅系统当作书架来理解：是它们容纳内容，而不是把它们本身当成内容装起来。比起声明它们的尺寸，把格栅系统和元素的其它属性分来开处理更有助于布局，也使得我们的前端工作更高效。在格栅系统上不应当添加任何样式，它们仅仅是为布局而用。在格栅系统内部再添加样式。在格栅系统中任何情况下都不要添加盒模型相关属性。

#### 盒模型

整个文档的盒模型应该保持一致。如无必要，避免改变特定元素默认的盒模型。避免使用全局样式 ` * { box-sizing: border-box; } `
```css
/* bad */
div {
  box-sizing: border-box;
  width: 100%;
  padding: 10px;
}

/* good */
div {
  padding: 10px;
}
```

#### 文档流

> 不要改变元素的默认行为。尽量保持元素在普通的文档流中。
```css
/* bad */
div {
  position: absolute;
  right: 0;
  width: 100px;
}

/* good */
div {
  width: 100px;
  margin-left: auto;
}
```
例如，不应该通过改变图片的默认显示的方式来删除其下面的空白
```css
/* bad */
img {
  display: block;
}

/* good */
img {
  vertical-align: middle;
}
```

#### 清除浮动

块状元素内部元素浮动导致的高度坍塌，需要在外部容器清除浮动。严禁使用增加空标签形式清除浮动。
```css
/* 清除浮动固定写法 */
.clearfix::before,
.clearfix::after {
  content: "";
  display: table;
}
.clearfix::after {
  clear: both;
}
.clearfix {
  zoom: 1;
}
```
当元素需要撑起高度以包含内部的浮动元素时，通过对伪类设置 clear 或触发 BFC 的方式进行 clearfix。触发 BFC 的方式很多，常见的有：

- float 非 none
- position 非 static
- overflow 非 visible

`reference` [A new micro clearfix hack](http://nicolasgallagher.com/micro-clearfix-hack/) 了解更小副作用的清除浮动方法

#### 文本排版

##### 字体族

###### 英文

font-family 属性值中的字体族应使用字体的英文名称。其中如有空格，须用双引号包围。常见名称如下：

字体 | 操作系统 | Family Name
-----|----------|------------
宋体 (中易宋体) | Windows | SimSun
黑体 (中易黑体) | Windows | SimHei
微软雅黑 | Windows | Microsoft YaHei
微软正黑 | Windows | Microsoft JhengHei
华文黑体 | Mac/iOS | STHeiti
冬青黑体 | Mac/iOS | Hiragino Sans GB
文泉驿正黑 | Linux | WenQuanYi Zen Hei
文泉驿微米黑 | Linux | WenQuanYi Micro Hei

```css
h1 {
  font-family: "Microsoft YaHei";
}
```

###### 顺序

font-family 按「西文字体在前、中文字体在后」、「效果佳 (质量高/更能满足需求) 的字体在前、效果一般的字体在后」的顺序编写。最后必须指定一个通用字体族(serif / sans-serif)
`reference: ` [知乎上关于字体的讨论](http://www.zhihu.com/question/19911793/answer/13329819)
```css
/* Display according to platform */
.article {
  font-family: Arial, sans-serif;
}

/* Specific for most platforms */
h1 {
  font-family: "Helvetica Neue", Arial, "Hiragino Sans GB", "WenQuanYi Micro Hei", "Microsoft YaHei", sans-serif;
}
```

###### 大小写

font-family 不区分大小写。但在同一个项目中大小写必须统一。
```css
/* good */
body {
  font-family: Arial, sans-serif;
}
  h1 {
    font-family: Arial, "Microsoft YaHei", sans-serif;
  }

/* bad */
body {
  font-family: arial, sans-serif;
}
  h1 {
    font-family: Arial, "Microsoft YaHei", sans-serif;
  }
```

##### 字号

需要在 Windows 平台显示的中文内容，其`字号应不小于 12px`。由于 Windows 的字体渲染机制，小于 12px 的文字显示效果极差、难以辨认。

##### 字体风格

需要在 Windows 平台显示的中文内容，不要使用除 normal 外的 font-style。其他平台也应慎用。由于中文字体没有 italic 风格的实现，所有浏览器下都会 fallback 到 obilique 实现(自动拟合为斜体)，小字号下(特别是 Windows 下会在小字号下使用点阵字体的情况下)显示效果差，造成阅读困难。

##### 字重

font-weight 属性必须使用数值方式描述。

`WHY: ` CSS 的字重分「100 – 900」共九档，但目前受字体本身质量和浏览器的限制，实际上支持 400 和 700 两档，分别等价于关键词 normal 和 bold。浏览器本身使用一系列 [启发式规则](http://www.w3.org/TR/CSS21/fonts.html#propdef-font-weight) 来进行匹配，在 <700 时一般匹配 Regular 字重，>=700 时匹配 Bold 字重。但已有浏览器开始支持 =600 时匹配 Semibold 字重 (见[此表](http://justineo.github.io/slideshows/font/#/3/15))。故使用数值描述增加了灵活性，也更简短。
```css
/* good */
h1 {
  font-weight: 700;
}

/* bad */
h1 {
  font-weight: bold;
}
```

##### 行高

line-height 在定义文本段落时，应使用数值。

`WHY: ` 将 line-height 设置为数值，浏览器会基于当前元素设置的 font-size 进行再次计算。在不同字号的文本段落组合中，能达到较为舒适的行间间隔效果，避免在每个设置了 font-size 都需要设置 line-height。
`reference: ` [深入了解行高属性](http://www.cnblogs.com/fengzheng126/archive/2012/05/18/2507632.html)

```css
.container {
  line-height: 1.5;
}
```

`reference: ` [网页字体排印指南](http://aaaaaashu.me/shu/)

#### UI尺寸

用 rem 定义字号，并且辅以 px 以兼容旧浏览器。这可以兼具 em 和 px 的优势。

下面是一个非常漂亮的 Sass Mixin，假设你在别处声明了基本字号（base-font-size）的话，用它就可以生成 rem 以及兼容旧浏览器的 px。
```sass
@mixin font-size($font-size) {
  font-size: $font-size + px;
  font-size: $font-size / $base-font-size + rem;
}
```

#### 动画
- 优先使用过渡而不是动画
```css
/* bad */
div:hover {
  animation: move 1s forwards;
}
@keyframes move {
  100% {
    margin-left: 100px;
  }
}

/* good */
div:hover {
  transition: transform 1s;
  transform: translateX(100px);
}
```
- 使用 transition 时应指定 transition-property
```css
/* good */
.box {
  transition: color 1s, border-color 1s;
}

/* bad */
.box {
  transition: all 1s;
}
```
- 尽可能在浏览器能高效实现的属性上添加过渡和动画。在可能的情况下应选择这样四种变换：

> - `transform: translate(npx, npx);`
> - `transform: scale(n);`
> - `transform: rotate(ndeg);`
> - `opacity: 0..1;`
> `reference: ` [high-performance-animations](http://www.html5rocks.com/en/tutorials/speed/high-performance-animations/)

使用 translate 来代替 left 作为动画属性是个典型的例子
```css
/* good */
.box {
  transition: transform 1s;
}
.box:hover {
  transform: translate(20px); /* move right for 20px */
}

/* bad */
.box {
  left: 0;
  transition: left 1s;
}
.box:hover {
  left: 20px; /* move right for 20px */
}
```

#### 重载

重载让选择器和调试都变得更加困难，应尽可能避免
```css
/* bad */
li {
  visibility: hidden;
}
li:first-child {
  visibility: visible;
}

/* good */
li + li {
  visibility: hidden;
}
```

#### 继承

可继承的属性不要重复样式声明
```css
/* bad */
div h1,
div p {
  text-shadow: 0 1px 0 #fff;
}

/* good */
div {
  text-shadow: 0 1px 0 #fff;
}
```

### 兼容性 

#### 欺骗W3C

为了欺骗 W3C 的验证工具,可将代码分为两个文件，一个针对所有浏览器,一个只针对 IE。即将所有符合 W3C 的代码写到一个文件中,而一些 IE 中必须实现而又不能通过 W3C 验证的代码(如 cursor: hand;)放到另一个文件中，再用下面的方法导入
```html
<!-- 放置所有浏览器样式-->
<link rel="stylesheet" href="path/to/allBrowser.css">

<!-- 放置IE必须实现而不能通过w3c验证的样式 -->
<!--[if IE]
  <link rel="stylesheet" href="path/to/ie.css">
<![endif]-->
```
而实际上，`专门为 IE 写的样式基本上都是可以避免的`，唯一需要为 IE 专门处理的是为了处理 IE 不支持的内容（例如 PNG）。

#### 属性前缀

##### 浏览器厂商前缀

带私有前缀的属性由长到短排列，标准属性放在最后，按冒号对齐。方便阅读，也便于在编辑器内进行多行编辑。
```css
/* Prefixed properties */
.box {
  -webkit-box-sizing: border-box;  /* Chrome && Safari */
     -moz-box-sizing: border-box;  /* Firefox */
       -O-box-sizing: border-box;  /* Opera */
          box-sizing: border-box;  /* Opera 10.5+, 以及使用 IE-CSS3 的IE浏览器 */
}
```
##### 积极删除过时的浏览器厂商前缀
```css
/* bad */
div {
  -webkit-transform: scale(2);
     -moz-transform: scale(2);
      -ms-transform: scale(2);
       -o-transform: scale(2);
          transform: scale(2);
          
  -webkit-transition: 1s;
     -moz-transition: 1s;
      -ms-transition: 1s;
       -o-transition: 1s;
          transition: 1s;
}

/* good */
div {
  -webkit-transform: scale(2);
          transform: scale(2);
  transition: 1s;
}
```

##### Autoprefixer
[Autoprefixer](https://github.com/postcss/autoprefixer) 参考 [Can I Use](http://caniuse.com/) 里的浏览器兼容性，对相应的 CSS 代码自动添加浏览器厂商前缀。因此，使用 Autoprefixer 后，在编写CSS时直接使用标准的属性而不需要手动添加浏览器前缀。

`reference: ` [如何处理CSS3属性前缀](http://www.w3cplus.com/css3/autoprefixer-css-vender-prefixes.html)


#### `Hack`

```css
/* Firefox */
@-moz-document url-prefix() {}
/* iPhone/mobile webkit */
@media screen and (max-device-width: 480px) {}
/* Safari 3+/Chrome 1+ */
@media all and (-webkit-min-device-pixel-ratio:0) {}
/* Opera */
@media all and (-webkit-min-device-pixel-ratio:10000), not all and (-webkit-min-device-pixel-ratio:0) {} 

\* html selector {}                /* IE6 */
\*:first-child + html selector {}  /* IE7 */
   html > body selector {}         /* 非IE6 */

.selector {
   property: value;    /* all browser */
  _property: value;    /* IE6 */ 
  +property: value;    /* IE7 */
  *property: value;    /* IE6/7 */
   property: value\9;  /* IE6/7/8/9 */
}
```
##### 避免使用Hack 

hack 使得维护更加困难。当需要添加 hack 时应三思而后行。如果能通过合理的 HTML 结构或使用其他的 CSS 定义达到理想的样式，则不应该使用 hack。

##### 尽量使用`选择器hack`

尽量使用符合 CSS 语法的选择hack，可以避免一些第三方库无法识别 hack 语法的问题

```css
/* IE 7 */
*:first-child + html #header {
  margin-top: 3px;
  padding: 5px;
}

/* IE 6 */
* html #header {
  margin-top: 5px;
  padding: 4px;
}
```

##### 尽量使用简单的`属性hack`
```css
.box {
  _display: inline; /* fix double margin */
  float: left;
  margin-left: 20px;
}

.container {
  overflow: hidden;
  *zoom: 1; /* triggering hasLayout */
}
```

#### Expression

优先使用英文而不是数学表达式
```css
/* good */
:nth-child(odd) {
  transform: rotate(1turn);
}

/* bad */
:nth-child(2n+1) {
  transform: rotate(360deg);
}
```

### 响应式

#### 媒体查询的位置

将媒体查询（Media Query）尽可能放在相关规则的附近。不要将它们打包放在一个单一样式文件中或者放在文档底部。这样很容易被人遗忘。
```css
.element {}
.element-avatar {}
.element-selected {}

@media (max-width: 768px) {
  .element {}
  .element-avatar {}
  .element-selected {}
}
```
#### 媒体查询的编排

媒体查询不得单独编排，必须与相关的规则一起定义。
```css
/* Good */

/* header styles */
@media (...) {
  /* header styles */
}
/* main styles */
@media (...) {
  /* main styles */
}
/* footer styles */
@media (...) {
  /* footer styles */
}

/* Bad */

/* header styles */
/* main styles */
/* footer styles */
@media (...) {
  /* header styles */
  /* main styles */
  /* footer styles */
}
```

#### 媒体查询单独成行

媒体查询如果有多个逗号分隔的条件时，应将每个条件放在单独一行中。
```css
@media
(-webkit-min-device-pixel-ratio: 2), /* Webkit-based browsers */
(min--moz-device-pixel-ratio: 2),    /* Older Firefox browsers (prior to Firefox 16) */
(min-resolution: 2dppx),             /* The standard way */
(min-resolution: 192dpi) {           /* dppx fallback */
  /* Retina-specific stuff here */
}
```

#### 高分辨率效果更佳

尽可能给出在高分辨率设备(Retina)下效果更佳的样式。

### 补丁和调试

#### 原则

CSS 样式新建或修改尽量遵循以下原则
1. 根据新建样式的适用范围分为三级：全站级、产品级、页面级
2. 不要轻易改动全站级CSS，改动后，要经过全面测试
3. 尽量通过继承和层叠重用已有样式
4. 禁止在标签上写样式

#### 步骤

##### 删除旧代码

如果你要解决 CSS 问题的话，先删除旧代码再写新的代码。如果旧的 CSS 中有问题的话，写新代码是无法解决的。把 HTML 结构和 CSS 代码删掉，直到没有 BUG 为止，那么我们就知道问题出在哪里了。有时候写上一个 overflow: hidden 或者其它能把问题藏起来的代码的确效果立竿见影，但是 overflow 方面可能根本就没问题。所以要治本，而不是单纯治标。

##### 避免`!important`

尽量不使用 !important 声明。不要让选择器难以覆盖。只有当需要强制指定样式且不允许任何场景覆盖时，才通过 !important 定义样式。比较好的方法是增加选择器的专一程度，或者添加新的 class 然后将声明块放在最后覆盖之前的样式。
```css
/* bad */
.bar {
  color: green !important;
}
.foo {
  color: red;
}

/* good */
.foo.bar {
  color: green;
}
.foo {
  color: red;
}
```

## JavaScript
#### 使用严格模式编码
```javascript
"use strict";
```
#### 注释
##### 原则
- As short as possible（如无必要，勿增注释）：尽量提高代码本身的清晰性、可读性
- As long as necessary（如有必要，尽量详尽）：合理的注释、空行排版等，可以让代码更易阅读、更具美感
##### 单行注释
必须独占一行。`//` 后跟一个空格，缩进与下一行被注释说明的代码一致。
##### 多行注释
避免使用 /*...*/ 这样的多行注释。有多行注释内容时，使用多个单行注释。
##### 函数/方法注释
```javascript
/**
 * [sliceArray description] 函数说明
 * @param  {[type]} array [description] 参数类型和说明
 * @param  {[type]} star  [description] 参数类型和说明
 * @param  {[type]} end   [description] 参数类型和说明
 * @return {[type]}       [description] 返回值类型和说明
 */
function sliceArray(array, star, end) {
  var initialArray = array,
           starPos = star,
            endPos = end;
  var sliceArray = initialArray.slice(starPos, endPos);
  return sliceArray;
}
```
##### 文件注释
文件注释用于告诉不熟悉这段代码的读者这个文件中包含哪些东西。 应该提供文件的大体内容, 它的作者, 依赖关系和兼容性信息。
```javascript
/**
 *      @function:
 *  @fileoverview: 
 *  @dependencies:
 * @compatibility:
 *        @author:
 */
```
#### 命名
##### 变量
使用 Camel 命名法
```javascript
var loadingModules = {};
```
##### 私有属性、变量和方法
以下划线 _ 开头
```javascript
var _privateVariable = null;
```
##### 常量
使用全部字母大写，单词间下划线分隔的命名方式。
```javascript
var HTML_ENTITY = null;
```
##### 函数
使用 Camel 命名法。
```javascript
function stringFormat() {}
```
##### 函数的参数
使用 Camel 命名法
```javascript
function hear(theBells) {}
```
##### 对象
使用 Pascal 命名法
##### 对象的方法 / 属性
使用 Camel 命名法
```javascript
function TextNode(value, engine) {
    this.value = value;
    this.engine = engine;
}
TextNode.prototype.clone = function () {
    return this;
};
```
##### 枚举变量
使用 Pascal 命名法
##### 枚举的属性
使用全部字母大写，单词间下划线分隔的命名方式
```javascript
var TargetState = {
  READING: 1,
  APPLIED: 2,
  READED: 3,
  READY: 4
};
```
由多个单词组成的 `缩写词`，在命名中，根据`当前命名法`和出现的位置，所有字母的大小写与首字母的大小写保持一致。
```javascript
function XMLParser() {}

function insertHTML(element, html) {}

var httpRequest = new HTTPRequest();
```
#### 命名语法
##### 类名构造器()
使用名词，使用 Camel ，首字母大写
```javascript
function Engine(options) {}
```
##### 函数名
使用 Camel ，使用动宾短语
```javascript
function getStyle(element) {}
```
##### 布尔类型
使用 is 或 has 开头
```javascript
var isReady = false;
var hasMoreCommands = false;
```
##### Promise 对象
用动宾短语的进行时表达
```javascript
var loadingData = ajax.get('url');
loadingData.then(callback);
```

#### 接口命名规范
- 可读性强，见名晓义；
- 尽量不与 jQuery 社区已有的习惯冲突；
- 尽量写全。不用缩写，除非是下面列表中约定的；（变量以表达清楚为目标，uglify 会完成压缩体积工作）
| 常用词 | 说明 |
| : | : |
| options | 表示选项，与 jQuery 社区保持一致，不要用 config, opts 等|
| active | 表示当前，不要用 current 等 |
| index | 表示索引，不要用 idx 等 |
| trigger | 触点元素 |
| triggerType | 触发类型、方式 |
| context | 表示传入的 this 对象 |
| object | 推荐写全，不推荐简写为 o, obj 等 |
| element | 推荐写全，不推荐简写为 el, elem 等 |
| length | 不要写成 len, l |
| prev | previous 的缩写 |
| next | next 下一个 |
| constructor | 不能写成 ctor |
| easing | 表示动画平滑函数|
| min | minimize 的缩写 |
| max | maximize 的缩写 |
| DOM| 不要写成 dom, Dom |
| .hbs | 使用 hbs 后缀表示模版 |
| btn | button 的缩写 |
| link | 超链接 |
| title | 主要文本 |
| img | 图片路径（img标签src属性） |
| dataset | html5 data-xxx 数据接口 |
| theme| 主题 |
| className | 类名 |
| classNameSpace | class 命名空间 |
#### 代码格式
- "()"前后需要跟空格
- "="前后需要跟空格
- ","后面需要跟空格
- JSON对象需格式化对象参数
- if、while、for、do语句的执行体用"{}"括起来
#### True 和 False 布尔表达式
类型检测优先使用 typeof。对象类型检测使用 instanceof。null 或 undefined 的检测使用 == null。

下面的布尔表达式都返回 false
- null
- undefined
- '' 空字符串
- 0 数字0

但小心下面的, 可都返回 true:
- '0' 字符串0
- [] 空数组
- {} 空对象

#### 不要在 Array 上使用 for-in 循环
for-in 循环只用于 object/map/hash 的遍历, 对 Array 用 for-in 循环有时会出错. 因为它并不是从 0 到 length - 1 进行遍历, 而是所有出现在对象及其原型链的键值。
```javascript
i.e.
function exportArray(array) {
  for (var key in array) {
    console.log(array[key]);
  }
}

exportArray([0,1,2,3]);
// We Guess: 0, 1, 2, 3
// Actually: 0, 1, 2, 3

var array = new Array(10);
exportArray(array);
// We Guess: undefined x 10
// Actually: nothing at ll (cause key is undefined)

var elements = document.getElementsByTagName('*');
exportArray(elements);
// We Guess: html, head, meta, title, link, script, body
// Actually: html, head, meta, title, link, script, body, 7, item(){[native code]}, namedItem(){[native code]}
// key: length, value: 7; key: item, value: item(); key: namedItem, value: namedItem().

array = [0,1,2,3];
array.addkey = 'wine';
exportArray(array);
// We Guess: 0, 1, 2, 3, wine
// Actually: 0, 1, 2, 3, wine

var array = new Array();
array[3] = 3;
exportArray(array);
// We Guess: undefined x 3, 3
// Actually: 3 (cause key of item 0~2 is undefined)

/* Recommended */
function exportArray(array) {
  var l = array.length;
  for (var i = 0; i < l; i++) {
    console.log(array[i]);
  }
}
```
for-in循环体中必须用hasOwnProperty方法检查成员是否为自身成员，避免来自原型链上的污染。
#### 二元和三元操作符
避免和JSLint的检验机制冲突，操作符始终写在前一行行尾, 以免分号的隐式插入产生预想不到的问题
```javascript
var x = a ? b : c;

var y = a ?
        longButSimpleOperandB : longButSimpleOperandC;

var z = a ?
        moreComplicatedB :
        moreComplicatedC;

var x = foo.bar().
        doSomething().
        doSomethingElse();
```
#### 条件(三元)操作符 (?:)
三元操作符用于替代 if 条件判断语句。
```javascript
// Not Recommended
if (val) {
  return foo();
}
else {
  return bar();
}

// Recommended
return val ? foo() : bar();
```
#### && 和 ||
二元布尔操作符是可短路的, 只有在必要时才会计算到最后一项
```JavaScript
/* Not Recommended */
function foo(opt_win) {
  var win;
  if (opt_win) {
    win = opt_win;
  } else {
      win = window;
  }
}

if (node) {
  if (node.kids) {
    if (node.kids[index]) {
      foo(node.kids[index]);
    }
  }
}

/* Recommended */
function foo(opt_win) {
  var win = opt_win || window;
}

var kid = node && node.kids && node.kids[index];
if (kid) {
  // kid equals to node.kids[index] now
  foo(kid);
}
```
#### 使用严格的条件判断符
用===代替==，用!==代替!=
在==时，则会有一些让人难以理解的陷阱。
```JavaScript
(function () {
  var undefined;
  undefined == null;   // true
          1 == true;   // true
          2 == true;   // false
          0 == false;  // true
          0 == '';     // true
        NaN == NaN;    // false
         [] == false;  // true
         [] == ![];    // true
})();
```
对于不同类型的 == 判断，有这样一些规则，顺序自上而下：
- undefined与null相等
- 一个是number一个是string时，会尝试将string转换为number
- 尝试将boolean转换为number
- 0或1
- 尝试将Object转换成number或string 

而这些取决于另外一个对比量，即值的类型，所以对于0、空字符串的判断，建议使用===
#### 类型转换
##### number -> string
```JavaScript
/* Not Recommended */
var x = 1,
    y = 1;
x = new String(x);
y = y.toString();

/* Recommended */
var z = 1;
z = z + '';
```
##### string -> number
```JavaScript
/* Recommended */
var x = 1;
x = parseInt(x,10);  // 必须显式指定第二个参数的进制
```
##### float -> integer
```JavaScript
/* Not Recommended */
var x = 7.14;
x = parseInt(x,10);

/* Recommended */
var y = 7.14;
y = Math.floor(y);  // 向下取整
y = Math.round(y);  // 向上取整
y = Math.ceil(y);   // 四舍五入 
```
#### 字符串拼接
字符串拼接应使用数组保存字符串片段，使用时调用join方法。避免使用+或+=的方式拼接较长的字符串，每个字符串都会使用一个小的内存片段，过多的内存片段会影响性能。



## 参考
- [前端开发规范手册 - 知笔墨](http://zhibimo.com/read/Ashu/front-end-style-guide/index.html)
- [Web 前端开发规范文档](https://github.com/kahn1990/kahn1990.github.io/wiki/web_develop_standard)
- [frontend-guidelines](https://github.com/bendc/frontend-guidelines/blob/master/README.md)
- [前端参考指南](http://web.jobbole.com/82387/)
- [编码规范 - @chinakids](http://chinakids.github.io/PicturesStore/html/coding/index.html#userconsent#)
- [编码规范 - @mdo](http://www.css88.com/doc/codeguide/)
- [Github GuideLines](http://primercss.io/guidelines/)
- [JavaScript Style Guide](https://github.com/ecomfe/spec/blob/master/javascript-style-guide.md)

## 移动端
[详情](http://zhibimo.com/read/Ashu/front-end-style-guide/mobile-optimize/index.html)

# 工具箱
[详情](http://zhibimo.com/read/Ashu/front-end-style-guide/tool/index.html)

# 资料
[详情](http://zhibimo.com/read/Ashu/front-end-style-guide/reference/index.html)
