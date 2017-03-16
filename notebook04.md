
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


















a
