# CSS Floats

### The background of floats

Originally, the [`float`](https://developer.mozilla.org/en-US/docs/Web/CSS/float) property was introduced to allow web developers to implement simple layouts involving an image floating inside a column of text, with the text wrapping around the left or right of it. The kind of thing you might get in a newspaper layout.

But web developers quickly realised that you can float anything, not just images, so the use of float broadened. Our [fancy paragraph example](https://developer.mozilla.org/en-US/Learn/CSS/Introduction_to_CSS/Selectors#Active_learning_A_fancy_paragraph) from earlier in the course shows how you can use float in the creation of a fun drop-cap effect.

Floats are used very commonly these days to create entire web site layouts featuring multiple columns of information floated so they sit alongside one another \(the default behaviour would be for the columns to sit below one another, in the same order as they appear in the source\). There are newer, better layout techniques available, which we'll explore later in this module, but floats remain an old favourite, as they are supported as far back as Internet Explorer 4.

#### A simple float example

Let's explore how to use floats. We'll start with a really simple example involving floating a block of text around an image. You can follow along by creating a new `index.html` file on your computer, filling it with a [simple HTML template](https://github.com/mdn/learning-area/blob/master/html/introduction-to-html/getting-started/index.html), and inserting the below code into it at the appropriate places. At the bottom of the section you can see a live example of what the final code should look like.

First, we'll start off with some simple HTML — add the following to your HTML body, removing anything that was inside there before:

```text
<h1>Simple float example</h1>
​
<img src="butterfly.jpg" alt="A pretty butterfly with red, white, and brown coloring, sitting on a large leaf">
​
<p> Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla luctus aliquam dolor, eu lacinia lorem placerat vulputate. Duis felis orci, pulvinar id metus ut, rutrum luctus orci. Cras porttitor imperdiet nunc, at ultricies tellus laoreet sit amet. Sed auctor cursus massa at porta. Integer ligula ipsum, tristique sit amet orci vel, viverra egestas ligula. Curabitur vehicula tellus neque, ac ornare ex malesuada et. In vitae convallis lacus. Aliquam erat volutpat. Suspendisse ac imperdiet turpis. Aenean finibus sollicitudin eros pharetra congue. Duis ornare egestas augue ut luctus. Proin blandit quam nec lacus varius commodo et a urna. Ut id ornare felis, eget fermentum sapien.</p>
​
<p>Nam vulputate diam nec tempor bibendum. Donec luctus augue eget malesuada ultrices. Phasellus turpis est, posuere sit amet dapibus ut, facilisis sed est. Nam id risus quis ante semper consectetur eget aliquam lorem. Vivamus tristique elit dolor, sed pretium metus suscipit vel. Mauris ultricies lectus sed lobortis finibus. Vivamus eu urna eget velit cursus viverra quis vestibulum sem. Aliquam tincidunt eget purus in interdum. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus.</p>
```

Now apply the following CSS to your HTML \(using a [`<style>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/style) element or a [`<link>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/link) to a separate `.css` file — your choice\):

```text
body {
  width: 90%;
  max-width: 900px;
  margin: 0 auto;
}
​
p {
  line-height: 2;
  word-spacing: 0.1rem;
}
```

If you save and refresh now, you'll see something much like what you'd expect — the image is sitting above the text, which currently looks a bit ugly. We could center it in its container, but instead, we'll float the text around it using a float. Add the following rule below your previous rules:

```text
img {
  float: left;
  margin: 0 30px 0 0;
}
```

Now if you save and refresh you'll see something like the following:

So let's have a think about how the float works — the element with the float set on it \(the [`<img>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img)element in this case\) is taken out of the normal layout flow of the document and stuck to the left hand side of its parent container \([`<body>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/body), in this case\). Any content that comes below the floated element in the normal layout flow will now wrap around it, filling up the space to the right hand side of it as far up as the top of the floated element. There, it will stop.

Note that floated content still obeys normal box behaviour with things such as margin and borders. We put some right-hand margin on the image to stop the text to the right of it from sitting right next to it.

Floating the content to the right has exactly the same effect, but in reverse — the floated element will stick to the right, and the content will wrap around it to the left. Try changing the float value to `right` and replace `margin-right` with `margin-left` in the last ruleset and see what the result is.

#### Revisiting our drop cap example

As mentioned above, our [fancy paragraph example](https://developer.mozilla.org/en-US/Learn/CSS/Introduction_to_CSS/Selectors#Active_learning_A_fancy_paragraph) from earlier in the course featured a nice little drop cap. For this example we have a single simple paragraph:

```text
<p>This is my very important paragraph.
 I am a distinguished gentleman of such renown that my paragraph
 needs to be styled in a manner befitting my majesty. Bow before
my splendour, dear students, and go forth and learn CSS!</p>
```

Our CSS looks like this:

```text
p {
  width: 400px;
  margin: 0 auto;
}
​
p::first-line {
  text-transform: uppercase;
}
​
p::first-letter {
  font-size: 3em;
  border: 1px solid black;
  background: red;
  float: left;
  padding: 2px;
  margin-right: 4px;
}
```

And the live result is as follows:

The effect here is not very different to what we had in our first example with the image — this time however we are floating the rest of the paragraph around its first letter, after making the letter in question look big and bold and interesting.

You can pretty much float anything around anything else, as long as there is space for both items to fit alongside one another. This leads us nicely to talking about multiple-column layouts.

#### Multiple column floated layouts

Floats are commonly used to create multiple column layouts and have been for quite some time due to their widespread browser support. This is despite that fact that they were not really intended for this job, and have some strange side effects that have to be dealt with, as you'll see later on in the article.

#### A two column layout

Let's start with the simplest possible example — a two column layout. You can follow along by creating a new `index.html` file on your computer, filling it with a [simple HTML template](https://github.com/mdn/learning-area/blob/master/html/introduction-to-html/getting-started/index.html), and inserting the below code into it at the appropriate places. At the bottom of the section you can see a live example of what the final code should look like.

First of all, we need some content to put into our columns. Replace whatever is inside the body currently with the following:

```text
<h1>2 column layout example</h1>
<div>
  <h2>First column</h2>
  <p> Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla luctus aliquam dolor, eu lacinia lorem placerat vulputate. Duis felis orci, pulvinar id metus ut, rutrum luctus orci. Cras porttitor imperdiet nunc, at ultricies tellus laoreet sit amet. Sed auctor cursus massa at porta. Integer ligula ipsum, tristique sit amet orci vel, viverra egestas ligula. Curabitur vehicula tellus neque, ac ornare ex malesuada et. In vitae convallis lacus. Aliquam erat volutpat. Suspendisse ac imperdiet turpis. Aenean finibus sollicitudin eros pharetra congue. Duis ornare egestas augue ut luctus. Proin blandit quam nec lacus varius commodo et a urna. Ut id ornare felis, eget fermentum sapien.</p>
</div>
​
<div>
  <h2>Second column</h2>
  <p>Nam vulputate diam nec tempor bibendum. Donec luctus augue eget malesuada ultrices. Phasellus turpis est, posuere sit amet dapibus ut, facilisis sed est. Nam id risus quis ante semper consectetur eget aliquam lorem. Vivamus tristique elit dolor, sed pretium metus suscipit vel. Mauris ultricies lectus sed lobortis finibus. Vivamus eu urna eget velit cursus viverra quis vestibulum sem. Aliquam tincidunt eget purus in interdum. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus.</p>
</div>
```

Each one of the columns needs an outer element to contain its content and let us manipulate all of it at once. In this example case we've chosen [`<div>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/div)s, but you could choose something more semantically appropriate like [`<article>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/article)s, [`<section>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/section)s, and [`<aside>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/aside), or whatever.

Now for the CSS. First, of all, apply the following to your HTML to provide some basic setup:

```text
body {
  width: 90%;
  max-width: 900px;
  margin: 0 auto;
}
```

The body will be 90% of the viewport wide until it gets to 900px wide, in which case it will stay fixed at this width and center itself in the viewport. By default, it's children \(the [`<h1>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/h1) and the two [`<div>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/div)s\) will span 100% of the width of the body. If we want the two [`<div>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/div)s to be floated alongside one another, we need to set their widths to total 100% of the width of their parent element or smaller so they can fit alongside one another. Add the following to the bottom of your CSS:

```text
div:nth-of-type(1) {
  width: 48%;
}
​
div:nth-of-type(2) {
  width: 48%;
}
```

Here we've set both to be 48% of their parent's width — this totals 96%, leaving us 4% free to act as a gutter between the two columns, giving the content some space to breathe. Now we just need to float the columns, like so:

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

Putting this all together should give us a result like so:

You'll notice here that we are using percentages for all the widths — this is quite a good strategy, as it creates a **liquid layout**, one that adjusts to different screen sizes and keeps the same proportions for the column widths at smaller screen sizes. Try adjusting the width of your browser window to see for yourself. This is a valuable tool for responsive web design, which we'll look at later on in a future module.

**Note**: You can see this example running at [0\_two-column-layout.html](http://mdn.github.io/learning-area/css/css-layout/floats/0_two-column-layout.html) \(see also [the source code](https://github.com/mdn/learning-area/blob/master/css/css-layout/floats/0_two-column-layout.html)\).

One thing you do need to be aware of is that columns can start to look terrible when they become really narrow. It generally makes sense to switch back to a single column layout for narrow screens \(like mobile phones\), which can be achieved using media queries. Again, you'll learn about these in the future responsive web design module.

The other option would be to set the widths to a fixed unit like rems or pixels — you can see an example at `two-column-layout-fixed.html` \([see source code](https://github.com/mdn/learning-area/blob/master/css/css-layout/floats/two-column-layout-fixed.html)\), or convert your own example by removing the `max-width` declaration, and changing the widths to `900px`, `430px`, and `430px` respectively. This is called a **fixed-width layout** — if you adjust your browser size now, you will see that the layout no longer adjusts to suit the viewport width, and you'll need to scroll to see it all at smaller sizes.

We'll stick to liquid layouts for now.

#### A three column layout

One you've got a two column layout working, adding a third column \(or more\) is really not too hard. You just need to add in another column inside the same parent element as the others. Start by adding the following [`<div>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/div) just after the other two \(or use `0_two-column-layout.html` as a starting point\):

```text
<div>
  <h2>Third column</h2>
  <p>Nam consequat scelerisque mattis. Duis pulvinar dapibus magna, eget congue purus mollis sit amet. Sed euismod lacus sit amet ex tempus, a semper felis ultrices. Maecenas a efficitur metus. Nullam tempus pharetra pharetra. Morbi in leo mauris. Nullam gravida ligula eros, lacinia sagittis lorem fermentum ut. Praesent dapibus eros vel mi pretium, nec convallis nibh blandit. Sed scelerisque justo ac ligula mollis laoreet. In mattis, risus et porta scelerisque, augue neque hendrerit orci, sit amet imperdiet risus neque vitae lectus. In tempus lectus a quam posuere vestibulum. Duis quis finibus mi. Nullam commodo mi in enim maximus fermentum. Mauris finibus at lorem vel sollicitudin.</p>
</div>
```

Now update your CSS to the following:

```text
body {
  width: 90%;
  max-width: 900px;
  margin: 0 auto;
}
​
div:nth-of-type(1) {
  width: 36%;
  float: left;
}
​
div:nth-of-type(2) {
  width: 30%;
  float: left;
  margin-left: 4%;
}
​
div:nth-of-type(3) {
  width: 26%;
  float: right;
}
```

This will give us the following result:

There is very little here that we've not seen before; the only real difference is that we've got this extra column to contend with — to get this to sit in the right place we've floated it left; we've also given it a [`margin-left`](https://developer.mozilla.org/en-US/docs/Web/CSS/margin-left) of 4%, to create a gutter between the first and second columns. We've set the column widths so that they will all fit — 36% + 30% + 4% + 26% = 96%, which leaves a 4% remainder to form a gutter between the second and third columns \(this natural gutter will always appear at the point between the left-floated and right-floated columns, wherever that is.\)

One thing to note here is that you have to think carefully about what source order you place your columns in, and how you float them, to get the desired result. Your content should make sense anyway when read in its source order \(think of a visually impaired person using a screen reader to hear your content — how you layout your content makes no difference to them\), but you also need to consider that floated content earlier in the source order will appear earlier in the order of floated elements too — so further to the left in the case of left floats, and further to the right in the case of right floats. To illustrate what we mean, try changing the value of [`float`](https://developer.mozilla.org/en-US/docs/Web/CSS/float)for the second column to `right` \(or have a look at [three-column-layout-wrong-order.html](http://mdn.github.io/learning-area/css/css-layout/floats/three-column-layout-wrong-order.html) \([source code](https://github.com/mdn/learning-area/blob/master/css/css-layout/floats/three-column-layout-wrong-order.html)\)\). You'll see that the order now comes out like so:

```text
div1  div3  div2
```

This is because the second `<div>` is higher in the source order than the third `<div>`, so will appear higher up in the float order — because both are floated right, this means the second second `<div>` will appear further to the right than the third `<div>`.

**Note**: You can find the example finished up to this point in [1\_three-column-layout.html](http://mdn.github.io/learning-area/css/css-layout/floats/1_three-column-layout.html) \([see source code](https://github.com/mdn/learning-area/blob/master/css/css-layout/floats/1_three-column-layout.html)\).

#### Clearing floats

By now you've already started to see how fun floats can be. However, you soon start to run into a problem — any and all content below the floats that isn't floated itself will wrap around the floated elements, which can start to look terrible if it isn't dealt with. To illustrate what we mean, try adding the following HTML below your third [`<div>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/div) element \(and check out `2_float-disaster.html` \([source code](https://github.com/mdn/learning-area/blob/master/css/css-layout/floats/2_float-disaster.html)\)\):

```text
<footer>
  <p>&copy;2016 your imagination. This isn't really copyright, this is a mockery of the very concept. Use as you wish.</p>
</footer>
```

You'll see that the footer is wrapping around the space beside the longest column, which looks awful — we really want the footer to stay at the bottom, below all the columns. Well, fortunately there's an easy way to solve this problem — the [`clear`](https://developer.mozilla.org/en-US/docs/Web/CSS/clear) property. When you apply this to an element, it basically says "stop floating here" — this element and those after it in the source will not float, unless you apply a new [`float`](https://developer.mozilla.org/en-US/docs/Web/CSS/float) declaration to another element later on.

So, to fix our problem, add the following rule to your CSS:

```text
footer {
  clear: both;
}
```

This will give you a footer that behaves itself and sits underneath your columns, like it should do:

[`clear`](https://developer.mozilla.org/en-US/docs/Web/CSS/clear) can take three values:

* `left`: Stop any active left floats
* `right`: Stop any active right floats
* `both`: Stop any active left and right floats

You'll usually just want to set `clear: both` on the element where you want the floating to stop; in some cases you'll want to just cancel `left` or `right` quotes.

**Note**: You can find the example at this stage at `2a_fixed-by-clear.html` \([see source code](https://github.com/mdn/learning-area/blob/master/css/css-layout/floats/2a_fixed-by-clear.html)\).

#### Float problems

The above sections have provided a basis for creating simple layouts with floats, but there are a few problems that need to be addressed. Let's cover the main issues.

**The whole width can be tricky to calculate**

Our examples so far have shown us floating boxes that have no styling applied — this is easy. The troubles start to come when you want to start styling those boxes — adding in backgrounds, borders, padding, etc. To illustrate the problem, try adding the following into your CSS \(you can also see the example at `3_broken-layout.html` \([source code](https://github.com/mdn/learning-area/blob/master/css/css-layout/floats/3_broken-layout.html)\)\):

```text
div, footer {
  padding: 1%;
  border: 2px solid black;
  background-color: red;
}
```

At this point, you'll see that your layout has broken — because of the extra width introduced by the padding and the border, the three columns no longer fit on one line, so the third column drops below the other two. Ouch!

There are a couple of ways to fix this. The best way is to add the following to your CSS:

```text
* {
  box-sizing: border-box;
}
```

[`box-sizing`](https://developer.mozilla.org/en-US/docs/Web/CSS/box-sizing) comes to our rescue by making the box model change so the width of the box is taken as content + padding + border, not just content — so adding padding and border won't make the box any wider — it'll just make the content narrower to accomodate.

At this point we have another problem — the footer is pressed right up against the longest column, which isn't ideal — let's try fixing this by giving the footer some [`margin-top`](https://developer.mozilla.org/en-US/docs/Web/CSS/margin-top) to go along with its clearing:

```text
footer {
  clear: both;
  margin-top: 4%;
}
```

This however doesn't work — floated elements exist outside the normal document layout flow, and behave quite strangely in some ways:

* For a start, the area they inhabit inside their parent elements has an effective height of 0 — try loading up 1\_three-column-layout.html in your browser and checking the height of the [`<body>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/body) element using your [developer tools](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_are_browser_developer_tools), and you'll see what we mean — the body height is reported as the height of the [`<h1>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/h1) only. This can be fixed in a variety of ways, but the one we rely on is clearing the float at the bottom of the parent container, as we have done in our current example. If you check the height of the body in your current example, you should see that its height is behaving itself.
* Secondly, you can't use margins on non-floated elements to create space between them and floated elements — this is the immediate problem we have here, and we'll implement a fix below.
* There are some other weird things about floats — Chris Coyier's excellent [All About Floats](https://css-tricks.com/all-about-floats/) article outlines some others, plus fixes.

So, let's fix this! First, add the following new [`<div>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/div) into your HTML, just above the footer:

```text
<div class="clearfix"></div>
```

Adding an invisible "clearfix div" after floats you want to clear is very useful if you haven't got an element available to clear your floats with \(like our footer\), but is also useful here. The next thing we'd like to do is move the `clear: both;` declaration off the rule that is styling our footer, and put it on the clearfix div instead:

```text
.clearfix {
  clear: both;
}
```

We have a nice top margin on our footer now, but we also have another problem — the cleardiv div is being given the same background, padding and border as our columns and the footer! To fix this, let's first give each of our column divs a `class` of `column`:

```text
<div class="column">
  ...
</div>
```

Now let's change our rule that applies the box styling to the divs and footer so that only the column divs are styled:

```text
.column, footer {
  padding: 1%;
  border: 2px solid black;
  background-color: red;
}
```

That just about fixes it for now.

**Note**: The final fixed example at this stage can be seen in [4\_fixed-layout-border-box.html](http://mdn.github.io/learning-area/css/css-layout/floats/4_fixed-layout-border-box.html) \([source code](https://github.com/mdn/learning-area/blob/master/css/css-layout/floats/4_fixed-layout-border-box.html)\).

Another small point to note here is that [`box-sizing`](https://developer.mozilla.org/en-US/docs/Web/CSS/box-sizing) works as far back as Internet Explorer 8 — if you explicitly need to support older browsers, you may need to adjust the column widths manually to allow for the padding and border widths. This is not a very exact technique, especially considering that you can't size borders using percentages — you just need to allow enough space while filling the parent width as much as possible. You can see such a fix in action in `fixed-layout-adjusted-percentages.html` \([see source code](https://github.com/mdn/learning-area/blob/master/css/css-layout/floats/fixed-layout-adjusted-percentages.html)\).

**Background height of floated items**

So, the example we have built up so far works, but another problem is that the column heights are different — it would look a lot better if the columns were all the same height.

We can fix this by giving all the columns a fixed [`height`](https://developer.mozilla.org/en-US/docs/Web/CSS/height) \(see `5_fixed-height-columns.html` \([source code](https://github.com/mdn/learning-area/blob/master/css/css-layout/floats/5_fixed-height-columns.html)\)\):

```text
.column {
  height: 550px;
}
```

This is not ideal in many situations however — it makes the design inflexible. It is ok if you can guarantee that the columns will always have the same amount of content in them, but this is not always the case — content changes regularly on many types of sites.

This is exactly the kind of problem new layout technologies like flexbox were designed to solve. Flexbox can automatically stretch columns so that they will be as long as the longest column.

You could also consider:

1. Setting the background color of the columns to the same as the background color of their parent, so you can't see that the heights are different. This is the best other option at the moment.
2. Setting them to a fixed height and make the content scroll using [`overflow`](https://developer.mozilla.org/en-US/docs/Web/CSS/overflow) \(see our section on overflow for an example.\)
3. Using a technique called faux columns — this involves taking the background \(and borders\) off the actual columns, and drawing a fake background on the column's parent element that looks like the column backgrounds. Unfortunately, this wouldn't be able to handle the column borders. See [Faux Columns](http://alistapart.com/article/fauxcolumns) and [Faux Columns for Liquid Layouts](https://www.addedbytes.com/blog/code/faux-columns-for-liquid-layouts/) for some useful tutorials on this.

**Clearing floats can get complex**

The clearing in the simple example we've built up over the course of the article is easy to understand, but clearing can become a lot more complex as the layout becomes more complex. You need to make sure that any floats are cleared as soon as possible to avoid them making trouble for the content lower down. Use clearfix divs where necessary, if you haven't got a convenient container to put the clearing on.

