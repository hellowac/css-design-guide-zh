
## HTML基础

### 标签

**闭合标签**: <标签名>文本内容</标签名>
**自闭合标签**: <标签名 属性_1="属性值" 属性_n="属性值" />

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

**li标签只有在ol和ul标签中才有效，它表示一个列表项.**

```html
<ol>
 <li>Save HTML file</li>
 <li>Move file to Web server via FTP</li>
 <li>Preview in browser</li>
</ol>
```
