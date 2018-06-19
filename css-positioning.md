# CSS Positioning

### **Document flow**

Positioning is a fairly complex topic, so before we dive into the code let's revisit and expand on at a bit of layout theory to give us an idea of how this works.

First of all, individual element boxes are laid out by taking the elements' content, then adding any padding, border and margin around them — it's that [box model](https://developer.mozilla.org/en-US/docs/Learn/CSS/Introduction_to_CSS/Box_model) thing again, which we looked at earlier. By default, a block level element's content is 100% of the width of its parent element, and as tall as its content. Inline elements are all tall as their content, and as wide as their content. You can't set width or height on inline elements — they just sit inside the content of block level elements. If you want to control the size of an inline element in this manner, you need to set it to behave like a block level element with `display: block;`.

That explains individual elements, but what about how elements interact with one another? The **normal layout flow** \(mentioned in the layout introduction article\) is the system by which elements are placed inside the browser's viewport. By default, block level elements are laid out vertically in the viewport — each one will appear on a new line below the last one, and they will be separated by any margin that is set on them.

Inline elements behave differently — they don't appear on new lines; instead, they sit on the same line as one another and any adjacent \(or wrapped\) text content, as long as there is space for them to do so inside the width of the parent block level element. If there isn't space, then the overflowing text or elements wil move down to a new line.

If two adjacent elements both have margin set on them and the two margins touch, the larger of the two remains, and the smaller one disappears — this is called [margin collapsing](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model/Mastering_margin_collapsing), and we have met this before too.

Let's look at a simple example that explains all this:

```text
<h1>Basic document flow</h1>
​
<p>I am a basic block level element. My adjacent block level elements sit on new lines below me.</p>
​
<p>By default we span 100% of the width of our parent element, and we are as tall as our child content. Our total width and height is our content + padding + border width/height.</p>
​
<p>We are separated by our margins. Because of margin collapsing, we are separated by the width of one of our margins, not both.</p>
​
<p>inline elements <span>like this one</span> and <span>this one</span> sit on the same line as one another, and adjacent text nodes, if there is space on the same line. Overflowing inline elements will <span>wrap onto a new line if possible (like this one containing text)</span>, or just go on to a new line if not, much like this image will do: <img src="https://mdn.mozillademos.org/files/13360/long.jpg"></p>
```

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

We will be revisiting this example a number of times as we go through this article, as we show the effects of the different positioning options available to us.

We'd like you to follow along with the exercises on your local computer, if possible — grab a copy of `0_basic-flow.html` from our Github repo \([source code here](https://github.com/mdn/learning-area/blob/master/css/css-layout/positioning/0_basic-flow.html)\) and use that as a starting point.

#### Introducing positioning

The whole idea of positioning is to allow us to override the basic document flow behaviour described above, to produce interesting effects. What if you want to slightly alter the position of some boxes inside a layout from their default layout flow position, to give a slightly quirky, distressed feel? Positioning is your tool. Or if you want to create a UI element that floats over the top of other parts of the page, and/or always sits in the same place inside the browser window no matter how much the page is scrolled? Positioning makes such layout work possible.

There are a number of different types of positioning that you can put into effect on HTML elements. To make a specific type of positioning active on an element, we use the [`position`](https://developer.mozilla.org/en-US/docs/Web/CSS/position)property.

#### Static positioning

Static positioning is the default that every element gets — it just means "put the element into it's normal position in the document layout flow — nothing special to see here".

To demonstrate this, and get your example set up for future sections, first add a `class` of `positioned` to the second [`<p>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/p) in the HTML:

```text
<p class="positioned"> ... </p>
```

Now add the following rule to the bottom of your CSS:

```text
.positioned {
   position: static;
  background: yellow;
}
```

If you now save and refresh, you'll see no difference at all, except for the updated background color of the 2nd paragraph. This is fine — as we said before, static positioning is the default behaviour!

**Note**: You can see the example at this point live at `1_static-positioning.html` \([see source code](https://github.com/mdn/learning-area/blob/master/css/css-layout/positioning/1_static-positioning.html)\).

#### Relative positioning

Relative positioning is the first position type we'll take a look at. This is very similar to static positioning, except that once the positioned element has taken its place in the normal layout flow, you can then modify its final position, including making it overlap other elements on the page. Go ahead and update the position declaration in your code:

```text
position: relative;
```

If you save and refresh at this stage, you won't see a change in the result at all — so how do you modify the element's position? You need to use the [`top`](https://developer.mozilla.org/en-US/docs/Web/CSS/top), [`bottom`](https://developer.mozilla.org/en-US/docs/Web/CSS/bottom), [`left`](https://developer.mozilla.org/en-US/docs/Web/CSS/left), and [`right`](https://developer.mozilla.org/en-US/docs/Web/CSS/right) properties, which we'll explain in the next section.

#### Introducing top, bottom, left, and right

[`top`](https://developer.mozilla.org/en-US/docs/Web/CSS/top), [`bottom`](https://developer.mozilla.org/en-US/docs/Web/CSS/bottom), [`left`](https://developer.mozilla.org/en-US/docs/Web/CSS/left), and [`right`](https://developer.mozilla.org/en-US/docs/Web/CSS/right) are used alongside [`position`](https://developer.mozilla.org/en-US/docs/Web/CSS/position) to specify exactly where to move the positioned element to. To try this out, add the following declarations to the `.positioned` rule in your CSS:

```text
top: 30px;
left: 30px;
```

**Note**: The values of these properties can take any [units](https://developer.mozilla.org/en-US/docs/Learn/CSS/Introduction_to_CSS/Values_and_units) you'd logically expect — pixels, mm, rems, %, etc.

If you now save and refesh, you'll get a result something like this:

Cool, huh? Ok, so this probably wasn't what you were expecting — why has it moved to the bottom and right if we specified top and left? Illogical as it may initially sound, this is just the way that relative positioning works — you need to think of an invisible force that pushes the side of the positioned box, moving it in the opposite direction. So for example, if you specify `top: 30px;`, a force pushes the top of the box, causing it to move downwards by 30px.

**Note**: You can see the example at this point live at `2_relative-positioning.html` \([see source code](https://github.com/mdn/learning-area/blob/master/css/css-layout/positioning/2_relative-positioning.html)\).

#### Absolute positioning

Absolute positioning brings very different results. Let's try changing the position declaration in your code as follows:

```text
position: absolute;
```

If you now save and refresh, you should see something like so:

First of all, note that the gap where the positioned element should be in the document flow is no longer there — the first and third elements have closed together like it no longer exists! Well, in a way, this is true. An absolutely positioned element no longer exists in the normal document layout flow. Instead, it sits on it's own layer separate from everything else. This is very useful — it means that we can create isolated UI features that don't interfere with the position of other elements on the page — for example popup information boxes and control menus, rollover panels, UI features that can be dragged and dropped anywhere on the page, and so on.

Second, notice that the position of the element has changed — this is because [`top`](https://developer.mozilla.org/en-US/docs/Web/CSS/top), [`bottom`](https://developer.mozilla.org/en-US/docs/Web/CSS/bottom), [`left`](https://developer.mozilla.org/en-US/docs/Web/CSS/left), and [`right`](https://developer.mozilla.org/en-US/docs/Web/CSS/right) behave in a different way with absolute positioning. Instead of specifying the direction the element should move in, they specify the distance the element should be from each containing element's sides. So in this case, we are saying that the absolutely positioned element should sit 30px from the top of the "containing element", and 30px from the left.

**Note**: You can use [`top`](https://developer.mozilla.org/en-US/docs/Web/CSS/top), [`bottom`](https://developer.mozilla.org/en-US/docs/Web/CSS/bottom), [`left`](https://developer.mozilla.org/en-US/docs/Web/CSS/left), and [`right`](https://developer.mozilla.org/en-US/docs/Web/CSS/right) to resize elements if you need to. Try setting `top: 0; bottom: 0; left: 0; right: 0;` and `margin: 0;` on your positioned elements and see what happens! Put it back again afterwards...

**Note**: Yes, margins still affect positioned elements. Margin collapsing doesn't, however.

**Note**: You can see the example at this point live at `3_absolute-positioning.html` \([see source code](https://github.com/mdn/learning-area/blob/master/css/css-layout/positioning/3_absolute-positioning.html)\).

#### Positioning contexts

Which element is the "containing element" of an absolutely positioned element? By default, it is the [`<html>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/html) element — the positioned element is nested inside the [`<body>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/body) in the HTML source, but in the final layout, it is 30px away from the top and left of the edge of the page, which is the [`<html>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/html) element. This is more accurately called the element's **positioning context**.

We can change the **positioning context** — which element the absolutely positioned element is positioned relative to. This is done by setting positioning on one of the element's other ancestors — one of the elements it is nested inside \(you can't position it relative to an element it is not nested inside\). To demonstrate this, add the following declaration to your body rule:

```text
position: relative;
```

This should give the following result:

The positioned element now sits relative to the [`<body>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/body) element.

**Note**: You can see the example at this point live at `4_positioning-context.html` \([see source code](https://github.com/mdn/learning-area/blob/master/css/css-layout/positioning/4_positioning-context.html)\).

#### Introducing z-index

All this absolute positioning is good fun, but there is another thing we haven't considered yet — when elements start to overlap, what determines which elements appear on top of which other elements? In the example we've seen so far, we only have one positioned element in the positioning context, and it appears on the top, since positioned elements win over non-positioned elements. What about when we have more than one?

Try adding the following to your CSS, to make the first paragraph absolutely positioned too:

```text
p:nth-of-type(1) {
  position: absolute;
  background: lime;
  top: 10px;
  right: 30px;
}
```

At this point you'll see the first paragraph colored green, moved out of the document flow, and positioned a bit above from where it originally was. It is also stacked below the original `.positioned` paragraph, where the two overlap. This is because the `.positioned` paragraph is the second paragraph in the source order, and positioned elements later in the source order win over positioned elements earlier in the source order.

Can you change the stacking order? Yes, you can, by using the [`z-index`](https://developer.mozilla.org/en-US/docs/Web/CSS/z-index) property. "z-index" is a reference to the z-axis. You may recall from previous points in the source where we discussed web pages using horizontal \(x-axis\) and vertical \(y-axis\) coordinates to work out positioning for things like background images and drop shadow offsets. \(0,0\) is at the top left of the page \(or element\), and the x- and y-axes run across to the right and down the page \(for left to right languages, anyway.\)

Web pages also have a z-axis — an imaginary line that runs from the surface of your screen, towards your face \(or whatever else you like to have in front of the screen\). [`z-index`](https://developer.mozilla.org/en-US/docs/Web/CSS/z-index) values affect where positioned elements sit on that axis — positive values move them higher up the stack, and negative values move them lower down the stack. By default, positioned elements all have a `z-index` of auto, which is effectively 0.

To change the stacking order, try adding the following declaration to your `p:nth-of-type(1)`rule:

```text
z-index: 1;
```

You should now see the finished example:

Note that `z-index` only accepts unitless index values; you can't specify that you want one element to be 23 pixels up the Z-axis — it doesn't work like that. Higher values will go above lower values, and it is up to you what values you use. Using 2 and 3 would give the same effect as 300 and 40000.

Also note that we have only really discussed a single positioning context here. If you had two separate sets of positioned elements in the same page, and wanted to make them overlap and have the stacking order work in some specific kind of way, then things would get complicated. Fortunately you will very rarely encounter such complexity with z-index. If you want to read a lot more detail about exactly how z-index works, check out the [Web Standards Curriculum z-index writeup](https://www.w3.org/community/webed/wiki/CSS_absolute_and_fixed_positioning#The_third_dimension.E2.80.94z-index). In this article we've provided you with all you need to know at this stage in your learning.

**Note**: You can see the example at this point live at `5_z-index.html` \([see source code](https://github.com/mdn/learning-area/blob/master/css/css-layout/positioning/5_z-index.html)\).

#### Fixed positioning

There is one more type of positioning to cover — fixed. This works in exactly the same way as absolute positioning, with one key difference — whereas absolute positioning fixes an element in place relative to the [`<html>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/html) element or its nearest positioned ancestor, fixed positioning fixes an element in place relative to the browser viewport itself. This means that you can create useful UI items that are fixed in place, like persisting navigation menus.

Let's put together a simple example to show what we mean. First of all, delete the existing `p:nth-of-type(1)` and `.positioned` rules from your CSS.

Now, update the `body` rule to remove the `position: relative;` declaration and add a fixed height, like so:

```text
body {
  width: 500px;
  height: 1400px;
  margin: 0 auto;
}
```

Now we're going to give the [`<h1>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/h1) element `position: fixed;`, and get it to sit at the top center of the viewport. Add the following rule to your CSS:

```text
h1 {
  position: fixed;
  top: 0px;
  width: 500px;
  margin: 0 auto;
  background: white;
  padding: 10px;
}
```

The `top: 0;` is required to make it stick to the top of the screen; we then give the heading the same width as the content column and use the faithful old `margin: 0 auto;` trick to center it. We then give it a white background and some padding, so the content won't be visible underneath it.

If you save and refresh now, you'll see a fun little effect whereby the heading stays fixed, and the content appears to scroll up and disappear underneath it. But we could improve this more — at the moment some of the content starts off underneath the heading, because the positioned heading no longer appears in the document flow, so the rest of the content moves up to the top. We need to move it all down a bit; we can do this by setting some top margin on the first paragraph. Add this now:

```text
p:nth-of-type(1) {
  margin-top: 60px;
}
```

You should now see the finished example:

\[INSERT \(LINK TO\) LIVE EXAMPLE HERE\]

**Note**: You can see the example at this point live at `6_fixed-positioning.html` \([see source code](https://github.com/mdn/learning-area/blob/master/css/css-layout/positioning/6_fixed-positioning.html)\).

#### Experimental: position sticky

There is a new positioning value available called `position: sticky`, support for which is not very widespread yet. This is basically a hybrid between relative and fixed position, which allows a positioned element to act like it is relatively positioned until it is scrolled to a certain threshold point \(e.g. 10px from the top of the viewport\), after which it becomes fixed. See our [position: sticky reference entry](https://developer.mozilla.org/en-US/docs/Web/CSS/position#Sticky_positioning) for more details and an example.

