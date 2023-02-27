
# CSS工作原理

每个 HTML 元素都有一组样式属性，可以通过 CSS 来设定。

这些属性涉及元素在屏幕上显示时的不同方面，比如在屏幕上位置、边框的宽度，文本内容的字体、字号和颜色，等等。

CSS 就是一种先选择 HTML 元素，然后设定选中元素 CSS 属性的机制。

CSS 选择符和要应用的样式构成了一条 CSS 规则。

## 剖析css规则

规则实际上就是一条完整的 CSS 指令。

规则声明了要修改的元素和要应用给该元素的样式。

```CSS
/* 把段落的文本设置为红色 */
p {color:red;}
```

### 添加样式的三种方法

1. 行内样式 [写在特定 HTML 标签的 style 属性里]
2. 嵌入样式 [是放在 HTML 文档的 head 元素中的]
3. 链接样式 [把样式集中在一个单独的文件里，这个文件就叫样式表,是一个扩展名为.css 的文本文件.可以在任意多个 HTML 页面中链接同一个样式表文件]

```HTML
<!--行内样式-->
<!--
行内样式的作用范围非常有限。行内样式只能影响它所在的标签，而且总会覆盖嵌入样式和链
接样式。
-->
<p style="font-size: 12px; font-weight:bold; font-style:italic; color:red;">By
adding inline CSS styling to this paragraph, you override the default styles.</p>

<!--嵌入样式-->
<!--
嵌入样式的应用范围仅限于当前页面。
页面样式会覆盖外部样式表中的样式，但会被行内样式覆盖。
-->
<head>
 <!-- 其他 head 元素（如 meta、title）放在这里 -->
 <style type="text/css">
   h1 {font-size:16px;}
   p {color:blue;}
 </style>
</head>

<!--链接样式-->
<!--
链接样式的作用范围可以是整个网站。只要使用<link>标签把样式表链接到每个页面，相应的页面就可以使用其中的样式。
随后，只要修改了样式表中的样式，改动就会在所有被选中的元素上体现出来，无论这个元素在哪个页面里。
这样，既可以做到全站页面外观统一，又便于整站样式更新。
-->
<link href="styles.css" rel="stylesheet" type="text/css" />
<!--还有一种在样式表中链接其他样式表的方法:@import 指令-->
<!-- @import 指令必须出现在样式表中其他样式之前，否则@import 引用的样式表不会被加载。-->
@import url(css/styles2.css)
```

当浏览器遇到开标签`<style>`时，就会由解释 HTML 代码切换为解释 CSS 代码。
等遇到闭标签`</style>`时，它会再切换回解释 HTML 代码

## CSS规则命名惯例

CSS 规则由选择符和声明两部分组成. 即选择符和声明.

声明又由两部分组成，即属性和值。声明包含在一对花括号内 .

**3种扩展方法**

```css
/* 1.多个声明包含在一条规则里。 */
p {color:red; font-size:12px; font-weight:bold;}

/* 2.多个选择符组合在一起,每个选择符之间要用逗号分隔 */
h1, h2, h3 {color:blue; font-weight:bold;}

/* 3.多条规则应用给一个选择符 */
h1, h2, h3 {color:blue; font-weight:bold;}
h3 {font-style:italic;}      /* 再为 h3 写一条规则,只把 h3 变成斜体 */
```

**用于选择特定元素的选择符又分三种**

1. **上下文选择符**: 基于祖先或同胞元素选择一个元素。
2. **ID 和类选择符**: 基于 id 和 class 属性的值（你自己设定）选择元素。
3. **属性选择符**: 基于属性的有无和特征选择元素。

## 上下文选择符

格式: 标签 1 标签 2 {声明}

标签 2 就是我们想要选择目标，而且只有在标签 1 是其祖先元素（不一定是
父元素）的情况下才会被选中。

也叫: `后代组合式选择符`（descendant combinator selector），就是一组以空格分隔的标签名。用于选择作为指定祖先元素后代的标签。

如 : `article p {font-weight:bold;}`  只有是article后代的p元素才会应用后面的样式.

