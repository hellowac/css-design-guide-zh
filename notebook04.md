
## 字体和文本

### 字体

网页中的字体有三个来源:

- 用户机器中安装的字体。（直到最近，这些字体还是能在网页中放心使用的唯一一批字体。）
- 保存在第三方网站上的字体。最常见的是 Typekit 和 Google，可以使用 link 标签把它们链接到你的页面上。
- 保存在你的 Web 服务器上的字体。这些字体可以使用@font-face 规则随网页一起发送给浏览器。

#### 字体相关属性

- font-family
- font-size
- font-style
- font-weight
- font-variant
- font（简写属性）

#### 字体和文本的区别

```
字体是“文字的不同体式”或者“字的形体结构”。
对于英文而言，每种字体都是由一组具有独特样式的字母、数字和符号组成的。
根据外观，字体可以分为不同的类别（fontcollection），包括衬线字体（serif）、无衬线字体（sans-serif）和等宽字体（monospace）。
每一类字体可以分成不同的字体族（font family），比如 Times 和 Helvetica。
而字体族中又可以包含不同的字型（font face），反映了相应字体族基本设计的不同变化，
例如 TimesRoman、Times Bold、Helvetica Condensed 和 Bodoni italic。

文本就是一组字或字符，比如章标题、段落正文等等，跟使用什么字体无关。
CSS 为字体和文本分别定义了属性。字体属性主要描述一类字体的大小和外观。
比如，使用什么字体族（是 Times，还是 Helvitica），多大字号，粗体还是斜体。
文本属性描述对文本的处理方式。
比如，行高或者字符间距多大，有没有下划线和缩进。

这就是字体和文本之间的区别。
如果想让文字加粗，或者变斜体，可以设定字体属性。
而行高和缩进这种只有对文本块（比如标题和段落）才有意义的样式，则要使用文本属性设定。
```

### 字体族

font-family 用于设定元素中的文本使用什么字体。

一般来说，应该给整个页面设定一种主字体，然后只对那些需要使用不同字体的元素再应用 font-family。

为整个页面指定字体，可以设定 body 元素的 font-family 属性：`body {font-family:verdana, sans-serif;}`

font-family 是可以继承的属性，因此它的值会遗传给所有后代元素。

**用字体栈指定本地字体**

在指定文本的字体时，需要多列出几种后备字体，以防第一种字体无效。这个字体的列表就叫叫字体栈。
比如：`body {font-family:"trebuchet ms", tahoma, sans-serif;} `
如果字体名多于一个单词（有空格），应该加上引号。该设定会依次尝试使用字体，直到最后的通用字体。

通用的字体类：

- serif，也就是衬线字体，在每个字符笔画的末端会有一些装饰线；
- sans-serif，也就是无衬线字体，字符笔画的末端没有装饰线；
- monospace，也就是等宽字体，顾名思义，就是每个字符的宽度相等（也称代码体）；
- cursive，也就是草书体或手写体（在本章后面排版 The Hound of the Baskervilles，即《巴斯克维尔庄园的猎犬》的示例中可以看到）；
- fantasy，不能归入其他类别的字体（一般都是奇形怪状的字体）。

这些通用字体类的目的，就是确保在最坏的情况下，文档可以通过正确的字形来显示。

#### 字体大小

浏览器样式表默认为每个标签都设定了 font-size，在设定 font-size的时候，其实是在修改默认值。

font-size 在标签中是可以继承的，设定字体大小的单位有两种，一种是绝对单位，比如像素或点，另一种是相对单位，比如百分比或 em。

**1. 绝对字体大小**

像素、派卡（pica）或英寸

设定绝对字体大小时，也可以使用关键字值，比如 x-small、medium、x-large，等等

