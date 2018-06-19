# CSS Layout Introduction

### CSS Layout Introduction

CSS page layout techniques allow us to take elements contained in a web page and control where they are positioned relative to their default position in normal layout flow, the other elements around them, their parent container, or the main viewport/window. The page layout techniques we'll be covering in more detail in this module are:

* Floats
* Positioning
* CSS tables
* Flexbox
* Grid

Each technique has its uses, advantages, and disadvantages.

#### Normal layout flow

Normal flow is how the browser lays out HTML pages by default when you do nothing to control page layout. Let's look at a quick HTML example:

```text
<p>I love my cat.</p>
​
<ul>
  <li>Buy cat food</li>
  <li>Exercise</li>
  <li>Cheer up friend</li>
</ul>
​
<p>The end!</p>
```

By default, the browser will display this code as follows:

Note here how the HTML is displayed in the exact order in which it appears in the source code, with elements stacked up on top of one another — the first paragraph, followed by the unordered list, followed by the second paragraph.

Layout techniques tend to override this default behaviour, using:

* The [`position`](https://developer.mozilla.org/en-US/docs/Web/CSS/position) property — `static` is the default in normal flow, but you can cause elements to be laid out differently using other values, for example always fixed to the top left of the browser viewport.
* Floats — applying a [`float`](https://developer.mozilla.org/en-US/docs/Web/CSS/float) value such as `left` can cause block level elements to line up alongside one another rather than sit on top of one another
* The [`display`](https://developer.mozilla.org/en-US/docs/Web/CSS/display) property — standard values such as `block`, `inline` or `inline-block` can change how elements behave in normal flow \(see [Types of CSS boxes](https://developer.mozilla.org/en-US/docs/Learn/CSS/Introduction_to_CSS/Box_model#Types_of_CSS_boxes) for more information\), whereas uncommon or specialised values allow us to lay out elements in completely different ways using tools like Flexbox.

#### Floats

Floats is a technique that allows the elements to float to the left or right of one another, rather than the default of sitting on top of one another. The main uses of floats are to lay out columns and float text around an image. To get you started, let's take a quick look at the [`float`](https://developer.mozilla.org/en-US/docs/Web/CSS/float)property and then look at a simple example.

The float property has four possible values:

* `left` — floats the element to the left.
* `right` — floats the element to the right.
* `none` — specified no floating at all. This is the default value.
* inherit — specifies that the value of the `float` property should be inherited from the parent element.

#### Simple HTML example

Let's show how we can create a simple two column layout using floats. First, some HTML:

```text
<h1>2 column layout example</h1>
<div>
  <h2>First column</h2>
  <p> Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla luctus aliquam dolor, eu lacinia lorem placerat vulputate. </p>
</div>
​
<div>
  <h2>Second column</h2>
  <p>Nam vulputate diam nec tempor bibendum. Donec luctus augue eget malesuada ultrices. Phasellus turpis est, posuere sit amet dapibus ut.</p>
</div>
```

Here we have a top-level heading, and two simple `<div>`s, each containing a second-level heading and a paragraph. By default, the content will be laid out in source order, from top to bottom going down the page:

#### Making the columns float

Let's change things — we instead want our two `<div>`s to sit side by side. To do this, we can use the following code. Note how the two `<div>`s are floated one with a value of `left`, and one with a value of `right`, meaning that one will fly to the left, and one will fly to the right. They are also given [`width`](https://developer.mozilla.org/en-US/docs/Web/CSS/width) values that allow them to fit on the same line as one another and have a gutter in between \(the total width will never be more than 100!\)

```text
div:nth-of-type(1) {
  width: 48%;
  float: left;
}
​
div:nth-of-type(2) {
  width: 48%;
  float: right;
}
```

The updated example will look like so:

**Note**: To learn more about [CSS floats](http://moodle.friendsofdesign.co.za/mod/page/view.php?id=396), see our [Floats article](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Floats).

#### Positioning Techniques

Positioning allows you to move an element from it's original spot on the page to another spot with great accuracy.

There are four main types of positioning you should know about:

* **Static positioning** is the default that every element gets — it just means "put the element into it's normal position in the document layout flow — nothing special to see here".
* **Relative positioning** allows you to modify an element's position on the page, moving it relative to its position in normal flow — including making it overlap other elements on the page. This is useful for minor layout tweaks and design pinpointing.
* **Absolute positioning** moves an element completely out of the page's normal layout flow, like it is sitting on its own separate layer. From there, you can fix it in a position relative to the edges of the page's `<html>` element \(or it's nearest positioned ancestor element\). This is useful for creating complex layout effects such as tabbed boxes where different content panels sit on top of one another and are shown and hidden as desired, or information panels that sit off screen by default, but can be made to slide on screen using a control button.
* **Fixed positioning** is very similar to absolute positioning, except that it fixes an element relative to the browser viewport, not another element. This is useful for creating effects such as a persistent navigation menu that always stays in the same place on the screen as the rest of the content scrolls.

#### Simple positioning example

To provide familiarity with these page layout techniques, we'll show you a couple of quick examples. Our examples will all feature the same HTML, which is as follows:

```text
<h1>Positioning</h1>
​
<p>I am a basic block level element.</p>
<p class="positioned">I am a basic block level element.</p>
<p>I am a basic block level element.</p>
```

This HTML will be styled by default using the following CSS:

```text
body {
  width: 500px;
  margin: 0 auto;
}
​
p {
  background: aqua;
  border: 3px solid blue;
  padding: 10px;
  margin: 10px;
}
​
span {
  background: red;
  border: 1px solid black;
}
```

The rendered output is as follows:

#### Relative Positioning

A very common use of relative positioning is to make small tweaks in your layout, such as moving an icon down a bit so it lines up with a text label. To do this, we could add the following rule to add relative positioning:

```text
.positioned {
  position: relative;
  background: yellow;
  top: 30px;
  left: 30px;
}
```

Here we give our middle paragraph a [`position`](https://developer.mozilla.org/en-US/docs/Web/CSS/position) value of `relative` — this doesn't do anything on its own, so we also add [`top`](https://developer.mozilla.org/en-US/docs/Web/CSS/top) and [`left`](https://developer.mozilla.org/en-US/docs/Web/CSS/left) properties. These serve to move the affected element down and to the right — this might seem like the opposite of what you were expecting, but you need to think of it as the element being pushed on it's left and top sides, which result in it moving right and down.

Adding this code will give the following result:

#### Absolute Positioning

Absolute positioning is used to move your elements anywhere around the web page, to create complex layouts. Interestingly, it is often used in concert with relative positioning and floats.

Going back to our original non-positioned example, we could add the following CSS rule to implement absolute positioning:

```text
.positioned {
  position: absolute;
  background: yellow;
  top: 30px;
  left: 30px;
}
```

Here we give our middle paragraph a [`position`](https://developer.mozilla.org/en-US/docs/Web/CSS/position) value of `absolute`, and the same [`top`](https://developer.mozilla.org/en-US/docs/Web/CSS/top) and [`left`](https://developer.mozilla.org/en-US/docs/Web/CSS/left)properties as before. Adding this code, however, will give the following result:

This is very different! The positioned element has now been completely separated from the rest of the page layout, and sits over the top of it. The other two paragraphs now sit together as if their positioned sibling doesn't exist. The [`top`](https://developer.mozilla.org/en-US/docs/Web/CSS/top) and [`left`](https://developer.mozilla.org/en-US/docs/Web/CSS/left) properties have a different effect on absolutely positioned elements than they do on relatively positioned elements. In this case they don't specify how much the element moves relative to its original position; instead they specify the distance the element should sit from the top and left sides of the page's boundaries \(the `<html>` element, to be exact\).

We'll leave fixed positioning for now — it basically works in the same way, except that it remains fixed to the browser viewport's edges, not its positioned parent's edges.

**Note**: to find more out about positioning, see our [Positioning](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Positioning) and [Practical positioning examples](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Practical_positioning_examples) articles.

#### CSS tables

[HTML tables](http://moodle.friendsofdesign.co.za/mod/page/view.php?id=413) are fine for displaying tabular data, but many years ago — before even basic CSS was supported reliably across browsers — web developers used to also use tables for entire web page layouts — putting their headers, footers, different columns, etc. in various table rows and columns. This worked at the time, but it has many problems — table layouts are inflexible, very heavy on markup, difficult to debug, and semantically wrong \(e.g. screen reader users have problems navigating table layouts\).

CSS tables exist to allow you to layout elements like they were a table, without any of the issues described above — this may sound strange, and you should use table elements for tabular data, but sometimes this can be useful. For example, you might want to lay out a form with the labels and text inputs lined up; this can be tricky, but CSS tables make it easy.

Let's look at an example. First, some simple markup that creates an HTML form. Each input element has a label, and we've also included a caption inside a paragraph. Each label/input pair is wrapped in a [`<div>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/div), for layout purposes.

```text
<form>
  <p>First of all, tell us your name and age.</p>
  <div>
    <label for="fname">First name:</label>
    <input type="text" id="fname">
  </div>
  <div>
    <label for="lname">Last name:</label>
    <input type="text" id="lname">
  </div>
  <div>
    <label for="age">Age:</label>
    <input type="text" id="age">
  </div>
</form>
```

Now, the CSS for our example. Most of the CSS is fairly ordinary, except for the uses of the [`display`](https://developer.mozilla.org/en-US/docs/Web/CSS/display) property. The [`<form>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/form), [`<div>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/div)s, and [`<label>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/label)s and [`<input>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input)s have been told to display like a table, table rows, and table cells respectively — basically they'll act like HTML table markup, causing the labels and inputs to nicely line up by default. All we then have to do is add a bit of sizing, margin, etc. to make everything look a bit nicer and we're done.

You'll notice that the caption paragraph has been given `display: table-caption;` — which makes it act like a table [`<caption>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/caption) — and `caption-side: bottom;` to tell the caption to sit on the bottom of the table for styling purposes, even though the markup is before the inputs in the source. This allows for a nice bit of flexibility.

```text
html {
  font-family: sans-serif;
}
​
form {
  display: table;
  margin: 0 auto;
}
​
form div {
  display: table-row;
}
​
form label, form input {
  display: table-cell;
  margin-bottom: 10px;
}
​
form label {
  width: 200px;
  padding-right: 5%;
  text-align: right;
}
​
form input {
  width: 300px;
}
​
form p {
  display: table-caption;
  caption-side: bottom;
  width: 300px;
  color: #999;
  font-style: italic;
}
```

This gives us the following result:

\[WE WILL HAVE TO INCLUDE A \(LINK TO A\) LIVE EXAMPLE HERE\]

You can also see this example live at [css-tables-example.html](https://mdn.github.io/learning-area/css/styling-boxes/box-model-recap/css-tables-example.html) \(see the [source code](https://github.com/mdn/learning-area/blob/master/css/styling-boxes/box-model-recap/css-tables-example.html) too.\)

**Note**: We won't cover CSS tables in any more detail in this module.

#### Flexible boxes

CSS is a powerful language that can do many things, but it has traditionally fallen down in terms of layout. Traditional old-fashioned layout methods like [`float`](https://developer.mozilla.org/en-US/docs/Web/CSS/float) and [`positioning`](https://developer.mozilla.org/en-US/docs/Web/CSS/positioning) work, but sometimes they feel more complex, fiddly, inflexible and hacky than they need to be. For example, what if you wanted to:

* Vertically center a box of content \(not just text; `line-height` won't work\).
* Make several columns containing different amounts of content have the same height, without using a fixed height, or faking it with background images.
* Make several boxes in a line take up the same amount of the available space, regardless of how many of them there are, and if they have padding, margin, etc. applied.

The examples above are pretty much impossible to achieve with regular CSS — Flexible boxes \(or flexbox\) was invented to allow such things to be more easily achieved.

Let's look at an example; first, some simple HTML:

```text
<section>
  <div>This is a box</div>
  <div>This is a box</div>
  <div>This is a box</div>
</section>
​
<button class="create">Create box</button>
<button class="reset">Reset demo</button>
```

Here we've got a [`<section>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/section) element with three [`<div>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/div)s inside, plus a couple of buttons to create a new box, and reset the demo. By default, the child elements would not be laid out or sized at all, and using old traditional methods we'd have to carefully size each one, allowing for width, padding, border and margin, and if we added another child element we'd have to completely change all the values.

Let's instead do this with Flexbox:

```text
html {
  font-family: sans-serif;
}
​
section {
  width: 93%;
  height: 240px;
  margin: 20px auto;
  background: purple;
  display: flex;
}
​
div {
  color: white;
  background: orange;
  flex: 1;
  margin-right: 10px;
  text-shadow: 1px 1px 1px black;
}
​
div:last-child {
  margin-right: 0;
}
​
section, div {
  border: 5px solid rgba(0,0,0,0.85);
  padding: 10px;
}
```

Two lines of this CSS are really interesting:

* `display: flex;` tells the [`<section>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/section) element's children to be laid out as flexible boxes — by default, they will all stretch to fill the available height of the parent, whatever that is, and be laid out in a row — with enough width to wrap their content.
* `flex: 1;` tells each [`<div>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/div) element to take up an equal amount of the space available in the row, no matter how many there are.

To illustrate further how amazing this is, we'll also add a little JavaScript so that you can add further child `<div>`s by pressing the _Create box_ button. You can also reset the demo if you add too many `<div>`s, by pressing the _Reset demo_ button.

Here's the example live — have a play, to witness how powerful Flexbox is as a layout tool.

\[WE WILL HAVE TO INCLUDE A \(LINK TO A\) LIVE EXAMPLE HERE\]

You can also find this demo at [flexbox-example.html](https://mdn.github.io/learning-area/css/styling-boxes/box-model-recap/flexbox-example.html) \(see also the [source code](https://github.com/mdn/learning-area/blob/master/css/styling-boxes/box-model-recap/flexbox-example.html)\).

**Note**: To find more out about Flexbox, see our [Flexbox](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Flexbox) article.

#### Grid layout

The most experimental feature to mention here is CSS Grids, which aren't supported very widely across browsers yet. Web pages are often laid out using grid systems, in the same manner as print media, and the idea here is to make this process easier and more natural, by defining a grid, and then defining which parts of the content sit within each area of the grid.

CSS Grids in their present state aren't really supported anywhere yet \(except in experimental versions of Firefox and Chrome\). IE and Edge support an older, obsolete version of the technology. This is something we can look forward to in the future!

**Note**: To find more out about the current grid frameworks and other technologies in use today, and the upcoming native CSS Grids specification, see our [Grids](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Grids) article.