**上下文选择符以空格作为分隔符，而分组选择符则以逗号作为分隔符，不要弄混。**

## 特殊的上下文选择符

**子选择符`>`**

标签 1 > 标签 2 , 标签 2 必须是标签 1 的子元素.

```css
section > h2 {font-style:italic;}
```

**紧邻同胞选择符`+`**

标签 1 + 标签 2 , 标签 2 必须紧跟在其同胞标签 1 的后面

```css
h2 + p {font-variant:small-caps;}
```

**一般同胞选择符`~`**

标签 1 ~ 标签 2 , 标签 2 必须跟（不一定紧跟）在其同胞标签 1 后面。

```css
h2 ~ a {color:red;}
```

**通用选择符`*`**

\* （按 Shift+8）, 通用选择符*（常被称为星号选择符）是一个通配符，它匹配任何元素.

```css
/* 导致所有元素（的文本和边框）都变成绿色 */
* {color:green;}
/* color 属性设定的是前景色。前景色既影响文本也影响边框，但人们通常只用它设定文本颜色 */

/* 只会把 p 包含的所有元素的文本变成红色 */
p * {color:red;}

/* 构成非子选择符 */
section * a {font-size:1.3em;}
/* 任何是 section 孙子元素，而非子元素的 a 标签都会被选中. */
```

**总之，只有一个标签名的选择符会选中页面中所有相同标签的实例。而通过上下文选择符，则可以指定标签必须具备相应的祖先或同胞。**

## ID 和类选择符

在 HTML 标记中为元素添加了 id 和 class 属性，就可以在 CSS 选择符中使用ID 和类名，直接选中文档中特定的区域

**类属性**

类属性就是 HTML 元素的 class 属性，body 标签中包含的任何 HTML 元素都可以添加这个属性.

```HTML
<h1 class="specialtext">This is a heading with the <span>same class</span>
    as the second paragraph.</h1>
<p>This tag has no class.</p>
<p class="specialtext"> When a tag has a class attribute, you can target it
    <span>regardless</span> of its position in the hierarchy.</p>
```

**类选择符**

.类名 , 类选择符前面是点（.），紧跟着类名，两者之间没有空格

```css
.specialtext {font-style:italic;}
```

**标签带类选择符**

标签名.类名 ，

```css
p.specialtext {color:red;}
p.specialtext span {font-weight:bold;}
```

**多类选择符**

.类名.类名(等等) ，同时选择存在多个类名的选择

```css
.specialtext.featured {font-size:120%;}
```

**ID属性**

ID 与类的写法相似，而且表示 ID 选择符的#（井号）的用法，也跟表示类选择符的.（句号）类似

ID选择符号用“#”号. 其他的用法与类选择符类似（基本上一致）.

两者区别:

- ID 也可以用在页内导航链接中. (锚点)
- 暂时不知道某个 href 应该放什么 URL，也可以用#作为占位符，但不能把该属性留空。

## 什么时候用ID，什么时候用类

ID 的用途是在页面中唯一地标识一个元素。【同一个页面中的每一个 ID属性，都必须有独一无二的值（名字）。（每个 ID 名在页面中都只能用一次。）】

**ID 值的唯一性对 JavaScript 尤其重要，否则就会导致 JavaScript 行为异常。**

类的目的是为了标识一组具有相同特征的元素。

比如：

```HTML
<nav>
 <ul>
   <li class="boy"><a href="#">Alan</a></li>
   <li class="boy"><a href="#">Andrew</a></li>
   <li class="girl"><a href="#">Angela</a></li>
   <li class="boy"><a href="#">Angus</a></li>
   <li class="girl"><a href="#">Anne</a></li>
   <li class="girl"><a href="#">Annette</a></li>
 </ul>
</nav>
```

```CSS
.boy a {color:#6CF;}/*蓝色*/
.girl a {color:#F9C;}/*粉红色*/
```

**不要乱用类**

