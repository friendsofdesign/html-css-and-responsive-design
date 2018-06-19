# Responsive Web Design

#### 1. What is Responsive Web Design?

The base definition for web design is explained as such “Responsive web design \(RWD\) is an approach to web design aimed at crafting sites to provide an optimal viewing and interaction experience—easy reading and navigation with a minimum of resizing, panning, and scrolling—across a wide range of devices \(from desktop computer monitors to mobile phones\).” \(Wikipedia, 2016\).This could be said for all design across all mediums. We design to accommodate the canvas or media the design is going to be displayed upon. The core of Responsive Web Design focuses more specifically on ensure the design we creating responds directly to the dimensions and limitation of different devices and media.

#### 2. The History of Responsive Web Design

Graceful Degradation & Progressive EnhancementThe idea of Graceful Degradation comes originally from the field of engineering, in the early days \(not so long ago\) of the internet , the basic theory was that a website would degrade certain functionality and content to be accessible across all browsers and devices. When mobile phones and devices first became able to connect to the internet, they weren’t very “smart”, most used WAP as the base connection for the internet and browsers didn’t support all of the HTML & CSS it does currently. Thus the thinking was to make the change from a feature rich platform like desktop to mobile, at very least be graceful - in other words, the design and layout would conform to the screen limitations \(be fluid or liquid\) and functionality would degrade to meet the limitations of the phone. Smaller or less images for slower connections, fonts and layout compressed to allow more text to be legible and readable.After about a decade, it became very apparent that Graceful Degradation was lacking in a number of areas and not the perfect solution for the dream that Tim Berners-Lee had for a universally accessible internet. The term Progressive Enhancement was coined by Steve Champeon and Nick Finck in 2003 at the SXSW conference. They outlined a blueprint idea for approaching web development \(Gustafson, 2008\).Progressive Enhancement does not differ wildly from Graceful Degradation, each method attempts to provide that a site is accessible on wide range of devices and technologies. Graceful Degradation provides the latest browsers and strongest hardware with the most advanced features and functionality. Ensure that the sites are merely passable and minimally accessible on older browsers and hardware.While Progressive Enhancement on the other hand focuses on content. This is a key difference. Websites only exist because of content, without content one would not need website to display it through. Content has always been the core of any Design, print or digital. Content drives the communication, functionality, and experience.Responsive Web design is a major part of Progressive Enhancement, Responsive Web Design focuses more on visual and functional interaction with websites. Ensuring content is presented in legible, readable and functional manner to the typical human user, on as many browsers, devices and hardware as possible.

#### 3. The Flexible Grid

**960 Grid**

960 Grid allows us to put all of our site's elements in a 960px wide container, and dividing it into 12, 16, or 24 equally sized columns. So why 960px? It is the width that is suited for the wide number of platforms on which we browse the web. It essentially allows for a 1024px wide monitor to show the site accurately and without horizontal scrolling, accounting for the width of the browser chrome, scrollbars, and a bit of padding for legibility.All numbers in the 960 Grid are whole numbers based on the golden ratio - there are no decimal points or spacing issues. By designing on a 960 Grid with 12 columns we are able to directly relate our design to a 12 column responsive grid in our CSS. Thus we can create startlingly accurate pixel based designs in photoshop or illustrator and accurately reproduce them on the web.

**1200 Grid**

The 1200 Grid, acts the same as the 960 Grid however with the increase in screen sizes and resolutions. We as designers have had to accommodate for this, it allows us to use larger portions of the screen and still effectively ensure our designs scale correctly in code.

#### 4. Media Queries

Media queries are the backbone of ensuring our sites become responsive. These “magic” CSS rules allow developers to easily overwrite sizes, layouts, and CSS rules based on conditions.

**The All Important Viewport Meta Tag**

Media queries may be the “magic” developers need to competently make websites responsive, but before this magic can take hold, the browsers need to be aware that media queries will be called or used. It is thus vital developers remember to include the following meta tag in the head of their website. This meta tag was originally introduced by Apple Safari Mobile team as way to control size and scale. Without it the media queries will not work or be recognised.

