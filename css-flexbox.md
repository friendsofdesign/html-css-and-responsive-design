# CSS Flexbox

### **Why Flexbox?**

For a long time, the only reliable cross browser-compatible tools we've had available for creating CSS layouts are things like [floats](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Floats) and [positioning](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Positioning). These are fine and they work, but in some ways they are also rather limiting and frustrating.

The following simple layout requirements are either difficult or impossible to achieve with such tools, in any kind of convenient, flexible way:

* Vertically centering a block of content inside its parent.
* Making all the children of a container take up an equal amount of the available width/height, regardless of how much width/height is available.
* Making all columns in a multiple column layout adopt the same height even if they contain a different amount of content.

As you'll see in subsequent sections, flexbox makes a lot of layout tasks much easier. Let's dig in!

#### Introducing a simple example

In this article we are going to get you to work through a series of exercises to help you understand how flexbox works. To get started, you should make a local copy of the first starter file — [flexbox0.html](https://github.com/mdn/learning-area/blob/master/css/css-layout/flexbox/flexbox0.html) from our github repo — load it in a modern browser \(like Firefox or Chrome\), and have a look at the code in your code editor. You can [see it live here](http://mdn.github.io/learning-area/css/css-layout/flexbox/flexbox0.html) also.

You'll see that we have a [`<header>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/header) element with a top level heading inside it, and a [`<section>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/section)element containing three [`<article>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/article)s. We are going to use these to create a fairly standard three column layout.

![](https://mdn.mozillademos.org/files/13406/flexbox-example1.png)

#### Specifying what elements to lay out as flexible boxes

To start with, we need to select which elements are to be laid out as flexible boxes. To do this, we set a special value of [`display`](https://developer.mozilla.org/en-US/docs/Web/CSS/display) on the parent element of the elements you want to affect. In this case we want to lay out the [`<article>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/article) elements, so we set this on the [`<section>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/section) \(which becomes a flex container\):

```text
section {
  display: flex;
}
```

The result of this should be something like so:

![](https://mdn.mozillademos.org/files/13408/flexbox-example2.png)

So, this single declaration gives us everything we need — incredible, right? We have our multiple column layout with equal sized columns, and the columns are all the same height. This is because the default values given to flex items \(the children of the flex container\) are set up to solve common problems such as this. More on those later.

**Note**: You can also set a [`display`](https://developer.mozilla.org/en-US/docs/Web/CSS/display) value of `inline-flex` if you wish to lay out inline items as flexible boxes.

#### An aside on the flex model

When elements are laid out as flexible boxes, they are laid out along two axes:

![](https://developer.mozilla.org/files/3739/flex_terms.png)

* The **main axis** is the axis running in the direction the flex items are being laid out in \(e.g. as rows across the page, or columns down the page.\) The start and end of this axis are called the **main start** and **main end**.
* The **cross axis** is the axis running perpendicular to the direction the flex items are being laid out in. The start and end of this axis are called the **cross start** and **cross end**.
* The parent element that has `display: flex` set on it \(the [`<section>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/section) in our example\) is called the **flex container**.
* The items being laid out as flexible boxes inside the flex container are called **flex items** \(the [`<article>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/article) elements in our example\).

Bear this terminology in mind as you go through subsequent sections. You can always refer back to it if you get confused about any of the terms being used.

#### Columns or rows?

Flexbox provides a property called [`flex-direction`](https://developer.mozilla.org/en-US/docs/Web/CSS/flex-direction) that specifies what direction the main axis runs in \(what direction the flexbox children are laid out in\) — by default this is set to `row`, which causes them to be laid out in a row in the direction your browser's default laguage works in \(left to right, in the case of an English browser\).

Try adding the following declaration to your section rule:

```text
flex-direction: column
```

You'll see that this puts the items back in a column layout, much like they were before we added any CSS. Before you move on, delete this declaration from your example.

**Note**: You can also layout flex items in a reverse direction using the `row-reverse` and `column-reverse`values. Experiment with these values too!

#### Wrapping

One issue that arises when you have a fixed amount of width or height in your layout is that eventually your flexbox children will overflow their container, breaking the layout. Have a look at our [flexbox-wrap0.html](https://github.com/mdn/learning-area/blob/master/css/css-layout/flexbox/flexbox-wrap0.html) example, and try [viewing it live](http://mdn.github.io/learning-area/css/css-layout/flexbox/flexbox-wrap0.html) \(take a local copy of this file now if you want to follow along with this example\):

![](https://mdn.mozillademos.org/files/13410/flexbox-example3.png)

Here we see that the children are indeed breaking out of their container. One way in which you can fix this is to add the following declaration to your section rule:

```text
flex-wrap: wrap
```

Try this now; you'll see that the layout looks much better with this included:

![](https://mdn.mozillademos.org/files/13412/flexbox-example4.png)We now have multiple rows — as many flexbox children are fitted onto each row as makes sense, and any overflow is moved down to the next line. The `flex: 200px` declaration set on the articles means that each will be at least 200px wide; we'll discuss this property in more detail later on. You might also notice that the last few children on the last row are each made wider so that the entire row is still filled.

But there's more we can do here. First of all, try changing your [`flex-direction`](https://developer.mozilla.org/en-US/docs/Web/CSS/flex-direction) property value to `row-reverse` — now you'll see that you still have your multiple row layout, but it is started from the opposite corner of the browser window and now flows in reverse.

#### flex-flow shorthand

At this point it is worth noting that a shorthand exists for [`flex-direction`](https://developer.mozilla.org/en-US/docs/Web/CSS/flex-direction) and [`flex-wrap`](https://developer.mozilla.org/en-US/docs/Web/CSS/flex-wrap) — [`flex-flow`](https://developer.mozilla.org/en-US/docs/Web/CSS/flex-flow). So for example, you can replace

```text
flex-direction: row;
flex-wrap: wrap;
```

with

```text
flex-flow: row wrap;
```

#### Flexible sizing of flex items

Let's now return to our first example, and look at how we can control what proportion of space flex items take up. Fire up your local copy of [flexbox0.html](https://github.com/mdn/learning-area/blob/master/css/css-layout/flexbox/flexbox0.html), or take a copy of [flexbox1.html](https://github.com/mdn/learning-area/blob/master/css/css-layout/flexbox/flexbox1.html) as a new starting point \([see it live](http://mdn.github.io/learning-area/css/css-layout/flexbox/flexbox1.html)\).

First, add the following rule to the bottom of your CSS:

```text
article {
  flex: 1;
}
```

This is a unitless proportion value that dictates how much of the available space along the main axis each flex item will take up. In this case, we are giving each [`<article>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/article) element a value of 1, which means they will all take up an equal amount of the spare space left after things like padding and margin have been set. It is a proportion, meaning that giving each flex item a value of 400000 would have exactly the same effect.

Now add the following rule below the previous one:

```text
article:nth-of-type(3) {
  flex: 2;
}
```

Now when you refresh, you'll see that the third [`<article>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/article) takes up twice as much of the available width as the other two — there are now four proportion units available in total. The first two flex items have one each so they take 1/4 of the available space each. The third one has two units, so it takes up 2/4 of the available space \(or 1/2\).

You can also specify a minimum size value inside the flex value. Try updating your existing article rules like so:

```text
article {
  flex: 1 200px;
}
​
article:nth-of-type(3) {
  flex: 2 200px;
}
```

This basically states "Each flex item will first be given 200px of the available space. After that, the rest of the available space will be shared out according to the proportion units." Try refreshing and you'll see a difference in how the space is shared out.

![](https://mdn.mozillademos.org/files/13406/flexbox-example1.png)

The real value of flexbox can be seen in its flexibility/responsiveness — if you resize the browser window, or add another [`<article>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/article) element, the layout continues to work just fine.

#### flex: shorthand versus longhand

[`flex`](https://developer.mozilla.org/en-US/docs/Web/CSS/flex) is a shorthand property that can specify up to three different values:

* The unitless proportion value we discussed above. This can be specified individually using the [`flex-grow`](https://developer.mozilla.org/en-US/docs/Web/CSS/flex-grow) longhand property.
* A second unitless proportion value — [`flex-shrink`](https://developer.mozilla.org/en-US/docs/Web/CSS/flex-shrink) — that comes into play when the flex items are overflowing their container. This specifies how much of the overflowing amount is taken away from each flex item's size, to stop them overflowing their container. This is quite an advanced flexbox feature, and we won't be covering it any further in this article.
* The minimum size value we discussed above. This can be specified individually using the [`flex-basis`](https://developer.mozilla.org/en-US/docs/Web/CSS/flex-basis) longhand value.

We'd advise against using the longhand flex properties unless you really have to \(for example, to override something prevously set\). They lead to a lot of extra code being written, and they can be somewhat confusing.

#### Horizontal and vertical alignment

You can also use flexbox features to align flex items along the main or cross axes. Let's explore this by looking at a new example — [flex-align0.html](https://github.com/mdn/learning-area/blob/master/css/css-layout/flexbox/flex-align0.html) \([see it live also](http://mdn.github.io/learning-area/css/css-layout/flexbox/flex-align0.html)\) — which we are going to turn into a neat, flexible button/toolbar. At the moment you'll see a horizontal menu bar, with some buttons jammed into the top left hand corner.

![](https://mdn.mozillademos.org/files/13414/flexbox-example5.png)

First, take a local copy of this example.

Now, add the following to the bottom of the example's CSS:

```text
div {
  display: flex;
  align-items: center;
  justify-content: space-around;
}
```

Refresh the page and you'll see that the buttons are now nicely centered, horizontally and vertically. We've done this via two new properties.

[`align-items`](https://developer.mozilla.org/en-US/docs/Web/CSS/align-items) controls where the flex items sit on the cross axis.

* By default, the value is `stretch`, which stretches all flex items to fill the parent in the direction of the cross axis. If the parent hasn't got a fixed width in the cross axis direction, then all flex items will become as long as the longest flex items. This is how our first example got equal height columns by default.
* The `center` value that we used in our above code causes the items to maintain their intrinsic dimensions, but be centered along the cross axis. This is why our current example's buttons are centered vertically.
* You can also have values like `flex-start` and `flex-end`, which will align all items at the start and end of the cross axis respectively. See [`align-items`](https://developer.mozilla.org/en-US/docs/Web/CSS/align-items) for the full details.

You can override the [`align-items`](https://developer.mozilla.org/en-US/docs/Web/CSS/align-items) behavior for individual flex items by applying the [`align-self`](https://developer.mozilla.org/en-US/docs/Web/CSS/align-self)property to them. For example, try adding the following to your CSS:

```text
button:first-child {
  align-self: flex-end;
}
```

Have a look at what effect this has, and remove it again when you've finished.

[`justify-content`](https://developer.mozilla.org/en-US/docs/Web/CSS/justify-content) controls where the flex items sit on the main axis.

* The default value is `flex-start`, which makes all the items sit at the start of the main axis.
* You can use `flex-end` to make them sit at the end.
* `center` is also a value for `justify-content`, and will make the flex items sit in the center of the main axis.
* The value we've used above, `space-around`, is useful — it distributes all the items evenly along the main axis, with a bit of space left at either end.
* There is another value, `space-between`, which is very similar to `space-around` except that it doesn't leave any space at either end.

We'd like to encourage you to play with these values to see how they work before you continue.

#### Ordering flex items

Flexbox also has a feature for changing the layout order of flex items, without affecting the source order. This is another thing that is impossible to do with traditional layout methods.

The code for this is simple: try adding the following CSS to your button bar example code:

```text
button:first-child {
  order: 1;
}
```

Refresh, and you'll now see that the "Smile" button has moved to the end of the main axis. Let's talk about how this works in a bit more detail:

* By default, all flex items have an [`order`](https://developer.mozilla.org/en-US/docs/Web/CSS/order) value of 0.
* Flex items with higher order values set on them will appear later in the display order than items with lower order values.
* Flex items with the same order value will appear in their source order. So if you have four items with order values of 2, 1, 1, and 0 set on them respectively, their display order would be 4th, 2nd, 3rd, then 1st.
* The 3rd item appears after the 2nd because it has the same order value and is after it in the source order.

You can set negative order values to make items appear earlier than items with 0 set. For example, you could make the "Blush" button appear at the start of the main axis using the following rule:

```text
button:last-child {
  order: -1;
}
```

#### Nested flex boxes

It is possible to create some pretty complex layouts with flexbox. It is perfectly ok to set a flex item to also be a flex container, so that its children are also laid out like flexible boxes. Have a look at [complex-flexbox.html](https://github.com/mdn/learning-area/blob/master/css/css-layout/flexbox/complex-flexbox.html) \([see it live also](http://mdn.github.io/learning-area/css/css-layout/flexbox/complex-flexbox.html)\).

![](https://mdn.mozillademos.org/files/13418/flexbox-example7.png)

The HTML for this is fairly simple. We've got a [`<section>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/section) element containing three [`<article>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/article)s. The third [`<article>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/article) contains three [`<div>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/div)s. :

```text
section - article
          article
          article - div - button   
                    div   button
                    div   button
                          button
                          button
```

Let's look at the code we've used for the layout.

First of all, we set the children of the [`<section>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/section) to be laid out as flexible boxes.

```text
section {
  display: flex;
}
```

Next, we set some flex values on the [`<article>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/article)s themselves. Take special note of the 2nd rule here — we are setting the third [`<article>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/article) to have its children laid out like flex items too, but this time we are laying them out like a column.

```text
article {
  flex: 1 200px;
}
​
article:nth-of-type(3) {
  flex: 3 200px;
  display: flex;
  flex-flow: column;
}
```

Next, we select the first [`<div>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/div). We first use `flex: 1 100px;` to effectively give it a minimum height of 100px, then we set its children \(the [`<button>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/button) elements\) to also be laid out like flex items. Here we lay them out in a wrapping row, and align them in the center of the available space like we did in the individual button example we saw earlier.

```text
article:nth-of-type(3) div:first-child {
  flex: 1 100px;
  display: flex;
  flex-flow: row wrap;
  align-items: center;
  justify-content: space-around;
}
```

Finally, we set some sizing on the button, but more interestingly we give it a flex value of 1. This has a very interesting effect, which you'll see if you try resizing your browser window width. The buttons will take up as much space as they can and sit as many on the same line as they can, but when they can no longer fit comfortably on the same line, they'll drop down to create new lines.

```text
button {
  flex: 1;
  margin: 5px;
  font-size: 18px;
  line-height: 1.5;
}
```

#### Cross browser compatibility

Flexbox support is available in most new browsers — Firefox, Chrome, Opera, Microsoft Edge and IE 11, newer versions of Android/iOS, etc. However you should be aware that there are still older browsers in use that don't support Flexbox \(or do, but support a really old, out-of-date version of it.\)

While you are just learning and experimenting, this doesn't matter too much; however if you are considering using flexbox in a real website you need to do testing and make sure that your user experience is still acceptable in as many browsers as possible.

Flexbox is a bit trickier than some CSS features. For example, if a browser is missing a CSS drop shadow, then the site will likely still be usable. Not supporting flexbox features however will probably break a layout completely, making it unusable.

We'll discuss strategies for overcoming tricky cross browser support issues in a future module.