- 要避免 Web 开发专家 Jeffrey Zeldman 说的“类泛滥——标记中的麻疹”出现。
- 什么意思呢？就是说你不要像使用 ID 一样，每个类都指定一个不同的类名，然后再为每个类编写规则。
- 如果你确实有这种随意使用类的习惯，那说明你可能像大多数对 CSS 充满激情的初学者一样，还不了解继承和上下文选择符的作用。
- 于是，你可能会给每个标签都重复写同样的样式（比如为页面中很多标签分别指定相同的字体）。
- 实际上，继承和上下文选择符能让不同的标签共享样式，从而降低你需要编写和维护的 CSS 量。

**小结**

1. ID 的用途是在页面标记中唯一地标识一个特定的元素。它能够为我们编写 CSS 规则提供必要的上下文，排除无关的标记，而只选择该上下文中的标签.
2. 类是可以应用给任意多个页面中的任意多个 HTML 元素的公共标识符，以便我们为这些元素应用相同的 CSS 样式。而且，使用类也让为不同标签名的元素应用相同的样式成为可能。

### 属性选择符

基于 HTML 标签的属性选择元素。

**属性名选择符**

标签名[属性名] ， 选择任何带有属性名的标签名。

```CSS
/* 带有 title 属性的 img 元素显示 2 像素宽的蓝色边框 */
img[title] {border:2px solid blue;}
```

```HTML
<img src="images/yellow_flower.jpg" title="yellow flower" alt="yellow flower" />
<!--
alt 属性中的文本会在图片因故未能加载时显示，或者由屏幕阅读器朗读出来.
title 属性会在用户鼠标移动到图片上时，显示一个包含相应文本的提示.
-->
```

**属性值选择符**

标签名[属性名="属性值"] , 选择任何带有值为属性值的属性名的标签名。 [在 HTML5 中，属性值的引号可加可不加]

```CSS
/* 在图片的 title 属性值为 red flower 的情况下，才会为图片添加边框 */
img[title="red flower"] {border:4px solid green;}
```