medium 等于基准大小(16px)，参考：[wiki](http://css-discuss.incutio.com/wiki/Using_Keywords)

**2. 相对字体大小**

使用百分比、em 或 rem（根元素的字体大小）设定字体大小，

给某个元素设定了相对字体大小，则该元素的字体大小要相对于最近的“被设定过字体大小的”祖先元素来确定。

事例HTML:

```HTML
<style>
p {font-size:.75em;}
strong {font-size:.75em;}
</style>
<body>
 <p>This is <strong>very important!</strong></p>
</body>
<!--
p 元素的文本为 12 像素（body 的 16 像素基准大小×.75＝12），折合成点单位是 9 点。
strong 是 p 的子元素，它的文本是多大呢？相对大小会逐层复合，
strong 的大小应该是 16 像素×.75×.75＝9 像素。
要熟悉相对单位的这种计算方式，需要多实践。
最终，改变一个元素的相对字体大小，其子元素的字体大小也会同比例变化。
-->
```

```
如果想使用 em，但又需要设定具体的像素大小，可以把 body 的 font-size 设定为62.5%。
这样，就等于把基准大小从 16 像素改为 10 像素（16×62.5%=10）。
然后，em 与像素的对应关系就十分明确了，
比如:
1em = 10 像素，
1.5em = 15 像素，
2em = 20 像素，等等。
```

好处：使用相对字体大小，自动调整各层元素。反复修改布局设计的时候，这样显然能节省时间。

坏处：毕竟是“牵一发而动全身”的事，所以使用相对字体大小时，必须事先规划好。

**3. 关于 rem 单位**

CSS3 新增了一个相对单位 rem（root em，根 em）

与 em 有什么区别：使用 rem 为元素设定字体大小时，仍然是相对大小，但相对的只是 HTML 根元素。
这个单位可谓集相对大小和绝对大小的优点于一身，通过它既可以做到只修改根元素就成比例地调整所有字体大小，
又可以避免字体大小逐层复合的连锁反应。

目前，除了 IE8 及更早版本外，所有浏览器均已支持rem。
对于不支持它的浏览器，可以多写一个绝对单位的声明。
这些浏览器会忽略用 rem 设定的字体大小。

下面就是一个例子：
/*IE8 及之前版本的 IE 浏览器使用 14 像素*/
p {font-size:14px; font-size:.875rem;}

### 字体样式

值：italic、oblique、normal。

示例：`h2 {font-style:italic;}`

italic:斜体
normal:正体

**所谓“常规”值**

```
font-style 有一个 normal 值，中文就是“常规”的意思。
这个值其实不仅 font-style 有，很多其他属性也有，它的作用就是取消所有的特殊样式。
什么情况下才会用它呢？

这个值是用来有选择地覆盖某个默认或你设定的全局属性的。
比如，h1 到 h6 默认为粗体，如果你想让 h3 以常规字体显示，就需要设定 h3 {font-weight:normal;}。
如果你的样式表里声明了 a {font-variant:small-caps;}，那网页中的英文链接都会变成小型大写字母。
要是你想让某一组链接仍然以常规的大小写形式显示，
可能得另写一个类似这样的声明：a.speciallink {font-variant:normal;}。
```

## 字体粗细

可能的值：100、200……900，或者 lighter、normal、bold 和 bolder。

示例：`a {font-weight:bold;}`

粗体的主要作用是表示重要。strong 也表示重要，而它的默认样式就是粗体。

## 字体变化

值：small-caps、normal。

示例：`blockquote {font-variant:small-caps;}`

font-variant 属性除了 normal，就只有一个值，即 small-caps。

这个值会导致所有小写英文字母变成小型大写字母.

### 简写字体属性

```HTML
<style>
  p {font: bold italic small-caps .9em helvetica, arial, sans-serif;}
</style>
<p>
  Here's a piece of text loaded up with every possible font property.
</p>
```

font 属性是一个简写形式，通过它只要一条 CSS 声明就可以设定所有字体属性。
不过，使用时要遵守两条规则：

规则一：必须声明 font-size 和 font-family 的值。

规则二：所有值必须按如下顺序声明。

1. font-weight、font-style、font-variant 不分先后；
2. 然后是 font-size；
3. 最后是 font-family。

### 文本属性

- text-indent
- letter-spacing
- word-spacing
- text-decoration
- text-align
- line-height
- text-transform
- vertical-align

#### 文本缩进

值：长度值（正、负均可）。

示例：`p {text-indent:3em;}`

text-indent 属性设定行内盒子相对于包含元素的起点。默认情况下，这个起点就是包含元素的左上角。

text-indent 设定正值，文本向右移，设定负值，文本向左移。

**继承的值与计算的值**

```
text-indent 是可以被子元素继承的。
如果你在一个 div 上设定了 text-indent 属性，
那么 div 中的所有段落都会继承该缩进值。
然而，与所有继承的 CSS 值一样，这个缩进值并不是祖先元素中设定的值，而是计算的值。

假设有一个 400 像素宽的 div，包含的文本缩进 5%，则缩进的距离是 20 像素（400 的 5%）。
在这个 div 中有一个 200 像素宽的段落。
作为子元素，它继承父元素的 text-indent 值，所以它包含的文本也缩进。
但继承的缩进值是多少呢？不是 5%，而是 20 像素。
也就是说，子元素继承的是根据父元素宽度计算得到的缩进值。
结果，虽然段落只有父元素一半宽，但其中的文本也会缩进 20 像素。
这样可以确保无论段落多宽，它们的缩进距离都一样。
当然，在子元素上重新设定 text-indent 属性，可以覆盖继承的值。
```

**文本之“蛇”**

```
在 CSS 中控制文本要理解一个重要概念。
CSS 会把元素中的文本放在一个不可见的盒子里，(文本被包含在一个细长的盒子中，这个盒子往往因为折行而断开，分布在多行中)
比如对 p 元素中的一段文本，CSS 将其视为很长的一行，只不过在遇到容器边界时会折行。
所有文本属性都会应用给这个细边框的文本盒子。

使用文本属性 text-indent,实际上你缩进的是这个文本盒子的起点位置。
后续的行是不会缩进的，因为在 CSS 看来，它们就是一个整体。

如果想缩进整个段落，可以使用段落的 margin-left 属性。(你得把整个包含盒子向右移动才行.)
而永远要记住，文本属性只应用于这个长长的、细细的、内部的文本盒子，而不是包含元素的盒子。
```

缩进给人一种专业版式的感觉，也能提示读者每段文本在哪儿开头。
注意，在设定缩进和外边距时要像这里一样使用 em，
以便在用户（或你自己）改变字体大小时，它们的长度能够按比例变化。

#### 字符间距

值：任何长度值（正、负值均可）。

示例：`p {letter-spacing:.2em;}`。

letter-spacing 为正值时增大字符间距，为负值时缩小间距。

无论设定字体大小时使用的是什么单位，设定字符间距一定要用相对单位，
以便字间距能随字体大小同比例变化。

letter-spacing 控制字距（tracking），也就是文本块中所有字符之间的间距。
与字距相对的一个排版术语叫字紧排（kerning），紧排只调整两个字符的间距。

letter-spacing 对英文字母、汉字及其他字符都起作用，另，letter-spacing 的值是在浏览器默认值基础上增加或减少的值。

#### 单词间距

值：任何长度值（正、负值均可）

示例：p {word-spacing:.2em;}

单词间距与字符间距非常相似，区别在于它只调整单词间距，而不影响字符间距。

CSS 把任何两边有空白的字符和字符串都视作“单词”。

_纯汉字文本一段之中没有空格，因此 word-spacing 对中文网页几乎没有用，但对中英混排段落可能有用。_

#### 文本装饰

值：underline、overline、line-through、blink、none

示例：`.retailprice {text-decoration:line-through;}`

除了 blink(为文本添加闪烁效果) 之外，属性其他值 blink 实际上很讨厌，应该少用，最好不用。

```CSS
/* 去掉导航条中链接的下划线。 */
nav a {text-decoration:none;}
/* 鼠标悬停状态下加上下划线，则是一种有效的视觉反馈 */
a:hover {text-decoration:underline;}
```

#### 文本对齐

值：left、right、center、justify （左对齐、右对齐、居中对齐和两端对齐）

示例：`p {text-align:right;}`

这些值控制着文本在水平方向对齐的方式。

#### 行高

值：任何数字值（不用指定单位）。

示例：`p {line-height:1.5;}`

CSS 通过 line-height 属性实现了印刷行业中常说的加铅条（[leading](http://www.ituring.com.cn/article/18076)）。铅条在活字排版时代用于在文本行之间增加间距。

line-height 增加的空白就像外边距一样，较大的标题（如 h1 和 h2）往往有较大的默认行高。

如果想把标题较大的空白去掉，那就只能把文本的行高设定为比字体高度（就是字体大小）还要小，比如设定为小于 1 的值。

以复合值的形式把 font-size 和 line-height 值写在一块，比如：`div#intro {font:1.2em/1.4 helvetica, arial, sans-serif;} ` [行高就是字体大小 1.2em 的 1.4 倍]

在设定行高时如果使用了绝对单位（如像素），那将来增大字体有可能导致行与行之间重叠。

#### 文本转换

值：none、uppercase、lowercase、capitalize。(默认,大写，小写，首字母大写)

示例：p {text-transform:capitalize;}

text-transform 属性用于转换元素中文本的大小写，它可以设定英文文本首字母大写、全部字母大写和全部字母小写。

实现小型大写字母的首字母放大效果，可以再加上 `font-variant:small-caps`

#### 垂直对齐

值：任意长度值以及 sub、super、top、middle、bottom 等。

示例：`span {vertical-align:60%;}`

vertical-align 以基线为参照上下移动文本，但这个属性只影响行内元素。

vertical-align 属性最常用于公式或化学分子式中的上标和下标，比如水的化学表示，或者用于文本中脚注的角标，比如把星号变成上角标。

事例HTML：

```HTML
<style>
p.custom sub {font-size:60%; vertical-align:-.4em;}
p.custom sup {font-size:65%; vertical-align:.65em;}
p.customsmall {font-size:.8em; vertical-align:1em;}
</style>
<h4>Default <code>sub</code> and <code>sup</code> styles</h4>
<p>Enjoy mountain spring H<sub>2</sub>O. It’s 10<sup>5</sup> times better than tap<sup>&dagger;</sup> water!</p>

<p class="customsmall"><sup>&dagger;</sup><em>This means water provided
  through a municipal distribution system</em></p>
<h4>Custom <code>sub</code> and <code>sup</code> styles</h4>
<p class="custom">Enjoy mountain spring H<sub>2</sub>O. It’s 10<sup>5</sup> times better than tap<sup>&dagger;</sup> water!</p>
<p class="customsmall"><sup>&dagger;</sup><em>This means water provided
  through a municipal distribution system</em></p>
```

### Web 字体大揭秘

使用@font-face 规则在网页中可嵌入下载字体。

\@font-face 规则为设计师提供了系统自带字体以外的广泛选择。

设定 Web 字体的方式有以下三种

- 使用 Google Web Fonts 或 Adobe 的 Typekit 等公共字体库。
- 使用事先打好包的@font-face 包。
- 使用 Font Squirrel 用你自己的字体生成@font-face 包

#### 公共字体库

- Google [Web Fonts](https://fonts.google.com/)
  - 引用方式,如：`<link href='http://fonts.googleapis.com/css?family=Anton|Niconne|Prata' rel='stylesheet' type='text/css'> `
  - 应用方式:如：`h3 {font: 20px "Prata", serif;}`
- Adobe [Typekit](https://typekit.com/)

#### 打包的@font-face包

可以自己的网站或第三方 Web 服务器下载到相应的字体。

[Font Squirrel](http://www.fontsquirrel.com)提供了很多现成的字体包,
每个字体包中都包含所有必要格式的字体和为每款浏览器提供正确格式的 CSS 代码.

用法事例：

```CSS
@font-face {
 /*这就是将来在字体栈中引用的字体族的名字*/
 font-family:'UbuntuTitlingBold';
 src: url('UbuntuTitling-Bold-webfont.eot');
 src: url('UbuntuTitling-Bold-webfont.eot?#iefix')
 format('embedded-opentype'),
 url('UbuntuTitling-Bold-webfont.woff')
 format('woff'),
 url('UbuntuTitling-Bold-webfont.ttf')
 format('truetype'),
 url('UbuntuTitling-Bold-webfont.svg#UbuntuTitlingBold') format('svg');
 font-weight: normal;
 font-style: normal;
}
```

Web 专家 Paul Irish 写过一个跨浏览器@font-face 的“笑脸版”，
可以保证用户机器中万一安装了同名字体时也不会混淆，详细内容参考这篇文章：[font-face](http://paulirish.com/2009/bulletproof-font-face-implementation-syntax/)

#### 生成@font-face包

希望在自己的网页中使用一种特殊字体，比如客户自己公司指定了一种字体，必须用在网站和设计中。
今天，只要你获得了把该字体转换为 Web 字体使用的授权（请查看许可协议或联系字体设计商），
就可以使用 Font Squirrel 的[转换程序](http://www.fontsquirrel.com/fontface/generator)把它转换成@font-face 字体包。

如果想深入理解@font-face 规则，参考 Tim Brown 的博客文章“[How to use
@font-face](http://nicewebtype.com/notes/2009/10/30/how-to-use-css-font-face/)”。

### 文字版式

文字排版讲求匀称，一般是由看不见的网格，框定页面文字的走向和布局。
匀称的版式可以增强页面的可读性。

#### 简单的文本布局

比如：

```HTML
<article>
 <h1>CSS</h1>
 <p>CSS stands for Cascading Style Sheets. CSS controls the presentational
 aspects of your Web pages.</p>
 <h2>Block-Level Elements</h2>
 <p>Block-level elements stack down the page. They include:</p>
 <ul>
   <li><code>header</code></li>
   <li><code>section</code></li>
   <li><code>h1, h2, etc.</code></li>
 </ul>
 <h2>Inline Elements</h2>
 <p>Inline elements sit next to each other, if there is room. They include:</p>
 <ul>
   <li><code>img</code></li>
   <li><code>a</code></li>
   <li><code>em</code></li>
 </ul>
 <blockquote>
    <q>Typography maketh the Web site.</q><cite>CWS</cite>
 </blockquote>
</article>
```

设定样式,首先，去掉元素的外边距，设定主字体大小，为包含所有文本元素的 article 应用样式，从视觉上突出它作为容器的角色，然后将它在页面上居中。

```CSS
/*删除所有元素的外边距*/
* {margin:0; padding:0;}
/*设定主字体族和字体大小*/
body {font:1.0em helvetica, arial, sans-serif;}
/*居中显示盒子*/
article {width:500px; margin:20px auto; padding:20px; border:2px solid #999;}
/* 删除默认的外边距显著减少了内容的高度 */
```

接下来，需要巧妙地安排一下元素间的垂直距离。
另外，去掉默认外边距后列表项目的符号也跑到了外面，这里一块儿修复。

```css
/*标题周围的空白*/
h1, h2, h3, h4, h5, h6 {line-height:1.15em; margin-bottom:.1em;}
/*文本元素周围的空白*/
p, ul, blockquote {line-height:1.15em; margin-bottom:.75em;}
/*缩进列表*/
ul {margin-left:32px;}
```
以上样式把所有元素的行高都缩小,
因为 line-height 会平均分布在文本上下，并且只想通过下外边距在每个元素下方添加空白。
同时，还留出少量行高，以防段落（和跨行的标题）中相邻的行紧挨上。

最后，让各级标题也更均衡一些，保证较大的标题突出，最小的标题也不至于不明显，同时也增大 code 元素的字体。

```css
/*调整标题文本*/
h1 {font-size:1.9em;}
h2 {font-size:1.6em;}
h3 {font-size:1.4em;}
h4 {font-size:1.2em;}
h5 {font-size:1em;}
h6 {font-size:.9em;}
/*调整段落文本*/
p {font-size:.9em;}
/*调整代码文本（默认值太小了）*/
code {font-size:1.3em;}
```

标题和代码都加大了，而且页面也更有层次感

#### 基于网格排版

借助网格可以保证布局匀称，同时让页面看起来也很流畅

下面的例子中，基于垂直的 18 像素网格来规划布局，并让页面中的每一个元素都按网格线对齐。
可以临时在 body元素的背景上添加一张图片，让它为整个页面生成辅助线。

```css
/*添加网格线*/
body {background-image:url(images/grid_18px.png);padding-top:22px; }
```

CSS规则

```css
/*去掉所有元素的内边距和外边距*/
* {margin:0; padding:0;}
body {
 /*添加网格背景*/
 background-image:url(images/grid_18px.png);
 /*设定字体*/
 font:100% helvetica, arial, sans-serif;
 /*加宽左右外边距，得到一栏的雏形*/
 margin:0 40px 0;
}
p {
 /*设定字体大小*/
 font-size:13px;
 /*将行高设定为等于网格高*/
 line-height:18px;
}
```

这里把文本的 line-height 设定为网格间的距离——18 像素。
在去掉默认外边距和内边距的情况下，这样就可以确保每一行都相距 18 像素.

再给容器 body 元素添加 4 像素的内边距，以便把元素向下推到文本基线与网格对齐的位置。
只要让第一个元素与网格对齐，其他元素就都能对齐了。
实际上，给 body上方添加了 22 像素（4+18）的内边距，

```css
body {
  background-image: url(images/grid_18px.png);
  padding-top:22px;
}

p {
 /*设定字体大小*/
 font-size:13px;
 /*把行高设定为等于网格高度*/
 line-height:18px;
 margin-bottom:18px;
}
/*这条声明恰好能在每个段落之间加上一个空行。
再加上一段文本，就能更清楚地看这两处修改的效果了*/
```

现在，文本与网格对齐了，段落之间的间距也合适了。

接着要设定其他文本元素的字体大小。
首先把 h3 设定为 18 像素，而为了让它恰好在网站中占一行，
必须得把它的 line-height 也设定为 18 像素。

```css
h3 {font-size:18px; line-height:18px;}
```

纠正h3字体过大的问题.

```CSS
h3 {
 font-size:18px;
 line-height:18px;
 margin-top:-2px;
 margin-bottom:2px;
}
```

上方的负外边距把文本向上拉，下方同样数量的正外边距用来抵消它，保证后面元素的位置不受影响

还需要一种类似技巧来对齐比网格高的元素（通常是标题）。
为此，要添加一个24 像素的 h1 元素。
显然，24 像素的文本占据的空间比一行网格要高，
因此给它设定的 line-height 是 36 像素，也就是两行网格的高度。
然后，就是把 h1 元素放到它应该出现的地方——页面的开头。

```css
h1 {font-size:24px; line-height:36px;}
```

占两行网格的大标题看起来不太舒服。
如果把它移动到下方最近的线上，那么其字母下伸部分就会接触到段落文本，所以我要把它向上移动。
经过一番试错，把它向上移动 13 像素.

```css
h1 {
 margin-top:-13px;
 margin-bottom:13px;
}
```
再加几个不同字体大小的标题、一个无序列表和一个blockquote 元素。看一看把网格去掉之后页面是什么样子。

```HTML
<style>
h2 {font-size: 18px;line-height: 18px;margin-top: -2px;margin-bottom: 2px;}
h3 {font-size: 16px;line-height: 18px;margin-top: -2px;margin-bottom: 2px;}
ul {margin-bottom: 18px;}
li {font-size: 13px;list-style-type: none;padding: 0 20px;line-height: 18px;}
a {color: #777;text-decoration: none;}
blockquote {font-size: 12px;line-height: 18px;padding-top: 2px;margin-bottom: 16px;}
</style>
<h2>Typography is Everywhere</h2>
<ul>
  <li><a href="#">Books and Magazines</a></li>
  <li><a href="#">Posters</a></li>
  <li><a href="#">Apparel</a></li>
  <li><a href="#">Graffiti</a></li>
  <li><a href="#">&#8230;everywhere you look!</a></li>
</ul>
<blockquote>
  <q>Typography is what language looks like.</q> <cite>Ellen Lupton</cite>
</blockquote>

<h3>Type for Every Use</h3>
<p>Prose fiction, non-fiction, editorial, educational, religious, scientific, spiritual and commercial writing all have differing characteristics and requirements of appropriate typefaces and fonts.</p>
<h3>Type over Time</h3>
<p>For historic material established text typefaces are frequently chosen according to a scheme of historical genre acquired by a long process of accretion, with considerable overlap between historical periods.</p>

```

。从技术角度讲，如果你
基于网格为一个网站设计了版式，而后将其交给了其他人维护，那这个网站的版式
就能始终保持一致，无论页面中包含什么元素，以及以什么顺序包含这些元素。

#### 经典的排版练习

节选 The Hound of the Baskervilles（《巴斯克维尔庄园的猎犬 》）
中的部分文本（为了示例需要进行了删减）来做一个排版练习.

这个练习将会用到讲过的很多字体和文本属性。
完成这个练习后，就能掌握实现专业排版的很多技术，
包括使用 `HTML 实体`、`调整字母和单词间距`、`首字下沉`、`垂直网格`（这一次是 24 像素）以及`可下载字体`。

```HTML
<!-- 只有两个标题、几个段落和一个块引用 -->

<h2>an excerpt from</h2>
<h1>The Hound of the Baskervilles</h1>
<p>Holmes stretched out his hand for the manuscript and flattened it upon his knee. &ldquo;You will observe, Watson, the alternative use of the long s and the short. It is one of several indications which enabled me to fix the date.&rdquo; At the head was written: &ldquo;Baskerville Hall,&rdquo; and below in large, scrawling figures: &ldquo;1742.&rdquo;</p>

<p>&ldquo;It appears to be a statement of some sort.&rdquo;</p>

<p>&ldquo;Yes&mdash;it is a statement of a certain legend which runs in the Baskerville family.&rdquo;</p>

<blockquote>
    <q>Of the origin of the Hound of the Baskervilles therehave been many statements, yet as I come in a directline from Hugo Baskerville, and as I had the story frommy father&hellip;</q>
</blockquote>

<p>When Dr. Mortimer had finished reading this singular narrative he pushed his spectacles up on his forehead and stared across at Mr. Sherlock Holmes.</p>
```

这段标记包含了几个 HTML 实体，它们代表的是几种标点符号。
其中，有表示 对话开始的左双引号（`&ldquo;`） 、表示对话结束的右双引号（`&rdquo;`）、表示省略的省略号（`&hellip;`）和表示暂停或代替括号的破折号（`&mdash;`）。

HTML实体

以下网站中列出了 HTML 实体：
- [htmlhelp](http://htmlhelp.com/reference/html40/entities/special.html)
  - 既包含 HTML 实体值，也包含实体需要作为::before 和::after 伪元素内容时的十六进制值。
  - 举个例子，如果你想在伪元素中添加十六进制值`&#x201C;`（左双引号），
  - 则需要改写成如下形式：e::before {content:"`\201C`";}就是在数字前面加了一个反斜杠。
  - 相应地，右双引号的十六进制值改写后是`\201D`。
- [stephenmorley](http://code.stephenmorley.org/html-and-css/character-entity-references-cheat-sheet/)

**第一步：设定字体和底层网格**

```CSS
/* 字体 */
@font-face {
 font-family:'CrimsonRoman';
 src: url('fonts/Crimson-fontfacekit/Crimson-Roman-webfont.eot');
 src: url('fonts/Crimson-fontfacekit/Crimson-Roman-webfont.eot?#iefix') format('embedded-opentype'),
 url('fonts/Crimson-fontfacekit/Crimson-Roman-webfont.woff') format('woff'),
 url('fonts/Crimson-fontfacekit/Crimson-Roman-webfont.ttf') format('truetype'),
 url('fonts/Crimson-fontfacekit/Crimson-Roman-webfont.svg#CrimsonRoman') format('svg');
 font-weight: normal;
 font-style: normal;
}
/* 去掉所有外边距和内边距 */
* {margin:0; padding:0;}
/* 设定了主字体，又添加了左、右外边距，还为对齐文本临时添加了网格 */
body {
 font-family:"CrimsonRoman", georgia, times, serif;
 background-color:#fff;
 margin:0 10% 0;
 background-image:url(images/grid_24px.png);
}
```

**第二步：设计标题**

从上到下，对齐页面中的每一个元素。
第一行的副标题应该与第二行的主标题形成对比，因为主标题要使用手写字体，
所以副标题就设定成间距较宽的小型大写字母。

```css
/* 上边距调整为19px */
body{margin:19px 10% 0;}
/* 调整栏高，粗细，对齐方式，大小写，字间隔，单词间隔 */
h2 {font-size:18px;
   line-height:24px;
   font-weight:bold;
   text-align:center;
   font-variant:small-caps;
   word-spacing:.5em;
   letter-spacing:.6em;
}
```

排版资源：

- [ilovetypography](http://ilovetypography.com/) 可以跟着设计师 John Boardley 一起深思，欣赏每一页中别具一格的排版。
- [Thinking with Type](http://www.thinkingwithtype.com/) 是 Thinking with Type 一书的网站，作者 Ellen Lupton。网站中展示了很多漂亮又经典的版式，还包含一些字体及字体族的信息。
- [webtypography](http://webtypography.net/)这个站点自称为 The Elements of Typographic Style Applied to the Web—A practical guide to web typography。跟随网站的目录，可以找到各种常用的排版知识和技巧。

接下来，找到一种名为 Pinyon 的手写体，这种字体与主标题挺配的.

`<link href='http://fonts.googleapis.com/css?family=Pinyon+Script' rel='stylesheet' type='text/css'> `

```css
h1 {
 font-size:60px;
 line-height:96px;
 font-family:"Pinyon Script", cursive;
 margin:4px 0 -4px;
 text-align:center;
 font-weight:normal;
 position:relative;
}
```

**第三步：设计段落和引用**

```css
/* 设定它的字体大小,以及行高 */
p {font-size:18px; line-height:24px;}
```

blockquote 中的文本包含在一个行内元素 q（quote）中，这个元素的默认样式是在文本开头和末尾加上引号。

在此，缩进 blockquote，但在其 q子元素上设定字体大小和行高，因为它才是包含文本的元素：

```css
blockquote {margin:0px 20%;}
q {font-size:18px; font-style:italic; line-height:24px;}
```

缩进引用并将文本变成斜体为页面增加了变化。另外，在 blockquote就位后，它后面的段落自然也就与网格对齐了。

**第四步：首字下沉效果**

第一段添加一个独特的首字下沉效果。
所谓首字下沉，就是将段落开头的第一个字母变大，
然后根据该字母与段落首行的位置关系，又可以分几种不同的风格。

让字母的顶部与段落首行顶部对齐，让字母的底部与段落第三行的基线对齐。

选择 h1 标题后面第一个段落的第一个字母，
而组合使用紧邻同胞选择符+和::first-letter 伪元素可以做到。

选择了第一个字母后，再增大字体并浮动它：

```css
h1 + p::first-letter {
 font-family:times, serif;
 font-size: 90px;
 float:left;
 border:1px solid;
}
```

首字母增大了，但位置不对。设定这个伪元素的line-height，让它的盒子能包含首字母。并添加一点内边距，包括3px的右边距。

*把 line-height 设定为小于 1 的值，以便元素盒子紧紧包住首字母，而不会强迫段落第四行也绕排。*

```css
h1 + p::first-letter {
 font-family:times, serif;
 font-size:90px;
 float:left;
 line-height:.65;
 border:1px solid;
 padding:.085em 3px 0 0;
}
```

**第五步：设计第一行**

首字母下沉效果做完了。可是希望大号首字母到小号正文之间有一个过渡，所以需要把段落第一行的文本变成小型大写字母。

```css
/* 紧邻同胞选择符，组合::first-line 伪元素，实现了第一行字形的转换 */
h1 + p::first-line {
 font-variant:small-caps;
 letter-spacing:.15em;
}
```

使用伪元素而不是额外加标签的好处在于，当行的长度改变时，大写字母的效果会随之扩展。

**第六步：最后的修饰**

段落之间没有足够的间距，让人很难看出它们的开头在哪里。

为了与这本书的版式保持一致，我们不给段落之间加空白，而是缩进跟在其他段落后面的每一段，作为一组段落起头的一段不缩进。

此外，引用内容两端的引号也太难看，所以要在<q>标签上应用::before 和::after 伪元素，插入 Crimson 字体的引号。
最后，再从 body元素中去掉网格背景

```css
/*只缩进跟在段落后面的段落*/
p + p {text-indent:14px;}
/*引用内容前面的引号*/
q::before {content:"\201C"}
/*引用内容后面的引号*/
q::after {content:"\201D"}
```

使用::before 和::after 伪元素给引用内容添加引号时使用的是十六进制值。
不能给 content 属性设定常规的 HTML 实体，只能使用十六进制实体值，而且只能是改写后的形式。

最终样式:

![fontgraph](img/fontgraph.png)
