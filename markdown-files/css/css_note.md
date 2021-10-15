# CSS Note

## 本文重要内容

- CSS 的单位
- 字体属性
- 文本属性
- 定位属性：position、float、overflow 等

## CSS 的单位

html 中的单位只有一种，那就是像素 px，所以单位是可以省略的，但是在 CSS 中不一样。
<font color="#0000FF">CSS 中的单位是必须要写的，因为它没有默认单位。</font>

### 绝对单位

1 `in`=2.54`cm`=25.4`mm`=72`pt`=6`pc`。

各种单位的含义：

- `in`：英寸 Inches (1 英寸 = 2.54 厘米)
- `cm`：厘米 Centimeters
- `mm`：毫米 Millimeters
- `pt`：点 Points，或者叫英镑 (1 点 = 1/72 英寸)
- `pc`：皮卡 Picas (1 皮卡 = 12 点)

### 相对单位

`px`：像素
`em`：印刷单位相当于 12 个点
`%`：百分比，相对周围的文字的大小

为什么说像素 px 是一个相对单位呢，这也很好理解。比如说，电脑屏幕的的尺寸是不变的，但是我们可以让其显示不同的分辨率，在不同的分辨率下，单个像素的长度肯定是不一样的啦。

百分比`%`这个相对单位要怎么用呢？这里也举个例子：

