# CSS Box Model

### CSS BOX MODEL

In a document, each element is represented as a rectangular box. Determining the size, properties — like its color, background, borders aspect — and the position of these boxes is the goal of the rendering engine.

In CSS, each of these rectangular boxes is described using the standard _box model_. This model describes the space of the content taken by an element. Each box has four edges: the **margin edge**, **border edge**, **padding edge**, and **content edge**.

![](https://mdn.mozillademos.org/files/8685/boxmodel-%283%29.png)

The **content area** is the area containing the real content of the element. It often has a background, a color or an image \(in that order, an opaque image hiding the background color\) and is located inside the _content edge_; its dimensions are the _content width_, or _content-box width_, and the _content height_, or _content-box height_.

If the CSS [`box-sizing`](https://developer.mozilla.org/en-US/docs/Web/CSS/box-sizing) property is set to default, the CSS properties [`width`](https://developer.mozilla.org/en-US/docs/Web/CSS/width), [`min-width`](https://developer.mozilla.org/en-US/docs/Web/CSS/min-width), [`max-width`](https://developer.mozilla.org/en-US/docs/Web/CSS/max-width), [`height`](https://developer.mozilla.org/en-US/docs/Web/CSS/height), [`min-height`](https://developer.mozilla.org/en-US/docs/Web/CSS/min-height) and [`max-height`](https://developer.mozilla.org/en-US/docs/Web/CSS/max-height) control the content size.

The **padding area** extends to the border surrounding the padding. When the content area has a background, color, or image set on it, this will extend into the padding, which is why you can think of the padding as extending the content. The padding is located inside the _padding edge_, and its dimensions are the _padding-box width_ and the _padding-box height_.

The space between the padding and the content edge can be controlled using the [`padding-top`](https://developer.mozilla.org/en-US/docs/Web/CSS/padding-top), [`padding-right`](https://developer.mozilla.org/en-US/docs/Web/CSS/padding-right), [`padding-bottom`](https://developer.mozilla.org/en-US/docs/Web/CSS/padding-bottom), [`padding-left`](https://developer.mozilla.org/en-US/docs/Web/CSS/padding-left) and the shorthand [`padding`](https://developer.mozilla.org/en-US/docs/Web/CSS/padding) CSS properties.

The **border area** extends the padding area to the area containing the borders. It is the area inside the _border edge_, and its dimensions are the _border-box width_ and the _border-box height_. This area depends on the size of the border that is defined by the [`border-width`](https://developer.mozilla.org/en-US/docs/Web/CSS/border-width) property or the shorthand [`border`](https://developer.mozilla.org/en-US/docs/Web/CSS/border).

The **margin area** extends the border area with an empty area used to separate the element from its neighbors. It is the area inside the _margin edge_, and its dimensions are the _margin-box width_ and the _margin-box height_.

The size of the margin area is controlled using the [`margin-top`](https://developer.mozilla.org/en-US/docs/Web/CSS/margin-top), [`margin-right`](https://developer.mozilla.org/en-US/docs/Web/CSS/margin-right), [`margin-bottom`](https://developer.mozilla.org/en-US/docs/Web/CSS/margin-bottom), [`margin-left`](https://developer.mozilla.org/en-US/docs/Web/CSS/margin-left) and the shorthand [`margin`](https://developer.mozilla.org/en-US/docs/Web/CSS/margin) CSS properties.

When [margin collapsing](https://developer.mozilla.org/en/CSS/margin_collapsing) happens, the margin area is not clearly defined since margins are shared between boxes.

Finally, note that, for non-replaced inline elements, the amount of space taken up \(the contribution to the height of the line\) is determined by the [`line-height`](https://developer.mozilla.org/en-US/docs/Web/CSS/line-height) property, even though the border and padding appear visually around the content.

