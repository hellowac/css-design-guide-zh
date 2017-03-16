
## 定位元素

盒模型: 浏览器为页面中的每个 HTML 元素生成的矩形盒子.

这些盒子们都要按照`可见版式模型`（visual formatting model）在页面上排布。

可见的页面版式主要由三个属性控制：position 属性、display 属性和 float 属性。

position 属性控制页面上元素间的 位置关系.
display 属性控制元素是 堆叠、并排，还是根本不在页面上出现.
float 属性提供 控制的方式，以便把元素组成成多栏布局.


### 理解盒模型

每一个元素都会在页面上生成一个盒子,因此，HTML页面实际上就是由一堆盒子组成的。

默认情况下，每个盒子的边框不可见，背景也是透明的，所以我们不能直接看到页面中盒子的结构。 (使用 Web Developer 工具条,可以方便的看见盒子的边框和背景)

每个元素盒子的属性可以分成三组：

1. **边框**（border）。可以设置边框的宽窄、样式和颜色。
2. **内边距**（padding）。可以设置盒子内容区与边框的间距。
3. **外边距**（margin）。可以设置盒子与相邻元素的间距。

一个盒子有 4 条边，因此与边框、内边距和外边距相关的属性也各有 4 个，分别是上（top）、右（right）、下（bottom）、左（left）。