![](http://img.smyhvae.com/2015-10-03-css-17.png)

## font 字体属性

CSS 中，有很多非布局样式（与布局无关），包括：字体、行高、颜色、大小、背景、边框、滚动、换行、装饰性属性（粗体、斜体、下划线）等。

这一段，我们先来讲一下字体属性。

css 样式中，常见的字体属性有以下几种：

```css
p {
  font-size: 50px; /*字体大小*/
  line-height: 30px; /*行高*/
  font-family: 幼圆, 黑体; /*字体类型：如果没有幼圆就显示黑体，没有黑体就显示默认*/
  font-style: italic; /*italic表示斜体，normal表示不倾斜*/
  font-weight: bold; /*粗体*/
  font-variant: small-caps; /*小写变大写*/
}
```

### 行高

CSS 中，所有的行，都有行高。盒子模型的 padding，绝对不是直接作用在文字上的，而是作用在“行”上的。

如下图所示：

![](http://img.smyhvae.com/20170808_2216.png)

上图中，我们设置行高为 30px，30px \* 5 = 150px，通过查看审查元素，这个 p 标签的高度果然为 150px。而且我们发现，我们并没有给这个 p 标签设置高度，显然是内容将其撑高的。

垂直方向来看，文字在自己的行里是居中的。比如，文字是 14px，行高是 24px，那么 padding 就是 5px：

![](http://img.smyhvae.com/20170808_2220.png)

为了严格保证字在行里面居中，我们的工程师有一个约定： 行高、字号，一般都是偶数。这样可以保证，它们的差一定偶数，就能够被 2 整除。

### 如何让单行文本垂直居中

小技巧：如果一段文本只有一行，如果此时设置行高 = 盒子高，就可以保证单行文本垂直居中。这个很好理解。

上面这个小技巧，只适用于单行文本垂直居中，不适用于多行。如果想让多行文本垂直居中，还需要计算盒子的 padding。计算方式如下：

![](http://img.smyhvae.com/20170808_2240.png)

### `vertical-align: middle;` 属性

`vertical-align`属性可用于指定行内元素（inline）、行内块元素（inline-block）、表格的单元格（table-cell）的垂直对齐方式。主要是用于图片、表格、文本的对齐。

代码举例：

```css
vertical-align: middle; /*指定行级元素的垂直对齐方式。*/
```

关于这一点，连 MDN 上都没我讲得详细。MDN 上的原话是 “vertical-align 用来指定行内元素（inline）或表格单元格（table-cell）元素的垂直对齐方式。” MDN 上的这种描述是不完整的，漏掉了行内块元素（inline-block）。

### 字号、行高、字体三大属性

（1）字号：

```
	font-size:14px;
```

（2）行高：

```
	line-height:24px;
```

（3）字体：（font-family 就是“字体”，family 是“家庭”的意思）

```
	font-family:"宋体";
```

是否加粗属性以及上面这三个属性，我们可以连写：（是否加粗、字号 font-size、行高 line-height、字体 font-family）

格式：

```
	font: 加粗 字号/行高/ 字体

```

举例：

```
	font: 400 14px/24px "宋体";
```

PS：400 是 nomal，700 是 bold。

上面这几个属性可以连写，但是有一个要求，font 属性连写至少要有字号和字体，否则连写是不生效的（相当于没有这一行代码）。

2、字体属性的说明：

（1）网页中不是所有字体都能用，因为这个字体要看用户的电脑里面装没装，比如你设置：

```
	font-family: "华文彩云";
```

上方代码中，如果用户的 Windows 电脑里面没有这个字体，那么就会变成宋体。

页面中，中文我们一般使用：微软雅黑、宋体、黑体。英文使用：Arial、Times New Roman。页面中如果需要其他的字体，就需要单独安装字体，或者切图。

（2）为了防止用户电脑里，没有微软雅黑这个字体。就要用英语的逗号，提供备选字体。如下：（可以备选多个）

```
	font-family: "微软雅黑","宋体";
```

上方代码表示：如果用户电脑里没有安装微软雅黑字体，那么就是宋体。

（3）我们须将英语字体放在最前面，这样所有的中文，就不能匹配英语字体，就自动的变为后面的中文字体：

```
	font-family: "Times New Roman","微软雅黑","宋体";
```

上方代码的意思是，英文会采用 Times New Roman 字体，而中文会采用微软雅黑字体（因为美国人设计的 Times New Roman 字体并不针对中文，所以中文会采用后面的微软雅黑）。比如说，对于`smyhvae哈哈哈`这段文字，`smyhvae`会采用 Times New Roman 字体，而`哈哈哈`会采用微软雅黑字体。

可是，如果我们把中文字体写在前面：(错误写法)

```
	font-family: "微软雅黑","Times New Roman","宋体";
```

上方代码会导致，中文和英文都会采用微软雅黑字体。

（4）所有的中文字体，都有英语别名。

微软雅黑的英语别名：

```
	font-family: "Microsoft YaHei";
```

宋体的英语别名：

```
	font-family: "SimSun";
```

于是，当我们把字号、行高、字体这三个属性合二为一时，也可以写成：

```
	font:12px/30px  "Times New Roman","Microsoft YaHei","SimSun";
```

（5）行高可以用百分比，表示字号的百分之多少。

一般来说，百分比都是大于 100%的，因为行高一定要大于字号。

比如说， `font:12px/200% “宋体”`等价于`font:12px/24px “宋体”`。`200%`可以理解成 word 里面的 2 倍行高。

反过来， `font:16px/48px “宋体”;`等价于`font:16px/300% “宋体”`。

### 字体加粗属性

```css
.div {
  font-weight: normal; /*正常*/
  font-weight: bold; /*加粗*/
  font-weight: 100;
  font-weight: 200;
  font-weight: 900;
}
```

在设置字体是否加粗时，属性值既可以填写`normal`、`bold`这样的加粗字体，也可以直接填写 100 至 900 这样的数字。`normal`的值相当于 400，`bold`的值相当于 700。

## 文本属性

CSS 样式中，常见的文本属性有以下几种：

- `letter-spacing: 0.5cm ;` 单个字母之间的间距
- `word-spacing: 1cm;` 单词之间的间距
- `text-decoration: none;` 字体修饰：none 去掉下划线、underline 下划线、line-through 中划线、overline 上划线
- `text-transform: lowercase;` 单词字体大小写。uppercase 大写、lowercase 小写
- `color:red;` 字体颜色
- `text-align: center;` 在当前容器中的对齐方式。属性值可以是：left、right、center（<font color="#0000FF">在当前容器的中间</font>）、justify
- `text-transform: lowercase;` 单词的字体大小写。属性值可以是：`uppercase`（单词大写）、`lowercase`（单词小写）、`capitalize`（每个单词的首字母大写）

这里来一张表格的图片吧，一览无遗：

![](http://img.smyhvae.com/2015-10-03-css-18.png)

## 列表属性

```css
ul li {
  list-style-image: url(images/2.gif); /*列表项前设置为图片*/
  margin-left: 80px; /*公有属性*/
}
```

另外还有一个简写属性叫做`list-style`，它的作用是：将上面的多个属性写在一个声明中。

我们来看一下`list-style-image`属性的效果：

![](http://img.smyhvae.com/2015-10-03-css-23.png)

给列表前面的图片加个边距吧，不然显示不完整：

![](http://img.smyhvae.com/2015-10-03-css-24_2.png)

这里来一张表格的图片吧，一览无遗：

![](http://img.smyhvae.com/2015-10-03-css-26.png)

## overflow 属性：超出范围的内容要怎么处理

`overflow`属性的属性值可以是：

- `visible`：默认值。多余的内容不剪切也不添加滚动条，会全部显示出来。
- `hidden`：不显示超过对象尺寸的内容。
- `auto`：如果内容不超出，则不显示滚动条；如果内容超出，则显示滚动条。
- `scroll`：Windows 平台下，无论内容是否超出，总是显示滚动条。Mac 平台下，和 `auto` 属性相同。

针对上面的不同的属性值，我们来看一下效果：
举例：

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="Generator" content="EditPlus®" />
    <meta name="Author" content="" />
    <meta name="Keywords" content="" />
    <meta name="Description" content="" />
    <title>Document</title>

    <style type="text/css">
      div {
        width: 100px;
        height: 100px;
        background-color: #00cc66;
        margin-right: 100px;
        float: left;
      }

      #div1 {
        overflow: auto; /*超出的部分让浏览器自行解决*/
      }
      #div2 {
        overflow: visible; /*超出的部分会显示出来*/
      }

      #div3 {
        overflow: hidden; /*超出的部分将剪切掉*/
      }
    </style>
  </head>

  <body>
    <div id="div1">
      其实很简单 其实很自然 两个人的爱由两人分担 其实并不难 是你太悲观
      隔着一道墙不跟谁分享 不想让你为难 你不再需要给我个答案
    </div>
    <div id="div2">
      其实很简单 其实很自然 两个人的爱由两人分担 其实并不难 是你太悲观
      隔着一道墙不跟谁分享 不想让你为难 你不再需要给我个答案
    </div>
    <div id="div3">
      其实很简单 其实很自然 两个人的爱由两人分担 其实并不难 是你太悲观
      隔着一道墙不跟谁分享 不想让你为难 你不再需要给我个答案
    </div>
  </body>
</html>
```

效果：

![](http://img.smyhvae.com/2015-10-03-css-31.png)

## 鼠标的属性 cursor

鼠标的属性`cursor`有以下几个属性值：

- `auto`：默认值。浏览器根据当前情况自动确定鼠标光标类型。
- `pointer`：IE6.0，竖起一只手指的手形光标。就像通常用户将光标移到超链接上时那样。
- `hand`：和`pointer`的作用一样：竖起一只手指的手形光标。就像通常用户将光标移到超链接上时那样。

比如说，我想让鼠标放在那个标签上时，光标显示手状，代码如下：

```html
p:hover{ cursor: pointer; }
```

另外还有以下的属性：（不用记，需要的时候查一下就行了）

- all-scroll :　 IE6.0 有上下左右四个箭头，中间有一个圆点的光标。用于标示页面可以向上下左右任何方向滚动。
- col-resize :　 IE6.0 有左右两个箭头，中间由竖线分隔开的光标。用于标示项目或标题栏可以被水平改变尺寸。
- crosshair :　 简单的十字线光标。
- default :　 客户端平台的默认光标。通常是一个箭头。
- hand :　 竖起一只手指的手形光标。就像通常用户将光标移到超链接上时那样。
- move :　 十字箭头光标。用于标示对象可被移动。
- help :　 带有问号标记的箭头。用于标示有帮助信息存在。
- no-drop :　 IE6.0 带有一个被斜线贯穿的圆圈的手形光标。用于标示被拖起的对象不允许在光标的当前位置被放下。
- not-allowed :　 IE6.0 禁止标记(一个被斜线贯穿的圆圈)光标。用于标示请求的操作不允许被执行。
- progress :　 IE6.0 带有沙漏标记的箭头光标。用于标示一个进程正在后台运行。
- row-resize :　 IE6.0 有上下两个箭头，中间由横线分隔开的光标。用于标示项目或标题栏可以被垂直改变尺寸。
- text :　 用于标示可编辑的水平文本的光标。通常是大写字母 I 的形状。
- vertical-text :　 IE6.0 用于标示可编辑的垂直文本的光标。通常是大写字母 I 旋转 90 度的形状。
- wait :　 用于标示程序忙用户需要等待的光标。通常是沙漏或手表的形状。
- \*-resize :　 用于标示对象可被改变尺寸方向的箭头光标。
-                      w-resize | s-resize | n-resize | e-resize | ne-resize | sw-resize | se-resize | nw-resize
- url ( url ) :　 IE6.0 用户自定义光标。使用绝对或相对 url 地址指定光标文件(后缀为 .cur 或者 .ani )。

## 滤镜

这里只举一个滤镜的例子吧。比如说让图片变成灰度图的效果，可以这样设置滤镜：

```html
<img src="3.jpg" style="filter:gray()" />
```

举例代码：

```html
<body>
  <table>
    <tr>
      <td>原始图片</td>
      <td>图片加入黑白效果</td>
    </tr>
    <tr>
      <td><img src="3.jpg" /></td>
      <td><img src="3.jpg" style="filter:gray()" /></td>
      /*滤镜：设置图片为灰白效果*/
    </tr>
  </table>
</body>
```

效果如下：（IE 有效果，google 浏览器无效果）

![](http://img.smyhvae.com/2015-10-03-css-36.png)

延伸：
滤镜本身是平面设计中的知识。如果你懂一点 PS 的话···打开 PS 看看吧：

![](http://img.smyhvae.com/2015-10-03-css-38.png)

爆料一下，表示博主有两年多的平面设计经验，我做设计的时间其实比写代码的时间要长，嘿嘿···

## 导航栏的制作（本段内容请忽略）

现在，我们利用 float 浮动属性来把无序列表做成一个简单的导航栏吧，效果如下：

![](http://img.smyhvae.com/2015-10-03-css-34.png)

代码：

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="Generator" content="EditPlus®" />
    <meta name="Author" content="" />
    <meta name="Keywords" content="" />
    <meta name="Description" content="" />
    <title>Document</title>

    <style type="text/css">
      ul {
        list-style: none; /*去掉列表前面的圆点*/
        width: 420px;
        height: 60px;
        background-color: black; /*设置整个导航栏的背景为灰色*/
      }

      li {
        float: left; /*平铺*/
        margin-right: 30px;
        margin-top: 16px;
      }

      a {
        text-decoration: none; /*去掉超链的下划线*/
        font-size: 20px;
        color: #bbbbbb; /*设置超链的字体为黑色*/
        font-family: 微软雅黑;
      }
    </style>
  </head>
  <body>
    <ul>
      <li><a href="">博客园</a></li>
      <li><a href="">新随笔</a></li>
      <li><a href="">联系</a></li>
      <li><a href="">订阅</a></li>
      <li><a href="">管理</a></li>
    </ul>
  </body>
</html>
```

实现效果如下：

![](http://img.smyhvae.com/2015-10-03-css-35.png)

国庆这四天，连续写了四天的博客，白天和黑夜，从未停歇，只交替没交换，为的就是这每日一发。以后会不断更新的。

> 本文最初发表于[博客园](http://www.cnblogs.com/smyhvae/p/8277895.html)，并在[GitHub](https://github.com/qianguyihao/Web)上持续更新前端的系列文章。欢迎在 GitHub 上关注我，一起入门和进阶前端。

> 以下是正文。

## background 的常见背景属性

css2.1 中，常见的背景属性有以下几种：（经常用到，要记住）

- `background-color:#ff99ff;` 设置元素的背景颜色。

- `background-image:url(images/2.gif);` 将图像设置为背景。

- `background-repeat: no-repeat;` 设置背景图片是否重复及如何重复，默认平铺满。（重要）

  - `no-repeat`不要平铺；
  - `repeat-x`横向平铺；
  - `repeat-y`纵向平铺。

- `background-position:center top;` 设置背景图片在当前容器中的位置。

- `background-attachment:scroll;` 设置背景图片是否跟着滚动条一起移动。
  属性值可以是：`scroll`（与 fixed 属性相反，默认属性）、`fixed`（背景就会被固定住，不会被滚动条滚走）。

- 另外还有一个综合属性叫做`background`，它的作用是：将上面的多个属性写在一个声明中。

CSS3 中，新增了一些 background 属性：

- background-origin

- background-clip 背景裁切

- background-size 调整尺寸

- 多重背景

上面这几个属性经常用到，需要记住。现在我们逐个进行讲解。

## background-color：背景颜色的表示方法

css2.1 中，颜色的表示方法有三种：单词、rgb 表示法、十六进制表示法。

比如红色可以有下面的三种表示方法：

```css
background-color: red;
background-color: rgb(255, 0, 0);
background-color: #ff0000;
```

CSS3 中，有一种新的表示颜色的方式：RGBA 或者 HSLA。

RGBA、HSLA 可应用于所有使用颜色的地方。

下面分别介绍。

### 用英语单词表示

能够用英语单词来表述的颜色，都是简单颜色，比如 red、green、blue、orange、gray 等。代码举例：

```css
background-color: red;
```

### RGB 表示法

RGB 表示三原色“红”red、“绿”green、“蓝”blue。

光学显示器中，每个像素都是由三原色的发光原件组成的，靠明亮度不同调成不同的颜色的。r、g、b 的值，每个值的取值范围 0~255，一共 256 个值。

比如红色：

```css
background-color: rgb(255, 0, 0);
```

黑色：

```css
background-color: rgb(0, 0, 0);
```

颜色可以叠加，比如黄色就是红色和绿色的叠加：

```css
background-color: rgb(255, 255, 0);
```

### RGBA 表示法

```javascript
    background-color: rgba(0, 0, 255, 0.3);

    border: 30px solid rgba(0, 255, 0, 0.3);
```

代码解释：

- RGBA 即：Red 红、Green 绿、Blue 蓝、Alpha 透明度。

- R、G、B 的取值范围是：0~255；透明度的取值范围是 0~1。

RGB 色彩模式：

- 自然界中所有的颜色都可以用红、绿、蓝(RGB)这三种颜色波长的不同强度组合而得，这就是人们常说的三原色原理。
- RGB 三原色也叫加色模式，这是因为当我们把不同光的波长加到一起的时候，可以得到不同的混合色。例：红+绿=黄色，红+蓝＝紫色，绿+蓝=青。
- 在数字视频中，对 RGB 三基色各进行 8 位编码就构成了大约 1678 万种颜色，这就是我们常说的真彩色。所有显示设备都采用的是 RGB 色彩模式。
- RGB 各有 256 级(0-255)亮度，256 级的 RGB 色彩总共能组合出约 1678 万种色彩，即 256×256×256=16777216。

### 十六进制表示法

比如红色：

```
background-color: #ff0000;
```

PS:所有用`#`开头的值，都是 16 进制的。

这里，我们就要学会 16 进制与 10 进制之间的转换。下面举几个例子。

问：16 进制中 28 等于 10 进制多少？
答：2\*16+8 = 40。

16 进制中的 af 等于 10 进制多少？
答：10 \* 16 + 15 = 175

所以，#ff0000 就等于 rgb(255,0,0)。

`background-color: #123456;`等价于`background-color: rgb(18,52,86);`

十六进制可以简化为 3 位，所有#aabbcc 的形式，能够简化为#abc。举例如下：

比如：

```
	background-color:#ff0000;
```

等价于：

```
	background-color:#f00;
```

比如：

```
	background-color:#112233;
```

等价于：

```
	background-color:#123;
```

但是，比如下面这个是无法简化的：

```
	background-color:#222333;
```

再比如，下面这个也是无法简化的：

```
	background-color:#123123;
```

几种常见的颜色简写可以记住。如下：

```
	#000   黑
	#fff   白
	#f00   红
	#222   深灰
	#333   灰
	#ccc   浅灰
```

### HSLA 表示法

举例：

```javascript
	background-color: hsla(240,50%,50%,0.4);
```

解释：

- `H` 色调，取值范围 0~360。0 或 360 表示红色、120 表示绿色、240 表示蓝色。

- `S` 饱和度，取值范围 0%~100%。值越大，越鲜艳。

- `L` 亮度，取值范围 0%~100%。亮度最大时为白色，最小时为黑色。

- `A` 透明度，取值范围 0~1。

如果不知道 H 的值该设置多少，我们不妨来看一下色盘：

![](http://img.smyhvae.com/20180207_1545.png)

推荐链接：[配色宝典](http://www.uisdc.com/how-to-create-color-palettes)

关于设置透明度的其他方式：

（1）`opacity: 0.3;` 会将整个盒子及子盒子设置透明度。也就是说，当盒子设置半透明的时候，会影响里面的子盒子。

（2）`background: transparent;` 可以单独设置透明度，但设置的是完全透明（不可调节透明度）。

## `background-repeat`属性

`background-repeat:no-repeat;`设置背景图片是否重复及如何重复，默认平铺满。属性值可以是：

- `no-repeat`（不要平铺）
- `repeat-x`（横向平铺）
- `repeat-y`（纵向平铺）

这个属性在开发的时候也是经常用到的。我们通过设置不同的属性值来看一下效果吧：

（1）不加这个属性时：（即默认时）（背景图片会被平铺满）

![](http://img.smyhvae.com/2015-10-03-css-19.png)

PS：padding 的区域也是有背景图的。

（2）属性值为`no-repeat`（不要平铺）时：

![](http://img.smyhvae.com/2015-10-03-css-20.png)

（3）属性值为`repeat-x`（横向平铺）时：

![](http://img.smyhvae.com/2015-10-03-css-21.png)

其实这种属性的作用还是很广的。举个例子，设计师设计一张宽度只有 1px、颜色纵向渐变的图片，然后我们通过这个属性将其进行水平方向的平铺，就可以看到整个页面都是渐变的了。

在搜索引擎上搜“平铺背景”，就可以发现，周期性的图片可以采用此种方法进行平铺。

（4）属性值为`repeat-y`（纵向平铺）时：

![](http://img.smyhvae.com/2015-10-03-css-22.png)

## `background-position`属性

`background-position`属性指的是背景定位属性。公式如下：

在描述属性值的时候，有两种方式：用像素描述、用单词描述。下面分别介绍。

1、用像素值描述属性值：

格式如下：

```
	background-position:向右偏移量 向下偏移量;
```

属性值可以是正数，也可以是负数。比如：`100px 200px`、`-50px -120px`。

举例如下：

![](http://img.smyhvae.com/20170812_1643.png)

![](http://img.smyhvae.com/20170812_1645.png)

2、用单词描述属性值：

格式如下：

```
	background-position: 描述左右的词 描述上下的词;
```

- 描述左右的词：left、center、right
- 描述上下的词：top 、center、bottom

比如说，`right center`表示将图片放到右边的中间；`center center`表示将图片放到正中间。

比如说，`bottom`表示图片的底边和父亲底边贴齐（好好理解）。

位置属性有很多使用场景的。我们来举两个例子。

场景 1：（大背景图）

打开“暗黑 3 台湾”的官网<https://tw.battle.net/d3/zh/>，可以看到官网的效果是比较炫的：

![](http://img.smyhvae.com/20170812_1945.jpg)

检查网页后，找到网站背景图片的 url：<https://tw.battle.net/d3/static/images/layout/bg-repeat.jpg>。背景图如下：

![](http://img.smyhvae.com/20170812_1950.jpg)

实际上，我们是通过把这张图片作为网站的背景图来达到显示效果的。只需要给 body 标签加如下属性即可：

```
        body{
            background-image: url(/Users/smyhvae/Dropbox/img/20170812_1950.jpg);
            background-repeat: no-repeat;
            background-position: center top;
        }
```

上方代码中，如果没加`background-position`这个属性，背景图会默认处于浏览器的左上角（显得很丑）；加了此属性之后，图片在水平方向就位于浏览器的中间了。

场景 2：（通栏 banner）

很多网站的首页都会有 banner 图（网站最上方的全屏大图叫做「通栏 banner」），这种图要求横向的宽度特别大。比如说，设计师给你一张 1920\*465 的超大 banner 图，如果我们把这个 banner 图作为 img 标签直接插入网页中，会有问题的：首先，图片不在网页的中间；其次，肯定会出现横向滚动条。如下图所示：

![](http://img.smyhvae.com/20170813_1102.gif)

正确的做法是，将 banner 图作为 div 的背景图，这样的话，背景图超出 div 的部分，会自动移溢出。需要给 div 设置的属性如下：

```css
div {
  height: 465px;
  background-image: url(http://img.smyhvae.com/20170813_1053.jpg);
  background-position: center top;
  background-repeat: no-repeat;
}
```

上方代码中，我们给 div 设置 height（高度为 banner 图的高度），不需要设置宽度（因为宽度会自动霸占整行）。效果如下：

![](http://img.smyhvae.com/20170813_1119.gif)

上图可以看出，将 banner 图作为 div 的背景后，banner 图会永远处于网页的正中间（水平方向来看）。

## background-attachment 属性

- `background-attachment:scroll;` 设置背景图片是否固定。属性值可以是：
  - `fixed`（背景就会被固定住，不会被滚动条滚走）。
  - `scroll`（与 fixed 属性相反，默认属性）

`background-attachment:fixed;`的效果如下：

![](http://img.smyhvae.com/20170813_1158.gif)

### background 综合属性

background 属性和 border 一样，是一个综合属性，可以将多个属性写在一起。(在[盒子模型](http://www.cnblogs.com/smyhvae/p/7256371.html)这篇文章中专门讲到 border)

举例 1:

```css
background: red url(1.jpg) no-repeat 100px 100px fixed;
```

等价于：

```css
background-color: red;
background-image: url(1.jpg);
background-repeat: no-repeat;
background-position: 100px 100px;
background-attachment: fixed;
```

以后，我们可以用小属性层叠掉大属性。

上面的属性中，可以任意省略其中的一部分。

比如说，对于下面这样的属性：

```css
background: blue url(images/wuyifan.jpg) no-repeat 100px 100px;
```

效果如下：

![](http://img.smyhvae.com/20170813_1515.png)

## `background-size`属性：背景尺寸

`background-size`属性：设置背景图片的尺寸。

格式举例：

```javascript
	/* 宽、高的具体数值 */
	background-size: 500px 500px;

	/* 宽高的百分比（相对于容器的大小） */
	background-size: 50% 50%;   // 如果两个属性值相同，可以简写成：background-size: 50%;

	background-size: 100% auto;  //这个属性可以自己试验一下。

	/* cover：图片始终填充满容器，且保证长宽比不变。图片如果有超出部分，则超出部分会被隐藏。 */
	background-size: cover;

	/* contain：将图片完整地显示在容器中，且保证长宽比不变。可能会导致容器的部分区域为空白。  */
	background-size: contain;
```

这里我们对属性值 `cover` 和 `contain` 进行再次强调：

- `cover`：图片始终填充满容器，且保证长宽比不变。图片如果有超出部分，则超出部分会被隐藏。

- `contain`：将图片完整地显示在容器中，且保证长宽比不变。可能会导致容器的部分区域留白。

代码举例：（这张图片本身的尺寸是 1080 \* 1350）

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
      .img_wrap {
        display: flex;
      }

      .img {
        width: 200px;
        height: 200px;
        border: 1px solid red;
        background: url(http://img.smyhvae.com/20191006_1330.jpg) no-repeat;
        margin-right: 20px;
      }

      .div1 {
        background-size: cover;
      }
      .div2 {
        background-size: contain;
      }
    </style>
  </head>

  <body>
    <section class="img_wrap">
      <div class="img div1"></div>
      <div class="img div2"></div>
    </section>
  </body>
</html>
```

效果如下：

![](http://img.smyhvae.com/20191006_1350.png)

在上方代码的基础之上，再加一个 `background-position: center`属性之后，图片就会在容器里居中显示：

![](http://img.smyhvae.com/20191006_1520.png)

## 背景原点：`background-origin` 属性

`background-origin` 属性：控制背景从什么地方开始显示。

格式举例：

```javascript

	/* 从 padding-box 内边距开始显示背景图 */
	background-origin: padding-box;           //默认值

	/* 从 border-box 边框开始显示背景图  */
	background-origin: border-box;

	/* 从 content-box 内容区域开始显示背景图  */
	background-origin: content-box;

```

如果属性值设置成了`border-box`，那边框部分也会显示图片哦。

如下图所示：

![](http://img.smyhvae.com/20180207_2115.png)

## `background-clip`属性：设置元素的背景（背景图片或颜色）是否延伸到边框下面

格式举例：

`background-clip: content-box;` 超出的部分，将裁剪掉。属性值可以是：

- `border-box` 超出 border-box 的部分，将裁剪掉

- `padding-box` 超出 padding-box 的部分，将裁剪掉

- `content-box` 超出 content-box 的部分，将裁剪掉

假设现在有这样的属性设置：

```javascript
	background-origin: border-box;

	background-clip: content-box;
```

上方代码的意思是，背景图片从边框部分开始加载，但是呢，超出内容区域的部分将被裁减掉。

## 同时设置多个背景

我们可以给一个盒子同时设置多个背景，用以逗号隔开即可。可用于自适应局。

代码举例：

```html
<!DOCTYPE html>
<html>
  <head lang="en">
    <meta charset="UTF-8" />
    <title></title>
    <style>
      .box {
        height: 416px;
        border: 1px solid #000;
        margin: 100px auto;
        /* 给盒子加多个背景，按照背景语法格式书写，多个背景使用逗号隔开 */
        background: url(images/bg1.png) no-repeat left top, url(images/bg2.png)
            no-repeat right top, url(images/bg3.png) no-repeat right bottom, url(images/bg4.png)
            no-repeat left bottom, url(images/bg5.png) no-repeat center;
      }
    </style>
  </head>
  <body>
    <div class="box"></div>
  </body>
</html>
```

实现效果如下：

![](http://img.smyhvae.com/20180207_2140.gif)

上方代码中，我们其实给盒子设置了五张小图，拼成的一张大图。当改变浏览器窗口大小时，可以自适应布局。

## 渐变：background-image

渐变是 CSS3 当中比较丰富多彩的一个特性，通过渐变我们可以实现许多炫丽的效果，有效的减少图片的使用数量，并且具有很强的适应性和可扩展性。

渐变分为：

- 线性渐变：沿着某条直线朝一个方向产生渐变效果。

- 径向渐变：从一个中心点开始沿着四周产生渐变效果。

- 重复渐变。

见下图：

![](http://img.smyhvae.com/20180208_1140.png)

### 线性渐变

格式：

```javascript

    background-image: linear-gradient(方向, 起始颜色, 终止颜色);

    background-image: linear-gradient(to right, yellow, green);
```

参数解释：

- 方向可以是：`to left`、`to right`、`to top`、`to bottom`、角度`30deg`（指的是顺时针方向 30°）。

格式举例：

```html
<!DOCTYPE html>
<html>
  <head lang="en">
    <meta charset="UTF-8" />
    <title></title>
    <style>
      div {
        width: 500px;
        height: 100px;
        margin: 10px auto;
        border: 1px solid #000;
      }

      /* 语法：
            linear-gradient(方向，起始颜色，终止颜色);
            方向：to left   to right  to top   to bottom 　角度　30deg
            起始颜色
            终止颜色
        */
      div:nth-child(1) {
        background-image: linear-gradient(to right, yellow, green);
      }

      /* 不写方向，表示默认的方向是：从上往下 */
      div:nth-child(2) {
        background-image: linear-gradient(yellow, green);
      }

      /* 方向可以指定角度 */
      div:nth-child(3) {
        width: 100px;
        height: 100px;
        background-image: linear-gradient(135deg, yellow, green);
      }

      /* 0%的位置开始出现黄色，40%的位置开始出现红色的过度。70%的位置开始出现绿色的过度，100%的位置开始出现蓝色 */
      div:nth-child(4) {
        background-image: linear-gradient(
          to right,
          yellow 0%,
          red 40%,
          green 70%,
          blue 100%
        );
      }

      /* 颜色之间，出现突变 */
      div:nth-child(5) {
        background-image: linear-gradient(
          45deg,
          yellow 0%,
          yellow 25%,
          blue 25%,
          blue 50%,
          red 50%,
          red 75%,
          green 75%,
          green 100%
        );
      }

      div:nth-child(6) {
        background-image: linear-gradient(
          to right,
          #000 0%,
          #000 25%,
          #fff 25%,
          #fff 50%,
          #000 50%,
          #000 75%,
          #fff 75%,
          #fff 100%
        );
      }
    </style>
  </head>
  <body>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
  </body>
</html>
```

效果如下：

![](http://img.smyhvae.com/20180207_2222.png)

举例：按钮

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>CSS3 渐变</title>
    <style>
      html,
      body {
        height: 100%;
      }

      body {
        margin: 0;
        padding: 0;
        background-color: #f8fcd4;
      }

      .nav {
        width: 800px;
        text-align: center;
        padding-top: 50px;
        margin: 0 auto;
      }

      /*设置按钮基本样式*/
      .nav a {
        display: inline-block;
        width: 100px;
        height: 30px;
        text-align: center;
        line-height: 30px;
        font-size: 14px;
        color: #fff;
        text-decoration: none;
        border: 1px solid #e59500;
        background-color: #ffb700;
        background-image: linear-gradient(to bottom, #ffb700 0%, #ff8c00 100%);
      }
    </style>
  </head>
  <body>
    <div class="nav">
      <a href="javascript:;">导航1</a>
      <a href="javascript:;">导航2</a>
      <a href="javascript:;">导航3</a>
      <a href="javascript:;">导航4</a>
      <a href="javascript:;">导航5</a>
      <a href="javascript:;">导航6</a>
    </div>
  </body>
</html>
```

效果：

![](http://img.smyhvae.com/20180207_2301.png)

### 径向渐变

格式：

```
	background-image: radial-gradient(辐射的半径大小, 中心的位置, 起始颜色, 终止颜色);

	background-image: radial-gradient(100px at center,yellow ,green);

```

解释：围绕中心点做渐变，半径是 150px，从黄色到绿色做渐变。

中心点的位置可以是：at left right center bottom top。如果以像素为单位，则中心点参照的是盒子的左上角。

当然，还有其他的各种参数。格式举例：

```html
<!DOCTYPE html>
<html>
  <head lang="en">
    <meta charset="UTF-8" />
    <title></title>
    <style>
      div {
        width: 250px;
        height: 250px;
        border: 1px solid #000;
        margin: 20px;
        float: left;
      }

      /*
            径向渐变：
            radial-gradient（辐射的半径大小, 中心的位置，起始颜色，终止颜色）;
            中心点位置：at  left  right  center bottom  top
        */

      /*辐射半径为100px，中心点在中间*/
      div:nth-child(1) {
        background-image: radial-gradient(100px at center, yellow, green);
      }

      /*中心点在左上角*/
      div:nth-child(3) {
        background-image: radial-gradient(at left top, yellow, green);
      }

      div:nth-child(2) {
        background-image: radial-gradient(at 50px 50px, yellow, green);
      }

      /*设置不同的颜色渐变*/
      div:nth-child(4) {
        background-image: radial-gradient(
          100px at center,
          yellow 0%,
          green 30%,
          blue 60%,
          red 100%
        );
      }

      /*如果辐射半径的宽高不同，那就是椭圆*/
      div:nth-child(5) {
        background-image: radial-gradient(100px 50px at center, yellow, green);
      }
    </style>
  </head>
  <body>
    <div class="box"></div>
    <div class="box"></div>
    <div class="box"></div>
    <div class="box"></div>
    <div class="box"></div>
  </body>
</html>
```

效果如下：

![](http://img.smyhvae.com/20180207_2256.png)

举例：利用径向渐变和边框圆角的属性，生成按钮。代码如下：

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>CSS3 渐变</title>
    <style>
      div:nth-child(1) {
        width: 200px;
        height: 200px;
        margin: 40px auto;
        border-radius: 100px;
        background-color: yellowgreen;
      }

      div:nth-child(2) {
        width: 200px;
        height: 200px;
        margin: 40px auto;
        border-radius: 100px;
        background-color: yellowgreen;
        background-image: radial-gradient(
          200px at 100px 100px,
          rgba(0, 0, 0, 0),
          rgba(0, 0, 0, 0.5)
        );
      }
    </style>
  </head>
  <body>
    <div></div>
    <div></div>
  </body>
</html>
```

效果如下：

![](http://img.smyhvae.com/20180208_1133.png)

上图中，给第二个 div 设置的透明度是从 0 到 0.5。如果设置的透明度是从 0 到 0，则样式无变化，和第一个 div 一样。如果设置的透明度是从 1 到 1，则盒子是全黑的。

## clip-path：裁剪出元素的部分区域做展示

`clip-path`属性可以创建一个只有元素的部分区域可以显示的剪切区域。区域内的部分显示，区域外的隐藏。

虽然`clip-path`不是背景属性，但这个属性非常强大，但往往会结合背景属性一起使用，达到一些效果。

举例：（鼠标悬停时，放大裁剪的区域）

```css
.div1 {
  width: 320px;
  height: 320px;
  border: 1px solid red;
  background: url(http://img.smyhvae.com/20191006_1410.png) no-repeat;
  background-size: cover;

  /* 裁剪出圆形区域 */
  clip-path: circle(50px at 100px 100px);
  transition: clip-path 0.4s;
}
.div1:hover {
  /* 鼠标悬停时，裁剪出更大的圆形 */
  clip-path: circle(80px at 100px 100px);
}
```

`clip-path`属性的好处是，即使做了任何裁剪，容器的占位大小是不变的。比如上方代码中，容器的占位大小一直都是 320px \* 320px。这样的话，也方便我们做一些动画效果。

`clip-path: polygon()`举例：

![](http://img.smyhvae.com/20191006_1430.png)

另外，通过 `clip-path: (svg)` 可以导入 svg 矢量图，实现 iOS 图标的圆角。这里就不详细展开了。

> 本文最初于 2015-10-03 发表于[博客园](http://www.cnblogs.com/smyhvae/p/4853995.html)，并在[GitHub](https://github.com/qianguyihao/Web)上持续更新前端的系列文章。欢迎在 GitHub 上关注我，一起入门和进阶前端。

## 本文主要内容

- CSS 概述
- CSS 和 HTML 结合的三种方式：`行内样式表`、`内嵌样式表`、`外部样式表`
- CSS 四种基本选择器：`标签选择器`、`类选择器`、`ID选择器`、`通用选择器`
- CSS 几种扩展选择器：`后代选择器`、`交集选择器`、`并集选择器`
- CSS 样式优先级

## 前言

## CSS 概述

CSS：Cascading Style Sheet，层叠样式表。CSS 的作用就是给 HTML 页面标签添加各种样式，定义网页的显示效果。简单一句话：CSS 将网页内容和显示样式进行分离，提高了显示功能。

css 的最新版本是 css3，我们目前学习的是 css2.1。 因为 css3 和 css2.1 不矛盾，必须先学 2.1 然后学 3。

接下来我们要讲一下为什么要使用 CSS。

HTML 的缺陷：

1. 不能够适应多种设备
2. 要求浏览器必须智能化足够庞大
3. 数据和显示没有分开
4. 功能不够强大

CSS 优点：

1. 使数据和显示分开
2. 降低网络流量
3. 使整个网站视觉效果一致
4. 使开发效率提高了（耦合性降低，一个人负责写 html，一个人负责写 css）

比如说，有一个样式需要在一百个页面上显示，如果是 html 来实现，那要写一百遍，现在有了 css，只要写一遍。现在，html 只提供数据和一些控件，完全交给 css 提供各种各样的样式。

### CSS 的重点知识点

盒子模型、浮动、定位

### CSS 整体感知

我们先来看一段简单的 css 代码：

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Document</title>
    <style>
      p {
        color: red;
        font-size: 30px;
        text-decoration: underline;
        font-weight: bold;
        text-align: center;
        font-style: italic;
      }
      h1 {
        color: blue;
        font-size: 50px;
        font-weight: bold;
        background-color: pink;
      }
    </style>
  </head>
  <body>
    <h1>我是大标题</h1>
    <p>我是内容</p>
  </body>
</html>
```

解释如下：

![](http://img.smyhvae.com/20170710_1605.png)

我们写 css 的地方是 style 标签，就是“样式”的意思，写在 head 里面。后面的课程中我们将知道，css 也可以写在单独的文件里面，现在我们先写在 style 标签里面。

如果在 sublime 中输入`<st`或者`<style`然后按 tab 键，可以自动生成的格式如下：（建议）

```html
<style type="text/css"></style>
```

type 表示“类型”，text 就是“纯文本”，css 也是纯文本。

但是，如果在 sublime 中输入`st`或者`style`然后按 tab 键，可以自动生成的格式如下：（不建议）

```html
<style></style>
```

css 对换行不敏感，对空格也不敏感。但是一定要有标准的语法。冒号，分号都不能省略。

## CSS 语法

语法格式：（其实就是键值对）

```html
选择器{ 属性名: 属性值; 属性名: 属性值; }
```

或者可以写成：

```css
选择器 {
  k: v;
  k: v;
  k: v;
  k: v;
}
选择器 {
  k: v;
  k: v;
  k: v;
  k: v;
}
```

解释：

- 选择器代表页面上的某类元素，选择器后一定是大括号。
- 属性名后必须用冒号隔开，属性值后用分号（最后一个属性可以不用分号，但最好还是加上分号）。
- 冒号和属性值之间可以留一个空格（编程习惯的经验）。
- 如果一个属性有多个值的话，那么多个值用空格隔开。

举例：

```css
p {
  color: red;
}
```

完整版代码举例：

```html
<style type="text/css">
  p {
    font-weight: bold;
    font-style: italic;
    color: red;
  }
</style>

<body>
  <p>洗白白</p>
  <p>你懂得</p>
  <p>我不会就这样轻易的狗带</p>
</body>
```

效果：

![](http://img.smyhvae.com/2015-10-03-css-01.png)

### css 代码的注释

格式：

```html
<style type="text/css">
  /*
		具体的注释
	*/

  p {
    font-weight: bold;
    font-style: italic;
    color: red;
  }
</style>
```

注意：CSS 只有`/* */`这种注释，没有`//`这种注释。而且注释要写在`<style>`标签里面才算生效哦。

接下来，我们要开始真正地讲 css 的知识咯。

css 怎么学？CSS 有两个知识部分：
1） 选择器，怎么选；
2） 属性，样式是什么

## CSS 的一些简单常见的属性

> 我们先来接触 CSS 的一些简单常见的属性，因为接下来需要用到。后期会专门用一篇文章来写 CSS 的属性。

以下属性值中，括号中的内容表示 sublime 中的快捷键。

字体颜色：（c）

```html
color:red;
```

color 属性的值，可以是英语单词，比如 red、blue、yellow 等等；也可以是 rgb、十六进制(后期详细讲)。

字号大小：（fos）

```html
font-size:40px;
```

font 就是“字体”，size 就是“尺寸”。px 是“像素”。单位必须加，不加不行。

背景颜色：（bgc）

```html
background-color: blue;
```

background 就是“背景”。

加粗：（fwb）

```html
font-weight: bold;
```

font 是“字体” weight 是“重量”的意思，bold 粗。

不加粗：（fwn）

```html
font-weight: normal;
```

normal 就是正常的意思。

斜体：（fsi）

```html
font-style: italic;
```

italic 就是“斜体”。

不斜体：（fsn）

```html
font-style: normal;
```

下划线：（tdu）

```html
text-decoration: underline;
```

decoration 就是“装饰”的意思。

没有下划线：（tdn）

```html
text-decoration:none;
```

## CSS 和 HTML 结合的方式（样式表）

CSS 和 HTML 结合的方式，其实就是问你 css 的代码放在哪里比较合适。CSS 代码理论上的位置是任意的，但通常写在`<style>`标签里。只要是`<style>`标签里的代码，那就是 css 代码，浏览器就是这样来进行解析的。

CSS 和 HTML 的结合方式有 3 种：

- 行内样式：在某个特定的标签里采用 style 属性。范围只针对此标签。
- 内嵌样式表：在页面的 head 里采用`<style>`标签。范围针对此页面。
- 引入外部样式表 css 文件的方式。这种引入方式又分为两种： - 1、采用`<link>`标签。例如：`<link rel = "stylesheet" type = "text/css" href = "a.css"></link>` - 2、采用 import，必须写在`<style>`标签中，并且必须是第一句。例如：`@import url(a.css) ;`

> 两种引入样式方式的区别：外部样式表中不能写<link>标签，但是可以写 import 语句。

下面来详细的讲一讲这三种方式。

### 1、CSS 和 HTML 结合方式一：行内样式

采用 style 属性。范围只针对此标签适用。

该方式比较灵活，但是对于多个相同标签的同一样式定义比较麻烦，适合局部修改。

举例：

```html
<p style="color:white;background-color:red">我不会就这样轻易的狗带</p>
```

效果：

![](http://img.smyhvae.com/2015-10-03-css-02.png)

### 2、CSS 和 HTML 结合方式二：内嵌样式表

在 head 标签中加入`<style>`标签，对多个标签进行统一修改，范围针对此页面。

该方式可以对单个页面的样式进行统一设置，但对于局部不够灵活。

举例：

```html
<style type="text/css">
  p {
    font-weight: bold;
    font-style: italic;
    color: red;
  }
</style>

<body>
  <p>洗白白</p>
  <p style="color:blue">你懂得</p>
</body>
```

![](http://img.smyhvae.com/2015-10-03-css-03.png)

### 3、CSS 和 HTML 结合方式三：引入外部样式表 css 文件

引入样式表文件的方式又分为两种：

- （1）采用`<link>`标签。例如：`<link rel = "stylesheet" type = "text/css" href = "a.css"></link>`

- （2）采用 import，必须写在`<style>`标签中，并且必须是第一句。例如：`@import url(a.css) ;`

> 两种引入样式方式的区别：外部样式表中不能写<link>标签，但是可以写 import 语句。

具体操作如下：

我们先在 html 页面的同级目录下新建一个`a.css`文件，那说明这里面的代码全是 css 代码，此时就没有必要再写`<style>`标签这几个字了。
`a.css`的代码如下：

```css
p {
  border: 1px solid red;
  font-size: 40px;
}
```

上方的 css 代码中，注意像素要带上 px 这个单位，不然不生效。
然后我们在 html 文件中通过`<link>`标签引入这个 css 文件就行了。效果如下：

![](http://img.smyhvae.com/2015-10-03-css-04.png)

这里再讲一个补充的知识：`<link>`标签的 rel 属性：。其属性值有以下两种：

- `stylesheet`：定义的样式表
- `alternate stylesheet`：候选的样式表

看字面意思可能比较难理解，我们来举个例子，一下子就明白了。
举例：

现在我们来定义 3 个样式表：

a.css：定义一个实线的黑色边框

```css
div {
  width: 200px;
  height: 200px;
  border: 3px solid black;
}
```

ba.css：蓝色的虚线边框

```css
div {
  width: 200px;
  height: 200px;
  border: 3px dotted blue;
}
```

c.css：来个背景图片

```css
div {
  width: 200px;
  height: 200px;
  border: 3px solid red;
  background-image: url("1.jpg");
}
```

然后我们在 html 文件中引用三个样式表：

```html
  <link rel = "stylesheet" type = "text/css" href = "a.css"></link>
  <link rel = "alternate stylesheet" type = "text/css" href = "b.css" title="第二种样式"></link>
  <link rel = "alternate stylesheet" type = "text/css" href = "c.css" title="第三种样式"></link>
```

上面引入的三个样式表中，后面两个样式表作为备选。注意备选的样式表中，title 属性不要忘记写，不然显示不出来效果的。现在来看一下效果：（在 IE 中打开网页）

![](http://img.smyhvae.com/2015-10-03-css-05.gif)

## CSS 的四种基本选择器

CSS 选择器：就是指定 CSS 要作用的标签，那个标签的名称就是选择器。意为：选择哪个容器。

CSS 的选择器分为两大类：基本选择题和扩展选择器。

基本选择器：

- 标签选择器：针对一类标签
- ID 选择器：针对某一个特定的标签使用
- 类选择器：针对你想要的所有标签使用
- 通用选择器（通配符）：针对所有的标签都适用（不建议使用）

下面来分别讲一讲。

### 1、标签选择器：选择器的名字代表 html 页面上的标签

标签选择器，选择的是页面上所有这种类型的标签，所以经常描述“共性”，无法描述某一个元素的“个性”。

举例：

```html
p{ font-size:14px; }
```

上方选择器的意思是说：所有的`<p>`标签里的内容都将显示 14 号字体。

效果：

![](http://img.smyhvae.com/2015-10-03-css-06.png)

再比如说，我想让“生命壹号学完了安卓，继续学前端哟”这句话中的“前端”两个变为红色字体，那么我可以用`<span>`标签把“前端”这两个字围起来，然后给`<span>`标签加一个标签选择器。

代码如下：

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Document</title>
    <style type="text/css">
      span {
        color: red;
      }
    </style>
  </head>
  <body>
    <p>生命壹号学完了安卓，继续学<span>前端</span>哟</p>
  </body>
</html>
```

【总结】需要注意的是：

（1）所有的标签，都可以是选择器。比如 ul、li、label、dt、dl、input。

（2）无论这个标签藏的多深，一定能够被选择上。

（3）选择的所有，而不是一个。

### 2、ID 选择器：规定用`#`来定义

针对某一个特定的标签来使用，只能使用一次。css 中的 ID 选择器以”#”来定义。

举例：

```html
#mytitle{ border:3px dashed green; }
```

效果：

![](http://img.smyhvae.com/2015-10-03-css-08.png)

id 选择器的选择符是“#”。

任何的 HTML 标签都可以有 id 属性。表示这个标签的名字。这个标签的名字，可以任取，但是：

- （1）只能有字母、数字、下划线。
- （2）必须以字母开头。
- （3）不能和标签同名。比如 id 不能叫做 body、img、a。

另外，特别强调的是：HTML 页面，不能出现相同的 id，哪怕他们不是一个类型。比如页面上有一个 id 为 pp 的 p，一个 id 为 pp 的 div，是非法的！

一个标签可以被多个 css 选择器选择：

比如，我们可以同时让标签选择器和 id 选择器作用于同一个标签。如下：

![](http://img.smyhvae.com/20170710_1737.png)

然后我们通过网页的审查元素看一下效果：

![](http://img.smyhvae.com/20170711_1540.png)

现在，假设选择器冲突了，比如 id 选择器说这个文字是红色的，标签选择器说这个文字是绿色的。那么听谁的？
实际上，css 有着非常严格的计算公式，能够处理冲突.

一个标签可以被多个 css 选择器选择，共同作用，这就是“层叠式”的第一层含义（第一层含义和第二层含义，放到 css 基础的第三篇文章里讲）。

### 3、类选择器：规定用圆点`.`来定义

、针对你想要的所有标签使用。优点：灵活。

css 中用`.`来表示类。举例如下：

```html
.one{ width:800px; }
```

效果：

![](http://img.smyhvae.com/2015-10-03-css-07.png)

和 id 非常相似，任何的标签都可以携带 id 属性和 class 属性。class 属性的特点：

- 特性 1：类选择器可以被多种标签使用。

- 特性 2：同一个标签可以使用多个类选择器。用空格隔开。举例如下：（正确）

```html
<h3 class="teshu  zhongyao">我是一个h3啊</h3>
```

初学者常见的错误，就是写成了两个 class。举例如下：（错误）

```html
<h3 class="teshu" class="zhongyao">我是一个h3啊</h3>
```

类选择器使用的举例：

类选择器的使用，能够决定一个人的 css 水平。

比如，我们现在要做下面这样一个页面：

![](http://img.smyhvae.com/20170711_1639.png)

正确的思路，就是用所谓“公共类”的思路，就是我们类就是提供“公共服务”，比如有绿、大、线，一旦携带这个类名，就有相应的样式变化。对应 css 里的代码如下：

```html
<style type="text/css">
  .lv {
    color: green;
  }
  .da {
    font-size: 30px;
  }
  .underline {
    text-decoration: underline;
  }
</style>
```

然后让每个标签去选取自己想要用的类选择器：

```html
<p class="lv da">段落1</p>
<p class="lv xian">段落2</p>
<p class="da xian">段落3</p>
```

也就是说：

（1）不要去试图用一个类名，把某个标签的所有样式写完。这个标签要多携带几个类，共同完成这个标签的样式。

（2）每一个类要尽可能小，有“公共”的概念，能够让更多的标签使用。

问题：到底用 id 还是用 class？

答案：尽可能的用 class，除非极特殊的情况可以用 id。

原因：id 是 js 用的。也就是说，js 要通过 id 属性得到标签，所以 css 层面尽量不用 id，要不然 js 就很别扭。另一层面，我们会认为一个有 id 的元素，有动态效果。

举例如下：

![](http://img.smyhvae.com/20170711_1706.png)

上图所示，css 和 js 都在用同一个 id，会出现不好沟通的情况。

我们记住这句话：类上样式，id 上行为。意思是说，`class`属性交给 css 使用，`id`属性交给 js 使用。

上面这三种选择器的区别：

- 标签选择器针对的是页面上的一类标签。
- ID 选择器是只针对特定的标签(一个)，ID 是此标签在此页面上的唯一标识。
- 类选择器可以被多种标签使用。

### 4、通配符`*`：匹配任何标签

通用选择器，将匹配任何标签。不建议使用，IE 有些版本不支持，大网站增加客户端负担。

效率不高，如果页面上的标签越多，效率越低，所以页面上不能出现这个选择器。

举例：

```css
* {
  margin-left: 0px;
  margin-top: 0px;
}
```

效果：

![](http://img.smyhvae.com/2015-10-03-css-09.png)

## CSS 的几种高级选择器

高级选择器：

- 后代选择器：用空格隔开
- 交集选择器：选择器之间紧密相连
- 并集选择器（分组选择器）：用逗号隔开
- 伪类选择器

下面详细讲一下这几种高级（扩展）选择器。

### 1、后代选择器: 定义的时候用空格隔开

对于`E F`这种格式，表示所有属于 E 元素后代的 F 元素，有这个样式。空格就表示后代。

后代选择器，就是一种平衡：共性、特性的平衡。当要把某一个部分的所有的什么，进行样式改变，就要想到后代选择器。

后代选择器，描述的是祖先结构。

看定义可能有点难理解，我们来看例子吧。

举例 1：

```html
<style type="text/css">
  .div1 p {
    color: red;
  }
</style>
```

空格就表示后代。`.div1 p` 表示`.div1`的后代所有的`p`。

这里强调一下：这两个标签不一定是连续紧挨着的，只要保持一个后代的关联即可。也就是说，选择的是后代，不一定是儿子。

举例：

```html
<style type="text/css">
  h3 b i {
    color: red;
  }
</style>
```

上方代码的意思是说：定义了`<h3>`标签中的`<b>`标签中的`<i>`标签的样式。
同理：h3 和 b 和 i 标签不一定是连续紧挨着的，只要保持一个后代的关联即可。

效果：

![](http://img.smyhvae.com/2015-10-03-css-11.png)

或者还有下面这种写法：

![](http://img.smyhvae.com/2015-10-03-css-12.png)

上面的这种写法，`<h3>`标签和`<i>`标签并不是紧挨着的，但他们保持着一种后代关系。

还有下面这种写法：（含类选择器、id 选择器都是可以的）

![](http://img.smyhvae.com/2015-10-03-css-13.png)

我们在开头说了：后代选择器，描述的是一种祖先结构。我们举个例子来说明这句话：

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Document</title>
    <style type="text/css">
      div div p {
        color: red;
      }
    </style>
  </head>
  <body>
    <div>
      <div class="div2">
        <div class="div3">
          <div class="div4">
            <p>我是什么颜色？</p>
          </div>
        </div>
      </div>
    </div>
  </body>
</html>
```

上面 css 中的`div div p`，也能使文字的颜色变红。通过浏览器的审查元素，我们可以看到 p 元素的祖先列表：

![](http://img.smyhvae.com/20170711_1836.png)

讲到这里，我们再提一个 sublme 的快捷键。

在 sublime 中输入`p#haha`，按 tab 键后，会生成`<p id="haha"></p>`。

在 sublime 中输入`p.haha`，按 tab 键后，会生成`<p class="haha"></p>`。

### 2、交集选择器：定义的时候紧密相连

定义交集选择器的时候，两个选择器之间紧密相连。一般是以标签名开头，比如`div.haha`，再比如`p.special`。

如果后一个选择器是类选择器，则写为`div.special`；如果后一个选择器 id 选择器，则写为`div#special`。

来看下面这张图就明白了：

![](http://img.smyhvae.com/20170711_1851.png)

```css
h3.special {
  color: red;
}
```

选择的元素要求同时满足两个条件：必须是 h3 标签，然后必须是 special 标签。

举例：

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>交集选择器测试</title>
    <style type="text/css">
      h3.special {
        color: red;
      }
    </style>
  </head>
  <body>
    <h3 class="special zhongyao">标题1</h3>
    <h3 class="special">我也是标题</h3>
    <p>我是段落</p>
  </body>
</html>
```

效果如下：

![](http://img.smyhvae.com/20170711_1852.png)

注意，交集选择器没有空格。所以，没有空格的`div.red`（交集选择器）和有空格的`div .red`（后代选择器）不是一个意思。

交集选择器可以连续交：（一般不要这么写）

```css
h3.special.zhongyao {
  color: red;
}
```

上面这种写法，是 IE7 开始兼容的，IE6 不兼容。

### 3、并集选择器：定义的时候用逗号隔开

三种基本选择器都可以放进来。

举例：

```css
p,
h1,
#mytitle,
.one {
  color: red;
}
```

效果：

![](http://img.smyhvae.com/2015-10-03-css-10.png)

## 一些 CSS3 选择器

> 所有的 CSS3 选择器，我们放在 CSS3 的内容里介绍。本文暂时先接触一部分。

### 浏览器的兼容性问题

> 我们可以用`IETester`这个软件测一下 CSS 在各个版本 IE 浏览器上的显示效果。

IE： 微软的浏览器，随着操作系统安装的。所以每个 windows 都有 IE 浏览器。各版本如下：

- windows xp 操作系统安装的 IE6
- windows vista 操作系统安装的 IE7
- windows 7 操作系统安装的 IE8
- windows 8 操作系统安装的 IE9
- windows10 操作系统安装的 edge

浏览器兼容问题，要出，就基本上就是出在 IE6、7 身上，这两个浏览器是非常低级的浏览器。

为了测试浏览器 CSS 3 的兼容性，我们可以在网上搜"css3 机器猫"关键字，然后在不同的浏览器中打开如下链接：

- <http://www1.pconline.com.cn/pcedu/specialtopic/css3-doraemon/>

测试结果如下：

![](http://img.smyhvae.com/20170711_1939.png)

我们可以在[百度统计](http://tongji.baidu.com/data/)里查看浏览器的市场占有率：

- IE9 5.94%
- IE8 21.19%
- IE7 4.79%
- IE6 4.11%

我们可以在<http://html5test.com/results/desktop.html>中查看

![](http://img.smyhvae.com/20170711_1948.png)

我们要知道典型的 IE6 兼容问题（面试要问），但是做项目我们兼容到 IE8 即可。不解决 IE8 以下的兼容问题，目的在于：培养更高的兴趣和眼光，别天天的跟 IE6 较劲。

我们可以用「IETester」软件看看 css 在各个浏览器中的显示效果。

### 1.子代选择器，用符号`>`表示

> IE7 开始兼容，IE6 不兼容。

```css
div > p {
  color: red;
}
```

div 的儿子 p。和 div 的后代 p 的截然不同。

能够选择：

```html
<div>
  <p>我是div的儿子</p>
</div>
```

不能选择：

```html
<div>
  <ul>
    <li>
      <p>我是div的重孙子</p>
    </li>
  </ul>
</div>
```

### 2.序选择器

> IE8 开始兼容；IE6、7 都不兼容

设置无序列表`<ul>`中的第一个`<li>`为红色：

```html
<style type="text/css">
  ul li:first-child {
    color: red;
  }
</style>
```

设置无序列表`<ul>`中的最后一个`<li>`为红色：

```css
ul li:last-child {
  color: blue;
}
```

序选择器还有更复杂的用法，以后再讲。

由于浏览器的更新需要过程，所以现在如果公司还要求兼容 IE6、7，那么就要自己写类名：

```html
<ul>
  <li class="first">项目</li>
  <li>项目</li>
  <li>项目</li>
  <li>项目</li>
  <li>项目</li>
  <li>项目</li>
  <li>项目</li>
  <li>项目</li>
  <li>项目</li>
  <li class="last">项目</li>
</ul>
```

用类选择器来选择第一个或者最后一个：

```html
ul li.first{ color:red; } ul li.last{ color:blue; }
```

### 3.下一个兄弟选择器

> IE7 开始兼容，IE6 不兼容。

`+`表示选择下一个兄弟

```html
<style type="text/css">
  h3 + p {
    color: red;
  }
</style>
```

上方的选择器意思是：选择的是 h3 元素后面紧挨着的第一个兄弟。

```html
<h3>我是一个标题</h3>
<p>我是一个段落</p>
<p>我是一个段落</p>
<p>我是一个段落</p>
<h3>我是一个标题</h3>
<p>我是一个段落</p>
<p>我是一个段落</p>
<p>我是一个段落</p>
<h3>我是一个标题</h3>
<p>我是一个段落</p>
<p>我是一个段落</p>
<p>我是一个段落</p>
<h3>我是一个标题</h3>
```

效果如下：

![](http://img.smyhvae.com/20170711_1950.png)

这种选择器作用不大。

> 本文最初发表于[博客园](http://www.cnblogs.com/smyhvae/p/8280814.html)，并在[GitHub](https://github.com/qianguyihao/Web)上持续更新前端的系列文章。欢迎在 GitHub 上关注我，一起入门和进阶前端。

> 以下是正文。

## 伪类（伪类选择器）

伪类：同一个标签，根据其不同的种状态，有不同的样式。这就叫做“伪类”。伪类用冒号来表示。

比如 div 是属于 box 类，这一点很明确，就是属于 box 类。但是 a 属于什么类？不明确。因为需要看用户点击前是什么状态，点击后是什么状态。所以，就叫做“伪类”。

### 静态伪类和动态伪类

伪类选择器分为两种。

（1）静态伪类：只能用于超链接的样式。如下：

- `:link` 超链接点击之前
- `:visited` 链接被访问过之后

PS：以上两种样式，只能用于超链接。

（2）动态伪类：针对所有标签都适用的样式。如下：

- `:hover` “悬停”：鼠标放到标签上的时候
- `:active` “激活”： 鼠标点击标签，但是不松手时。
- `:focus` 是某个标签获得焦点时的样式（比如某个输入框获得焦点）

## 超链接 a 标签

### 超链接的四种状态

a 标签有 4 种伪类（即对应四种状态），要求背诵。如下：

- `:link` “链接”：超链接点击之前
- `:visited` “访问过的”：链接被访问过之后
- `:hover` “悬停”：鼠标放到标签上的时候
- `:active` “激活”： 鼠标点击标签，但是不松手时。

对应的代码如下：

```html
<style type="text/css">
  /*让超链接点击之前是红色*/
  a:link {
    color: red;
  }

  /*让超链接点击之后是绿色*/
  a:visited {
    color: orange;
  }

  /*鼠标悬停，放到标签上的时候*/
  a:hover {
    color: green;
  }

  /*鼠标点击链接，但是不松手的时候*/
  a:active {
    color: black;
  }
</style>
```

记住，在 css 中，这四种状态必须按照固定的顺序写：

> a:link 、a:visited 、a:hover 、a:active

如果不按照顺序，那么将失效。“爱恨准则”：love hate。必须先爱，后恨。

看一下这四种状态的动图效果：

![](http://img.smyhvae.com/20180113_2239.gif)

### 超链接的美化

问：既然`a{}`定义了超链的属性，和`a:link{}`定义了超链点击之前的属性，那这两个有啥区别呢？

答：

`a{}`和`a:link{}`的区别：

- `a{}`定义的样式针对所有的超链接(包括锚点)
- `a:link{}`定义的样式针对所有写了 href 属性的超链接(不包括锚点)

超链接 a 标签在使用的时候，比较难。因为不仅仅要控制 a 这个盒子，也要控制它的伪类。

我们一定要将 a 标签写在前面，将`:link、:visited、:hover、:active`这些伪类写在后面。

针对超链接，我们来举个例子：

![](http://img.smyhvae.com/20170810_2235.gif)

为了实现上面这个效果，完整版代码如下：

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en">
  <head>
    <meta http-equiv="Content-Type" content="text/html;charset=UTF-8" />
    <title>Document</title>
    <style type="text/css">
      * {
        margin: 0;
        padding: 0;
      }
      .nav {
        width: 960px;
        height: 50px;
        border: 1px solid red;
        margin: 100px auto;
      }
      .nav ul {
        /*去掉小圆点*/
        list-style: none;
      }
      .nav ul li {
        float: left;
        width: 120px;
        height: 50px;
        /*让内容水平居中*/
        text-align: center;
        /*让行高等于nav的高度，就可以保证内容垂直居中*/
        line-height: 50px;
      }
      .nav ul li a {
        display: block;
        width: 120px;
        height: 50px;
      }
      /*两个伪类的属性，可以用逗号隔开*/
      .nav ul li a:link,
      .nav ul li a:visited {
        text-decoration: none;
        background-color: purple;
        color: white;
      }
      .nav ul li a:hover {
        background-color: orange;
      }
    </style>
  </head>
  <body>
    <div class="nav">
      <ul>
        <li><a href="#">网站栏目</a></li>
        <li><a href="#">网站栏目</a></li>
        <li><a href="#">网站栏目</a></li>
        <li><a href="#">网站栏目</a></li>
        <li><a href="#">网站栏目</a></li>
        <li><a href="#">网站栏目</a></li>
        <li><a href="#">网站栏目</a></li>
        <li><a href="#">网站栏目</a></li>
      </ul>
    </div>
  </body>
</html>
```

上方代码中，我们发现，当我们在定义`a:link`和 `a:visited`这两个伪类的时候，如果它们的属性相同，我们其实可以写在一起，用逗号隔开就好，摘抄如下：

```css
.nav ul li a {
  display: block;
  width: 120px;
  height: 50px;
}
/*两个伪类的属性，可以用逗号隔开*/
.nav ul li a:link,
.nav ul li a:visited {
  text-decoration: none;
  background-color: purple;
  color: white;
}
.nav ul li a:hover {
  background-color: orange;
}
```

如上方代码所示，最标准的写法，就是把 link、visited、hover 这三个伪类都要写。但是前端开发工程师在大量的实践中，发现不写 link、visited 也挺兼容。写法是：

> a:link、a:visited 都是可以省略的，简写在 a 标签里面。也就是说，a 标签涵盖了 link、visited 的状态（前提是都具有了相同的属性）。写法如下：

```css
.nav ul li a {
  display: block;
  width: 120px;
  height: 50px;
  text-decoration: none;
  background-color: purple;
  color: white;
}
.nav ul li a:hover {
  background-color: orange;
}
```

当然了，在写`a:link`、`a:visited`这两个伪类的时候，要么同时写，要么同时不写。如果只写`a`属性和`a:link`属性，不规范。

## 动态伪类举例

我们在第一段中描述过，下面这三种动态伪类，针对所有标签都适用。

- `:hover` “悬停”：鼠标放到标签上的时候
- `:active` “激活”： 鼠标点击标签，但是不松手时。
- `:focus` 是某个标签获得焦点时的样式（比如某个输入框获得焦点）

我们不妨来举下例子。

举例 1：

```html
<style type="text/css">
  /*
	伪类选择器：动态伪类
  */

  /*
	让文本框获取焦点时：
	边框：#FF6F3D这种橙色
	文字：绿色
	背景色：#6a6a6a这种灰色
   */
  input:focus {
    border: 3px solid #ff6f3d;
    color: white;
    background-color: #6a6a6a;
  }

  /*
	鼠标放在标签上时显示蓝色
    */
  label:hover {
    color: blue;
  }

  /*
	点击标签鼠标没有松开时显示红色
    */
  label:active {
    color: red;
  }
</style>
```

效果：

![](http://img.smyhvae.com/2015-10-03-css-02.gif)

利用这个`hover`属性，我们同样对表格做一个样式的设置：
表格举例：

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="Generator" content="EditPlus®" />
    <meta name="Author" content="" />
    <meta name="Keywords" content="" />
    <meta name="Description" content="" />
    <title>Document</title>
    <style type="text/css">
      /*整个表格的样式*/
      table {
        width: 300px;
        height: 200px;
        border: 1px solid blue;
        /*border-collapse属性：对表格的线进行折叠*/
        border-collapse: collapse;
      }

      /*鼠标悬停时，让当前行显示#868686这种灰色*/
      table tr:hover {
        background: #868686;
      }

      /*每个单元格的样式*/
      table td {
        border: 1px solid red;
      }
    </style>
  </head>
  <body>
    <table>
      <tr>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
      </tr>
      <tr>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
      </tr>
      <tr>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
      </tr>
    </table>
  </body>
</html>
```

效果：

![](http://img.smyhvae.com/2015-10-03-css-04.gif)

> 本文最初于 2017-07-29 发表于[博客园](http://www.cnblogs.com/smyhvae/p/7253929.html)，并在[GitHub](https://github.com/qianguyihao/Web)上持续更新前端的系列文章。欢迎在 GitHub 上关注我，一起入门和进阶前端。

> 以下是正文。

## 本文重点

- CSS 的继承性
- CSS 的层叠性
  - 计算权重
  - 权重问题大总结
  - CSS 样式表的冲突的总结
- 权重问题深入
  - 同一个标签，携带了多个类名
  - !important 标记

## CSS 的继承性

我们来看下面这样的代码，来引入继承性：

![](http://img.smyhvae.com/20170724_2359.png)

上方代码中，我们给 div 标签增加红色属性，却发现，div 里的每一个子标签`<p>`也增加了红色属性。于是我们得到这样的结论：

> 有一些属性，当给自己设置的时候，自己的后代都继承上了，这个就是继承性。

继承性是从自己开始，直到最小的元素。

但是呢，如果再给上方的代码加一条属性：

![](http://img.smyhvae.com/20170725_2122.jpg)

上图中，我们给 div 加了一个 border，但是发现只有 div 具备了 border 属性，而 p 标签却没有 border 属性。于是我们可以得出结论：

- 关于文字样式的属性，都具有继承性。这些属性包括：color、 text-开头的、line-开头的、font-开头的。

- 关于盒子、定位、布局的属性，都不能继承。

以后当我们谈到 css 有哪些特性的时候，我们要首先想到继承性。而且，要知道哪些属性具有继承性、哪些属性没有继承性。

## CSS 的层叠性

很多公司如果要笔试，那么一定会考层叠性。

### 层叠性：计算权重

层叠性：就是 css 处理冲突的能力。 所有的权重计算，没有任何兼容问题！

CSS 像艺术家一样优雅，像工程师一样严谨。

我们来看一个例子，就知道什么叫层叠性了。

![](http://img.smyhvae.com/20170725_2132.png)

上图中，三种选择器同时给 P 标签增加颜色的属性，但是，文字最终显示的是蓝色，这个时候，就出现了层叠性的情况。

当多个选择器，选择上了某个元素的时候，要按照如下顺序统计权重：

- id 选择器
- 类选择器、属性选择器、伪类选择器
- 标签选择器、伪元素选择器

因为对于相同方式的样式表，其选择器排序的优先级为：ID 选择器 > 类选择器 > 标签选择器

针对上面这句话，我们接下来举一些复杂一点的例子。

### 层叠性举例

#### 举例 1：计算权重

![](http://img.smyhvae.com/20170725_2138.png)

如上图所示，统计各个选择器的数量，优先级高的胜出。文字的颜色为红色。

PS：不进位，实际上能进位（奇淫知识点：255 个标签，等于 1 个类名）但是没有实战意义！

#### 举例 2：权重相同时

![](http://img.smyhvae.com/20170725_2250.png)

上图可以看到，第一个样式和第二个样式的权重相同。但第二个样式的书写顺序靠后，因此以第二个样式为准（就近原则）。

#### 举例 3：具有实战性的例子

![](http://img.smyhvae.com/20170726_2221.png)

现在我要让一个列表实现上面的这种样式：第一个 li 为红色，剩下的 li 全部为蓝色。

如果写成下面这种代码是无法实现的：

![](http://img.smyhvae.com/20170726_2225.png)

无法实现的原因很简单，计算一下三个选择器的权重就清楚了，显然第二个样式被第一个样式表覆盖了。

正确的做法是：（非常重要）

![](http://img.smyhvae.com/20170726_2229.png)

上图中，第二个样式比第一个样式的权重要大。因此在实战中可以实现这种效果：所有人当中，让某一个人为红，让其他所有人为蓝。

这种方式好用是好用，但用好很难。

就拿上方代码来举例，为了达到这种效果，即为了防止权重不够，比较稳妥的做法是：把第二个样式表照着第一个样式表来写，在此基础上，给第二个样式表再加一个权重。

上面这个例子很具有实战性。

#### 举例 4：继承性造成的影响

这里需要声明一点：

> 如果不能直接选中某个元素，通过继承性影响的话，那么权重是 0。

为了验证上面这句话，我们来看看下面这样的例子：

![](http://img.smyhvae.com/20170727_0843.png)

另外：如果大家的权重相同，那么就采用就近原则：谁描述的近，听谁的。举例如下：(box3 描述得最近，所以采用 box3 的属性)

![](http://img.smyhvae.com/20190122_1530.png)

上方代码的文字版如下：

```html
<!DOCTYPE html>
<html lang="">
  <head>
    <meta />
    <meta />
    <meta />
    <title>Document</title>
    <style>
      #box1 {
        color: red;
      }

      #box2 {
        color: green;
      }

      #box3 {
        color: blue;
      }
    </style>
  </head>
  <body>
    <div id="box1">
      <div id="box2">
        <div id="box3"><p>猜猜我是什么颜色</p></div>
      </div>
    </div>
  </body>
</html>
```

### 层叠性：权重计算的问题大总结（非常重要）

层叠性。层叠性是一种能力，就是处理冲突的能力。当不同选择器，对一个标签的同一个样式，有不同的值，听谁的？这就是冲突。css 有着严格的处理冲突的机制。

通过列举上面几个例子，我们对权重问题做一个总结。

![](http://img.smyhvae.com/20170727_2050.png)

上面这个图非常重要，我们针对这个图做一个文字描述：

- 选择上了，数权重，(id 的数量，类的数量，标签的数量)。如果权重一样，谁写在后面听谁的。
- 没有选择上，通过继承影响的，就近原则，谁描述的近听谁的。如果描述的一样近，比如选择器权重，如果权重再一样重，谁写在后面听谁的。

### CSS 样式表的冲突的总结

- 1、对于相同的选择器（比如同样都是类选择器），其样式表排序：行级样式 > 内嵌样式表 > 外部样式表（就近原则）
- 2、对于相同类型的样式表（比如同样都是内部样式表），其选择器排序：ID 选择器 > 类选择器 > 标签选择器
- 3、外部样式表的 ID 选择器 > 内嵌样式表的标签选择器

> 总结：就近原则。ID 选择器优先级最大。

举例：如果都是内嵌样式表，优先级的顺序如下：（ID 选择器 > 类选择器 > 标签选择器）

![](http://img.smyhvae.com/2015-10-03-css-14.png)

另外还有两个冲突的情况：

- 1、对同一个标签，如果用到的都是内嵌样式表，且权重一致，那它的优先级：定义的 CSS 样式表中，谁最近，就用谁。
- 2、对于同一个标签，如果用到的都是外部样式表，且权重一致，那它的优先级：html 文件中，引用样式表的位置越近，就用谁。

例如：

![](http://img.smyhvae.com/2015-10-03-css-16.png)

### 题目演示

CSS 的层叠性讲完了，我们来做几个题目吧。

#### 题目 1

![](http://img.smyhvae.com/20170727_0851.png)

#### 题目 2

![](http://img.smyhvae.com/20170727_0853.png)

#### 题目 3

![](http://img.smyhvae.com/20170727_0855.png)

#### 题目 4

![](http://img.smyhvae.com/20170727_0857.png)

## 权重问题深入

### 同一个标签，携带了多个类名，有冲突：

这里需要补充两种冲突的情况：

- 1、对同一个标签，如果用到了了多个相同的内嵌样式表，它的优先级：定义的样式表中，谁最近，就用谁。
- 2、对于同一个标签，如果引用了多个相同的外部样式表，它的优先级：html 文件中，引用样式表的位置越近，就用谁。

例如：（就近原则）

![](http://img.smyhvae.com/20170727_2021.png)

上图中，文字显示的颜色均为红色。因为这和在标签中的挂类名的书序无关，只和 css 的顺序有关。

### !important 标记：优先级最高

来看个很简单的例子：

![](http://img.smyhvae.com/20170727_2029.png)

上图中，显然 id 选择器的权重最大，所以文字的颜色是红色。

如果我们想让文字的颜色显示为绿色，只需要给标签选择器的加一个`!important`标记，此时其权重为无穷大。如下：

![](http://img.smyhvae.com/20170727_2035_2.png)

important 是英语里面的“重要的”的意思。我们可以通过如下语法：

```
k:v !important;
```

来给一个属性提高权重。这个属性的权重就是无穷大。

注意，一定要注意语法的正确性。

正确的语法：

```
font-size:60px !important;
```

错误的语法：

```
font-size:60px; !important;    不能把!important写在外面
font-size:60px important;      不能忘记感叹号
```

`!important`标记需要强调如下 3 点：

（1）!important 提升的是一个属性，而不是一个选择器

```css
		p{
			color:red !important;    只写了这一个!important，所以只有字体颜色属性提升了权重
			font-size: 100px ;       这条属性没有写!important，所以没有提升权重
		}
		#para1{
			color:blue;
			font-size: 50px;
		}
		.spec{
			color:green;
			font-size: 20px;
		}
```

所以，综合来看，字体颜色是 red（听 important 的）；字号是 50px（听 id 的）。

（2）!important 无法提升继承的权重，该是 0 还是 0

比如 HTML 结构：

```html
<div>
  <p>哈哈哈哈哈哈哈哈</p>
</div>
```

有 CSS 样式：

```css
div {
  color: red !important;
}
p {
  color: blue;
}
```

由于 div 是通过继承性来影响文字颜色的，所以!important 无法提升它的权重，权重依然是 0。

干不过 p 标签，因为 p 标签是实实在在选中了，所以字是蓝色的（以 p 为准）。

(3)!important 不影响就近原则

如果大家都是继承来的，按理说应该按照“就近原则”，那么 important 能否影响就近原则呢？
答案是：不影响。远的，永远是远的。不能给远的写一个 important，干掉近的。

为了验证这个问题，我们可以搞两层具有继承性的标签，然后给外层标签加一个!important，最终看看就近原则有没有被打破。举例如下：

![](http://img.smyhvae.com/20170727_2046.png)

PS：做网站的时候，!important 尽量不要用。否则会让 css 写的很乱。

## 知识回顾

> 我们把以上内容和上一篇文章做一个简单的知识回顾。

### CSS 属性

> css 属性，面试的时候会有笔试，笔试没有智能提示的。

加粗，倾斜，下划线：

```
font-weight:bold;
font-style:italic;
text-decoration:underline;
```

背景颜色、前景色：

```
background-color:red;
color:red;
```

### class 和 id 的区别

class 用于 css 的，id 用于 js 的。

1）class 页面上可以重复。id 页面上唯一，不能重复。
2）一个标签可以有多个 class，用空格隔开。但是 id 只能有 id。

### 各种选择器(浏览器兼容性)

IE6 层面兼容的选择器： 标签选择器、id 选择器、类选择器、后代、交集选择器、并集选择器、通配符。如下：

```
p
#box
.spec
div p
div.spec
div,p
*
```

IE7 能够兼容的：儿子选择器、下一个兄弟选择器。如下：

```
div>p
h3+p
```

IE8 能够兼容的：

```
ul li:first-child
ul li:last-child
```

### css 两个性质

- 继承性：好的事儿。继承从上到下，哪些能？哪些不能？

- 层叠性：冲突，多个选择器描述了同一个属性，听谁的？

再看几个题目：

![](http://img.smyhvae.com/20170727_0900.png)

![](http://img.smyhvae.com/20170727_0901.png)

![](http://img.smyhvae.com/20170727_0902.png)

![](http://img.smyhvae.com/20170727_0903.png)

> 本文最初发表于[博客园](http://www.cnblogs.com/smyhvae/p/7256371.html)，并在[GitHub](https://github.com/qianguyihao/Web)上持续更新。以下是正文。

## 盒子模型

### 前言

盒子模型，英文即 box model。无论是 div、span、还是 a 都是盒子。

但是，图片、表单元素一律看作是文本，它们并不是盒子。这个很好理解，比如说，一张图片里并不能放东西，它自己就是自己的内容。

### 盒子中的区域

一个盒子中主要的属性就 5 个：width、height、padding、border、margin。如下：

- width 和 height：内容的宽度、高度（不是盒子的宽度、高度）。
- padding：内边距。
- border：边框。
- margin：外边距。

盒子模型的示意图：

![](http://img.smyhvae.com/20170727_2128.png)

代码演示：

![](http://img.smyhvae.com/20170727_2326.png)

上面这个盒子，width:200px; height:200px; 但是真实占有的宽高是 302\*302。 这是因为还要加上 padding、border。

注意：宽度和真实占有宽度，不是一个概念！来看下面这例子。

### 标准盒模型和 IE 盒模型

> 我们目前所学习的知识中，以标准盒子模型为准。

标准盒子模型：

![](http://img.smyhvae.com/2015-10-03-css-27.jpg)

IE 盒子模型：

![](http://img.smyhvae.com/2015-10-03-css-30.jpg)

上图显示：

在 CSS 盒子模型 (Box Model) 规定了元素处理元素的几种方式：

- width 和 height：内容的宽度、高度（不是盒子的宽度、高度）。
- padding：内边距。
- border：边框。
- margin：外边距。

CSS 盒模型和 IE 盒模型的区别：

- 在 <font color="#0000FF">标准盒子模型</font>中，<font color="#0000FF">width 和 height 指的是内容区域</font>的宽度和高度。增加内边距、边框和外边距不会影响内容区域的尺寸，但是会增加元素框的总尺寸。

- <font color="#0000FF">IE 盒子模型</font>中，<font color="#0000FF">width 和 height 指的是内容区域+border+padding</font>的宽度和高度。

注：Android 中也有 margin 和 padding 的概念，意思是差不多的，如果你会一点 Android，应该比较好理解吧。区别在于，Android 中没有 border 这个东西，而且在 Android 中，margin 并不是控件的一部分，我觉得这样做更合理一些，呵呵。

### `<body>`标签也有 margin

`<body>`标签有必要强调一下。很多人以为`<body>`标签占据的是整个页面的全部区域，其实是错误的，正确的理解是这样的：整个网页最大的盒子是`<document>`，即浏览器。而`<body>`是`<document>`的儿子。浏览器给`<body>`默认的 margin 大小是 8 个像素，此时`<body>`占据了整个页面的一大部分区域，而不是全部区域。来看一段代码。

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="Generator" content="EditPlus®" />
    <meta name="Author" content="" />
    <meta name="Keywords" content="" />
    <meta name="Description" content="" />
    <title>Document</title>

    <style type="text/css">
      div {
        width: 100px;
        height: 100px;
        border: 1px solid red;
        padding: 20px;
        margin: 30px;
      }
    </style>
  </head>

  <body>
    <div>有生之年</div>
    <div>狭路相逢</div>
  </body>
</html>
```

上面的代码中，我们对 div 标签设置了边距等信息。打开 google 浏览器，按住 F12，显示效果如下：

![](http://img.smyhvae.com/20151003_27.png)

## 认识 width、height

一定要知道，在前端开发工程师眼中，世界中的一切都是不同的。

比如说，丈量稿纸，前端开发工程师只会丈量内容宽度：

![](http://img.smyhvae.com/20170727_2329.png)

下面这两个盒子，真实占有宽高，都是 302\*302：

盒子 1：

```css
.box1 {
  width: 100px;
  height: 100px;
  padding: 100px;
  border: 1px solid red;
}
```

盒子 2：

```css
.box2 {
  width: 250px;
  height: 250px;
  padding: 25px;
  border: 1px solid red;
}
```

真实占有宽度 = 左 border + 左 padding + width + 右 padding + 右 border

上面这两个盒子的盒模型图如下：

![](http://img.smyhvae.com/20170728_0925.png)

如果想保持一个盒子的真实占有宽度不变，那么加 width 的时候就要减 padding。加 padding 的时候就要减 width。因为盒子变胖了是灾难性的，这会把别的盒子挤下去。

## 认识 padding

### padding 区域也有颜色

padding 就是内边距。padding 的区域有背景颜色，css2.1 前提下，并且背景颜色一定和内容区域的相同。也就是说，background-color 将填充所有 border 以内的区域。

效果如下：

![](http://img.smyhvae.com/20170728_1005.png)

### padding 有四个方向

padding 是 4 个方向的，所以我们能够分别描述 4 个方向的 padding。

方法有两种，第一种写小属性；第二种写综合属性，用空格隔开。

小属性的写法：

```css
padding-top: 30px;
padding-right: 20px;
padding-bottom: 40px;
padding-left: 100px;
```

综合属性的写法：(上、右、下、左)（顺时针方向，用空格隔开。margin 的道理也是一样的）

```css
padding: 30px 20px 40px 100px;
```

如果写了四个值，则顺序为：上、右、下、左。

如果只写了三个值，则顺序为：上、右、下。??和右一样。

如果只写了两个值，比如说：

```
padding: 30px 40px;
```

则顺序等价于：30px 40px 30px 40px;

要懂得，用小属性层叠大属性。比如：

```
padding: 20px;
padding-left: 30px;
```

上面的 padding 对应盒子模型为：

![](http://img.smyhvae.com/20170728_1039.png)

下面的写法：

```
padding-left: 30px;
padding: 20px;
```

第一行的小属性无效，因为被第二行的大属性层叠掉了。

下面的题，会做了，说明你明白了。

### 一些题目

题目 1：说出下面盒子真实占有宽高，并画出盒模型图。

```css
div {
  width: 200px;
  height: 200px;
  padding: 10px 20px 30px;
  padding-right: 40px;
  border: 1px solid #000;
}
```

答案：

![](http://img.smyhvae.com/20170728_1048.png)

题目 2：说出下面盒子真实占有宽高，并画出盒模型图。

```css
div {
  width: 200px;
  height: 200px;
  padding-left: 10px;
  padding-right: 20px;
  padding: 40px 50px 60px;
  padding-bottom: 30px;
  border: 1px solid #000;
}
```

答案：

`padding-left:10px；` 和`padding-right:20px;` 没用，因为后面的 padding 大属性，层叠掉了他们。

盒子模型如下：

![](http://img.smyhvae.com/20170728_1100.png)

题目 3：现在给你一个盒子模型图，请写出代码，试着用最最简单的方法写。

![](http://img.smyhvae.com/20170728_1401.png)

答案：

```css
width: 123px;
height: 123px;
padding: 20px 40px;
border: 1px solid red;
```

题目 4：现在给你一个盒子模型图，请写出代码，试着用最最简单的方法写。

![](http://img.smyhvae.com/20170728_1402.png)

答案：

```css
width: 123px;
height: 123px;
padding: 20px;
padding-right: 40px;
border: 1px solid red;
```

### 一些元素，默认带有 padding

一些元素，默认带有`padding`，比如 ul 标签。如下：

![](http://img.smyhvae.com/20170728_1413.png)

上图显示，不加任何样式的 ul，也是有 40px 的 padding-left。

所以，我们做站的时候，为了便于控制，总是喜欢清除这个默认的 padding。

可以使用`*`进行清除：

```css
* {
  margin: 0;
  padding: 0;
}
```

但是，`*`的效率不高，所以我们使用并集选择器，罗列所有的标签（不用背，有专业的清除默认样式的样式表，今后学习）：

```
body,div,dl,dt,dd,ul,ol,li,h1,h2,h3,h4,h5,h6,pre,code,form,fieldset,legend,input,textarea,p,blockquote,th,td{
    margin:0;
    padding:0;
}
```

## 认识 border

border 就是边框。边框有三个要素：像素（粗细）、线型、颜色。

比如：

```css
.div1 {
  width: 10px;
  height: 10px;
  border: 2px solid red;
}
```

颜色如果不写，默认是黑色。另外两个属性如果不写，则无法显示边框。

### border-style

border 的所有的线型如下：（我们可以通过查看`CSS参考手册`得到）

![](http://img.smyhvae.com/20170728_1435.png)

比如`border:10px ridge red;`这个属性，在 chrome 和 firefox、IE 中有细微差别：（因为可以显示出效果，因此并不是兼容性问题，只是有细微差别而已）

![](http://img.smyhvae.com/20170728_1619.png)

如果公司里面的设计师是处女座的，追求极高的页面还原度，那么不能使用 css 来制作边框。就要用到图片，就要切图了。

所以，比较稳定的 border-style 就几个：solid、dashed、dotted。

### border 拆分

border 是一个大综合属性。比如说：

```css
border: 1px solid red;
```

就是把上下左右这四个方向的边框，都设置为 1px 宽度、线型实线、red 颜色。

PS：小技巧：在 sublime text 中，为了快速输入`border:1px solid red;`这个属性，可以直接输入`bd`，然后选第二个后回车。

border 属性是能够被拆开的，有两大种拆开的方式：

- （1）按三要素拆开：border-width、border-style、border-color。（一个 border 属性是由三个小属性综合而成的）

- （2）按方向拆开：border-top、border-right、border-bottom、border-left。

现在我们明白了：一个 border 属性，是由三个小属性综合而成的。如果某一个小属性后面是空格隔开的多个值，那么就是上右下左的顺序。举例如下：

```
border-width:10px 20px;
border-style:solid dashed dotted;
border-color:red green blue yellow;
```

效果如下：

![](http://img.smyhvae.com/20170728_1516.png)

（1）按三要素拆：

```css
border-width: 10px; //边框宽度
border-style: solid; //线型
border-color: red; //颜色。
```

等价于：

```
border:10px solid red;
```

(2)按方向来拆：

```css
border-top: 10px solid red;
border-right: 10px solid red;
border-bottom: 10px solid red;
border-left: 10px solid red;
```

等价于：

```css
border: 10px solid red;
```

（3）按三要素和方向来拆：(就是把每个方向的，每个要素拆开。3\*4 = 12)

```css
border-top-width: 10px;
border-top-style: solid;
border-top-color: red;
border-right-width: 10px;
border-right-style: solid;
border-right-color: red;
border-bottom-width: 10px;
border-bottom-style: solid;
border-bottom-color: red;
border-left-width: 10px;
border-left-style: solid;
border-left-color: red;
```

等价于：

```css
border: 10px solid red;
```

工作中到底用什么？很简答：什么简单用什么。但要懂得，用小属性层叠大属性。举例如下：

![](http://img.smyhvae.com/20170728_1606.png)

为了实现上方效果，写法如下：

```css
border: 10px solid red;
border-right-color: blue;
```

![](http://img.smyhvae.com/20170728_1608.png)

为了实现上方效果，写法如下：

```css
border: 10px solid red;
border-style: solid dashed;
```

border 可以没有：

```css
border: none;
```

可以某一条边没有：

```css
border-left: none;
```

也可以调整左边边框的宽度为 0：

```css
border-left-width: 0;
```

### border-image 属性

比如：

```css
border-image: url(.img.png) 30 round;
```

这个属性在实际开发中用得不多，暂时忽略。

### 举例 1：利用 border 属性画一个三角形（小技巧）

完整代码如下：

```css
div {
  width: 0;
  height: 0;
  border: 50px solid transparent;
  border-top-color: red;
  border-bottom: none;
}
```

步骤如下：

（1）当我们设置盒子的 width 和 height 为 0 时，此时效果如下：

![](http://img.smyhvae.com/20170728_1639.png)

（2）然后将 border 的底部取消：

![](http://img.smyhvae.com/20170728_1645.png)

（3）最后设置 border 的左边和右边为白色或者透明：

![](http://img.smyhvae.com/20170728_1649.png)

这样，一个三角形就画好了。

### 举例 2：利用 border 属性画一个三角形（更推荐的技巧）

上面的例子 1 中，画出来的是直角三角形，可如果我想画等边三角形，要怎么做呢？

完整代码如下：（用 css 画等边三角形）

```css
.div1 {
  width: 0;
  height: 0;
  border-top: 30px solid red;
  /* 通过改变 border-left 和 border-right 中的像素值，来改变三角形的形状 */
  border-left: 20px solid transparent;
  border-right: 20px solid transparent;
}
```

效果如下：

![](http://img.smyhvae.com/20191004_1830.png)

另外，我们在上方代码的基础之上，再加一个 `border-radus: 20px;` 就能画出一个扇形。

关于盒模型的更多内容，请查看本项目的另外一篇文章：《13-前端面试/面试必看/02-CSS 盒模型及 BFC.md》

> 本文最初发表于[博客园](http://www.cnblogs.com/smyhvae/p/7297736.html)，并在[GitHub](https://github.com/qianguyihao/Web)上持续更新。以下是正文。

## 文本主要内容

- 标准文档流
  - 标准文档流的特性
  - 行内元素和块级元素
  - 行内元素和块级元素的相互转换
- 浮动的性质
- 浮动的清除
- 浏览器的兼容性问题
- 浮动中 margin 相关
- 关于 margin 的 IE6 兼容问题

## 标准文档流

宏观地讲，我们的 web 页面和 photoshop 等设计软件有本质的区别：web 页面的制作，是个“流”，必须从上而下，像“织毛衣”。而设计软件，想往哪里画个东西，都能画。

### 标准文档流的特性

**（1）空白折叠现象：**

无论多少个空格、换行、tab，都会折叠为一个空格。

比如，如果我们想让 img 标签之间没有空隙，必须紧密连接：

```
<img src="images/0.jpg" /><img src="images/1.jpg" /><img src="images/2.jpg" />
```

**（2）高矮不齐，底边对齐：**

举例如下：

![](http://img.smyhvae.com/20170729_1508_2.png)

**（3）自动换行，一行写不满，换行写。**

### 行内元素和块级元素

学习的初期，我们就要知道，标准文档流等级森严。标签分为两种等级：

- 行内元素
- 块级元素

我们可以举一个例子，看看块级元素和行内元素的区别：

![](http://img.smyhvae.com/20170729_1529_2.png)

上图中可以看到，`h1`标签是块级元素，占据了整行，`span`标签是行内元素，只占据内容这一部分。

现在我们尝试给两个标签设置宽高。效果如下：

![](http://img.smyhvae.com/20170729_1532_2.png)

上图中，我们尝试给两个标签设置宽高，但发现，宽高属性只对块级元素`h1`生效。于是我们可以做出如下总结。

**行内元素和块级元素的区别：**（非常重要）

行内元素：

- 与其他行内元素并排；
- 不能设置宽、高。默认的宽度，就是文字的宽度。

块级元素：

- 霸占一行，不能与其他任何元素并列；
- 能接受宽、高。如果不设置宽度，那么宽度将默认变为父亲的 100%。

**行内元素和块级元素的分类：**

在以前的 HTML 知识中，我们已经将标签分过类，当时分为了：文本级、容器级。

从 HTML 的角度来讲，标签分为：

- 文本级标签：p、span、a、b、i、u、em。
- 容器级标签：div、h 系列、li、dt、dd。

> PS：为甚么说 p 是文本级标签呢？因为 p 里面只能放文字&图片&表单元素，p 里面不能放 h 和 ul，p 里面也不能放 p。

现在，从 CSS 的角度讲，CSS 的分类和上面的很像，就 p 不一样：

- 行内元素：除了 p 之外，所有的文本级标签，都是行内元素。p 是个文本级，但是是个块级元素。

- 块级元素：所有的容器级标签都是块级元素，还有 p 标签。

我们把上面的分类画一个图，即可一目了然：

![](http://img.smyhvae.com/20170729_1545.png)

### 行内元素和块级元素的相互转换

我们可以通过`display`属性将块级元素和行内元素进行相互转换。display 即“显示模式”。

#### 块级元素可以转换为行内元素：

一旦，给一个块级元素（比如 div）设置：

```
display: inline;
```

那么，这个标签将立即变为行内元素，此时它和一个 span 无异。inline 就是“行内”。也就是说：

- 此时这个 div 不能设置宽度、高度；
- 此时这个 div 可以和别人并排了。

举例如下：

![](http://img.smyhvae.com/20170729_1629.png)

#### 行内元素转换为块级元素：

同样的道理，一旦给一个行内元素（比如 span）设置：

```
display: block;
```

那么，这个标签将立即变为块级元素，此时它和一个 div 无异。block”是“块”的意思。也就是说：

- 此时这个 span 能够设置宽度、高度
- 此时这个 span 必须霸占一行了，别人无法和他并排
- 如果不设置宽度，将撑满父亲

举例如下：

![](http://img.smyhvae.com/20170729_1638.png)

标准流里面的限制非常多，导致很多页面效果无法实现。如果我们现在就要并排、并且就要设置宽高，那该怎么办呢？办法是：移民！**脱离标准流**！

css 中一共有三种手段，使一个元素脱离标准文档流：

- （1）浮动
- （2）绝对定位
- （3）固定定位

这便引出我们今天要讲的内容：浮动。

## 浮动的性质

> 浮动是 css 里面布局用的最多的属性。

现在有两个 div，分别设置宽高。我们知道，它们的效果如下：

![](http://img.smyhvae.com/20170729_1722.png)

此时，如果给这两个 div 增加一个浮动属性，比如`float: left;`，效果如下：

![](http://img.smyhvae.com/20170729_1723.png)

这就达到了浮动的效果。此时，两个元素并排了，并且两个元素都能够设置宽度、高度了（这在上一段的标准流中，不能实现）。

浮动想学好，一定要知道三个性质。接下来讲一讲。

### 性质 1：浮动的元素脱标

脱标即脱离标准流。我们来看几个例子。

证明 1：

![](http://img.smyhvae.com/20170729_2028.png)

上图中，在默认情况下，两个 div 标签是上下进行排列的。现在由于 float 属性让上图中的第一个`<div>`标签出现了浮动，于是这个标签在另外一个层面上进行排列。而第二个`<div>`还在自己的层面上遵从标准流进行排列。

证明 2：

![](http://img.smyhvae.com/20180111_2320.png)

上图中，span 标签在标准流中，是不能设置宽高的（因为是行内元素）。但是，一旦设置为浮动之后，即使不转成块级元素，也能够设置宽高了。

所以能够证明一件事：**一旦一个元素浮动了，那么，将能够并排了，并且能够设置宽高了。无论它原来是个 div 还是个 span。**所有标签，浮动之后，已经不区分行内、块级了。

### 性质 2：浮动的元素互相贴靠

我们来看一个例子就明白了。

我们给三个 div 均设置了`float: left;`属性之后，然后设置宽高。当改变浏览器窗口大小时，可以看到 div 的贴靠效果：

![](http://img.smyhvae.com/20170730_1910.gif)

上图显示，3 号如果有足够空间，那么就会靠着 2 号。如果没有足够的空间，那么会靠着 1 号大哥。
如果没有足够的空间靠着 1 号大哥，3 号自己去贴左墙。

不过 3 号自己去贴墙的时候，注意：

![](http://img.smyhvae.com/20170730_1928.gif)

上图显示，3 号贴左墙的时候，并不会往 1 号里面挤。

同样，float 还有一个属性值是`right`，这个和属性值`left`是对称的。

### 性质 3：浮动的元素有“字围”效果

来看一张图就明白了。我们让 div 浮动，p 不浮动。

![](http://img.smyhvae.com/20170730_2005.png)

上图中，我们发现：**div 挡住了 p，但不会挡住 p 中的文字**，形成“字围”效果。

总结：**标准流中的文字不会被浮动的盒子遮挡住**。（文字就像水一样）

关于浮动我们要强调一点，浮动这个东西，为避免混乱，我们在初期一定要遵循一个原则：**永远不是一个东西单独浮动，浮动都是一起浮动，要浮动，大家都浮动。**

### 性质 4：收缩

收缩：一个浮动的元素，如果没有设置 width，那么将自动收缩为内容的宽度（这点非常像行内元素）。

举例如下：

![](http://img.smyhvae.com/20170801_1720.png)

上图中，div 本身是块级元素，如果不设置 width，它会单独霸占整行；但是，设置 div 浮动后，它会收缩

### 浮动的补充（做网站时注意）

![](http://img.smyhvae.com/20170731_2248.png)

上图所示，将 para1 和 para2 设置为浮动，它们是 div 的儿子。此时 para1+para2 的宽度小于 div 的宽度。效果如上图所示。可如果设置 para1+para2 的宽度大于 div 的宽度，我们会发现，para2 掉下来了：

![](http://img.smyhvae.com/20170731_2252_2.png)

### 布置一个作业

布置一个作业，要求实现下面的效果：

![](http://img.smyhvae.com/20170801_0858.png)

为实现上方效果，代码如下：

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en">
  <head>
    <meta http-equiv="Content-Type" content="text/html;charset=UTF-8" />
    <title>Document</title>
    <style type="text/css">
      * {
        margin: 0;
        padding: 0;
      }
      .header {
        width: 970px;
        height: 103px;
        /*居中。这个语句的意思是：居中：*/
        margin: 0 auto;
      }
      .header .logo {
        float: left;
        width: 277px;
        height: 103px;
        background-color: red;
      }
      .header .language {
        float: right;
        width: 137px;
        height: 49px;
        background-color: green;
        margin-bottom: 8px;
      }
      .header .nav {
        float: right;
        width: 679px;
        height: 46px;
        background-color: green;
      }

      .content {
        width: 970px;
        height: 435px;
        /*居中，这个语句今天没讲，你照抄，就是居中：*/
        margin: 0 auto;
        margin-top: 10px;
      }
      .content .banner {
        float: left;
        width: 310px;
        height: 435px;
        background-color: gold;
        margin-right: 10px;
      }
      .content .rightPart {
        float: left;
        width: 650px;
        height: 435px;
      }
      .content .rightPart .main {
        width: 650px;
        height: 400px;
        margin-bottom: 10px;
      }
      .content .rightPart .links {
        width: 650px;
        height: 25px;
        background-color: blue;
      }
      .content .rightPart .main .news {
        float: left;
        width: 450px;
        height: 400px;
      }
      .content .rightPart .main .hotpic {
        float: left;
        width: 190px;
        height: 400px;
        background-color: purple;
        margin-left: 10px;
      }
      .content .rightPart .main .news .news1 {
        width: 450px;
        height: 240px;
        background-color: skyblue;
        margin-bottom: 10px;
      }
      .content .rightPart .main .news .news2 {
        width: 450px;
        height: 110px;
        background-color: skyblue;
        margin-bottom: 10px;
      }
      .content .rightPart .main .news .news3 {
        width: 450px;
        height: 30px;
        background-color: skyblue;
      }
      .footer {
        width: 970px;
        height: 35px;
        background-color: pink;
        /*没学，就是居中：*/
        margin: 0 auto;
        margin-top: 10px;
      }
    </style>
  </head>
  <body>
    <!-- 头部 -->
    <div class="header">
      <div class="logo">logo</div>
      <div class="language">语言选择</div>
      <div class="nav">导航条</div>
    </div>

    <!-- 主要内容 -->
    <div class="content">
      <div class="banner">大广告</div>
      <div class="rightPart">
        <div class="main">
          <div class="news">
            <div class="news1"></div>
            <div class="news2"></div>
            <div class="news3"></div>
          </div>
          <div class="hotpic"></div>
        </div>
        <div class="links"></div>
      </div>
    </div>

    <!-- 页尾 -->
    <div class="footer"></div>
  </body>
</html>
```

其实，这个页面的布局是下面这个网站：

![](http://img.smyhvae.com/20170801_0900.png)

## 浮动的清除

> 这里所说的清除浮动，指的是清除浮动与浮动之间的影响。

### 前言

通过上面这个例子，我们发现，此例中的网页就是通过浮动实现并排的。

比如说一个网页有 header、content、footer 这三部分。就拿 content 部分来举例，如果设置 content 的儿子为浮动，但是，这个儿子又是一个全新的标准流，于是儿子的儿子仍然在标准流里。

从学习浮动的第一天起，我们就要明白，浮动有开始，就要有清除。我们先来做个实验。

下面这个例子，有两个块级元素 div，div 没有任何属性，每个 div 里有 li，效果如下：

![](http://img.smyhvae.com/20170801_2122.png)

上面这个例子很简单。可如果我们给里面的`<li>`标签加浮动。效果却成了下面这个样子：

代码如下：

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Document</title>
    <style type="text/css">
      * {
      }
      li {
        float: left;
        width: 100px;
        height: 20px;
        background-color: pink;
      }
    </style>
  </head>
  <body>
    <div class="box1">
      <ul>
        <li>生命壹号1</li>
        <li>生命壹号2</li>
        <li>生命壹号3</li>
        <li>生命壹号4</li>
      </ul>
    </div>
    <div class="box2">
      <ul>
        <li>许嵩1</li>
        <li>许嵩2</li>
        <li>许嵩3</li>
        <li>许嵩4</li>
      </ul>
    </div>
  </body>
</html>
```

效果如下：

![](http://img.smyhvae.com/20170801_2137.png)

上图中，我们发现：第二组中的第 1 个 li，去贴靠第一组中的最后一个 li 了（我们本以为这些 li 会分成两排）。

这便引出我们要讲的：清除浮动的第一种方式。
那该怎么解决呢？

### 方法 1：给浮动元素的祖先元素加高度

造成前言中这个现象的根本原因是：li 的**父亲 div 没有设置高度**，导致这两个 div 的高度均为 0px（我们可以通过网页的审查元素进行查看）。div 的高度为零，导致不能给自己浮动的孩子，撑起一个容器。

撑不起一个容器，导致自己的孩子没办法在自己的内部进行正确的浮动。

好，现在就算给这个 div 设置高度，可如果 div 自己的高度小于孩子的高度，也会出现不正常的现象：

![](http://img.smyhvae.com/20170801_2152.png)

给 div 设置一个正确的合适的高度（至少保证高度大于儿子的高度），就可以看到正确的现象：

![](http://img.smyhvae.com/20170801_2153.png)

**总结：**

**如果一个元素要浮动，那么它的祖先元素一定要有高度。**

**有高度的盒子，才能关住浮动**。（记住这句过来人的经验之语）

只要浮动在一个有高度的盒子中，那么这个浮动就不会影响后面的浮动元素。所以就是清除浮动带来的影响了。

![](http://img.smyhvae.com/20170801_2200.png)

![](http://img.smyhvae.com/20170801_2201.png)

### 方法 2：clear:both;

网页制作中，高度 height 其实很少出现。为什么？因为能被内容撑高！也就是说，刚刚我们讲解的方法 1，工作中用得很少。

那么，能不能不写 height，也把浮动清除了呢？也让浮动之间，互不影响呢？

这个时候，我们可以使用`clear:both;`这个属性。如下：

![](http://img.smyhvae.com/20170801_2233.png)

```
clear:both;
```

clear 就是清除，both 指的是左浮动、右浮动都要清除。`clear:both`的意思就是：**不允许左侧和右侧有浮动对象。**

这种方法有一个非常大的、致命的问题，**它所在的标签，margin 属性失效了**。读者可以试试看。

margin 失效的本质原因是：上图中的 box1 和 box2，高度为零。

### 方法 3：隔墙法

上面这个例子中，为了防止第二个 div 贴靠到第二个 div，我们可以在这两个 div 中间用一个新的 div 隔开，然后给这个新的 div 设置`clear: both;`属性；同时，既然这个新的 div 无法设置 margin 属性，我们可以给它设置 height，以达到 margin 的效果（曲线救国）。这便是隔墙法。

我们看看例子效果就知道了：

![](http://img.smyhvae.com/20170802_1109.png)

上图这个例子就是隔墙法。

**内墙法：**

近些年，有演化出了“内墙法”：

![](http://img.smyhvae.com/20170802_1123.png)

上面这个图非常重要，当作内墙法的公式，先记下来。

为了讲内墙法，我们先记住一句重要的话：**一个父亲是不能被浮动的儿子撑出高度的**。举例如下：

（1）我们在一个 div 里放一个有宽高的 p，效果如下：（很简单）

![](http://img.smyhvae.com/20170802_1716.png)

（2）可如果在此基础之上，给 p 设置浮动，却发现父亲 div 没有高度了：

![](http://img.smyhvae.com/20170802_1730.png)

（3）此时，我么可以在 div 的里面放一个 div（作为内墙），就可以让父亲 div 恢复高度：

![](http://img.smyhvae.com/20170802_1812.png)

于是，我们采用内墙法解决前言中的问题：

![](http://img.smyhvae.com/20170802_1834.png)

与外墙法相比，内墙法的优势（本质区别）在于：内墙法可以给它所在的家撑出宽度（让 box1 有高）。即：box1 的高度可以自适应内容。

而外墙法，虽然一道墙可以把两个 div 隔开，但是这两个 div 没有高，也就是说，无法 wrap_content。

### 清除浮动方法 4：overflow:hidden;

我们可以使用如下属性：

```
overflow:hidden;
```

overflow 即“溢出”， hidden 即“隐藏”。这个属性的意思是“溢出隐藏”。顾名思义：所有溢出边框的内容，都要隐藏掉。如下：

![](http://img.smyhvae.com/20170804_1449.png)

上图显示，`overflow:hidden;`的本意是清除溢出到盒子外面的文字。但是，前端开发工程师发现了，它能做偏方。如下：

一个父亲不能被自己浮动的儿子，撑出高度。但是，只要给父亲加上`overflow:hidden`; 那么，父亲就能被儿子撑出高了。这是一个偏方。

举个例子：

![](http://img.smyhvae.com/20170804_1920.png)

那么对于前言中的例子，我们同样可以使用这一属性：

![](http://img.smyhvae.com/20170804_1934.png)

## 浮动清除的总结

> 我们在上一段讲了四种清除浮动的方法，本段来进行一个总结。

浮动的元素，只能被有高度的盒子关住。 也就是说，如果盒子内部有浮动，这个盒子有高，那么妥妥的，浮动不会互相影响。

### 1、加高法

工作上，我们绝对不会给所有的盒子加高度，这是因为麻烦，并且不能适应页面的快速变化。

```html
<div>
  //设置height
  <p></p>
  <p></p>
  <p></p>
</div>

<div>
  //设置height
  <p></p>
  <p></p>
  <p></p>
</div>
```

### 2、`clear:both;`法

最简单的清除浮动的方法，就是给盒子增加 clear:both；表示自己的内部元素，不受其他盒子的影响。

```html
<div>
  <p></p>
  <p></p>
  <p></p>
</div>

<div>
  //clear:both;
  <p></p>
  <p></p>
  <p></p>
</div>
```

浮动确实被清除了，不会互相影响了。但是有一个问题，就是 margin 失效。两个 div 之间，没有任何的间隙了。

### 3、隔墙法

在两部分浮动元素中间，建一个墙。隔开两部分浮动，让后面的浮动元素，不去追前面的浮动元素。
墙用自己的身体当做了间隙。

```html
<div>
  <p></p>
  <p></p>
  <p></p>
</div>

<div class="cl h10"></div>

<div>
  <p></p>
  <p></p>
  <p></p>
</div>
```

我们发现，隔墙法好用，但是第一个 div，还是没有高度。如果我们现在想让第一个 div，自动根据自己的儿子撑出高度，我们就要想一些“小伎俩”。

内墙法：

```html
<div>
  <p></p>
  <p></p>
  <p></p>
  <div class="cl h10"></div>
</div>

<div>
  <p></p>
  <p></p>
  <p></p>
</div>
```

内墙法的优点就是，不仅仅能够让后部分的 p 不去追前部分的 p 了，并且能把第一个 div 撑出高度。这样，这个 div 的背景、边框就能够根据 p 的高度来撑开了。

### 4、`overflow:hidden;`

这个属性的本意，就是将所有溢出盒子的内容，隐藏掉。但是，我们发现这个东西能够用于浮动的清除。
我们知道，一个父亲，不能被自己浮动的儿子撑出高度，但是，如果这个父亲加上了 overflow:hidden；那么这个父亲就能够被浮动的儿子撑出高度了。这个现象，不能解释，就是浏览器的偏方。
并且,overflow:hidden;能够让 margin 生效。

**清除浮动的例子：**

我们现在举个例子，要求实现下图中无序列表部分的效果：

![](http://img.smyhvae.com/20170804_2321.png)

对比一下我们讲的四种清除浮动的方法。如果用外墙法，ul 中不能插入 div 标签，因为 ul 中只能插入 li，如果插入 li 的墙，会浪费语义。如果用内墙法，不美观。综合对比，还是用第四种方法来实现吧，这会让标签显得极其干净整洁：

![](http://img.smyhvae.com/20170805_1615.png)

上方代码中，如果没有加`overflow:hidden;`，那么第二行的 li 会紧跟着第一行 li 的后面。

## 浏览器的兼容性问题

> 讲一下上述知识点涉及到的浏览器兼容问题。

### 兼容性 1（微型盒子）

**兼容性的第一条**：IE6 不支持小于 12px 的盒子，任何小于 12px 的盒子，在 IE6 中看都大。即：IE 6 不支持微型盒子。

举个例子。我们设置一个 height 为 5px 、宽度为 200px 的盒子，看下在 IE 8 和 IE 6 中的显示效果：

![](http://img.smyhvae.com/20170805_1726.png)

解决办法很简单，就是将盒子的字号大小，设置为**小于盒子的高**，比如，如果盒子的高为 5px，那就把 font-size 设置为 0px(0px < 5px)。如下：

```
height: 5px;
_font-size: 0px;
```

我们现在介绍一下浏览器 hack。hack 就是“黑客”，就是使用浏览器提供的后门，针对某一种浏览器做兼容。

IE6 留了一个**后门**：只要给 css 属性之前，加上**下划线**，这个属性就是 IE6 的专有属性。

比如说，我们给背景颜色这个属性加上下划线，就变成了`_background-color: green;`。效果如下：

![](http://img.smyhvae.com/20170805_2026.png)

于是乎，为了解决微型盒子（即 height 小于 12px）的问题，正确写法：（注意不要忘记下划线）

```
height: 10px;
_font-size:0;
```

### 兼容性 2

**兼容性的第二条：**IE6 不支持用`overflow:hidden;`来清除浮动。

解决办法，以毒攻毒。追加一条：

```
_zoom:1;
```

完整写法：

```
overflow: hidden;
_zoom:1;
```

实际上，`_zoom:1;`能够触发浏览器 hasLayout 机制。这个机制，不要深究了，因为只有 IE6 有。我们只需要让 IE6 好用，具体的实现机制，可以自行查阅。

需要强调的是，`overflow:hidden;`的本意，就是让溢出盒子的 border 的内容隐藏，这个功能是 IE6 兼容的。不兼容的是`overflow:hidden;`清除浮动的时候。

**总结：**

我们刚才学习的两个 IE6 的兼容问题，都是通过多写一条 hack 来解决的，这个我们称为伴生属性，即两个属性，要写一起写。

属性 1：

```
height:6px;
_font-size:0;
```

属性 2：

```
overflow:hidden;
_zoom:1;
```

## margin 相关

> 我们来讲一下浮动中和 margin 相关的知识。

### margin 塌陷/margin 重叠

**标准文档流中，竖直方向的 margin 不叠加，取**较大的值\*\*作为 margin(水平方向的 margin 是可以叠加的，即水平方向没有塌陷现象)。如下图所示：

![](http://img.smyhvae.com/20170805_0904.png)

如果不在标准流，比如盒子都浮动了，那么两个盒子之间是没有塌陷现象的。

### 盒子居中`margin:0 auto;`

margin 的值可以为 auto，表示自动。当 left、right 两个方向都是 auto 的时候，盒子居中了：

```
margin-left: auto;
margin-right: auto;
```

盒子居中的简写为：

```
margin:0 auto;
```

对上方代码的理解：上下的 margin 为 0，左右的 margin 都尽可能的大，于是就居中了。

注意：

- （1）只有标准流的盒子，才能使用`margin:0 auto;`居中。也就是说，当一个盒子浮动了、绝对定位了、固定定位了，都不能使用 margin:0 auto;
- （2）使用`margin:0 auto;`的盒子，必须有 width，有明确的 width。（可以这样理解，如果没有明确的 witdh，那么它的 witdh 就是霸占整行，没有意义）
- （3）`margin:0 auto;`是让盒子居中，不是让盒子里的文本居中。文本的居中，要使用`text-align:center;`

对上面的第三条总结一下：（非常重要）

```
margin:0 auto;    //让这个div自己在大容器中的水平方向上居中。
text-align: center;  //让这个div内部的文本居中。
```

顺便普及一下知识，text-align 还有：

```
text-align:left;     //没啥用，因为默认居左
text-align:right;    //文本居右
```

### 善于使用父亲的 padding，而不是儿子的 margin

我们来看一个奇怪的现象。现在有下面这样一个结构：（div 中放一个 p）

```
	<div>
		<p></p>
	</div>
```

上面的结构中，我们尝试通过给儿子`p`一个`margin-top:50px;`的属性，让其与父亲保持 50px 的上边距。结果却看到了下面的奇怪的现象：

![](http://img.smyhvae.com/20170806_1537.png)

此时我们给父亲 div 加一个 border 属性，就正常了：

![](http://img.smyhvae.com/20170806_1544.png)

如果父亲没有 border，那么儿子的 margin 实际上踹的是“流”，踹的是这“行”。所以，父亲整体也掉下来了。

**margin 这个属性，本质上描述的是兄弟和兄弟之间的距离； 最好不要用这个 marign 表达父子之间的距离。**

所以，如果要表达父子之间的距离，我们一定要善于使用父亲的 padding，而不是儿子的 margin。

## 关于 margin 的 IE6 兼容问题

### IE6 的双倍 margin 的 bug：

当出现连续浮动的元素，携带与浮动方向相同的 margin 时，队首的元素，会双倍 marign。

```
	<ul>
		<li></li>
		<li></li>
		<li></li>
	</ul>
```

![](http://img.smyhvae.com/20170806_1558.png)

解决方案：

（1）使浮动的方向和 margin 的方向，相反。

所以，你就会发现，我们特别喜欢，浮动的方向和 margin 的方向相反。并且，前端开发工程师，把这个当做习惯了。

```
	float: left;
	margin-right: 40px;
```

（2）使用 hack：（没必要，别惯着这个 IE6）

单独给队首的元素，写一个一半的 margin：

```
<li class="no1"></li>
```

```
ul li.no1{
	_margin-left:20px;
}
```

PS：双倍 margin 的问题，面试经常问哦。

### IE6 的 3px bug

![](http://img.smyhvae.com/20170806_1616.png)

解决办法：不用管，因为根本就不允许用儿子踹父亲（即描述父子之间的距离，请用 padding，而不是 margin）。所以，如果你出现了 3px bug，说明你的代码不标准。

IE6，千万不要跟他死坑、较劲，它不配。 格调要高，我们讲 IE6 的兼容性问题，就是为了增加面试的成功率，不是为了成为 IE6 的专家。

## Fireworks 和 others

### Fireworks

fireworks 是 Adobe 公司的一个设计软件。功能非常多，我们以后用啥讲啥。Fireworks 的默认文件格式是 png。

标尺的快捷键：Ctrl + Alt+ R

### others

首行缩进两个汉字：

```
text-indent: 2em;
```

上方属性中，单位比较奇怪，叫做 em，em 就是汉字的一个宽度。indent 的意思是缩进。

> 本文最初发表于[博客园](http://www.cnblogs.com/smyhvae/p/8296748.html)，并在[GitHub](https://github.com/qianguyihao/Web)上持续更新**前端的系列文章**。欢迎在 GitHub 上关注我，一起入门和进阶前端。

> 以下是正文。

CSS 的定位属性有三种，分别是绝对定位、相对定位、固定定位。

```
	position: absolute;  <!-- 绝对定位 -->

	position: relative;  <!-- 相对定位 -->

	position: fixed;     <!-- 固定定位 -->

```

下面逐一介绍。

## 相对定位

**相对定位**：让元素相对于自己原来的位置，进行位置调整（可用于盒子的位置微调）。

我们之前学习的背景属性中，是通过如下格式：

```
	background-position:向右偏移量 向下偏移量;
```

但这回的定位属性，是通过如下格式：

```
	position: relative;
	left: 50px;
	top: 50px;
```

相对定位的举例：

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="Generator" content="EditPlus®" />
    <meta name="Author" content="" />
    <meta name="Keywords" content="" />
    <meta name="Description" content="" />
    <title>Document</title>

    <style type="text/css">
      body {
        margin: 0px;
      }

      .div1 {
        width: 200px;
        height: 200px;
        border: 1px solid red;
      }

      .div2 {
        position: relative; /*相对定位：相对于自己原来的位置*/
        left: 50px; /*横坐标：正值表示向右偏移，负值表示向左偏移*/
        top: 50px; /*纵坐标：正值表示向下偏移，负值表示向上偏移*/

        width: 200px;
        height: 200px;
        border: 1px solid red;
      }
    </style>
  </head>

  <body>
    <div class="div1">有生之年</div>
    <div class="div2">狭路相逢</div>
  </body>
</html>
```

效果：

![](http://img.smyhvae.com/2015-10-03-css-28.png)

### 相对定位不脱标

**相对定位**：不脱标，老家留坑，**别人不会把它的位置挤走**。

也就是说，相对定位的真实位置还在老家，只不过影子出去了，可以到处飘。

### 相对定位的用途

如果想做“压盖”效果（把一个 div 放到另一个 div 之上），我们一般**不用**相对定位来做。相对定位，就两个作用：

- （1）微调元素
- （2）做绝对定位的参考，子绝父相

### 相对定位的定位值

- left：盒子右移

- right：盒子左移

- top：盒子下移

- bottom：盒子上移

PS：负数表示相反的方向。

↘：

```
	position: relative;
	left: 40px;
	top: 10px;
```

↙：

```
	position: relative;
	right: 100px;
	top: 100px;
```

↖：

```
	position: relative;
	right: 100px;
	bottom: 100px;
```

↗：

```
	position: relative;
	left: 200px;
	bottom: 200px;

```

![](http://img.smyhvae.com/20180115_1716.png)

如果要描述上面这张图的方向，我们可以首先可以这样描述：

```
	position: relative;
	left: 200px;
	top: 100px;

```

因为`left: 200px`等价于`right: -200px`，所以这张图其实有四种写法。

## 绝对定位

**绝对定位**：定义横纵坐标。原点在父容器的左上角或左下角。横坐标用 left 表示，纵坐标用 top 或者 bottom 表示。

格式举例如下：

```
	position: absolute;  /*绝对定位*/
	left: 10px;  /*横坐标*/
	top/bottom: 20px;  /*纵坐标*/
```

### 绝对定位脱标

**绝对定位的盒子脱离了标准文档流。**

所以，所有的标准文档流的性质，绝对定位之后都不遵守了。

绝对定位之后，标签就不区分所谓的行内元素、块级元素了，不需要`display:block`就可以设置宽、高了。

### 绝对定位的参考点（重要）

（1）如果用**top 描述**，那么参考点就是**页面的左上角**，而不是浏览器的左上角：

![](http://img.smyhvae.com/20180115_2120.png)

（2）如果用**bottom 描述**，那么参考点就是**浏览器首屏窗口尺寸**（好好理解“首屏”二字），对应的页面的左下角：

![](http://img.smyhvae.com/20180115_2121.png)

为了理解“**首屏**”二字的含义，我们来看一下动态图：

![](http://img.smyhvae.com/20180115_2200.gif)

问题：

![](http://img.smyhvae.com/20180115_2131.png)

答案：

用 bottom 的定位的时候，参考的是浏览器首屏大小对应的页面左下角。

![](http://img.smyhvae.com/20180115_2132.png)

### 以盒子为参考点

一个绝对定位的元素，如果父辈元素中也出现了已定位（无论是绝对定位、相对定位，还是固定定位）的元素，那么将以父辈这个元素，为参考点。

如下：（子绝父相）

![](http://img.smyhvae.com/20180115_2210.png)

以下几点需要注意。

（1） 要听最近的已经定位的祖先元素的，不一定是父亲，可能是爷爷：

```
		<div class="box1">        相对定位
			<div class="box2">    没有定位
				<p></p>           绝对定位，将以box1为参考，因为box2没有定位，box1就是最近的父辈元素
			</div>
		</div>

```

再比如：

```
		<div class="box1">        相对定位
			<div class="box2">    相对定位
				<p></p>           绝对定位，将以box2为参考，因为box2是自己最近的父辈元素
			</div>
		</div>
```

（2）不一定是相对定位，任何定位，都可以作为儿子的参考点：

子绝父绝、**子绝父相**、子绝父固，都是可以给儿子定位的。但是在工程上，如果子绝、父绝，没有一个盒子在标准流里面了，所以页面就不稳固，没有任何实战用途。

**工程应用：**

“**子绝父相**”有意义：这样可以保证父亲没有脱标，儿子脱标在父亲的范围里面移动。于是，工程上经常这样做：

> 父亲浮动，设置相对定位（零偏移），然后让儿子绝对定位一定的距离。

（3）绝对定位的儿子，无视参考的那个盒子的 padding：

下图中，绿色部分是父亲 div 的 padding，蓝色部分 p 是 div 的内容区域。此时，如果 div 相对定位，p 绝对定位，那么，
p 将无视父亲的 padding，在 border 内侧为参考点，进行定位：

![](http://img.smyhvae.com/20180116_0812.png)

**工程应用：**

绝对定位非常适合用来做“压盖”效果。我们来举个 lagou.com 上的例子。

现在有如下两张图片素材：

![](http://img.smyhvae.com/20180116_1115.png)

![](http://img.smyhvae.com/20180116_1116.jpg)

要求作出如下效果：

![](http://img.smyhvae.com/20180116_1117.png)

代码实现如下：

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Document</title>
    <style type="text/css">
      .box {
        margin: 100px;
        width: 308px;
        height: 307px;
        border: 1px solid #ff7e00;
        position: relative; /*子绝父相*/
      }
      .box .image img {
        width: 308px;
        height: 196px;
      }
      .box .dtc {
        display: block; /*转为块级元素，才能设置span的宽高*/
        width: 52px;
        height: 28px;
        background-image: url(http://img.smyhvae.com/20180116_1115.png);
        background-position: -108px 0px; /*这里用到了精灵图*/
        position: absolute; /*采用绝对定位的方式，将精灵图盖在最上层*/
        top: -9px;
        left: 13px;
      }
      .box h4 {
        background-color: black;
        color: white;
        width: 308px;
        height: 40px;
        line-height: 40px;
        position: absolute;
        top: 156px;
      }
    </style>
  </head>
  <body>
    <div class="box">
      <span class="dtc"></span>
      <div class="image">
        <img src="http://img.smyhvae.com/20180116_1116.jpg" alt="" />
      </div>
      <h4>广东深圳宝安区建安一路海雅缤纷城4楼</h4>
    </div>
  </body>
</html>
```

代码解释如下：

- 为了显示“多套餐”那个小图，我们需要用到精灵图。

- “多套餐”下方黑色背景的文字都是通过“子绝父相”的方式的盖在大海报 image 的上方的。

代码的效果如下：

![](http://img.smyhvae.com/20180116_1335.png)

### 让绝对定位中的盒子在父亲里居中

我们知道，如果想让一个**标准流中的盒子在父亲里居中**（水平方向看），可以将其设置`margin: 0 auto`属性。

可如果盒子是绝对定位的，此时已经脱标了，如果还想让其居中（位于父亲的正中间），可以这样做：

```
	div {
		width: 600px;
		height: 60px;
		position: absolute;  绝对定位的盒子
		left: 50%;           首先，让左边线居中
		top: 0;
		margin-left: -300px;  然后，向左移动宽度（600px）的一半
	}
```

如上方代码所示，我们先让这个宽度为 600px 的盒子，左边线居中，然后向左移动宽度（600px）的一半，就达到效果了。

![](http://img.smyhvae.com/20180116_1356.png)

我们可以总结成一个公式：

> left:50%; margin-left:负的宽度的一半

## 固定定位

**固定定位**：就是相对浏览器窗口进行定位。无论页面如何滚动，这个盒子显示的位置不变。

备注：IE6 不兼容。

**用途 1**：网页右下角的“返回到顶部”

比如我们经常看到的网页右下角显示的“返回到顶部”，就可以固定定位。

```html
<style type="text/css">
  .backtop {
    position: fixed;
    bottom: 100px;
    right: 30px;
    width: 60px;
    height: 60px;
    background-color: gray;
    text-align: center;
    line-height: 30px;
    color: white;
    text-decoration: none; /*去掉超链接的下划线*/
  }
</style>
```

**用途 2：**顶部导航条

我们经常能看到固定在网页顶端的导航条，可以用固定定位来做。

需要注意的是，假设顶部导航条的高度是 60px，那么，为了防止其他的内容被导航条覆盖，我们要给 body 标签设置 60px 的 padding-top。

顶部导航条的实现如下：

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en">
  <head>
    <meta http-equiv="Content-Type" content="text/html;charset=UTF-8" />
    <title>Document</title>
    <style type="text/css">
      * {
        margin: 0;
        padding: 0;
      }
      body {
        /*为什么要写这个？*/
        /*不希望我们的页面被nav挡住*/
        padding-top: 60px;
        /*IE6不兼容固定定位，所以这个padding没有什么用，就去掉就行了*/
        _padding-top: 0;
      }
      .nav {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 60px;
        background-color: #333;
        z-index: 99999999;
      }
      .inner_c {
        width: 1000px;
        height: 60px;
        margin: 0 auto;
      }
      .inner_c ul {
        list-style: none;
      }
      .inner_c ul li {
        float: left;
        width: 100px;
        height: 60px;
        text-align: center;
        line-height: 60px;
      }
      .inner_c ul li a {
        display: block;
        width: 100px;
        height: 60px;
        color: white;
        text-decoration: none;
      }
      .inner_c ul li a:hover {
        background-color: gold;
      }
      p {
        font-size: 30px;
      }
      .btn {
        display: block;
        width: 120px;
        height: 30px;
        background-color: orange;
        position: relative;
        top: 2px;
        left: 1px;
      }
    </style>
  </head>
  <body>
    <div class="nav">
      <div class="inner_c">
        <ul>
          <li><a href="#">网页栏目</a></li>
          <li><a href="#">网页栏目</a></li>
          <li><a href="#">网页栏目</a></li>
          <li><a href="#">网页栏目</a></li>
          <li><a href="#">网页栏目</a></li>
          <li><a href="#">网页栏目</a></li>
          <li><a href="#">网页栏目</a></li>
          <li><a href="#">网页栏目</a></li>
          <li><a href="#">网页栏目</a></li>
          <li><a href="#">网页栏目</a></li>
        </ul>
      </div>
    </div>
  </body>
</html>
```

### 5、z-index 属性：

**z-index**属性：表示谁压着谁。数值大的压盖住数值小的。

有如下特性：

（1）属性值大的位于上层，属性值小的位于下层。

（2）z-index 值没有单位，就是一个正整数。默认的 z-index 值是 0。

（3）如果大家都没有 z-index 值，或者 z-index 值一样，那么在 HTML 代码里写在后面，谁就在上面能压住别人。定位了的元素，永远能够压住没有定位的元素。

（4）只有定位了的元素，才能有 z-index 值。也就是说，不管相对定位、绝对定位、固定定位，都可以使用 z-index 值。**而浮动的元素不能用**。

（5）从父现象：父亲怂了，儿子再牛逼也没用。意思是，如果父亲 1 比父亲 2 大，那么，即使儿子 1 比儿子 2 小，儿子 1 也能在最上层。

针对（1）（2）（3）条，举例如下：

这是默认情况下的例子：（div2 在上层，div1 在下层）

![](http://img.smyhvae.com/2015-10-03-css-32.png)

现在加一个`z-index`属性，要求效果如下：

![](http://img.smyhvae.com/2015-10-03-css-33.png)

第五条分析：

![](http://img.smyhvae.com/20180116_1445.png)

z-index 属性的应用还是很广泛的。当好几个已定位的标签出现覆盖的现象时，我们可以用这个 z-index 属性决定，谁处于最上方。也就是**层级**的应用。

**层级：**

（1）必须有定位（除去 static）

（2）用`z-index`来控制层级数。

## 前言

> CSS 已经学了一些基础内容了，我们来讲解一个小案例吧。以[博雅互动](http://www.boyaa.com/)的官网首页举例。

### 版心

首页的**版心**如下：

![](http://img.smyhvae.com/20170813_1535.png)

这里我们要普及一个概念，叫“[版心](https://baike.baidu.com/item/%E7%89%88%E5%BF%83)”。**版心是页面中主要内容所在的区域。**

比如说，网站左上角的 logo，设计图给出的左边距是 143 像素，此时，我们千万不要以为，logo 的左边距真的是 143 像素。因为设计图只是一个版心；而整个页面是处于浏览器的中间，浏览器的宽度是可以随时调整的。

我们量一下中间四个方形图的 width，是 1000px，所以，网页版心的宽度是 1000px。

### 网页的结构

从结构上来看，网页分为头部（导航栏）、banner 区、内容区、底部。

## 导航栏的制作

在此我们只讲基础知识的使用，不涉及浏览器的优化。

`class==header`这个 div 是顶部的通栏，我们在里面放一个 1000px 宽的 div，作为通栏的版心，我一般把这个版心称为`class=inner_c`，c 指的是 center。

`class=inner_c`不需要给高，因为它可以被内容撑高。

现在我们需要在`class=inner_c`里放三个东西：左侧的 logo、中间的导航栏、右侧的“加入我们”。

接下来我们开始做右侧的「加入我们」，「加入我们」的背景是带圆角的矩形，这个圆角，实现的方式有两种：要么切图，要么用 CSS3 实现（IE 7、IE 8 不兼容）。我们暂时使用切图来实现。

我们最好把「加入我们」这个超链接`<a>`放到`div`里，然后设置 div 的 margin 和 padding，而不是直接设置`<a>`的边距。

我们起个名字叫`class=jrwm`是没有问题的，这在工作当中很常见，如果写成`class=join_us`反倒很别扭。

暂时我们的做法是：

- （1）给`class=jrwm_box`这个 div 里放一个`class=jrwm`的 div。`class=jrwm`用来放绿色的背景图片。
- （2）在`class=jrwm`里放一个超链接，并将超链接转为块级元素。

最终，导航栏的代码如下：

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Document</title>
    <style type="text/css">
      * {
        margin: 0px;
        padding: 0px;
      }
      body {
        font-size: 14px;
        font-family: "Microsoft YaHei", "SimSun";
        height: 8888px;
      }
      .header {
        height: 58px;
        background-color: #191d3a;
      }
      /*版心*/
      .inner_c {
        width: 1000px;
        margin: 0 auto; /*让导航条、内容区域等部分的版心在父亲里居中*/
      }
      /*导航条的logo*/
      .header .logo {
        float: left;
        margin-right: 40px;
      }
      .header .nav {
        float: left;
      }
      .header .nav ul {
        list-style: none; /*去掉列表前面的圆点*/
      }
      .header .nav ul li {
        float: left;
        width: 100px;
        line-height: 58px; /*让行高等于这一行的高度，保证里面的文字垂直居中*/
        border-left: 1px solid #252947; /*每个li之间有间隔线*/
      }
      .header .nav ul li.last {
        border-right: 1px solid #252947; /*最后一个li的右边加间隔线*/
      }
      .header .nav ul li a {
        display: block; /*将超链接转为块儿，可以保证其霸占父亲的整行*/
        height: 58px;
        text-decoration: none; /*去掉超链的下划线*/
        color: #818496;
        text-align: center; /*让这个div内部的文本居中*/
      }
      .header .nav ul li a.current {
        color: white;
        background: #252947;
      }
      .header .nav ul li a:hover {
        color: white;
        background: #252947;
      }

      .header .jrwm_box {
        float: left;
        height: 58px;
        width: 100px;
        padding-left: 48px;
        padding-top: 12px;
      }
      /*放背景图片的div*/
      .header .jrwm_box .jrwm {
        height: 34px;
        background-image: url(images/jrwm.png);
        background-repeat: no-repeat;
        text-align: center; /*让这个div内部的超链接居中*/
      }
      .header .jrwm_box .jrwm a {
        display: block; /*将超链接转为块儿，可以保证其霸占父亲的整行*/
        line-height: 34px; /*让行高为背景图片的高度，可以保证超链接的文字在背景图片里垂直居中*/
        text-decoration: none; /*去掉超链的下划线*/
        color: white;
      }
    </style>
  </head>
  <body>
    <div class="header">
      <div class="inner_c">
        <div class="logo">
          <img src="images/logo.png " alt="" />
        </div>
        <div class="nav">
          <ul>
            <li><a href="#" class="current">首页</a></li>
            <li><a href="#">博雅游戏</a></li>
            <li><a href="#">博雅新闻</a></li>
            <li><a href="#">关于我们</a></li>
            <li><a href="#">客服中心</a></li>
            <li class="last"><a href="#">投资者关系</a></li>
          </ul>
        </div>
        <div class="jrwm_box">
          <div class="jrwm">
            <a href="https://www.google.com/" target="_blank">加入我们</a>
          </div>
        </div>
      </div>
    </div>
  </body>
</html>
```

导航栏的效果如下：

![](http://img.smyhvae.com/20180114_1332.gif)

## banenr 图

> 因为涉及到 js 的内容，这里先不讲内容区域**轮播图**的效果。

我们首先在导航条和 banner 图之间加一道墙，即`class=cl`，然后采用隔墙法对其设置`clear: both;`的属性。

然后设置 banner 的背景图片属性，添加 banner 图。

## 内容区域的制作

导航栏+banner+内容区域的完整代码如下：

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Document</title>
    <style type="text/css">
      * {
        margin: 0px;
        padding: 0px;
      }

      /*清除浮动的影响*/
      .cl {
        clear: both;
      }
      body {
        font-size: 14px;
        font-family: "Microsoft YaHei", "SimSun";
        height: 8888px;
      }
      .header {
        height: 58px;
        background-color: #191d3a;
      }
      /*版心*/
      .inner_c {
        width: 1000px;
        margin: 0 auto; /*让导航条、内容区域等部分的版心在父亲里居中*/
      }
      /*导航条的logo*/
      .header .logo {
        float: left;
        margin-right: 40px;
      }
      .header .nav {
        float: left;
      }
      .header .nav ul {
        list-style: none; /*去掉列表前面的圆点*/
      }
      .header .nav ul li {
        float: left;
        width: 100px;
        line-height: 58px; /*让行高等于这一行的高度，保证里面的文字垂直居中*/
        border-left: 1px solid #252947; /*每个li之间有间隔线*/
      }
      .header .nav ul li.last {
        border-right: 1px solid #252947; /*最后一个li的右边加间隔线*/
      }
      .header .nav ul li a {
        display: block; /*将超链接转为块儿，可以保证其霸占父亲的整行*/
        height: 58px;
        text-decoration: none; /*去掉超链的下划线*/
        color: #818496;
        text-align: center; /*让这个div内部的文本居中*/
      }
      .header .nav ul li a.current {
        color: white;
        background: #252947;
      }
      .header .nav ul li a:hover {
        color: white;
        background: #252947;
      }

      .header .jrwm_box {
        float: left;
        height: 58px;
        width: 100px;
        padding-left: 48px;
        padding-top: 12px;
      }
      /*放背景图片的div*/
      .header .jrwm_box .jrwm {
        height: 34px;
        background-image: url(images/jrwm.png);
        background-repeat: no-repeat;
        text-align: center; /*让这个div内部的超链接居中*/
      }
      .header .jrwm_box .jrwm a {
        display: block; /*将超链接转为块儿，可以保证其霸占父亲的整行*/
        line-height: 34px; /*让行高为背景图片的高度，可以保证超链接的文字在背景图片里垂直居中*/
        text-decoration: none; /*去掉超链的下划线*/
        color: white;
      }

      .banner {
        height: 465px;
        background: url(images/banner.jpg) no-repeat center top;
      }
      .content {
        padding-top: 50px;
      }
      .content .product {
        height: 229px;
        border-bottom: 1px solid #dbe1e7;
      }
      .content .product ul {
        list-style: none;
      }
      .content .product ul li {
        float: left;
        width: 218px;
        margin-right: 43px;
      }
      .content .product ul li.last {
        margin-right: 0;
        width: 217px;
      }
      .content .product ul li img {
        width: 218px;
        height: 130px;
      }
      .content .product ul li.last img {
        width: 217px;
      }

      .content .product ul li h3 {
        text-align: center;
        line-height: 38px;
        font-size: 14px;
        font-weight: bold;
      }
      .content .product ul li p.djbf {
        text-align: center;
        line-height: 16px;
      }
      .content .product ul li p.djbf a {
        font-size: 12px;
        color: #38b774;
        text-decoration: none;
        background: url(images/sanjiaoxing.png) no-repeat right 5px;
        padding-right: 12px;
      }
    </style>
  </head>
  <body>
    <div class="header">
      <div class="inner_c">
        <div class="logo">
          <img src="images/logo.png " alt="" />
        </div>
        <div class="nav">
          <ul>
            <li><a href="#" class="current">首页</a></li>
            <li><a href="#">博雅游戏</a></li>
            <li><a href="#">博雅新闻</a></li>
            <li><a href="#">关于我们</a></li>
            <li><a href="#">客服中心</a></li>
            <li class="last"><a href="#">投资者关系</a></li>
          </ul>
        </div>
        <div class="jrwm_box">
          <div class="jrwm">
            <a href="https://www.google.com/" target="_blank">加入我们</a>
          </div>
        </div>
      </div>
    </div>

    <!-- 在导航条和banner之间隔一堵墙 -->
    <div class="cl"></div>

    <div class="banner"></div>

    <!-- 内容区域 -->
    <div class="content inner_c">
      <div class="product">
        <ul>
          <li>
            <p><img src="images/pro1.jpg" alt="" /></p>
            <h3>BPT宣传片</h3>
            <p class="djbf">
              <a href="#">点击播放</a>
            </p>
          </li>
          <li>
            <p><img src="images/pro2.jpg" alt="" /></p>
            <h3>BPT宣传片</h3>
            <p class="djbf">
              <a href="#">点击播放</a>
            </p>
          </li>
          <li>
            <p><img src="images/pro3.jpg" alt="" /></p>
            <h3>BPT宣传片</h3>
            <p class="djbf">
              <a href="#">点击播放</a>
            </p>
          </li>
          <li class="last">
            <p><img src="images/pro4.jpg" alt="" /></p>
            <h3>BPT宣传片</h3>
            <p class="djbf">
              <a href="#">点击播放</a>
            </p>
          </li>
        </ul>
      </div>
    </div>
  </body>
</html>
```

代码解释：

（1）导航栏，左侧的 logo：

**错误的写法：**

可能会有人直接将 img 标签作为 logo 的布局：

```html
<div class="logo">
  <img src="images/logo.png " alt="" />
</div>
```

然后将 img 的样式设置为：

```css
.header .logo {
  float: left;
  margin-right: 40px;
}
```

这样写虽然视觉效果上达到了，但是搜索引擎是搜不到图片的，不利于 SEO。

**正确的写法：**

正确的写法是将超链接作为 logo 的布局，里面放入文字（文字可以被 SEO）：

```html
<h1 class="logo">
  <a href="#"> 博雅互动-世界上最好的游戏公司 </a>
</h1>
```

然后将**logo 设置为背景图**：

```css
.header .logo {
  float: left;
  padding-left: 12px;
  margin-right: 39px;
  width: 174px;
  height: 58px;
}
.header .logo a {
  display: block;
  width: 174px;
  height: 58px;
  background: url(images/logo.png) no-repeat;
  text-indent: -999em;
}
```

由于搜索引擎是搜不到图片的，所以一定要把“博雅互动”这几个文字加上去，**然后通过`text-indent`缩进的属性把文字赶走到视线以外的地方**。这是做搜索引擎优化的一个重要的技巧。

另外，背景要放在里层的 a 标签里，不要放在外层的 h1 标签里。假设背景图放在 h1 里，那么不管 h1 的 padding 有多大，背景图的位置都不会变。

（1）内容区域，“点击播放”右侧的小三角形：

我们在“点击播放”的右侧放了一个三角形。这个很有技巧。

![](http://img.smyhvae.com/20180115_1356.png)

代码截取如下：

```css
.content .product ul li p.djbf a {
  font-size: 12px;
  color: #38b774;
  text-decoration: none;
  background: url(images/sanjiaoxing.png) no-repeat right center;
  padding-right: 12px;
}
```

上方代码中，我们在第 6 行给“点击播放”这个超链接加一个右 padding（很关键），然后在第 5 行把小三角这个背景图放在右 padding 的位置，就能达到想要的视觉效果。

（2）导航栏+banner+内容区域的效果如下：

![](http://img.smyhvae.com/20180114_1405.png)

工程文件如下：

- [2018-03-20-boya.rar](https://download.csdn.net/download/smyhvae/11832612)

## CSS3 介绍

CSS3 在 CSS2 基础上，**增强**或**新增**了许多特性， 弥补了 CSS2 的众多不足之处，使得 Web 开发变得更为高效和便捷。

### CSS3 的现状

- 浏览器支持程度不够好，有些需要添加**私有前缀**

- 移动端支持优于 PC 端

- 不断改进中

- 应用相对广泛

### 应对的策略：渐进增强

- （1）坚持**渐进增强**的原则：**让低版本浏览器能正常访问页面，高版本的浏览器用户体验更好**。【重要】

比如说，同样是一个头像，可能在低版本的浏览器中，头像方的；在高版本的浏览器中，头像是圆的。

- （2）考虑用户群体。

- （3）遵照产品的方案。

参考链接：

- [渐进增强 VS 优雅降级 | 简书](https://www.jianshu.com/p/d313f1108862)

- [渐进增强和优雅降级之间的不同（面试题目）](https://www.cnblogs.com/iceflorence/archive/2017/03/27/6625466.html)

### 浏览器的版本问题

由于 CSS3 普遍存在兼容性问题，为了避免因兼容性带来的干扰，浏览器的建议版本为：

- Chrome 浏览器 version 46+

- Firefox 浏览器 firefox 42+

### 如何使用手册

CSS 参考手册的网址：<http://css.doyoe.com/>

CSS 参考手册的下载链接：<http://download.csdn.net/download/smyhvae/10243974>

在查看[CSS 参考手册](http://download.csdn.net/download/smyhvae/10243974)时，需要注意以下符号：

![](http://img.smyhvae.com/20180206_2150.png)

比如说，`{1,4}`表示可以设置一至四个参数。

下面讲 CSS3 的基础知识。本文讲一下 CSS3 选择器的内容。

## CSS3 选择器

我们之前学过 CSS 的选择器，比如：

```
     div 标签选择器

     .box 类名选择器

     #box　id选择器

     div p 后代选择器

     div.box 交集选择器

     div,p,span 并集选择器

     div>p 子代选择器

     * : 通配符

     div+p: 选中div后面相邻的第一个p

     div~p: 选中的div后面所有的p

```

CSS3 新增了许多**灵活**查找元素的方法，极大的提高了查找元素的效率和**精准度**。CSS3 选择器与 jQuery 中所提供的**绝大部分**选择器兼容。

### 属性选择器

属性选择器的标志性符号是 `[]`。

匹配含义：

```
^：开头  $：结尾  *：包含
```

格式：

- `E[title]` 选中页面的 E 元素，并且 E 存在 title 属性即可。

- `E[title="abc"]`选中页面的 E 元素，并且 E 需要带有 title 属性，且属性值**完全等于**abc。

- `E[attr~=val]` 选择具有 att 属性且属性值为：用空格分隔的字词列表，其中一个等于 val 的 E 元素。

- `E[attr|=val]` 表示要么是一个单独的属性值，要么这个属性值是以“-”分隔的。

- `E[title^="abc"]` 选中页面的 E 元素，并且 E 需要带有 title 属性,属性值以 abc 开头。

- `E[title$="abc"]` 选中页面的 E 元素，并且 E 需要带有 title 属性,属性值以 abc 结尾。

- `E[title*="abc"]` 选中页面的 E 元素，并且 E 需要带有 title 属性,属性值任意位置包含 abc。

比如说，我们用属性选择器去匹配标签的 className，是非常方便的。

这里我们用 class 属性来举例。代码举例：

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>选择器 - 属性</title>
    <style>
      body {
        margin: 0;
        padding: 0;
        font-family: "微软雅黑";
        background-color: #f7f7f7;
      }

      .wrapper {
        width: 1024px;
        margin: 0 auto;
      }

      .wrapper > section {
        min-height: 300px;
        margin-bottom: 30px;
        box-shadow: 1px 1px 4px #ddd;
        background-color: #fff;
      }

      .wrapper > header {
        text-align: center;
        line-height: 1;
        padding: 20px;
        margin-bottom: 10px;
        font-size: 30px;
      }

      .wrapper section > header {
        line-height: 1;
        padding: 10px;
        font-size: 22px;
        color: #333;
        background-color: #eee;
      }

      .wrapper .wrap-box {
        padding: 20px;
      }

      form {
        width: 300px;
        height: 300px;
        margin: 0 auto;
      }

      form input[type="text"] {
        width: 200px;
        height: 30px;
      }

      form input[type="password"] {
        width: 200px;
        height: 30px;
      }

      .attr1 {
      }

      .download {
      }

      .attr1 a[href="./a.rmvb"] {
        color: red;
      }

      .attr1 a[href="./b.rmvb"] {
        color: pink;
      }

      /*  E[attr~=val] 表示的一个单独的属性值 这个属性值是以空格分隔的*/
      .attr2 a[class~="download"] {
        color: red;
      }

      /*  E[attr|=val] 表示的要么一个单独的属性值 要么这个属性值是以"-"分隔的*/
      .attr3 a[class|="download"] {
        color: red;
      }

      /*  E[attr*=val] 表示的属性值里包含val字符并且在“任意”位置 */
      .attr4 a[class*="download"] {
        color: red;
      }

      /*  E[attr^=val] 表示的属性值里包含val字符并且在“开始”位置 */
      .attr5 a[class^="download"] {
        color: red;
      }

      /*  E[attr$=val] 表示的属性值里包含val字符并且在“结束”位置 */
      .attr6 a[class$="download"] {
        color: red;
      }
    </style>
  </head>
  <body>
    <div class="wrapper">
      <header>CSS3-属性选择器</header>
      <section>
        <header>简介</header>
        <div class="wrap-box">
          <form action="">
            <ul>
              <li>姓名: <input type="text" /></li>
              <li>密码: <input type="password" /></li>

              <li>性别: <input type="radio" />男 <input type="radio" /> 女</li>
              <li>兴趣: <input type="checkbox" name="" id="" />写代码</li>
              <li>
                <input type="submit" value="提交" />
              </li>
            </ul>
          </form>
        </div>
      </section>
      <section class="attr1">
        <header>E[attr]</header>
        <div class="wrap-box">
          <a href="./a.rmvb" class="download download-movie">下载</a>
          <a href="./b.rmvb" class="download download-movie">下载</a>
          <a href="./a.mp3" class="download download-music">下载</a>
        </div>
      </section>
      <section class="attr2">
        <header>E[attr~=attr]</header>
        <div class="wrap-box">
          <a href="./a.rmvb" class="download download-movie">下载</a>
          <a href="./b.rmvb" class="download download-movie">下载</a>
          <a href="./a.mp3" class="download download-music">下载</a>
        </div>
      </section>
      <section class="attr3">
        <header>E[attr|=attr]</header>
        <div class="wrap-box">
          <a href="./a.rmvb" class="download">下载</a>
          <a href="./b.rmvb" class="download-movie">下载</a>
          <a href="./a.mp3" class="download-music">下载</a>
        </div>
      </section>
      <section class="attr4">
        <header>E[attr*=val]</header>
        <div class="wrap-box">
          <a href="./a.rmvb" class="download">下载</a>
          <a href="./b.rmvb" class="moviedownload">下载</a>
          <a href="./a.mp3" class="downloadmusic">下载</a>
        </div>
      </section>
      <section class="attr5">
        <header>E[attr^=val]</header>
        <div class="wrap-box">
          <a href="./a.rmvb" class="download">下载</a>
          <a href="./b.rmvb" class="moviedownload">下载</a>
          <a href="./a.mp3" class="downloadmusic">下载</a>
        </div>
      </section>
      <section class="attr6">
        <header>E[attr$=val]</header>
        <div class="wrap-box">
          <a href="./a.rmvb" class="download">下载</a>
          <a href="./b.rmvb" class="moviedownload">下载</a>
          <a href="./a.mp3" class="downloadmusic">下载</a>
        </div>
      </section>
    </div>
  </body>
</html>
```

最后来张表格：

![](http://img.smyhvae.com/20180207_1500.png)

### 结构伪类选择器

伪类选择器的标志性符号是 `:`。

CSS 中有一些伪类选择器，比如`:link`、`:active`、`:visited`、`:hover`，这些是动态伪类选择器。

CSS3 又新增了其它的伪类选择器。这一小段，我们来学习 CSS3 中的**结构伪类选择器**：即通过**结构**来进行筛选。

**1、格式：（第一部分）**

- `E:first-child` 匹配父元素的第一个子元素 E。

- `E:last-child` 匹配父元素的最后一个子元素 E。

- `E:nth-child(n)` 匹配父元素的第 n 个子元素 E。**注意**，盒子的编号是从`1`开始算起，不是从`0`开始算起。

- `E:nth-child(odd)` 匹配奇数

- `E:nth-child(even)` 匹配偶数

- `E:nth-last-child(n)` 匹配父元素的倒数第 n 个子元素 E。

理解：

（1）这里我们要好好理解**父元素**的含义，它指的是：以 E 元素的父元素为参考。

（2）注意：以上选择器中所选到的元素的类型，必须是指定的类型 E，如果选不中，则无效。这个要好好理解，具体可以看 CSS 参考手册中的`E:nth-child(n)`的示例。我们可以理解成：**先根据选择器找到选中的全部位置，如果发现某个位置不是类型 E，则该位置失效**。

（3）另外，`E:nth-child(n)`这个属性也很有意思。比如，针对下面这样一组标签：

```html
<ul>
  <li>1</li>
  <li>2</li>
  <li>3</li>
  <li>4</li>
  <li>5</li>
  <li>6</li>
  <li>7</li>
  <li>8</li>
  <li>9</li>
  <li>10</li>
</ul>
```

上方代码中：

- 如果选择器写成`li:nth-child(2)`，则表示第 2 个 `li`。

- 如果选择器写成`li:nth-child(n)`，则表示**所有的**`li`。因为此时的 `n` 表示 0,1,2,3,4,5,6,7,8.....（当 n 小于 1 时无效，因为 n = 0 也是不会选中的）

- 如果选择器写成`li:nth-child(2n)`，则表示所有的**第偶数个** li。

- 如果选择器写成`li:nth-child(2n+1)`，则表示所有的**第奇数个** li。

- 如果选择器写成`li:nth-child(-n+5)`，则表示**前 5 个** li。

- 如果选择器写成`li:nth-last-child(-n+5)`，则表示**最后 5 个** li。

- 如果选择器写成`li:nth-child(7n)`，则表示选中 7 的倍数。。

上面列举的选择器中，我们只要记住： `n` 表示 0,1,2,3,4,5,6,7,8.....就很容易明白了。

**2、格式：（第二部分）**

- `E:first-of-type` 匹配同类型中的第一个同级兄弟元素 E。

- `E:last-of-type` 匹配同类型中的最后一个同级兄弟元素 E。

- `E:nth-of-type(n)` 匹配同类型中的第 n 个同级兄弟元素 E。

- `E:nth-last-of-type(n)` 匹配同类型中的倒数第 n 个同级兄弟元素 E。

既然上面这几个选择器带有`type`，我们可以这样理解：先在同级里找到所有的 E 类型，然后根据 n 进行匹配。

**3、格式：（第三部分）**

- `E:empty` 匹配没有任何子节点（包括空格等 text 节点）的元素 E。

- `E:target` 匹配相关 URL 指向的 E 元素。要配合锚点使用。

**举例：**

我们可以把多个伪类选择器结合起来使用，比如：

![](http://img.smyhvae.com/20180207_1340.png)

如果想把上图中，第一行的前三个 span 标红，我们可以这样使用结构伪类选择器：

```css
dt:first-child span:nth-of-type(-n + 3) {
  color: red;
}
```

最后来张表格：

![](http://img.smyhvae.com/20180207_1502.png)

### 伪元素选择器

伪元素选择器的标志性符号是 `::`。

**1、格式：（第一部分）**

- `E::before` 设置在 元素 E 前面（依据对象树的逻辑结构）的内容，配合 content 属性一起使用。

- `E::after` 设置在 元素 E 后面（依据对象树的逻辑结构）的内容，配合 content 属性一起使用。

`E:after`、`E:before `在旧版本里是伪类，在 CSS3 这个新版本里是伪元素。新版本里，`E:after`、`E:before`会被自动识别为`E::after`、`E::before`，按伪元素来对待，这样做的目的是用来做兼容处理。

举例：

```html
<!DOCTYPE html>
<html>
  <head lang="en">
    <meta charset="UTF-8" />
    <title></title>
    <style>
      /*::before 和::after 是通过 css 模拟出的html标签的效果*/
      span::before {
        content: "smyhvae";
        color: red;
        background-color: pink;
        width: 50px;
        height: 50px;
        display: inline-block;
      }

      span::after {
        content: "永不止步";
        color: yellowgreen;
      }

      /*给原本的span标签设置一个默认的属性*/
      span {
        border: 1px solid #000;
      }
    </style>
  </head>
  <body>
    <span>生命壹号</span>
  </body>
</html>
```

效果如下：

![](http://img.smyhvae.com/20180207_1409.png)

**上图可以看出**：

- 通过伪元素选择器，就可以添加出类似于 span 标签的效果（记得要结合 content 属性使用）。

- 通过这两个属性添加的伪元素，是**行内元素**，需要转换成块元素才能设置宽高。

**2、格式：（第二部分）**

- `E::first-letter` 设置元素 E 里面的**第一个字符**的样式。

- `E::first-line` 设置元素 E 里面的**第一行**的样式。

- `E::selection` 设置元素 E 里面被鼠标选中的区域的样式（一般设置颜色和背景色）。

`E::first-letter` 的举例：

![](http://img.smyhvae.com/20180207_1430.png)

`E::first-line`的举例：

![](http://img.smyhvae.com/20180207_1433.png)

最后来张表格：

![](http://img.smyhvae.com/20180207_1503.png)

> 以下是正文。

## 前言

我们在上一篇文章中学习了[CSS3 的选择器](http://www.cnblogs.com/smyhvae/p/8426799.html)，本文来学一下 CSS3 的一些属性。

本文主要内容：

- 文本

- 盒模型中的 box-sizing 属性

- 处理兼容性问题：私有前缀

- 边框

- 背景属性

- 渐变

## 文本

### text-shadow：设置文本的阴影

格式举例：

```javascript
	text-shadow: 20px 27px 22px pink;
```

参数解释：水平位移 垂直位移 模糊程度 阴影颜色。

效果举例：

![](http://img.smyhvae.com/20180207_1600.png)

### 举例：凹凸文字效果

text-shadow 可以设置多个阴影，每个阴影之间使用逗号隔开。我们来看个例子。

代码如下：

```html
<!DOCTYPE html>
<html>
  <head lang="en">
    <meta charset="UTF-8" />
    <title></title>
    <style>
      body {
        background-color: #666;
      }

      div {
        font-size: 100px;
        text-align: center;
        font-weight: bold;
        font-family: "Microsoft Yahei";
        color: #666;
      }

      /* text-shadow 可以设置多个阴影，每个阴影之间使用逗号隔开*/
      .tu {
        text-shadow: -1px -1px 1px #fff, 1px 1px 1px #000;
      }

      .ao {
        text-shadow: -1px -1px 1px #000, 1px 1px 1px #fff;
      }
    </style>
  </head>
  <body>
    <div class="ao">生命壹号</div>
    <div class="tu">生命壹号</div>
  </body>
</html>
```

效果如下：

![](http://img.smyhvae.com/20180207_1617.png)

上图中，实现凹凸文字效果的方式比较简单，给左上角放黑色的阴影，右下角放白色的阴影，就达到了凹下去的效果。

## 盒模型中的 box-sizing 属性

我们在**[之前的文章](http://www.cnblogs.com/smyhvae/p/7256371.html)**中专门讲过盒子模型。

CSS3 对盒模型做出了新的定义，即允许开发人员**指定盒子宽度和高度的计算方式**。

这就需要用到 `box-sizing`属性。它的属性值可以是：`content-box`、`border-box`。解释如下。

**外加模式：**（css 的默认方式）

```javascript
	box-sizing: content-box;
```

解释：此时设置的 width 和 height 是**内容区域**的宽高。`盒子的实际宽度 = 设置的 width + padding + border`。此时改变 padding 和 border 的大小，也不会改变内容的宽高，而是盒子的总宽高发生变化。

**内减模式：**【需要注意】

```javascript
	box-sizing: border-box;
```

解释：此时设置的 width 和 height 是**盒子**的总宽高。`盒子的实际宽度 = 设置的 width`。此时改变 padding 和 border 的大小，会改变内容的宽高，盒子的总宽高不变。

## 处理兼容性问题：私有前缀

通过网址<http://caniuse.com/> 可以查询 CSS3 各特性的支持程度。

处理兼容性问题的常见方法：为属性添加**私有前缀**。

如此方法不能解决，应尽量避免使用，无需刻意去处理 CSS3 的兼容性问题。

**私有前缀的举例**：

比如说，我想给指定的 div 设置下面这样一个属性：

```css
background: linear-gradient(left, green, yellow);
```

上面这个属性的作用是：添加从左到右的线性渐变，颜色从绿色变为黄色。

如果直接这样写属性，是看不到效果的：

![](http://img.smyhvae.com/20180207_1700.png)

此时，我们可以**为浏览器添加不同的私有前缀**，属性就可以生效了。

格式如下：

```html
-webkit-: 谷歌 苹果 -moz-:火狐 -ms-：IE -o-：欧朋
```

格式举例如下：

```css
background: -webkit-linear-gradient(left, green, yellow);
background: -moz-linear-gradient(left, green, yellow);
background: -ms-linear-gradient(left, green, yellow);
background: -o-linear-gradient(left, green, yellow);
background: linear-gradient(left, green, yellow);
```

效果如下：

![](http://img.smyhvae.com/20180207_1710.png)

## 边框

边框的属性很多，其中**边框圆角**和**边框阴影**这两个属性，应用十分广泛，兼容性也相对较好，且符合**渐进增强**的原则，需要重点熟悉。

### 边框圆角：`border-radius` 属性

边框的每个圆角，本质上是一个圆，圆有**水平半径**和**垂直半径**：如果二者相等，就是圆；如果二者不等， 就是椭圆。

单个属性的写法：

```css
border-top-left-radius: 60px 120px; //参数解释：水平半径   垂直半径

border-top-right-radius: 60px 120px;

border-bottom-left-radius: 60px 120px;

border-bottom-right-radius: 60px 120px;
```

复合写法：

```
	border-radius: 60px/120px;             //参数：水平半径/垂直半径

	border-radius: 20px 60px 100px 140px;  //从左上开始，顺时针赋值。如果当前角没有值，取对角的值

	border-radius: 20px 60px;
```

最简洁的写法：（四个角的半径都相同时）

```
	border-radius: 60px;
```

举例：

```html
<!DOCTYPE html>
<html>
  <head lang="en">
    <meta charset="UTF-8" />
    <title></title>
    <style>
      .parent {
        width: 400px;
      }
      .box {
        width: 100px;
        height: 100px;
        float: left;
        border: 1px solid rgb(144, 12, 63);
        margin: 20px;
        text-align: center;
        line-height: 100px;
        color: #fff;
        font-size: 50px;
        background-color: rgb(255, 141, 26);
      }

      /*画圆形的方式一*/
      .box:nth-child(1) {
        border-radius: 50px;
      }

      /*画圆形的方式二*/
      .box:nth-child(2) {
        border-radius: 50%;
      }

      .box:nth-child(3) {
        border-radius: 100px 0 0 0;
      }

      .box:nth-child(4) {
        border-radius: 100px/50px;
      }

      .box:nth-child(5) {
        border-radius: 10%;
      }

      .box:nth-child(6) {
        border-radius: 0 100px;
      }
    </style>
  </head>
  <body>
    <div class="parent">
      <div class="box">1</div>
      <div class="box">2</div>
      <div class="box">3</div>
      <div class="box">4</div>
      <div class="box">5</div>
      <div class="box">6</div>
    </div>
  </body>
</html>
```

效果如下：

![](http://img.smyhvae.com/20180207_1750.png)

### 边框阴影：`box-shadow` 属性

格式举例：

```javascript
	box-shadow: 水平偏移 垂直偏移 模糊程度 阴影大小 阴影颜色

	box-shadow: 15px 21px 48px -2px #666;
```

参数解释：

- 水平偏移：正值向右 负值向左。

- 垂直偏移：正值向下 负值向上。

- 模糊程度：不能为负值。

效果如下：

![](http://img.smyhvae.com/20180207_2027.png)

另外，后面还可以再加一个 inset 属性，表示内阴影。如果不写，则默认表示外阴影。例如：

```javascript
	box-shadow:3px 3px 3px 3px #666 inset;
```

效果如下：

20180207_2028.png
![](http://img.smyhvae.com/20180206_2150.png)

**注意**：设置边框阴影不会改变盒子的大小，即不会影响其兄弟元素的布局。

我们还可以设置多重边框阴影，实现更好的效果，增强立体感。

### 边框图片

边框图片有以下属性：

```javascript
	/* 边框图片的路径*/
	border-image-source: url("images/border.png");

	/* 图片边框的裁剪*/
	border-image-slice: 27;

	/*图片边框的宽度*/
	border-image-width: 27px;

	/*边框图片的平铺*/
	/* repeat :正常平铺 但是可能会显示不完整*/
	/*round: 平铺 但是保证 图片完整*/
	/*stretch: 拉伸显示*/
	border-image-repeat: stretch;
```

我们也可以写成一个综合属性：

```javascript
	 border-image: url("images/border.png") 27/20px round;
```

这个属性要好好理解，我们假设拿下面这张图来作为边框图片：

![](http://img.smyhvae.com/20180207_2045.png)

![](http://img.smyhvae.com/20180207_2046.png)

这张图片将会被“切割”成**九宫格**形式，然后进行平铺。四个角位置、形状保持不变，中心位置和水平垂直向两个方向平铺：

![](http://img.smyhvae.com/20180207_2050.png)

再具体一点：

![](http://img.smyhvae.com/20180207_2051.png)

### 常见的边框图片汇总

```html

```

CSS3 的更多属性，且看下文继续。

我们在 div 里放一个 img，发现：

在 html 和 html5 中，div 的长宽是不同的，后者的高度要超过几个像素。

比如说，下面这个是 html 的。

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Document</title>
    <style type="text/css">
      * {
        margin: 0px;
        padding: 0px;
      }
    </style>
  </head>
  <body>
    <div>
      <img src="/Users/smyhvae/Dropbox/img/20170813_1143.jpg" alt="" />
    </div>
  </body>
</html>
```