`<meta name="viewport" content="width=device-width, initial-scale=1.0">`

Official Safari Documentation - [https://developer.apple.com/library/safari/documentation/AppleApplications/Reference/SafariWebContent/UsingtheViewport/UsingtheViewport.html](https://developer.apple.com/library/safari/documentation/AppleApplications/Reference/SafariWebContent/UsingtheViewport/UsingtheViewport.html)

In the meta tag developers can define the NAME this informs the browser of which component it needs to adhere too. Then define the CONTENT, this informs the browser of the base scale and response the CSS media queries will be applied to. WIDTH=DEVICE-WIDTH informs the browser to act at the rendered width of the device on which the site is being used. INITIAL-SCALE=1.0 informs the browser that this device width as previously defined will be representative of a scale of 1:1 for the units of measure as defined in the CSS.In other words it informs the site that a font of 12pt will be equal to 12pt, thus when users look at the site on mobile phone the 12pt font will be accurate to how the phone renders that size font. This allow developers to make the correct adjustments to the content as the scale in accurate to the devices natural screen size, pixel density and resolution.

For more information about this topic see the following good recommended reads: [http://www.quirksmode.org/blog/archives/2010/04/a\_pixel\_is\_not.html](http://www.quirksmode.org/blog/archives/2010/04/a_pixel_is_not.html)&lt;[http://www.quirksmode.org/mobile/viewports2.html](http://www.quirksmode.org/mobile/viewports2.html)

**Basics of Media Queries**

As mentioned developers can use media queries to overwrite or change CSS rules based on a number conditions. This means if a mobile or desktop site meets a certain condition, the CSS will update according to rules applied to the condition.

**Basic Syntax**

@media not\|only mediatype and \(media feature\) {

Our CSS Rules;

}

**NB!! The “only” keyword can only be used before a media type. A media query consisting only of media features, or one with another media query modifier like not, will be treated as false by legacy user agents automatically.**

Above first the @Media call is defined, this informs the browser we will now be interacting with the Viewport as defined by the META tag defined in the HEAD of the document. Next the media type is defined, this can be all, screen, print, speech, as of June 2016 many have been deprecated and thus are not suggested to be used. Use only those mentioned above.

**NB!! It is expected that all of the media types will also be deprecated in time, as appropriate media features are defined which capture their important differences.**

Once the media type is defined the media feature can be defined, like max-width, max-height, color etc.

For a full list of media-features see &lt;[http://www.w3schools.com/cssref/css3\_pr\_mediaquery.asp](http://www.w3schools.com/cssref/css3_pr_mediaquery.asp)

\*\*Example 01:

Normal CSS rule applied to `<div>` with a class of “.col-6”.

```text
.col-6 {
    width:50%;
}
```

Media Query CSS rule applied to the same `<div>` when the screen size is between 0 and 320px wide.

```text
@media screen and (0px <= max-width <= 320px) {    
    .col-6 {    
            width:100%;     
    }
}
```

**Example 02:**

Normal CSS rule applied to `<h1>` with class of “.large-title”.

```text
h1.large-title {
    font-size: 120pt;   
}
```

Media Query CSS rule applied to the same `<h1>` when the screen is between 1366px and 1920px wide, using a different syntax structure.

```text
@media screen and (min-width=1366px) and (max-width=1920px) {
    h1.large-title {
        font-size:240pt;
    }
}
```

Using just this simple syntax structure to declare media specific rules developers can easily manipulate a sites content to become responsive.

#### 5. Flexible Images

Within flexible layouts websites require content, and images are an important part of any website content. Luckily making sure your images remain in the correct proportions has become a lot simpler due to a number of simple techniques. Developers and designers need to consider some points however:

* Image Aspect Ratio - 16:9, 5:4 etc
* Quality - Resolution & PPI
* Orientation - Landscape & PortraitFile
* Size - Bytes, Kilobytes, Megabytes etc.

First discovered by designer Richard Rutter, there is one rule that provides a handy constraint for every image in our design, that will respect the Aspect Ratio and Orientation, however not necessarily the Quality. Thus applying this rule isn’t necessarily a all-in-one solution.

```text
img {     
    max-width: 100%;
}
```

This CSS rule will work for many instances, as it considers and respects Aspect Ratio and Orientation. However to ensure websites look great and load fast developers need to deal with image quality as a separate issue altogether.

The images on the site may be flexible but quality isn’t good on all sizes and the website loads slowly. To solve this developers need to be more careful with images, thus they will need to optimize file sizes and resolutions for the best fit at different screen dimension. There are a number of ways this can be accomplished.

* Create multiple images for each screen size - small, medium, large etc.
* Use Media Queries to load images for correct screen sizes - small, medium, large, etc.
* New HTML `<img>` tag data attributes

The first two options are fairly straightforward.

* Export the images to the appropriate sizes for different device layouts.
  * Mobile \(small\), Tablet \(medium\), Laptop \(large\), Desktop \(extra-large\) and 4K \(xx-large\)
* Apply our media queries to the correct screen sizes.
  * We can hide `<img>` based on screen size
  * Or load images as background-images in CSS and swap them based on screen sizes

Seeing as working with images has been difficult over the years a new set of attributes for the `<img>` tag have been introduced by the W3C and will soon be compatible across all browsers. The new markup for these attributes are as follows:

```text
<img src="small.jpg”
​
srcset="large.jpg 1024w, medium.jpg 640w, small.jpg 320w" 
sizes="(min-width:1024px) 33.3vw, 100vw" 
alt="A properly sized image">
```

First the src or source is defined, then a source set is defined - srcset - this provides the instructions to show the correct version of the image at the correct screen size. This followed by defining the correct size for the images listed for each srcset.

It is vital that developers and designers take special care with images on sites and use the tools available to best load images on the site. Images are often the cause of the longest load times and thus can disrupt the user experience the most.

#### 6. Flex-box

Flex-box is focused on providing an efficient way to lay out, align and distribute elements in a container. The key here is that flex-box focuses on managing the space between items, not the items themselves. This gives the container the ability to alter its element’s width or height as well as the order to best fit in the space provided.

Flex-box layout is also direction independent \(direction-agnostic\) if flows left/right and top/bottom as space allows. Flex-box requires the use of 2 sets of CSS properties - Parent & Child. The parent is the flex container. The child is the flex items.

| Parent Properties | Child Properties |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Display | Order |
| Flex-direction | Flex-grow |
| Flex-wrap | Flex-shrink |
| Flex-flow | Flex-basis |
| Justify-content | Flex |
| Align-items | Align-self |
| Align-content |  |

**CSS For Parent**

```text
 .my-flexbox-parent {
     display: flex; /* or inline-flex */
     flex-direction: row | row-reverse | column | column-reverse;
     flex-wrap: nowrap | wrap | wrap-reverse;
     flex-flow: <‘flex-direction’> || <‘flex-wrap’> /*shorthand*/
     justify-content:flex-start|flex-end|center|space-between|space-around;
     align-items:flex-start|flex-end|center|baseline|stretch;
     align-content:flex-start|flex-end|center|space-between|space-around|stretch;
}
```

**CSS For Child**

```text
.my-flexbox-item {
    order: <integer>;
    flex-grow: <number>; /* default 0 */
    flex-shrink: <number>;/* default 1 */
    flex-basis: <length> | auto; /* default auto */
    flex:none|[<'flex-grow'><'flex-shrink'>||<'flex-basis'>] /* shorthand */
    align-self: auto | flex-start | flex-end | center | baseline | stretch;
}
```

**NB!! Note that float, clear and vertical-align have no effect on a flex item.**

**Example:**

```text
section.flex-container  {
    display: flex;
    flex-direction: 
    row;
    flex-wrap: wrap;
    justify-content: space-around;
}
​
article {
    width:16%;
    margin:1%;
    padding:1%;
}
​
article h1 {
    font-size:32pt;
}
​
article p {
    font-size:12pt;
}
```

#### 7. Responsive Frameworks

A framework is a standardized set of concepts, practices and criteria for dealing with a common type of problem, which can be used as a reference to help us approach and resolve new problems of a similar nature. \(awwwards-team, 2016\)

Basically it is a tool that is specifically developed to solve a series design problems encountered across similar projects. In web development we commonly use CSS or Responsive Frameworks to help solve the design problem of responsive web sites. Many frameworks have been developed to make designing responsive sites easier.

* Bootstrap - The most famous and most used framework worldwide
* Foundation 6 - Claims to be the most advanced front-end framework worldwide
* Pure.css - Claims to be the most lightweight and smallest framework worldwide

**Bootstrap**

To begin developers need to download the framework of their choice in this case, Bootstrap 3. At the time of writing, Bootstrap 4 is in Alpha testing and will be released soon, meaning it will up to developers to learn what changes have been made and what they need to do to implement the new version.Download the Bootstrap 3 files from [http://getbootstrap.com/getting-started/\#download](http://getbootstrap.com/getting-started/#download). Once the download is complete these files can be added to the website design project folder and developers can link the files and utilise the power of the Bootstrap framework.Bootstrap requires that developers link a minimum of 2 files to be able to use it in their project.

* bootstrap.min.css
* bootstrap.min.js

These minified files contain all the code from the framework necessary, developers can link the files as follows. Link the “bootstrap.min.css” file in the `<HEAD>` of the website like any other CSS file.

```text
<link rel=”stylesheet” type=”text/css” src=”bootstrap.min.css”>
```

Then link the JS file at the end of your website page before the closing `</BODY>` tag.

```text
<script src=”bootstrap.min.js”></script>
```

**How to Apply Bootstrap Classes**

Next the developer will need to become comfortable with bootstrap classes and the basics of applying them. Keep the reference link close by as referring to the reference documentation is core to any web development using a library or framework. Bootstrap like any framework has rules and guidelines for applying the correct classes to the elements to ensure the framework acts accordingly.

Reference files - [http://getbootstrap.com/css/](http://getbootstrap.com/css/)Bootstrap includes a responsive, mobile first fluid grid system that appropriately scales up to 12 columns as the device or viewport size increases \(Bootstrap, 2016\). Bootstrap has it’s own Grid System which will correlate with any 1200px or 960px grid based on a 12 column layout. This grid system is very flexible but has rules on how to use it.

Grid System Rules - [http://getbootstrap.com/css/\#grid](http://getbootstrap.com/css/#grid)Below are a series of columns in different variations, all using Bootstrap classes to arrange themselves. Using bootstrap is as simple as apply classes as developers would normally in any website design, however we need to use the specific bootstrap classes provided to us by the reference documentation.

```text
<div class="container">      
    <div class="row">        
        <div class="col-md-1">.col-md-1</div>         
        <div class="col-md-1">.col-md-1</div>         
        <div class="col-md-1">.col-md-1</div>         
        <div class="col-md-1">.col-md-1</div>         
        <div class="col-md-1">.col-md-1</div>         
        <div class="col-md-1">.col-md-1</div>         
        <div class="col-md-1">.col-md-1</div>        
        <div class="col-md-1">.col-md-1</div>         
        <div class="col-md-1">.col-md-1</div>         
        <div class="col-md-1">.col-md-1</div>         
        <div class="col-md-1">.col-md-1</div>         
        <div class="col-md-1">.col-md-1</div>       
    </div>       
    
    <div class="row">         
        <div class="col-md-8">.col-md-8</div>         
        <div class="col-md-4">.col-md-4</div>       
    </div>       
    
    <div class="row">         
        <div class="col-md-4">.col-md-4</div>         
        <div class="col-md-4">.col-md-4</div>         
        <div class="col-md-4">.col-md-4</div>       
    </div>       
    
    <div class="row">        
        <div class="col-md-6">.col-md-6</div>         
        <div class="col-md-6">.col-md-6</div>       
    </div>   
</div>
```

This is only the basic grid shown above, Bootstrap also allows for many controls and elements to be created with responsive elements.Further Reading - 22 Best Responsive CSS Frameworks [http://www.awwwards.com/what-are-frameworks-22-best-responsive-css-frameworks-for-web-design.html](http://www.awwwards.com/what-are-frameworks-22-best-responsive-css-frameworks-for-web-design.html)

