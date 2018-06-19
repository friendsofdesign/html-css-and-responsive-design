# CSS Grid Layouts

### **What is grid layout?**

A grid is simply a collection of horizontal and vertical lines creating a pattern against which we can line up our design elements. They help us to create designs where elements don’t jump around or change width as we move from page to page, providing greater consistency on our websites.

A grid will typically have **columns**, **rows**, and then gaps between each row and column — commonly referred to as **gutters**.

![](https://mdn.mozillademos.org/files/13899/grid.png)

\[Temporary diagram; will be replaced by a better diagram soon.\]

**Note**: It may seem surprising to anyone coming from a design background that CSS doesn’t have an inbuilt grid system, and instead we seem to be using a variety of suboptimal methods to create grid-like designs. As you’ll discover in the last part of this article this is set to change, however you are likely to need to know the existing methods of creating grids for some time to come.

#### Using a “grid system” in your projects

In order to ensure a consistent experience across your site or application, basing it upon a grid system from the outset means you don’t need to think about how wide a certain element is in relation to the other elements. Your choice is limited to “how many columns of the grid this element will span”.

Your “grid system” could simply be a decision made in the design process to use a regular grid. If your designs start life in a graphics editing application like Photoshop you can create a grid to reference during that process as described in [A better Photoshop grid for responsive web design](http://www.elliotjaystocks.com/blog/a-better-photoshop-grid-for-responsive-web-design/) by Elliot Jay Stocks.

Your grid system may also be a framework — either third party or created by you just for your project — that you use to enforce the grid via CSS.

#### Creating simple grid frameworks

We will start by having a look at how you might create a simple grid framework for your project.

At the present time the majority of grid type layouts are created using floats. If you have read [our previous article about floats](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Floats), you’ve already seen how we can use this technique to create a multiple column layout — which is the essence of any grid system using this method.

The easiest type of grid framework to create is a fixed width one — we just need to work out how much total width we want our design to be, how many columns we want, and how wide the gutters and columns should be. If we instead decided to lay out our design on a grid with columns that grow and shrink according to browser width, we would need to calculate percentage widths for the columns and gutters between them.

In the next sections we will look at how to create both. We will create a 12 column grid — a very common choice that is seen to be very adaptable to different situations given that 12 is nicely divisible by 6, 4, 3, and 2.

#### A simple fixed width grid

Lets first create a grid system that uses fixed width columns.

Start out by making a local copy of our sample [simple-grid.html](https://github.com/mdn/learning-area/blob/master/css/css-layout/grids/simple-grid.html) file, which contains the following markup in its body.

```text
<div class="wrapper">
  <div class="row">
    <div class="col">1</div>
    <div class="col">2</div>
    <div class="col">3</div>
    <div class="col">4</div>
    <div class="col">5</div>
    <div class="col">6</div>
    <div class="col">7</div>
    <div class="col">8</div>
    <div class="col">9</div>
    <div class="col">10</div>
    <div class="col">11</div>
    <div class="col">12</div>
  </div>
  <div class="row">
    <div class="col span1">13</div>
    <div class="col span6">14</div>
    <div class="col span3">15</div>
    <div class="col span2">16</div>    
  </div>
</div>
```

The aim is to turn this into a demonstration grid of two rows on a twelve column grid — the top row demonstrating the size of the individual columns, the second row some different sized areas on the grid.

![](https://mdn.mozillademos.org/files/13901/simple-grid-finished.png)

In the [`<style>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/style) element, add the following code, which first makes all the elements on the page [sized as border boxes](https://developer.mozilla.org/en-US/docs/Learn/CSS/Styling_boxes/Box_model_recap#Changing_the_box_model_completely) and then gives the wrapper container a width of 980 pixels, with padding on the right hand side of 20 pixels. This leaves us with 960 pixels for our total column/gutter widths.

```text
* {
  box-sizing: border-box;
}
    
​
body {
  width: 980px;
  margin: 0 auto;
}
​
.wrapper {
  padding-right: 20px;
}
```

Now use the row container that is wrapped around each row of the grid to clear one row from another. Add the following rule below your previous one:

```text
.row {
  clear: both;
}
```

Applying this clearing means that we don’t need to completely fill each row with elements making the full twelve columns. The rows will remain separated, and not interfere with each other.

The gutters between the columns are 20 pixels wide. We create these gutters as a margin on the left side of each column — including the first column, to balance out the 20 pixels of padding on the right hand side of the container. So we have 12 gutters in total — 12 x 20 = 240.

We need to subtract that from our total width of 960 pixels, giving us 720 pixels for our columns. If we now divide that by 12, we know that each column should be 60 pixels wide.

Our next step is to create a rule for the class `.col`, floating it left, giving it a [`margin-left`](https://developer.mozilla.org/en-US/docs/Web/CSS/margin-left) of 20 pixels to form the gutter, and a [`width`](https://developer.mozilla.org/en-US/docs/Web/CSS/width) of 60 pixels. Add the following rule to the bottom of your CSS:

```text
.col {
  float: left;
  margin-left: 20px;
  width: 60px;
  background: rgb(255, 150, 150);
}
```

The top row of single columns will now lay out neatly as a grid.

**Note**: We've also given each column a light red color so you can see exactly how much space each one takes up.

Layout containers that we want to span more than one column need to be given special classes to adjust their [`width`](https://developer.mozilla.org/en-US/docs/Web/CSS/width) values to the required number of columns \(plus gutters in between\). We need to create an additional class to allow containers to span 2 to 12 columns. Each width is the result of adding up the column width of that number of columns plus the gutter widths, which will always number one less than the number of columns.

Add the following at the bottom of your CSS:

```text
/* Two column widths (120px) plus one gutter width (20px) */
.col.span2 { width: 140px; }
/* Three column widths (180px) plus two gutter widths (40px) */
.col.span3 { width: 220px; }
/* And so on... */
.col.span4 { width: 300px; }
.col.span5 { width: 380px; }
.col.span6 { width: 460px; }
.col.span7 { width: 540px; }
.col.span8 { width: 620px; }
.col.span9 { width: 700px; }
.col.span10 { width: 780px; }
.col.span11 { width: 860px; }
.col.span12 { width: 940px; }
```

With these classes created we can now lay out different width columns on the grid. Try saving and loading the page in your browser to see the effects.

**Note**: If you are having trouble getting the above example to work, try comparing it against our [finished version](https://github.com/mdn/learning-area/blob/master/css/css-layout/grids/simple-grid-finished.html) on GitHub \([see it running live](http://mdn.github.io/learning-area/css/css-layout/grids/simple-grid-finished.html) also\).

Try modifying the classes on your elements or even adding and removing some containers, to see how you can vary the layout. For example, you could make the second row look like this:

```text
<div class="row">
  <div class="col span8">13</div>
  <div class="col span4">14</div>
</div>
```

Now you've got a grid system working, you can simply define the rows and the number of columns in each row, then fill each container with your required content. Great!

#### Creating a fluid grid

Our grid works nicely, but it has a fixed width. We really want a flexible \(fluid\) grid that will grow and shrink with the available space in the browser [viewport](https://developer.mozilla.org/en-US/docs/Glossary/viewport). To achieve this we can use the reference pixel widths and turn them into percentages.

The equation that turns a fixed width into a flexible percentage-based one is as follows.

```text
target / context = result
```

For our column width, our **target width** is 60 pixels and our **context** is the 960 pixel wrapper. We can use the following to calculate a percentage.

```text
60 / 960 = 0.0625
```

We then move the decimal point 2 places giving us a percentage of 6.25%. So, in our CSS we can replace the 60 pixel column width with 6.25%.

We need to do the same with our gutter width:

```text
20 / 960 = 0.02083333333
```

So we need to replace the 20 pixel [`margin-left`](https://developer.mozilla.org/en-US/docs/Web/CSS/margin-left) on our `.col` rule and the 20 pixel [`padding-right`](https://developer.mozilla.org/en-US/docs/Web/CSS/padding-right) on `.wrapper` with 2.08333333%.

#### Updating our grid

To get started in this section, make a new copy of your previous example page, or make a local copy of our [simple-grid-finished.html](https://github.com/mdn/learning-area/blob/master/css/css-layout/grids/simple-grid-finished.html) code to use as a starting point.

Update the second CSS rule \(with the `.wrapper` selector\) as follows:

```text
body {
  width: 90%;
  max-width: 980px;
  margin: 0 auto;
}
​
.wrapper {
  padding-right: 2.08333333%;
}
```

Not only have we given it a percentage [`width`](https://developer.mozilla.org/en-US/docs/Web/CSS/width), we have also added a [`max-width`](https://developer.mozilla.org/en-US/docs/Web/CSS/max-width) property in order to stop the layout becoming too wide.

Next, update the fourth CSS rule \(with the `.col` selector\) like so:

```text
.col {
  float: left;
  margin-left: 2.08333333%;
  width: 6.25%;
  background: rgb(255, 150, 150);
}
```

Now comes the slightly more laborious part — we need to update all our `.col.span` rules to use percentages rather than pixel widths. This takes a bit of time with a calculator; to save you some effort, we've done it for you below.

Update the bottom block of CSS rules with the following:

```text
/* Two column widths (12.5%) plus one gutter width (2.08333333%) */
.col.span2 { width: 14.58333333%; }
/* Three column widths (18.75%) plus two gutter widths (4.1666666) */
.col.span3 { width: 22.91666666%; }
/* And so on... */
.col.span4 { width: 31.24999999%; }
.col.span5 { width: 39.58333332%; }
.col.span6 { width: 47.91666665%; }
.col.span7 { width: 56.24999998%; }
.col.span8 { width: 64.58333331%; }
.col.span9 { width: 72.91666664%; }
.col.span10 { width: 81.24999997%; }
.col.span11 { width: 89.5833333%; }
.col.span12 { width: 97.91666663%; }
```

Now save your code, load it in a browser, and try changing the viewport width — you should see the column widths adjust nicely to suit. Great!

**Note**: If you are having trouble getting the above example to work, try comparing it against our [finished version on GitHub](https://github.com/mdn/learning-area/blob/master/css/css-layout/grids/fluid-grid.html) \([see it running live](http://mdn.github.io/learning-area/css/css-layout/grids/fluid-grid.html) also\).

#### Easier calculations using the calc\(\) function

You could use the [`calc()`](https://developer.mozilla.org/en-US/docs/Web/CSS/calc%28%29) function to do the math right inside your CSS — this allows you to insert simple mathematical equations into your CSS values, to calculate what a value should be. It is especially useful when there is complex math to be done, and you can even compute a calculation that uses different units, for example "I want this element's height to always be 100% of its parent's height, minus 50px". See [this example from a MediaRecorder API tutorial](https://developer.mozilla.org/en-US/docs/Web/API/MediaRecorder_API/Using_the_MediaRecorder_API#Keeping_the_interface_constrained_to_the_viewport_regardless_of_device_height_with_calc%28%29).

Anyway, back to our grids! Any column that spans more than one column of our grid has a total width of 6.25% multiplied by the number of columns spanned plus 2.08333333% multiplied by the number of gutters \(which will always be the number of columns minus 1\). The `calc()`function allows us to do this calculation right inside the width value, so for any item spanning 4 columns we can do this, for example:

```text
.col.span4 {
  width: calc((6.25%*4) + (2.08333333%*3));
}
```

Try replacing your bottom block of rules with the following, then reload it in the browser to see if you get the same result:

```text
.col.span2 { width: calc((6.25%*2) + 2.08333333%); }
.col.span3 { width: calc((6.25%*3) + (2.08333333%*2)); }
.col.span4 { width: calc((6.25%*4) + (2.08333333%*3)); }
.col.span5 { width: calc((6.25%*5) + (2.08333333%*4)); }
.col.span6 { width: calc((6.25%*6) + (2.08333333%*5)); }
.col.span7 { width: calc((6.25%*7) + (2.08333333%*6)); }
.col.span8 { width: calc((6.25%*8) + (2.08333333%*7)); }
.col.span9 { width: calc((6.25%*9) + (2.08333333%*8)); }
.col.span10 { width: calc((6.25%*10) + (2.08333333%*9)); }
.col.span11 { width: calc((6.25%*11) + (2.08333333%*10)); }
.col.span12 { width: calc((6.25%*12) + (2.08333333%*11)); }
```

**Note**: You can see our finished version in [fluid-grid-calc.html](https://github.com/mdn/learning-area/blob/master/css/css-layout/grids/fluid-grid-calc.html) \(also [see it live](http://mdn.github.io/learning-area/css/css-layout/grids/fluid-grid-calc.html)\).

**Note**: If you can't get this to work, it might be because your browser does not support the `calc()`function, although it is fairly well supported across browsers — as far back as IE9.

#### Semantic versus “unsemantic” grid systems

Adding classes to your markup to define layout means that your content and markup becomes tied to its visual presentation. You will sometimes hear this use of CSS classes described as being “unsemantic” — describing how the content looks — rather than a semantic use of classes that describes the content. This is the case with our `span2`, `span3`, etc., classes.

These are not the only approach. You could instead decide on your grid and then add the sizing information to the rules for existing semantic classes. For example, if you had a [`<div>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/div) with a class of `content` on it that you wanted to span 8 columns, you could copy across the width from the `span8` class, giving you a rule like so:

```text
.content {
  width: calc((6.25%*8) + (2.08333333%*7));
}
```

**Note**: If you were to use a preprocessor such as [Sass](http://sass-lang.com/), you could create a simple mixin to insert that value for you.

#### Enabling offset containers in our grid

The grid we have created works well as long as we want to start all of the containers flush with the left hand side of the grid. If we wanted to leave an empty column space before the first container — or between containers — we would need to create an offset class to add a left margin to our site to push it across the grid visually. More math!

Let's try this out.

Start with your previous code, or use our [fluid-grid.html](https://github.com/mdn/learning-area/blob/master/css/css-layout/grids/fluid-grid.html) file as a starting point.

Let's create a class in our CSS that will offset a container element by one column width. Add the following to the bottom of your CSS:

```text
.offset-by-one {
  margin-left: calc(6.25% + (2.08333333%*2));
}
```

Or if you prefer to calculate the percentages yourself, use this one:

```text
.offset-by-one {
  margin-left: 10.41666666%;
}
```

You can now add this class to any container you want to leave a one column wide empty space on the left hand side of it. For example, if you have this in your HTML:

```text
<div class="col span6">14</div>
```

Try replacing it with

```text
<div class="col span5 offset-by-one">14</div>
```

**Note**: Notice that you need to reduce the number of columns spanned, to make room for the offset!

Try loading and refreshing to see the difference, or check out our [fluid-grid-offset.html](https://github.com/mdn/learning-area/blob/master/css/css-layout/grids/fluid-grid-offset.html) example \(see it [running live](http://mdn.github.io/learning-area/css/css-layout/grids/fluid-grid-offset.html) also\). The finished example should look like this:

![](https://mdn.mozillademos.org/files/13903/offset-grid-finished.png)

**Note**: As an extra exercise, can you implement an `offset-by-two` class?

#### Floated grid limitations

When using a system like this you do need to take care that your total widths add up correctly, and that you don’t include elements in a row that span more columns than the row can contain. Due to the way floats work, if the number of grid columns becomes too wide for the grid, the elements on the end will drop down to the next line, breaking the grid.

Also bear in mind that the content of the elements gets wider than the rows they occupy, it will overflow and look like a mess.

The biggest limitation of this system is that it is essentially one dimensional. We are dealing with columns, and spanning elements across columns, but not rows. It is very difficult with these older layout methods to control the height of elements without explicitly setting a height, and this is a very inflexible approach too — it only works if you can guarantee that your content will be a certain height.

#### Flexbox grids?

If you read our previous article about [flexbox](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Flexbox), you might think that flexbox is the ideal solution for creating a grid system. There are currently any number of flexbox-based grid systems available and flexbox can solve many of the issues that we’ve already discovered when creating our grid above.

However, flexbox was never designed as a grid system and poses a new set of challenges when used as one. As a simple example of this, we can take the same example markup we used above and use the following CSS to style the `wrapper`, `row`, and `col` classes:

```text
body {
  width: 90%;
  max-width: 980px;
  margin: 0 auto;
}
​
.wrapper {
  padding-right: 2.08333333%;
}
​
​
.row {
  display: flex;
}
​
.col {
  margin-left: 2.08333333%;
  margin-bottom: 1em;
  width: 6.25%;
  flex: 1 1 auto;
  background: rgb(255,150,150);
}
```

You can try making these replacements in your own example, or look at our [flexbox-grid.html](https://github.com/mdn/learning-area/blob/master/css/css-layout/grids/flexbox-grid.html) example code \(see it [running live](http://mdn.github.io/learning-area/css/css-layout/grids/flexbox-grid.html) also\).

Here we are turning each row into a flex container. With a flexbox-based grid we still need rows in order to allow us to have elements that add up to less than 100%. We set that container to `display: flex`.

On `.col` we set the [`flex`](https://developer.mozilla.org/en-US/docs/Web/CSS/flex) property's first value \([`flex-grow`](https://developer.mozilla.org/en-US/docs/Web/CSS/flex-grow)\) to 1 so our items can grow, the second value \([`flex-shrink`](https://developer.mozilla.org/en-US/docs/Web/CSS/flex-shrink)\) to 1 so the items can shrink, and the third value \([`flex-basis`](https://developer.mozilla.org/en-US/docs/Web/CSS/flex-basis)\) to `auto`. As our element has a [`width`](https://developer.mozilla.org/en-US/docs/Web/CSS/width) set, `auto` will use that width as the `flex-basis` value.

On the top line we get twelve neat boxes on the grid and they grow and shrink equally as we change the viewport width. On the next line, however, we only have four items and these also grow and shrink from that 60px basis. With only four of them they can grow a lot more than the items in the row above, the result being that they all occupy the same width on the second row.

![](https://mdn.mozillademos.org/files/13905/flexbox-grid-incomplete.png)

To fix this we still need to include our `span` classes to provide a width that will replace the value used by `flex-basis` for that element.

They also don’t respect the grid used by the items above because they don’t know anything about it.

Flexbox is **one-dimensional** by design. It deals with a single dimension, that of a row or a column. We can’t create a strict grid for columns and rows, meaning that if we are to use flexbox for our grid, we still need to calculate percentages as for the floated layout.

In your project you might still choose to use a flexbox ‘grid’ due to the additional alignment and space distribution capabilities flexbox provides over floats. You should, however, be aware that you are still using a tool for something other than what it was designed for. So you may feel like it is making you jump through additional hoops to get the end result you want.

#### Third party grid systems

Now that we understand the math behind our grid calculations, we are in a good place to look at some of the third party grid systems in common use. If you search for "CSS Grid framework" on the Web, you will find a huge list of options to choose from. Popular frameworks such as [Bootstrap](http://getbootstrap.com/) and [Foundation](http://foundation.zurb.com/) include a grid system. There are also standalone grid systems, either developed using CSS or using preprocessors.

Let's take a look at one of these standalone systems as it demonstrates common techniques for working with a grid framework. The grid we will be using is part of Skeleton, a simple CSS framework.

To get started visit the [Skeleton website](http://getskeleton.com/), and choose "Download" to download the ZIP file. Unzip this and copy the skeleton.css and normalize.css files into a new directory.

Make a copy of our [html-skeleton.html](https://github.com/mdn/learning-area/blob/master/css/css-layout/grids/html-skeleton.html) file and save it in the same directory as the skeleton and normalize CSS.

Include the skeleton and normalize CSS in the HTML page, by adding the following to its head:

```text
<link href="normalize.css" rel="stylesheet">
<link href="skeleton.css" rel="stylesheet">
```

Skeleton includes more than a grid system — it also contains CSS for typography and other page elements that you can use as a starting point. We’ll leave these at the defaults for now, however — it’s the grid we are really interested in here.

**Note**: Normalize is a really useful little CSS library written by Nicolas Gallagher, which automatically does some useful basic layout fixes and makes default element styling more consistent across browsers.

We will use similar HTML to our earlier example. Add the following into your HTML body:

```text
<div class="container">
  <div class="row">
    <div class="col">1</div>
    <div class="col">2</div>
    <div class="col">3</div>
    <div class="col">4</div>
    <div class="col">5</div>
    <div class="col">6</div>
    <div class="col">7</div>
    <div class="col">8</div>
    <div class="col">9</div>
    <div class="col">10</div>
    <div class="col">11</div>
    <div class="col">12</div>
  </div>
  <div class="row">
    <div class="col">13</div>
    <div class="col">14</div>
    <div class="col">15</div>
    <div class="col">16</div>   
  </div>
</div>
```

To start using Skeleton we need to give the wrapper [`<div>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/div) a class of `container` — this is already included in our HTML. This centers the content with a maximum width of 960 pixels. You can see how the boxes now never become wider than 960 pixels.

You can take a look in the skeleton.css file to see the CSS that is used when we apply this class. The `<div>` is centered using `auto` left and right margins, and a padding of 20 pixels is applied left and right. Skeleton also sets the [`box-sizing`](https://developer.mozilla.org/en-US/docs/Web/CSS/box-sizing) property to `border-box` like we did earlier, so the padding and borders of this element will be included in the total width.

```text
.container {
  position: relative;
  width: 100%;
  max-width: 960px;
  margin: 0 auto;
  padding: 0 20px;
  box-sizing: border-box;
}
```

Elements can only be part of the grid if they are inside a row, so as with our earlier example we need an additional `<div>` or other element with a class of `row` nested between the ```content``<div>``` and our actual content container `<div>`s. We've done this already as well.

Now let's lay out the container boxes. Skeleton is based on a 12 column grid. The top line boxes all need classes of `one column` to make them span one column.

Add these now, as shown in the following snippet:

```text
<div class="container">
  <div class="row">
    <div class="col one column">1</div>
    <div class="col one column">2</div>        
    <div class="col one column">3</div>
    /* and so on */
  </div>
</div>
```

Next, give the containers on the second row classes explaining the number of columns they should span, like so:

```text
<div class="row">
  <div class="col one column">13</div>
  <div class="col six columns">14</div>
  <div class="col three columns">15</div>
  <div class="col two columns">16</div>   
</div>
```

Try saving your HTML file and loading it in your browser to see the effect.

**Note**: If you are having trouble getting this example to work, try comparing it to our [html-skeleton-finished.html](https://github.com/mdn/learning-area/blob/master/css/css-layout/grids/html-skeleton-finished.html) file \(see it [running live](http://mdn.github.io/learning-area/css/css-layout/grids/html-skeleton-finished.html) also\).

If you look in the skeleton.css file you can see how this works. For example, Skeleton has the following defined to style elements with “three columns” classes added to them.

```text
.three.columns { width: 22%; }
```

All Skeleton \(or any other grid framework\) is doing is setting up predefined classes that you can use by adding them to your markup. It’s exactly the same as if you did the work of calculating these percentages yourself.

As you can see, we need to write very little CSS when using Skeleton. It deals with all of the floating for us when we add classes to our markup. It is this ability to hand responsibility for layout over to something else that makes using a framework for a grid system a compelling choice!

Skeleton is a simpler grid system than some of the frameworks you may come across. The grids in large frameworks such as Bootstrap and Foundation offer more functionality and additional breakpoints for various screen widths. However, they all work in a similar way — by adding specific classes to your markup you can control how the element is laid out using the predefined grid.

#### Native CSS Grids with Grid Layout

We said at the beginning of this article that CSS has not previously had a real system for creating grid layouts, but this is going to change. While we can’t use a native CSS grid system yet, in the coming year we should see browser support appear for the [CSS Grid Layout Module](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout).

Currently you can only use the technique we’ll be showing you in browsers that are implementing CSS Grid Layout “behind a flag” — meaning it is currently implemented, but in an experimental state that you need to switch on to use.

In Firefox, for example, you need to navigate to a URL of `about:config`, search for the `layout.css.grid.enabled` preference, and double click it to enable CSS Grids. You can find out how to use it in other browsers by visiting [Grid by Example](http://gridbyexample.com/browsers).

We looked at the Skeleton Grid framework above — like other third party grids and even hand-built grids, it requires that you add `<div>`s to form rows and then specify the number of columns the items in these rows will span.

With CSS Grid Layout you can specify your grid entirely in CSS, without needing to add these helper classes to the markup at all. Let’s take our simple example and see how we would create that same layout using CSS Grid Layout.

#### Building a native grid

First, get started by making a local copy of the [css-grid.html](https://github.com/mdn/learning-area/blob/master/css/css-layout/grids/css-grid.html) file. It contains the following markup:

```text
<div class="wrapper">
  <div class="col">1</div>
  <div class="col">2</div>
  <div class="col">3</div>
  <div class="col">4</div>
  <div class="col">5</div>
  <div class="col">6</div>
  <div class="col">7</div>
  <div class="col">8</div>
  <div class="col">9</div>
  <div class="col">10</div>
  <div class="col">11</div>
  <div class="col">12</div>
  <div class="col">13</div>
  <div class="col span6">14</div>
  <div class="col span3">15</div>
  <div class="col span2">16</div>       
</div>
```

This time we have a parent `<div>` with a class of `wrapper`, and then all of the child elements just appear directly inside the wrapper — no row elements. We have added a class to the items that should span more than one column.

Now add the following into the [`<style>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/style) element:

```text
.wrapper {
  width: 90%;
  max-width: 960px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  grid-gap: 20px;
}
​
.col {
  background: rgb(255,150,150);
}
```

Here we set the `.wrapper` rule so it is 90% of the body width, centered, and has a [`max-width`](https://developer.mozilla.org/en-US/docs/Web/CSS/max-width) of 960px.

Now for the CSS grid properties. We can declare a grid using the `grid` value of the [`display`](https://developer.mozilla.org/en-US/docs/Web/CSS/display)property, set up a gutter with the [`grid-gap`](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-gap) property and then create a grid of 12 columns of equal width using [`grid-template-columns`](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-template-columns), the new `repeat()` function, and a new unit defined for grid layout — the `fr` unit.

The `fr` unit is a fraction unit — it describes a fraction of the available space in the grid container. If all columns are `1fr`, they will each take up an equal amount of space. This removes the need to figure out percentages to create a flexible grid.

Having created a grid, the grid auto-placement rules will immediately lay out our boxes on this grid and we get a twelve column flexible grid layout.

![](https://mdn.mozillademos.org/files/13907/css-grid-incomplete.png)

To style the containers that span multiple column tracks on the grid we can use the [`grid-column`](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-column)property. To span 6 columns for example:

```text
.span6 {
  grid-column: auto / span 6;
}
```

To span 3:

```text
.span3 {
  grid-column: auto / span 3;
}
```

The value before the forward slash is the start line — in this case we are not explicitly setting that and allowing the browser to place the item on the next available line. We can then set it to span 6, 3 or however many lines we want.

Add the following at the bottom of your CSS:

```text
.span2 { grid-column: auto / span 2;}
.span3 { grid-column: auto / span 3;}
.span4 { grid-column: auto / span 4;}
.span5 { grid-column: auto / span 5;}
.span6 { grid-column: auto / span 6;}
.span7 { grid-column: auto / span 7;}
.span8 { grid-column: auto / span 8;}
.span9 { grid-column: auto / span 9;}
.span10 { grid-column: auto / span 10;}
.span11 { grid-column: auto / span 11;}
.span12 { grid-column: auto / span 12;}
```

Try saving and refreshing, and you'll see that the containers span multiple columns as appropriate. Cool!

CSS grids are **two-dimensional**, so as the layout grows and shrinks the elements remain lined up horizontally and vertically.

You can test this by replacing your last 4 col `<div>`s with the following:

```text
<div class="col">13some<br>content</div>
<div class="col span6">14this<br>is<br>more<br>content</div>
<div class="col span3">15this<br>is<br>less</div>
<div class="col span2">16</div>
```

Here we've deliberately added in some line break \([`<br>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/br)\) tags to force some of the columns to become taller than others. If you try saving and refreshing, you'll see that the columns adjust their height to be as tall as the tallest container, so everything stays neat and tidy.

The final layout looks like so:

![](https://mdn.mozillademos.org/files/13909/css-grid-finished.png)

**Note**: If you are having trouble getting this example to work, you can check your code against our [finished version](https://github.com/mdn/learning-area/blob/master/css/css-layout/grids/css-grid-finished.html) \(also see it [running live](http://mdn.github.io/learning-area/css/css-layout/grids/css-grid-finished.html)\).

#### Other nice CSS grid features

With CSS grids, we don’t need to push things along by way of margins to offset them. Trying making these changes in your CSS:

```text
.content {
  grid-column: 2 / 8;
}
```

```text
<div class="col span2 content">16</div>
```

Container 16 will now span columns 2 to 8, on the next available row where it can fit.

We can span rows just as easily as columns:

```text
.content {
  grid-column: 2 / 8;
  grid-row: 3 / 5;
}
```

Container 16 will now span rows 3 to 5, as well as columns 2 to 8.

csWe also don’t need to use a margin to fake gutters or calculate their widths explicitly — CSS grid has this functionality built right in with the `grid-gap` property.

We’re just touching the surface of what is possible with CSS Grid Layout, but the key thing to understand in the context of this article is that you don’t need to create a grid system with grid — it is one. You can write CSS that places an item directly onto a predefined grid. This is the first time it has been possible with CSS, and this will get a lot more use once browser support solidifies.

