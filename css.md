# CSS

## Layout System
### Box positioning
CSS2.1 定义的三种布局方案：
- 正常流, 三种 Formatting Context 组成, Block, Inline, Relative
- 浮动， which interact with normal flow in their own way and form the basis of most modern CSS grid frameworks
- 绝对定位，处理相对于正常流的绝对定位和固定定位元素

#### Normal Flow
BFC:
1. 每个块级元素宽度默认充满父元素
2. 每个块级元素都位于父元素的左外边缘。

IFC:
1. boxes are laid out horizontally onto one or more line boxes. Line boxes are generated as needed; 
2. their width is generally the width of the containing block (minus floats) and their height is always sufficient for all the boxes it contains.
3. when inline boxes exceed the width of a line box, it will be split if possible. When the rules disallow splitting the box, it will simply horizontally overflow the line box. 例如可替换元素（video 或者 image）是不可 split 的

line-boxes 内的对齐方式：
1. 水平
- text-align: 应用于行内内容分到line boxes后
2. 竖直
- line-height: 行内元素的高度取决于其字体大小和line-height（the height of the font * line-height）
- vertical-align: controls the vertical alignment of inline boxes within line boxes - not the vertical alignment of the line boxes themselves.

Relative:
1. 属于正常文档流，开启后可设置top、left、right、bottom 偏移量。
2. 对于正常流的其他元素来说，就当此元素还在之前的位置一样，不会受影响。


#### Float
1. 浮动元素在布局时脱离正常流，因此它们不会影响块级元素的垂直定位。
2. 浮动元素会与其容器的左外边缘或右外边缘对齐。
3. 浮动元素从左侧或右侧开始堆叠，并按照它们在标记中出现的顺序排列。换句话说，对于右浮动的盒子，第一个右浮动的盒子位于包含它的盒子的右边缘，第二个右浮动的盒子紧邻第一个盒子的左侧排列。
4. 浮动可以影响当前及后续元素的内联级别内容的行框（line boxes）。具体来说，任何当前及后续的行框都会缩短以腾出空间给浮动元素。
5.  由于浮动不在正常流中，它们通常不会影响父容器的高度。这也是“清除浮动”（clearfix）技术被开发出来的原因之一。
6. 可以使用 clear 属性来清除浮动效果。
7. Floats do not affect the line boxes inside elements in normal flow that establish new block formatting contexts. Instead, such elements are either placed to the side of the float, or cleared by placing them below any preceding floats:

#### Margin collapsing
1. 大吃小
2. 只有垂直边距会发生折叠——水平边距永远不会折叠
3. Only margins from block-level boxes can collapse. In other words, margins of floats, absolutely positioned elements, and inline-block elements never collapse. Inline-level boxes don't have margins, so they don't collapse either.
4. Only margins from boxes that participate in the same block formatting context can collapse. Note that block formatting contexts are not established by block boxes with overflow: visible (the default value). In this sense, margin collapsing behaves similar to floats, which only affect line boxes of block-level boxes in the same formatting context.
5. Only margins that are considered to be adjoining can collapse.

#### Stacking contexts and z-index
The z-axis positioning of elements in CSS is determined by their type (float, block-level, inline-level, absolutely positioned) and their z-index relative to the current stacking context.

Ignoring stacking context for a moment, elements are drawn in the following order:

- block-level descendants in the normal flow
- floats
- inline descendants in the normal flow
- positioned elements

A stacking context is formed, anywhere in the document, by any element which is either

- the root element (HTML),
- positioned (absolutely or relatively) with a z-index value other than "auto",
- a flex item with a z-index value other than "auto",
- elements with an opacity value less than 1. (See the specification for opacity),
- elements with a transform value other than "none", e.g. transform: translateX(0);
- position: fixed always creates a new stacking context, even when z-index is "auto" (See this post)


1. only positioned elements can have z-index, e.g. setting z-index for normal flow blocks or floats will have no effect on their rendering order.
2.  elements with a negative stacking context are drawn below the normal flow and floats and elements with a positive stacking context are drawn above the normal flow and floats. If two elements have the same z-index, then they are stacked back-to-front according to their order in the HTML markup.
