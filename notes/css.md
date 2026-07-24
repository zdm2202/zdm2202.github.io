# css 笔记

## padding 与 margin

`padding`: 内间距

`margin`: 外间距

`border`: 边框介于外间距区域和内间距区域的中间

`body` 默认会有一段通常为 8px 的外边距
如果希望`body`占满屏幕则需要设置`margin: 0;`

## 弹性盒子 flexbox

> [runoob上的一篇好文章](https://www.runoob.com/w3cnote/flex-grammar.html)

### 使用方式

在父元素中标注 `display: flex;`。

> 我的 vscode 还提示 `display: flexbox`，实际上似乎压根就没这个东西。

```css
.container {
    display: flex;
}
```

### 布局方向 `flex-direction`
并且默认是左右布局，如果想配置为上下堆叠的话应当如下设置:

```css
.container {
    display: flex;
    /* 默认值是 row */
    flex-direction: column;
}
```
`flex-direction` 属性共有四个值：
 - `row`
 - `row-reverse`
 - `column`
 - `column-reverse`

## 小坑：令 html 块和 body 块占满全屏

```css
html, body {
    height: 100%;
}
```

如果内容无法占满整个屏幕，则`html`块并不会主动占满屏幕。

**经验教训**: 不要用 background-color 调试，因为会有背景传播，导致实际颜色和尺寸不符。**用开发者工具！**

> Background Propagation（背景传播）:
> 如果 <html> 根元素没有设置自己的背景（或者背景为 transparent / none），那么 body 的背景会被“提升”到整个画布（canvas）上，看起来好像整个浏览器窗口都变成了那个颜色。

## flexbox 之外的另一种布局方式: float

我在一个人的 github 主页上面研究侧栏实现时发现的。
首先， `body` 块采用的是 `display: block;` ，显然不是通过弹性盒子来实现的侧边栏。
其次，侧栏的 `div` 和主要内容部分的 `div` 直接作为 `body` 的子节点，所以可以彻底排除 `flexbox` 的可能性。
实际上是这样实现的，这是主体部分的 css :

```css
.wrapper-content {
    float: right;
    width: 70%;
}
```

另一侧也是类似的方式声明其占据了左侧 30% 的空间（多了个 `height: 100%;`）。
这样的好处似乎是兼容性好，不过不如 `flexbox` 方便。

> float 可以脱离正常的文档流，但是不会真的让元素飞起来。
> 如果想要元素真的飘在上方或者绝对定位，可以使用 `position` 与 `z-index` 设置。