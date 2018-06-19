# Ingredients for Responsive Web Design

### The parts needed for consistent design across multiple devices

#### Flexible Grids

In his book Grid Systems in Graphic Design, Müller-Brockmannreferred to this process as “creating a typographic space on thepage”.

**Common Grid Types960 Grid** is based on a width of 960 pixels & divisible by 12 & 16. -[http://960.gs](http://960.gs)/

**1200 Grid** is based on a width of 1200 pixels & divisible by 2, 3, 4,5, 6, 8, 10, 12, 15, 16, 20, 24, 30, 40, 48, 60, 80, 120, 150, 200, 240and 400. - [http://1200px.com](http://1200px.com)/

#### Pixels to Percentage

Grid systems aid us in creating consistent designs across multiple screens but through this layout system we are also able to define the proportional sizes we require to work with percentages

**Example: Using 960 grid our blog container has a width of 900px**

```text
.blog .main {
    float: left;
    width: 566px;
}
 
.blog .other {
    float: right;
    width: 331px;
}
​
(566 ÷ 900) * 100 = 62.8888889%
(331 ÷ 900) * 100 = 36.7777778%
​
.blog .main {
    float: left;
    width: 62.8888889%;
}
​
.blog .other {
    float: right;
    width: 36.7777778%;
}
```

#### Flexible Images

Within flexible layouts we need to have content, andimages are an important part of any website content.Luckily making sure your images remain in the correctproportions isn’t a very difficult task. We do need toconsider some points however:

● Image Aspect Ratio - 16:9, 5:4 etc

● Quality - Resolution & PPI

● Orientation - Landscape & Portrait

● File Size - Bytes, Kilobytes, Megabytes etc.

First discovered by designer Richard Rutter, there is onerule that provides a handy constraint for every image inour design, that will respect the **Aspect Ratio** and **Orientation**, however not necessarily the **Quality**.

So what is the this special rule?

```text
img {
    max-width: 100%;
}
```

This CSS rule will work for many instances, as it considersand respects **Aspect Ratio** and **Orientation**, however it doesn’t respect, **Quality** or **File Size**.

To ensure our sites look great and load fast we need todeal with image quality separately.

#### Optimizing Images

Our images are now flexible but quality isn’t good on all sizesand the website loads slowly.

To solve this we need to be more careful with images. Weneed to optimize their file sizes and resolutions for the best fitat different screen dimension. How do we do this?

● Create multiple images for each screen size - small,medium, large etc.

● Use Media Queries to load images for correct screensizes - small, medium, large, etc.

● New HTML `<img>` tag data attributes

● Consider using LazyLoading \(JavaScript\)

The first two options are fairly straightforward.

● Export the images to the appropriate sizes for differentdevice layouts.

​ ○ Mobile \(small\), Tablet \(medium\), Laptop \(large\), Desktop\(extra-large\) and 4K \(xx-large\)

● Apply our media queries to the correct screen sizes.

​ ○ We can hide `<img>` based on screen size

​ ○ Or we can load images as background-images in CSS and swap them based on screen sizes

**HTML Markup**

```text
 <div class=”hidden-sm hidden-md”>
       <img src=”img/large.jpeg”>
  </div>
```

**CSS Rules**

```text
@media screen and (max-width:1366px){
      .hidden-sm {
            display:none;
      }
      
      .hidden-md {
            display:none;         
      }
}
```

#### Images with the NEW HTML

While the previous examples are fairly good ways to do it theyaren’t the best. Seeing as working with images has beenproblematic over the years a new set of attributes for the `<img>` tag have been introduced by the W3C and will soon becompatible across all browsers.

We will tackle LazyLoading in the JS subject.

**HTML Markup**

```text
<img src="small.jpg”
     srcset="large.jpg 1024w, medium.jpg 640w, small.jpg 320w"
     sizes="(min-width:1024px) 33.3vw,100vw"
     alt="A properly sized image">   
```

**NB!! Not 100% compatible across all browsers use with caution!**

#### Flex-box

Flex-box is focused on providing an efficient way to lay out,align and distribute elements in a container. The key here isthat flex-box focuses on managing the space between items,not the items themselves.

This gives the container the ability to alter its elements’ widthor height as well as the order to best fit in the space provided.

Flex-box layout is also direction independent\(direction-agnostic\) if flows left/right and top /bottom asspace allows.

#### Flex-box Structure & Syntax

Flex-box requires the use of 2 sets of CSS properties - Parent &Child.

● The parent is the **flex container**.

● The child is the **flex items**.

**Parent Properties**

● Display

● Flex-direction

● Flex-wrap

● Flex-flow

● Justify-content

● Align-items

● Align-content

**Child Properties**

● Order

● Flex-grow

● Flex-shrink

● Flex-basis

● Flex

● Align-self

#### Flex-box Structure & Syntax

CSS For Parent

```text
.my-flexbox-parent {
    display: flex; /* or inline-flex */
    flex-direction: row | row-reverse | column | column-reverse;
    flex-wrap: nowrap | wrap | wrap-reverse;
    flex-flow: <‘flex-direction’> || <‘flex-wrap’> /*shorthand*/
    justify-content: flex-start | flex-end | center | space-between |
    space-around;    
    align-items: flex-start | flex-end | center | baseline | stretch;           align-content: flex-start | flex-end | center | space-between |
    space-around | stretch;
}
```

CSS For Child

```text
.my-flexbox-item {
    order: <integer>;
    flex-grow: <number>; /* default 0 */
    flex-shrink: <number>; /* default 1 */
    flex-basis: <length> | auto; /* default auto */
    flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ] /*
    shorthand */
    align-self: auto | flex-start | flex-end | center | baseline |
    stretch;}
```

**NB!! - Note that float, clear and vertical-align have no effect on a flex item.**