官网文档：[box](https://www.w3.org/TR/REC-CSS2/box.html)

可以用总共 12 个属性分别为 4 条边的边框、外边距和内边距指定宽度，但 CSS也提供了简写属性。

```
CSS 为边框、内边距和外边距分别规定了简写属性,通过一条声明就可以完成设定.
在每个简写声明中，属性值的顺序都是上、右、下、左。想象一下顺时针旋转就记住了。

如: {margin-top:5px; margin-right:10px; margin-bottom:12px; margin-left:8px;}
简写成:{margin:5px 10px 12px 8px;}
注意，4 个值之间有空格，但不能是其他分隔符（比如逗号之类的）。


{margin:12px 10px 6px;}
不用把 4 值全都写出来——如果哪个值没有写，那就使用对边的值，由于没有写最后一个值（左边的值），所以左边就会使用右边的值，即 10px

{margin:12px 10px;}
只写了两个值，上和右，因此缺少的下和左就会被设定为 12px 和 10px。

{margin:12px;}
如果只写一个值，那么 4 个边都取这个值。

{margin:0 0 2px 4px;}
绕开上和右，只给下和左设定值，

每个盒子的属性也分三种粒度(宽度，样式，颜色)。

1. 全部 3 个属性，全部 4 条边
 {border:2px dashed red;}

2. 1 个属性，全部 4 条边
  {border-style:dashed;}

3. 1 个属性，1 条边
 {border-left-style:dashed;}

{border:4px solid red;} /* 先给 4 条边设置相同的样式 */
{border-left-width:1px;} /* 修改左边框宽度 */
{border-right:none;} /* 移除右边框 */
其他属性也都有这三级粒度，例如 padding 和 border-radius 等
```

#### 盒子边框

边框（border）有 3 个相关属性。

- 宽度（border-width）。可以使用 thin、medium 和 thick 等文本值，也可以使用除百分比和负值之外的任何绝对值。
- 样式（border-style）。有 none、hidden、dotted、dashed、solid、double、groove、ridge、inset 和 outset 等文本值。
- 颜色（border-color）。可以使用任意颜色值，包括 RGB、HSL、十六进制颜色值和颜色关键字。

```CSS
p.warning {border:solid #F33;}
/* 任何带有 warning 类的段落都会带上一个吸引眼球的、4 像素宽的红色实心边框 */
p.warning {border-width:4px 1px 1px 4px;}
/* 把右边框和下边框变窄一些 */
```

默认情况下，边框的三个相关属性的值分别为 border-width:medium;、border-style:none;、border-color:black;。

由于 border-style 的默认值是 none，所以不会显示盒子的边框.

```CSS
p {border:solid 1px;}
/* 这样设定就边框出现了.这里把边框宽度由默认的 3像素变窄为 1像素，从而把边框对布局宽度和高度的影响降到最低。 */
```

#### 盒子内边距

内边距是盒子内容区与盒子边框之间的距离。

```CSS
p {font:16px helvetica, sans-serif; width:220px; border:2px solid red; background-color:#caebff;}
/* 在没有设定内边距的情况下，内容紧挨着边框 */

p {padding: 10px;}
/* 给元素添加一点内边距,看着会舒服点。 */
```

由于内边距在盒子的内部，所以它也会取得盒子的背景。

内边距实际加在了声明的盒子宽度之上。

#### 盒子外边距

与边框和内边距相比，盒子的外边距要复杂一些。

学会控制元素周围的外边距是布局的重要技能

**中和外边距和内边距**

```
推荐大家把下面这条规则作为样式表的第一条规则：
* {margin:0; padding:0;}

这条规则把所有元素默认的外边距和内边距都设定为零。
把这条规则放到样式表里后，所有默认的外边距和内边距都会消失。

然后，你可以为那些真正需要外边距的元素再添加外边距。

不同浏览器默认的内边距和外边距也不一样，特别是对表单和列表等复合元素。
在这种情况下，用前面那条规则“中和”默认值，然后再根据需要添加，则会在各浏览器上获得一致的效果。

我在自己的项目中使用了 Eric Meyer 写的重置样式表 reset.css。
这个样式表不仅重置了外边距和内边距，还对很多元素在跨浏览器显示时的外观进行了标准化。
至于 Eric 为什么要写一个涉及面如此之广的重置样式表，
可以参考他的文章 http://meyerweb.com/eric/thoughts/2007/04/18/reset-reasoning，reset.css 的下载地址是 http://meyerweb.com/eric/tools/css/reset。
```

#### 叠加外边距

垂直方向上的外边距会叠加。

上下外边距相遇时，它们就会相互重叠，直至一个外边距碰到另一个元素的边框,较宽的外边距决定两个元素最终离多远.这个过程就叫外边距叠加。

#### 外边距的单位

根据经验，为文本元素设置外边距时通常需要混合使用不同的单位。

比如说，一个段落的左、右外边距可以使用像素，以便该段文本始终与包含元素边界保持固定间距，不受字号变大或变小的影响。

而对于上、下外边距，以 em 为单位则可以让段间距随字号变化而相应增大或缩小，比如：

```css
/*这里使用了简写属性把上、下外边距设置为.75em，把左、右外边距设置为 30 像素*/
p {font-size:1em; margin:.75em 30px;}
```

这样，段落的垂直间距始终会保持为字体高度的四分之三（上下外边距都是.75em，叠加后还是.75em）。

如果用户增大了字号，那么不仅段落中的文本会变大，段间距也会成比例变大。

这样，页面的整体布局就会比较协调一致。与此同时，使用像素单位的左、右外边距不会改变。


### 盒子有多大

**没有宽度的盒子**

所谓“没有宽度”就是指没有显式地设置元素的 width 属性.

如果不设置块级元素的 width 属性，那么这个属性的默认值是 auto，结果会让元素的宽度扩展到与父元素同宽。

**盒模型结论一**：没有（就是没有设置 width 的）宽度的元素始终会扩展到填满其父元素的宽度为止。添加水平边框、内边距和外边距，会导致内容宽度减少，减少量等于水平边框、内边距和外边距的和。

**有宽度的盒子**

**盒模型结论二**：为设定了宽度的盒子添加边框、内边距和外边距，会导致盒子扩展得更宽。实际上，盒子的 width 属性设定的只是盒子内容区的宽度，而非盒子要占据的水平宽度。

这两种盒子所表现出来的完全不同的行为，对将来构建多栏布局具有重要的启示.

因为在多栏布局中，每一栏都必须时刻维护自己的宽度。

“浮动布局”，在列宽由于边框、内边距和边距被修改而意外加宽的情况下，会出现显示错误。

*CSS3 新增了一个 box-sizing 属性，通过它可以将有宽度的盒子也设定成具有默认的auto 状态下的行为。但只有最新版本的浏览器才支持该属性.*

设定了元素的 width 属性后，再给元素添加边框、内边距和外边距，元素的行为与默认的 auto 状态下会有截然不同的表现。

### 浮动与清除

浮动和清除是用来组织页面布局的又一柄利剑，这柄剑的剑刃就是 float 和 clear属性。

浮动，意思就是把元素从 常规文档流(从上到下，但不从左至右。块元素依次展开) 中拿出来。脱离了常规文档流之后，原来紧跟其后的元素就会在空间允许的情况下，向上提升到与浮动元素平起平坐。

一是可以实现传统出版物上那种文字绕排图片的效果，

二是可以让原来上下堆叠的块级元素，变成左右并列，从而实现布局中的分栏。

如果浮动元素后面有两个段落，而你只想让第一段与浮动元素并列（就算旁边还能放下第二段，也不想让它上来），怎么办？用 clear 属性来“清除”第二段，然后它就乖乖地呆在浮动元素下面了。

```
影响浮动的因素还有很多，推荐读者看一看Eric Meyer的那本 Cascading Style Sheets2.0 Programmer’s Reference（2006，McGraw-Hill Osborne Media）。
这里摘录 Eric在那本书里写的一句话：“当你浮动一个元素的时候……这些（浮动）规则就好像在说：‘尽量把这个元素往上放，能放多高放多高，直到碰到某个元素的边界为止。’”
即使这本书的出版年份是 2006 年，但它仍然是任何 CSS 高手必备的一本参考书。
这本书涵盖了 CSS 运行机制的方方面面，其中很多在别的书里是找不到的。
```

#### 浮动

CSS 设计 float 属性的主要目的，是为了实现文本绕排图片的效果。然而，这个属性居然也成了创建多栏布局最简单的方式

*CSS3 Multi-column Layout Module 规定了如何用 CSS 定义多栏布局。*

**文本绕排图片**

```HTML
<style>
/*外边距防止图片紧挨文本*/
img {float:left; margin:0 4px 4px 0;}
/*为简明起见，省略了字体声明*/
p {margin:0; border:1px solid red;}
</style>

<img …… />
<p>…the paragraph text…</p>
```

在浮动一张图片或者其他元素时，是在要求浏览器把它往上方推，直到它碰到父元素（也就是 body 元素）的内边界。

后面的段落（带灰色边框）不再认为浮动元素在文档流中位于它的前面了，因而它会占据父元素左上角的位置。

不过，它的内容（文本）会绕开浮动的图片。

*浮动非图片元素时，必须给它设定宽度，否则后果难以预料。图片无所谓，因为它本身有默认的宽度。*

**创建分栏**

在此基础上创建多栏，只要再用一次 float 属性

```css
p {float: left; width: 200px;}
```

同时浮动图片和“有宽度的”段落，会导致段落的文本绕排效果消失，而浮动的段落也会尽可能向左向上移动。

这样，这个段落就构成了紧挨着图片的一栏。

这就是使用 float 属性创建多栏布局的原理。

换句话说，如果几个相邻的元素都具有设定的宽度，都是浮动的，而且水平空间也足以容纳它们，它们就会并列排在一行。

浮动元素位于“文档流外部”，因而它已经不被包含在标记中的父元素之内了。

正因为如此，它对布局可能产生破坏性影响。

#### 围住浮动元素的三种方法

事例HTML：

```HTML
<section>
 <img src="images/rubber_duck2.jpg">
 <p>It's fun to float.</p>
</section>
<footer> Here is the footer element that runs across the bottom of the page.</footer>

<style>
section {border:1px solid blue; margin:0 0 10px 0;}
/*删除默认的上下外边距*/
p {margin 0;}
/*为简明起见，省略了字体声明*/
footer {border:1px solid red;}
</style>
```

应用 `img {float:left;} ` 样式,

标题倒是跑到右边了，可 section 也不再包围浮动元素了，它只包围非浮动的元素。于是，footer 被提了上来，紧挨着前一个块级元素——section。这样是没错儿，可结果呢，不是我们想要的。

**方法一：为父元素添加 overflow:hidden**

为父元素应用 overflow:hidden，以强制它包围浮动元素。

`section{ overflow:hidden;}`

```
overflow:hidden 声明的真正用途是防止包含元素被超大内容撑大。
应用 overflow:hidden 之后，包含元素依然保持其设定的宽度，而超大的子内容则会被容器剪切掉。

除此之外，overflow:hidden 还有另一个作用，即它能可靠地迫使父元素包含其浮动的子元素。
```

**方法二：同时浮动父元素**

应用:`section{float:left; width:100%;} footer{clear:left;}`

浮动 上级元素 以后，不管其子元素是否浮动，它都会紧紧地包围（也称`收缩包裹`）住它的子元素。因此，需要用 width:100%再让 section 与浏览器容器同宽。

为了强制 footer 依然呆在 section 下方，要给它应用 clear:left。被清除的元素不会被提升到浮动元素的旁边。

**方法三：添加非浮动的清除元素**

给父元素的最后添加一个非浮动的子元素，然后清除该子元素的浮动。

由于包含元素(section)一定会包围非浮动的子元素，而且清除浮动会让这个子元素位于浮动元素的下方，因此包含元素一定会包含这个子元素—-以及前面的浮动元素。

在包含元素最后添加子元素作为清除元素的方式有两种。

第一种方式不太理想，也就是简单地在 HTML 标记中添加一个子元素，并给它应用clear 属性。

由于没有默认的样式，不会引入多余空间，div 元素很适合这个目的。

```HTML
<section>
 <img src="images/rubber_duck.jpg">
 <p>It's fun to float.</p>
 <div class="clear_me"></div>     <!-- 清除浮动 -->
</section>
<footer> Here is the footer element…</footer>

<style>
.clear_me {clear:left;}
</style>
```

应用样式 ` `

第二种方式由程序员 Tony Aslett 发明，给 上级元素 添加类并应用如下样式：

```HTML
<section class="clearfix">    <!--上级元素添加类-->
 <img src="images/rubber_duck.jpg">
 <p>It's fun to float.</p>
</section>
<footer> Here is the footer element…</footer>

<style>
.clearfix:after {
 content:".";
 display:block;
 height:0;
 visibility:hidden;
 clear:both;
}
/*
添加了一个清除的包含句点作为非浮动元素（必须得有内容，而句点是最小的内容）。
规则中的其他声明是为了确保这个伪元素没有高度，而且在页面上不可见。

clear:both 意味着 section 中新增的子元素会清除左、右浮动元素（位于左、右浮动元素下方）。
这里当然可以只用 left，但 both 也适用于将来图片 float:right 的情况。
*/
</style>
```

围住浮动的三种方式:

- 为父元素应用 overflow:hidden
- 浮动父元素
- 在父元素内容的末尾添加非浮动元素，可以直接在标记中加，也可以通过给父元素添加 clearfix 类来加（当然，样式表中得需要相应的 clearfix 规则）

这三种方法的使用要因地制宜。

比如，不能在下拉菜单的顶级元素上应用overflow:hidden，否则作为其子元素的下拉菜单就不会显示了。

因为下拉菜单会显示在其父元素区域的外部，而这恰恰是 overflow:hidden 所要阻止的。

再比如，不能对已经靠自动外边距居中的元素使用“浮动父元素”技术，否则它就不会再居中，而是根据浮动值浮动到左边或右边了。

**没有父元素时如何清除**

有时候，在清除某些浮动元素时，不一定正好有那么个父元素可以作为容器来强行包围它们。

此时，最简单的办法就是给一个浮动元素应用 clear:both，强迫它定位在前一个浮动元素下方。

然而，在空间足以容纳多个元素向上浮动时，这个简单的办法未必奏效，我们还得另辟蹊径。

事例HTML：

```HTML
<section>
 <img src="images/rubber_duck3.jpg">
 <p>This text sits next to the image and because the…</p>
 <img src="images/beach_ball.jpg">
 <p>This text is short, so the next image can float up…</p>
 <img src="images/yellow_float.jpg">
 <p>Because the previous image’s text does not…</p>
</section>

<style>
section {width:300px; border:1px solid red;}
img {float:left; margin:0 4px 4px 0;}
/*为简明起见，省略了字体声明*/
p {margin:0 0 5px 0;}
</style>
```

由于每一对儿图片/段落都没有包含元素，在此就无法使用前面讨论的“强制父元素包围”的战术。不过，照样可以使用 clearfix 规则呀！

```HTML
<section>
 <img src="images/rubber_duck3.jpg">
 <p class="clearfix">This text sits next to the image and because the…</p>
 <img src="images/beach_ball.jpg">
 <p class="clearfix">This text is short, so the next image can float up…</p>
 <img src="images/yellow_float.jpg">
 <p class="clearfix">Because the previous image’s text does not…</p>
</section>
<style>
section {
  width: 300px;
  border: 1px solid red;
}

img {
  float: left;
  margin: 0 4px 4px 0;
}

p {
  font-family: helvetica, arial, sans-serif;
  margin: 0 0 5px 0;
}

.clearfix::after {
  content: ".";
  display: block;
  height: 0;
  visibility: hidden;
  clear: both;
}
</style>
```

### 定位

CSS 布局的核心是 position 属性，对元素盒子应用这个属性，可以相对于它在常规文档流中的位置重新定位。

position 属性有 4 个值：static、relative、absolute、fixed，默认值为 static。

事例html：

```HTML
<style>
body {background-color:#caebff;}
p {font-size:24px; color:#555; font-family:Helvetica, Arial, sans-serif; background-color:#ccc; margin:10px 0;}
p#specialpara {color: red; background:#fff;}
</style>
<p>First Paragraph</p>
<p>Second Paragraph</p>
<p id="specialpara">Third Paragraph (with ID)</p>
<p>Fourth Paragraph</p>
```

#### 静态定位

静态定位下的块级元素会在默认文档流中上下堆叠

在静态定位的情况下，每个元素在处在常规文档流中。
它们都是块级元素，所以就会在页面中自上而下地堆叠起来。

要突破 static 定位提供的这种按顺序布局元素的方式，
必须把盒子的 position 属性改为其他三个值。

#### 相对定位

把第三段的 position 属性设置为 relative。
即只设置了它的定位方式是“相对定位”。
相对的是它原来在文档流中的位置（或者默认位置）。
可以使用 top、right、bottom 和 left 属性来改变它的位置。
但多数情况下，只用 top 和 left 就可以实现想要的效果。

```CSS
p#specialpara {position:relative; top:25px; left:30px;}
/*可以给 top 和 left 属性设定负值，把元素向上、向左移动。*/
```
第三段与它在文档流中的默认位置相比，向下移动了 25 像素，向右移动了30 像素。
相当于它把自己从原来的包含元素（body）中挣脱出来了，而且有一部分还跑到了屏幕之外。
要注意，除了这个元素自己相对于原始位置挪动了一下之外，页面没有发生任何变化。
换句话说，这个元素原来占据的空间没有动，其他元素也没动。

#### 绝对定位

绝对定位跟静态定位和相对定位比，绝对不一样。
因为绝对定位会把元素彻底从文档流中拿出来。

```CSS
p#specialpara {position:absolute; top:25px; left:30px;}
```

绝对定位下，元素从文档流中被“连根拔起”，然后再相对于其他元素（在这里，是默认的定位上下文 body）定位

元素之前占据的空间被“回收了”。
这说明，绝对定位的元素完全脱离了常规文档流，它现在是相对于顶级元素 body 在定位。
而这自然而然就引出了一个关于定位的重要概念：`定位上下文`。

关于定位上下文，首先要知道绝对定位元素默认的定位上下文是 body 元素。
通过 top 和 left 设定的偏移值，决定了元素相对于 body 元素（标记层次中的祖先容器），
而不是相对于它在文档流中的位置偏移多远[这一点与相对定位的元素不同]。

由于绝对定位元素的定位上下文是 body，所以在页面滚动的时候，
为了维护与 body元素的相对位置关系，它也会相应地移动。

#### 固定定位

从完全移出文档流的角度说，固定定位与绝对定位类似。

```css
p#specialpara {position:fixed; top:30px; left:20px;}
```

不同之处在于，固定定位元素的定位上下文是视口（浏览器窗口或手持设备的屏幕），
因此它不会随页面滚动而移动。

固定定位并不常用，最常见的情况是用它创建不随页面滚动而移动的导航元素。

#### 定位上下文

把元素的 position 属性设定为 relative、absolute 或 fixed 后，
继而可以使用 top、right、bottom 和 left 属性，相对于 另一个元素 移动该元素的位置。
这里的“另一个元素”，就是该元素的定位上下文。

绝对定位元素默认的定位上下文是 body。是因为body 是标记中所有元素唯一的祖先元素。

而实际上，绝对定位元素的任何祖先元素都可以成为它的定位上下文，
只要你把相应祖先元素的 position 设定为 relative 即可。

事例HTML：

```HTML
<body>
 <div id="outer">
 <div id="inner">This is text…</div>
 </div>
</body>
<style>
div#outer {position:relative; width:250px; margin:50px 40px; border-top:3px
 solid red;}
div#inner {position:absolute; top:10px; left:20px; background:#ccc;}
</style>
```

内外部 div 默认都是静态定位，它们之间不存在谁是谁的定位上下文这个问题。
在常规文档流中，由于外部div 没有内容，内部 div 就会跟它共享相同的起点。
只有将元素的 position 属性设定为 relative、absolute 或 fixed，
这个元素的 top、right、bottom 和 left 属性才会起作用。

```
事实上,只要把元素的外边距和内边距设定好，多数情况下只用静态定位就足以实现页面布局了。
很多刚开始接触 CSS 的初学者都会错误地设定 position 属性，
最终才发现从文档流中挪出来的这些元素一点也不好控制。
因此，除非真需要那么做，否则不要轻易修改元素默认的 position 属性。
```

#### 显示属性

正如所有元素都有 position 属性，所有元素也都有 display 属性。
尽管 display 属性的值有很多，但大多数元素 display 属性的默认值不是 block，就是 inline。

再讲一讲块级元素与行内元素的区别：

- **块级元素**：比如段落、标题、列表等，在浏览器中上下堆叠显示。
- **行内元素**：比如 a、span 和 img，在浏览器中左右并排显示，只有前一行没有空间时才会显示到下一行。

转换块级元素和行级元素:

```CSS
/*默认为 block*/
p {display:inline;}
/*默认为 inline*/
a {display:block;}
```

做CSS 下拉菜单的时候，就会用到这个技巧。

display 属性还有一个值 none。设置该元素及所有包含在其中的元素，都不会在页面中显示。
原先占据的所有空间也都会被“回收”，就好像相关的标记根本不存在一样。

与此相对的visibility属性，这个属性最常用的两个相对的值是 visible（默认值）和 hidden。
把值设定为 hidden时，元素会隐藏，但占据的页面空间仍然“虚位以待”。

总结:

display属性：常用的block、inline、none属性
visibility属性：常用的visible、hidden属性.

#### 背景

CSS 里，每个元素盒子都可以想象成由两个图层组成。
元素的前景层包含内容（如文本或图片）和边框，
元素的背景层可以用实色填充（使用 background-color 属性），
也可以包含任意多个背景图片（使用background-image 属性），
背景图片叠加在背景颜色之上。

**CSS背景属性**

- background-color
- background-image
- background-repeat
- background-position
- background-size
- background-attachment
- background（简写属性）
- background-clip、background-origin、background-break（目前尚未得到广泛支持）

**背景颜色**

通过 background-color 可以设定元素的颜色。

例如:

```HTML
<style>
body {background-color:#caebff;}
p {/*盒子布局样式*/
 font-family:helvetica, arial, sans-serif; font-size:18px;
 width:350px; margin:20px auto; padding:10px;
 /*这个例子中讨论背景和前景样式*/
 background-color:#fff; color:#666; border:4px solid;
}
</style>
<p>This text and t...</p>
```

作用范围，前景色会影响元素的内容和边框。
当然，有一个前提条件，就是在使用 border 设定边框的样式和宽度，而没有设定边框颜色（或者没有使用 border-color 单独设定边框颜色）的情况下，
边框会使用 color 属性设定的字体颜色。
默认颜色是黑色。
如果想让边框的颜色有别于文本，就需要单独设定。

**背景图片**


例如:

```HTML
<style>
  body {
    background-color: #43f3f3;
  }
  p {
    background-color: #FFF;
    background-image: url(images/blue_circle.png)
  }
</style>
<p>This text and t...</p>
```

默认情况下背景图片会以元素左上角为起点，沿水平和垂直方向重复出现，最终填满整个背景区域。

注意，指定背景图片来源的方式要这样：

`background-image:url(图片路径/图片文件名)` 图片地址两边不用加引号，当然加了也没问题。

要改变默认的 水平和垂直重复 效果，可以修改 background-repeat 属性；

要改变背景图片的 起点，可以修改 background-position 属性。

**背景重复**

控制背景重复方式的 background-repeat 属性有 4 个值:repeat、repeat-x、repeat-y、no-repeat。

- repeat: 水平和垂直方向都重复.
- repeat-x: 水平方向重复.
- repeat-y: 垂直方向上重复.
- no-repeat: 任何方向上都不重复.

CSS3 还规定另外两个值（但尚未得到浏览器支持），以控制背景图片重复确切的次数，即所有图片都是完整的，不会出现半张图片的现象。

- background-repeat:round：为确保图片不被剪切，通过调整图片大小来适应背景区域。
- background-repeat:space: 为确保图片不被剪切，通过在图片间添加空白来适应背景区域。

**背景位置**

background-position 属性，是所有背景属性中最复杂的.
属性有5个关键字值，分别是top、left、bottom、right和center，

关键字中的任意两个组合起来都可以作为该属性的值。

比如，top right 表示把图片放在元素的右上角位置，center center 把图片放在元素的中心位置。

```CSS3
/*center center 的简化写法*/
p#center {background-position:center;}
/* 相当于 background-position:center cetner */
```

用百分比来设定位置，并且不重复。
```HTML
<p>
A centered background image!
</p>
<style>
div {
 height:150px;
 width:250px;
 border:2px solid #aaa;
 margin:20px auto;
 background-image:url(images/turq_spiral_150.png);
 background-repeat:no-repeat;
 background-position:50% 50%;
}
</style>
```

文本也居中的办法:

1. line-height 设定成了元素的高度
2. text-align 设定为 center

**背景位置的值**

```
设定背景位置时可以使用三种值：关键字、百分比、绝对或相对单位的数值。
可以使用两个值分别设定水平和垂直位置。

关键字指的顺序不重要，left bottom 和 bottom left 意思相同。
为了设定的值在所有浏览器中都有效，最好不要混用关键字值与数字值。

使用数值（比如 40% 30%）时，
第一个值表示水平位置，
第二个值表示垂直位置。
要是只设定一个值，则将其用来设定水平位置，而垂直位置会被设为 center。

在使用 关键字 和 百分比值 的情况下，设定的值同时应用于元素和图片。
换句话说，如果设定了33% 33%，则图片水平 33%的位置与元素水平 33%的位置对齐。
垂直方面也一样。

像素之类的绝对单位数值就不一样了。要是用像素单位来设定位置，
那么图片的左上角会被放在距离元素左上角指定位置的地方。

还可以使用负值。这样就可以把图片的左上角定位到元素外部，从而在元素中只能看到部分图片。
当然，给图片设定足够大的正值，也可以把图片的右下角推到元素外部，从而在元素中也只能看到部分图片。
位于元素外部的那部分图片不会显示。
```

**背景尺寸**

background-size 是 CSS3 规定的属性，这个属性用来控制背景图片的尺寸，可以给它设定的值及含义如下。

- **50%**：缩放图片，使其填充背景区的一半。
- **100px 50px**：把图片调整到 100 像素宽，50 像素高。
- **cover**：拉大图片，使其完全填满背景区；保持宽高比。
- **contain**：缩放图片，使其恰好适合背景区；保持宽高比。

**背景粘附**

background-attachment 属性控制滚动元素内的背景图片是否随元素滚动而移动。
属性的默认值是 scroll，即背景图片随元素移动。
如果改为 fixed，那么背景图片不会随元素滚动而移动。

该属性常用于给 body 元素中心位置添加淡色水印，让水印不随页面滚动而移动。规则:

```CSS
body {
 background-image:url(images/watermark.png);
 background-position:center;
 background-color:#fff;
 background-repeat:no-repeat;
 background-size:contain;
 background-attachment:fixed;
}
```

**简写背景属性**

background 属性可以用来设定所有背景相关的值。

比如，上面的例子可以写成：

`body {background:url(images/watermark.png) center #fff no-repeat contain fixed;}`

声明中少写了哪个属性的值（比如没写 no-repeat），就会使用相应属性的默认值（repeat）

**其他CSS3 背景属性**

- background-clip。控制背景绘制区域的范围，比如可以让背景颜色和背景图片只出现在内容区，而不出现在内边距区域。默认情况下，背景绘制区域是扩展到边框外边界的。
- background-origin。控制背景定位区域的原点，可以设定为元素盒子左上角以外的位置。比如，可以设定以内容区左上角作为原点。
- background-break。 控制分离元素（比如跨越多行的行内盒子）的显示效果。

[Modernizr](https://modernizr.com/)是一个 JavaScript 库,用于检测用户浏览器支持哪些 HTML5 和 CSS3 功能.

**多背景图片**

```css
p {
 height:150px;
 width:348px;
 border:2px solid #aaa;
 margin:20px auto;
 font:24px/150px helvetica, arial, sansserif;
 text-align:center;
 background:
 url(images/turq_spiral.png) 30px -10px no-repeat,
 url(images/pink_spiral.png) 145px 0px no-repeat,
 url(images/gray_spiral.png) 140px -30px no-repeat, #ffbd75;
}
/* 多张图片可以在背景中叠加起来，CSS 规则中先列出的图片在上层  */
```

查看CSS3最新信息，参考[can i use](http://caniuse.com)

**背景渐变**

渐变就是在一定长度内两种或多种颜色之间自然的过渡。

渐变分两种，一种线性渐变，一种放射性渐变。

线性渐变从元素的一端延伸到另一端，
放射性渐变则从元素内一点向四周发散。

事例HTML：

```HTML
<div class='gradient1'></div>
<div class='gradient2'></div>
<div class='gradient3'></div>

<style>
/*为元素盒子添加样式*/
div {
 height:150px;
 width:200px;
 border:1px solid #ccc;
 float:left;
 margin:16px;
}
/*例 1：定义一种开始颜色，一种结束颜色，默认的方向（从下到下） */
.gradient1 {
 background:linear-gradient(#e86a43, #fff);
}
/*例 2：从左到右，left，渐变方向变成了从左到另一端 */
.gradient2 {
 background:linear-gradient(left, #64d1dd, #fff);
}
/*例 3：左上到右下, deg 是“度”, 等于把起点从默认的中上设定到了左上。*/
.gradient3 {
 background:linear-gradient(-45deg, #e86a43, #fff);
}
</style>
```

**1. 渐变点**

渐变点就是渐变方向上的点，可以在这些点上设定颜色和不透明度。

通过设定下一个渐变点的颜色值，就可以控制渐变的效果。

可以添加任意多个渐变点。

渐变点的位置一般使用整个渐变宽度的百分比来表示。

事例：

```css
/*例 1：50%处有一个渐变点*/
.gradient1 {
  background:linear-gradient(#64d1dd, #fff 50%, #64d1dd);
}
/*例 2：20%和 80%处有两个渐变点*/
.gradient2 {
   background:linear-gradient(#e86a43 20%, #fff 50%, #e86a43 80%);
}
/*例 3：25%、50%、75%处有三个渐变点*/
.gradient3 {
  background:linear-gradient(#64d1dd, #fff 25%, #64d1dd 50%, #fff 75%, #64d1dd);
}
/*例 4：为同一个渐变点设定两种颜色可以得到突变效果*/
.gradient4 {
  background:linear-gradient(#e86a43, #fff 25%, #64d1dd 25%, #64d1dd 75%, #fff 75%, #e86a43);
}
```

**2. 放射性渐变**

放射性渐变比线性渐变复杂那么一点点，因为可用的控制点多一些。

创建放射性渐变时，可以使用参数指定形状、位置、尺寸、颜色和不透明度。

事例HTML:

```HTML
<div class="gradient1"><h1>1</h1></div>
<div class="gradient2"><h1>2</h1></div>
<div class="gradient3"><h1>3</h1></div>

<style>
* {margin:0; padding:0;}
div {height:150px; width:200px; float:left; margin:16px;} /* styles the element box */
h1 {text-align:left; font:25px Helvetica, Arial, sans-serif; margin:120px 5px;} /* centers the headline vertically and horizontally */
.gradient1 {background: -webkit-radial-gradient(#fff, #64d1dd, #70aa25);}       /* 默认的填满图形渐变 */
.gradient2 {background: -webkit-radial-gradient(circle, #fff, #64d1dd, #e86a43);}   /* 圆形渐变 */
.gradient3 {background: -webkit-radial-gradient(50px 30px, circle, #fff, #64d1dd, #4947ba);}  /* 指定位置的圆形渐变 */
</style>
```

例 2 设定了形状关键字 circle，于是渐变的形状变得均匀，并在元素最近的边达到了终点，形成了圆形渐变。而长边剩下的区域则填充了终点的颜色。

例 3 中的位置参数 50px 30px 把渐变的圆心放到了靠近左上角的位置。
















a
