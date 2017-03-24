
## HTML基础

### 标签

- **闭合标签**: <标签名>文本内容</标签名>
- **自闭合标签**: <标签名 属性_1="属性值" 属性_n="属性值" />

其中，`文本`使用 闭合标签 ，`引用内容` 使用 自闭和标签.[例如，图片，资源文件]

HTML5中的新标准参考[syntactic](http://dev.w3.org/html5/html-author/#syntactic-overview),当然，HTML5也兼容以前的语法.

### 属性

src属性(source)：来源

alt属性(alternative)：替代内容

每个 HTML 标签都可以添加属性，class 和 id 等属性，几乎可以适用于任何标签。另一些属性，比如 src，则只适用于类似<img>这样的
引用源文件的标签。

如：

```HTML
块级标签
<h1>-<h6> ：6 级标签，<h1>表示最重要
<p>：段落
<ol>：有序列表
<li>：列表项
<blockquote>：独立引用

行内标签
<a>：链接（anchor，锚）
<img>：图片
<em>：斜体
<strong>：重要
<abbr>：简写
<cite>：引证
<q>：文本内引用
```

了解所有HTML标签和属性参考[HTML Dog](http://htmldog.com/references/html/tags/)

### 标题与段落

h1-h6标签，当搜索引擎进行搜索时，h1标签是仅次于title标签的

### 复合元素

由多个标签共同构成。

**li标签只有在ol和ul标签中才有效，它表示一个列表项. 其中ol代表有序，ul代表无序**

```html
<ol>
 <li>Save HTML file</li>
 <li>Move file to Web server via FTP</li>
 <li>Preview in browser</li>
</ol>
```

### 嵌套标签

基于li标签与ol标签的嵌套关系，我们还可以说li标签是 ol 标签的子标签（或子元素），或者说ol标签是li标签的父标签（父元素）

使用用em（emphasis，强调）标签来强调段落中一个单词.

```html
<p>That car is <em>fast</p>.</em>  #错误的方式
<p>That car is <em>fast</em>.</p>  #争取的方式
```
要在一个标签里嵌套另一个标签，必须要先关闭后一个标签再关闭前面那个标签

## HTML文档剖析

有几个 HTML 元素是所有 HTML 文档（也就是网页）中都必须包含的。这些元素为内容提供了框架，有了这个框架才能正确显示内容.

### HTML模板

按照 HTML5 语法编写的最简单的 HTML 页面的模板

```html
<!DOCTYPE html>                     # 文档声明，说明为HTML文档.
<html>                              # 根级标签
 <head>                             # 直接的子标签
 <meta charset="utf-8" />           # 告诉浏览器页面使用 UTF-8 编码
 <title>An HTML Template</title>    # 作为整个页面的标题,搜索引擎会给<title>标签中的文字内容赋予很高的权重,不要让的废话占据它.
 </head>

 <body>                             # 直接的子标签，包含着标记所有内容的 HTML 元素
 <!-- 这里是网页内容 -->
   <h1>Stylin' with CSS</h1>        # 内容标题
   <p>Great Web pages start with great HTML markup!</p>   # 内容.
   <a href="http://www.stylinwithcss.com">My Books</a>    # 该标签有一个必需的属性 href(hyperlink reference，超链接引用),链接指向的页面的 URL。
   <img src="images/cisco.jpg" alt="My dog Cisco" />      # src（source，来源）而不是 href 属性,给出图片所在位置的 URL.
 </body>
</html>
```

虽然标题和段落是上下堆叠在一起的，但链接和图片却是并排显示的。

为什么会这样呢？因为标题和段落是块级元素，而链接和图片是行内元素

### 块级元素和行内元素

几乎所有 HTML 元素的 display 属性值要么为 block，要么为 inline。最明显的一个例外是 table 元素，它有自己特殊的 display 属性值。

- **块级元素**（比如标题和段落）会相互堆叠在一起沿页面向下排列，每个元素分别占一行。
- **行内元素**（比如链接和图片）则会相互并列，只有在空间不足以并列的情况下才会折到下一行显示。

**使用块级元素和行内元素构建页面**

```html
<!DOCTYPE html>
<html>
<head>
 <meta charset="utf-8" />
 <title>Block and Inline Elements</title>
</head>
<body>
 <h1>Types of Guitars</h1>
 <p>Guitars come in two main types: electric and acoustic.</p>
 <h2>Acoustic Guitars</h2>
 <p>Acoustic guitars have a large hollow body that projects the sound of the
 strings.</p>
 <h3>Nylon String Acoustic Guitars</h3>
 <p>Descendants of the gut-strung instruments of yore, nylon string guitars
 have a mellow tone.</p>
 <h3>Steel String Acoustic Guitars</h3>
 <p>Steel string guitars first appeared in country music and today most acoustic
 guitars have steel strings.</p>
 <h2>Electric Guitars</h2>
 <p>Electric guitars have a solid or hollow body with pickups that capture
 the string vibration so it can be amplified.</p>
 <h3>Solid Body Electric Guitars</h3>
 <p>Solid body electric guitars are commonly used in rock and country music.</p>
 <h3>Hollow Body Electric Guitars</h3>
 <p>Hollow body acoustic guitars are commonly used in blues and jazz.</p>
 </body>
</html>
```

由于标题和段落都是块级元素，所以每个元素各占一行.

页面四周都添加了一定的边距，所以文本才不会碰到浏览器窗口.

**块级元素盒子会扩展到与父元素同宽**

可使用Firefox中的 web developer 插件 看 模型.

所有块级元素的父元素都是 body，而它的宽度默认与浏览器窗口一样宽（当然有少量边距）。

因此，所有块级元素就与浏览器窗口一样宽了。

这样一来，一个块级元素旁边也就没有空间容纳另一个块级元素了。

**行内元素盒子会“收缩包裹”其内容，并且会尽可能包紧**

### 嵌套的元素

**在标记中嵌套的是 HTML 标签，而在屏幕上嵌套的则是一个个的盒子**

```HTML
<nav id="toc">
....<ol>
........<li><a href="#">Introduction</a></li>
........<li><a href="#">Chapter 1</a></li>
........<li><a href="#">Chapter 2</a></li>
........<li><a href="#">Chapter 3</a></li>
....</ol>
</nav> <!-- end table of contents -->

<blockquote>&ldquo;Sometimes you want to give up the guitar, you'll hate the
 guitar. But if you stick with it, you're gonna be rewarded.&rdquo;
 <cite>Jimi Hendrix</cite> //使用 cite 元素包含作者姓名
</blockquote>
```
**blockqoute元素包含引用内容，而且在页面上看起来是独立的元素。**

**blockquote 元素默认会缩进**

HTML 实体常用于生成那些键盘上没有的印刷字符，比如 TM、† 、©，等等。

HTML 实体以一个和号（&）开头，一个分号（;）结尾，二者之间是表示实体的字符串。

在前面的例子中，两个实体的名字分别是“left-double-quote”（左双引号,&ldquo;`&ldquo;`）和“right-double-quote”（右双引号&rdquo;`&rdquo;`）的简写。

参考HTML中所有的实体.[entities](http://www.elizabethcastro.com/html/extras/entities.html)

**一个段落中嵌套着三个分别表示重要性、强调和简写的标签**

```html
<p>It is <strong>absolutely critical</strong> that <em>everyone</em> does this
 <abbr title="as soon as possible">ASAP</abbr>!</p>
```

- 文本被标记为段落，而其中包含三个行内元素。
- strong标签表示重要，默认以粗体显示。
- em标签表示强调，默认以斜体显示。
- abbr标签表示简写，在 Firefox 中默认会加上点下划线。

**HTML 标记在页面中创建盒子，嵌套标记实际上就是嵌套盒子。**

### 文档对象模型

DOM 是从浏览器的视角来观察页面中的元素以及每个元素的属性，由此得出这些元素的一个家族树.

通过 DOM，可以确定元素之间的相互关系。在 CSS 中引用 DOM 中特定的位置，就可以选中相应的HTML 元素，并修改其样式属性.

```html
// HTML 代码正确缩进，以表明标签的层次关系
<body>
 <section>
   <h1>The Document Object Model</h1>
   <p>The page's HTML markup structure defines the DOM.</p>
 </section>
</body>
```

- section 是 h1 和 p 的父元素，也是直接祖先元素。
- h1 和 p 是 section 的子元素，也是直接后代元素。
- h1 和 p 是同胞元素，它们有共同的父元素 section.
- section、h1 和 p 是 body 的后代元素，或者下面的元素（嵌套在后者的内部）。
- section 和 body 是 h1 和 p 的祖先元素，或者上面的元素（在某一层次上包含后者）。

**CSS 操作 DOM 的过程是先选择一个或一组元素，然后再修改这些元素的属性**
**通过CSS 修改了元素后，比如修改了宽度或者在标记里插入一个伪元素，这些变化会立即在 DOM 中发生，并体现在页面上**