更多属性选择符[resources_css_selectors](http://www.stylinwithcss.com/resources_css_selectors.php):

| Pattern       | Meaning                                                                                                                   | Described in Section                                                       |
| ------------- | ------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| E[foo]        | An E element with a “foo” attribute                                                                                       | [Attribute selectors](http://www.w3.org/TR/selectors/#attribute-selectors) |
| E[foo="bar"]  | An E element whose “foo” attribute value is exactly equal to “bar”                                                        | [Attribute selectors](http://www.w3.org/TR/selectors/#attribute-selectors) |
| E[foo~="bar"] | An E element whose “foo” attribute value is a list of whitespace-separated values, one of which is exactly equal to “bar” | [Attribute selectors](http://www.w3.org/TR/selectors/#attribute-selectors) |
| E[foo^="bar"] | An E element whose “foo” attribute value begins exactly with the string “bar”                                             | [Attribute selectors](http://www.w3.org/TR/selectors/#attribute-selectors) |
| E[foo$="bar"] | An E element whose “foo” attribute value ends exactly with the string “bar”                                               | [Attribute selectors](http://www.w3.org/TR/selectors/#attribute-selectors) |
| E[foo*="bar"] | An E element whose “foo” attribute value contains the substring “bar”                                                     | [Attribute selectors](http://www.w3.org/TR/selectors/#attribute-selectors) |
| E[foo\|="en"] | An E element whose “foo” attribute has a hyphen-separated list of values beginning (from the left) with “en”              | [Attribute selectors](http://www.w3.org/TR/selectors/#attribute-selectors) |

基于属性名和属性的其他特征选择元素，为我们提供了另一种区别对待相同标签的机会。只要事先规划好，就可以编写出适合属性选择符的标记来.

## 伪类

伪类这个叫法源自它们与类相似，但实际上并没有类会附加到标记中的标签上。

伪类分两种:

- UI（User Interface，用户界面）伪类 会在 HTML 元素处于某个状态时（比如鼠标指针位于链接上），为该元素应用 CSS 样式。
- 结构化伪类 会在标记中存在某种结构上的关系时（如某个元素是一组元素中的第一个或最后一个），为相应元素应用 CSS 样式。

### UI伪类

**链接伪类**

4种状态:

- Link。此时，链接就在那儿等着用户点击。
- Visited。用户此前点击过这个链接。
- Hover。鼠标指针正悬停在链接上。
- Active。链接正在被点击（鼠标在元素上按下，还没有释放）。

```CSS
a:link {color:black;}
a:visited {color:gray;}
a:hover {text-decoration:none;}
a:active {color:red;}
```

这 4 个伪类的特指度（本章后面再讨论特指度）相同，如果不按照这里列出的顺序使用它们，浏览器可能不会显示预期结果.

为了好记,建议可以这么想：“LoVe? HA!” 大写字母就是每个伪类的头一个字母。

通过在上下文选择符中使用链接伪类，可以轻易地为 nav、footer、aside 和 article 元素中的链接应用不同的外观和行为。

**一个冒号（:）表示伪类，两个冒号（::）表示 CSS3 新增的伪元素。**
**这些单冒号的伪元素最终可能都会被淘汰掉，参考[pseudo-elements](https://www.w3.org/TR/2005/WD-css3-selectors-20051215/#pseudo-elements)**

有些伪类可以用于任何元素，而不仅仅是 a 元素。

比如:

```CSS
/* 段落背景在鼠标悬停时变成灰色 */
p:hover {background-color:gray;}
```

**:focus 伪类**

获得焦点时应用的伪类。

```CSS
/* 光标位于 input 字段中时，为该字段添加一个蓝色边框 */
input:focus {border:1px solid blue;}
```

**:target 伪类**

如果用户点击一个指向页面中其他元素的链接，则那个元素就是目标（target），可以用:target 伪类选中它。

比如：

```HTML
<a href="#more_info">More Information</a>
<h2 id="more_info">This is the information you are looking for.</h2>
<style>
/* 在用户单击链接转向 ID 为 more_info 的元素时，为该元素添加浅灰色背景 */
#more_info:target {background:#eee;}
</style>
```

### 结构化伪类

e:first-child, 代表一组同胞元素中的第一个元素

e:last-child,  代表一组同胞元素中的最后一个元素.

e:nth-child(n), n 表示一个数值（也可以使用 odd 或 even）

```css
li:nth-child(3)  /* 选择一组列表项中的每个第三项 */
```

更多选择器信息参考[css_selectors](http://www.stylinwithcss.com/resources_css_selectors.php)

### 伪元素

e::first-letter , 选择e标签的首个字符

```CSS
p::first-letter {font-size:300%;}   /* 首字符放大效果 */
```

e::first-line , 选择e标签下的第一行

```CSS
p::first-line {font-variant:small-caps;}  /* 第一行以小型大写字母显示 */
```

e::before , 在特定元素前面添加特殊内容
e::after  , 在特定元素后面添加特殊内容

```HTML
<p class="age">25</p>

<style>
p.age::before {content:"Age: ";}
p.age::after {content:" years.";}
</style>

<!-- Age: 25 years. -->
```

## 继承

CSS 中的祖先元素会向后代传递一样东西：CSS 属性的值.

```CSS
body {font-family:helvetica, arial, sans-serif;}
```

文档中的所有元素，无论它在层次结构中多么靠下，都将继承这些样式

也有很多 CSS 属性不能继承，因为继承这些属性没有意义,比如：边框、外边距、内边距。

## 层叠

层叠，就是层叠样式表中的层叠，是一种样式在文档层次中逐层叠加的过程，目的是让浏览器面对某个标签特定属性值的多个来源，确定最终使用哪个值。

### 样式来源

浏览器层叠各个来源样式的顺序：

1. 浏览器默认样式表
2. 用户样式表
3. 作者链接样式表（按照它们链接到页面的先后顺序）
4. 作者嵌入样式
5. 作者行内样式

浏览器会按照上述顺序依次检查每个来源的样式，并在有定义的情况下，更新对每个标签属性值的设定。

整个检查更新过程结束后，再将每个标签以最终设定的样式显示出来。

### 层叠规则

层叠规则文档:[cascade](https://www.w3.org/TR/CSS2/cascade.html)

- **层叠规则一**：找到应用给每个元素和属性的所有声明。
  - 浏览器在加载每个页面时，都会据此查到每一条 CSS 规则，标识出所有受到影响的 HTML 元素。
- **层叠规则二**：按照顺序和权重排序。
  - 浏览器依次检查 5 个来源，并设定匹配的属性。
  - 如果匹配的属性在下一个来源也有定义，则更新该属性的值，如此循环，直到检查完页面中所有标签受影响属性的全部 5 个来源为止。
  - 最终某个属性被设定成什么值，就用什么值来显示。
- **层叠规则三**：按特指度排序。
  - 除了有点拗口之外，特指度（specificity）其实表示一条规则有多明确。
  - 如果没有特指度的考量，那为了让恰当的样式起作用，恐怕就免不了要频繁变换样式表中规则的顺序了。
- **层叠规则四**：顺序决定权重。
  - 如果两条规则都影响某元素的同一个属性，而且它们的特指度也相同，则位置最靠下（或后声明）的规则胜出。

**类名选择符比普通的标签选择符具有更高的特指度。一条规则的特指度，由它的选择符中包含多少个标签、类名和 ID 决定。**

### 计算特指度

公式: I-C-E , 短横线是分隔符，并非减号

ICE 并非真正的三位数，只不过大多情况下把结果看成一个三位数没有问题，三位数最大的胜出。
但是，千万得知道 0-1-12 与 0-2-0 相比，仍然是 0-2-0 的特指度更高。

计分办法:

1. 选择符中有一个 ID，就在 I 的位置上加 1；
2. 选择符中有一个类，就在 C 的位置上加 1；
3. 选择符中有一个元素（标签）名，就在 E 的位置上加 1；
4. 得到一个三位数。

例子:

```
P                               0-0-1 特指度=1
p.largetext                     0-1-1 特指度=11
p#largetext                     1-0-1 特指度=101
body p#largetext                1-0-2 特指度=102
body p#largetext ul.mylist      1-1-3 特指度=113
body p#largetext ul.mylist li   1-1-4 特指度=114
```

**简单层叠要点:**

- **规则一**：包含 ID 的选择符胜过包含类的选择符，包含类的选择符胜过包含标签名的选择符。
- **规则二**：如果几个不同来源都为同一个标签的同一个属性定义了样式，行内样式胜过嵌入样式，嵌入样式胜过链接样式。在链接的样式表中，具有相同特指度的样式，后声明的胜过先声明的。
- **规则三**：设定的样式胜过继承的样式，此时不用考虑特指度（即显式设定优先）。

## 规则声明

每个元素都有很多属性，可以通过 CSS 来设定。但每个元素具体有哪些属性，也会因元素而异。

CSS 属性值主要分三类。

- 文本值。
  - 例如，font-weight:bold 声明中的 bold 就一个文本值。文本值也叫做关键字。
- 数字值。数字值后面都有一个单位，比如英寸或点。
  - 例如。在声明 font-size:12px 中，12是数字值，而 px 是单位（像素）。如果数字值为 0，那么就不用带单位了。
- 颜色值。颜色值可以用几种不同的格式来写，
  - RGB（Red, Green, Blue，红绿蓝）
  - HSL（Hue, Saturation, Luminance，色相，饱和度，亮度）
  - 十六进制值（例如color:#336699）

### 文本值

所有 CSS 属性都有文本值

- visibility 属性有 visible 和 hidden 值
- border-style 属性有 solid、 dashed 以及 inset 值

等等.

### 数字值

数字值用于描述元素的各种长度（高度、宽度、粗细，等等）。数字值主要分两类：绝对值和相对值。

绝对值及示例:

| 绝对值 | 单位缩写 | 示 例        |
| ------ | -------- | ------------ |
| 英寸   | in       | height:6in   |
| 厘米   | cm       | height:40cm  |
| 毫米   | mm       | height:500mm |
| 点     | pt       | height:60pt  |
| 皮卡   | pc       | height:90pc  |
| 像素   | px       | height:72px  |

相对值及示例:

| 相对值 | 单位缩写 | 示 例        |
| ------ | -------- | ------------ |
| Em     | em       | height:1.2em |
| Ex     | ex       | height:6ex   |
| 百分比 | %        | height:120%  |

em 和 ex 都是字体大小的单位，但在 CSS 中，它们作为长度单位适用于任何元素。

em ，它表示一种字体中字母 M 的宽度，它具体大小取决于使用的字体。

ex ，等于给定字体中字母 x 的高度（小写字母 x 代表一种字体的字母中间部分的高度，不包括字母上、下突出的部分——如 d 和 p 上下都出头儿).

百分比非常适合设定被包含元素的宽度，此时的百分比就是相对于宽度而言的

### 颜色值

**颜色名**

如 red

W3C 定义了 16 个颜色关键字:

aqua（浅绿色）、black（黑色）、blue（蓝色）、 fuchsia（紫红色）、
gray（灰色）、green（绿色）、lime（黄绿色）、 maroon（褐红色）、
navy（深蓝色）、olive（茶青色 ）、purple（紫色）、red（红色）、
silver（银色）、teal（青色）、white（白色）和 yellow（黄色）

参考官网[RGB颜色值](https://www.w3.org/TR/css3-color/#html4)

更多杂颜色名:[X11 color names](https://en.wikipedia.org/wiki/X11_color_names)

**十六进制颜色**

 #RRGGBB 或 #RGB ,以 # 开头. 前两位定义红色，中间两位定义绿色，后两位定义蓝色

由于每种颜色用两位十六进制值表示，因此该颜色就有 256（16×16）种可能的值，
结果就是 16 777 216（256×256×256）种组合，也就是可以表示那么多种颜色。

比如：橙色（#ff8800）、纯红色（#ff0000），纯绿色（#00ff00），纯蓝色（#0000ff）。

如果三对值中的每一对是两个相同的数字，也可以使用简写形式：#rgb

比如：纯红色（#f00），纯绿色（#0f0），纯蓝色（#00f）。

!!! info ""

    大多数十六进制颜色值不仔细分析可不容易猜，比如#7ca9be 是深蓝绿色，我怎么知道的？ 首先我们来看每一对 rgb 值中的第一个值，也就是 7、a、b。蓝色和绿色值相差无几，而红色值也没有那么深。有了这些信息，就可以大致猜出这个颜色了，对，是蓝绿色。

**RGB 颜色值**

rgb(R,G,B),每种颜色都可以用一个 0 到 255（包含）之间的值指定.

比如，rgb(0,255,0)表示纯绿色。与十六进制 RGB 值一样，只不过使用的是十进制的数值。

**RGB 百分比值**

r%, g%, b% , 用百分比来表示每种颜色值的一种方法,可以接受的值是 0%到 100%,这种方法只能表示区区一百万（100 × 100 ×100）种颜色

比如：100%, 0%, 0%是纯红色，0%, 100%, 0%是纯绿色，而 46%, 76%, 80%接近
前面用十六进制值作例子分析的深蓝绿色

**HSL**

HSL 格式：HSL(0,0%,0%) ，色相, 饱和度%, 亮度%

红色是 0 或 360，青色是与之相对的 180。

- 红：0
- 橙：35
- 黄：60
- 绿：125
- 蓝：230
- 靛：280
- 紫：305

饱和度设定有多少颜色，灰色的饱和度低，而强烈的色彩饱和度高。

亮度设定颜色的明暗，0%就是黑色，100%就是白色，

中间的值是实际能看到的色相。

**Alpha 通道**

RGB 和 HSL 都支持 Alpha 通道，用于设置颜色的不透明度（能够透过多少背景）

相应的格式分别叫 RGBA 和 HSLA。
其中，两种格式中的 A（alpha）值可以是 1（完全不透明）也可以是 0（完全透明），
或者介于 1 和 0 之间的小数值

颜色资料:

- [Colrd](http://colrd.com/),一个 Pinterest 风格的站点，其中有很多能启发人创造力的图片和照片，以及相应的调色板。
- [Adobe Kuler](http://kuler.com),Adobe Kuler 的官方站点提供了数千种色样、调色板创建工具，以及其他人正在选用的时尚颜色。
