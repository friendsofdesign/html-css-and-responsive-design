# HTML Responsive Images



### Why responsive images?

So what problem are we trying to solve with responsive images? Let's examine a typical scenario. A typical website probably has a header image to make it look nice to visitors, plus maybe some content images below that. You probably want to make the header span the whole of the width of the header, and the content image fit somewhere inside the content column. Let's have a look at a simple example of this:

![](https://mdn.mozillademos.org/files/12940/picture-element-wide.png)

This works well on a wide screen device, such as a laptop or desktop \(you can [see the example live](http://mdn.github.io/learning-area/html/multimedia-and-embedding/responsive-images/not-responsive.html) and find the [source code](https://github.com/mdn/learning-area/blob/master/html/multimedia-and-embedding/responsive-images/not-responsive.html) on Github.\) We won't discuss the CSS much, except to say that:

* The body content has been set to a maximum width of 1200 pixels — in viewports above that width the body remains at 1200px and centers itself in the available space. In viewports below that width, the body will stay at 100% of the width of the viewport.
* The header image has been set so that its center always stays in the center of the header, no matter what width the heading is. So if the site is being viewed on a narrower screen, the important detail in the center of the image \(the people\) can still be seen, and the excess is lost off either side. It is 200px high.
* The content images have been set so that if the body element becomes smaller than the image, the images start to shrink down so that they always stays inside the body, rather than overflowing it.

This is ok, but the problem comes when you start to view the site on a narrow screen device — the header looks ok, but is starting to take up a lot of the screen height for a mobile device; the first content image on the other hand looks terrible — at this size you can barely see the people in it!

![](https://mdn.mozillademos.org/files/12936/non-responsive-narrow.png)

It would be much better to show a cropped version of the image that homes in on the important details of the shot when the site is viewed on a narrow screen, and maybe something in between the two for a medium width screen device like a tablet — this is commonly known as the **art direction problem**.

In addition, there is no need to embed such large images on the page if it is being viewed on a tiny mobile screen; this is called the **resolution switching problem** — a raster image is a set number of pixels wide and a set number of pixels tall; as we saw when we looked at [vector graphics](https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Adding_vector_graphics_to_the_Web), a raster image starts to look grainy and horrible if it is displayed larger than its original size \(whereas a vector graphic doesn't.\) And if it is shown significantly smaller than its original size, it is a waste of bandwidth — mobile users especially don't want to have to burn through their bandwidth by downloading a large image intended for desktop, when a small image would do for their device. An ideal situation would be to have multiple resolutions available and serve appropriate sizes depending on the different devices accessing the website.

To make things more complicated, some devices have high resolution screens that need larger images than you might expect them to need, to display nicely. This is essentially the same problem, but in a slightly different context.

You might think that vector images would solve these problems, and they do to a certain degree — they are both small in file size and scale well, and you should use them wherever possible. They aren't suitable for all image types however — while they are great for simple graphics, patterns, interface elements, etc., it starts to get very complex to create a vector-based image with the kind of detail that you'd find in say, a photo. Raster image formats such as JPEGs are more suited to the kind of images we see in the above example.

This kind of problem didn't exist when the web first existed, in the early to mid 90s — back then the only devices in existence to browse the Web were desktops and laptops, so browser engineers and spec writers didn't even think to implement solutions. _Responsive image technologies_ were implemented recently to solve the problems indicated above by letting you offer the browser several image files, either all showing the same thing but containing different numbers of pixels \(_resolution switching_\), or different images suitable for different space allocations \(_art direction_.\)

**Note**: The new features discussed in this article — `srcset`/`sizes`/[`<picture>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/picture) — are all supported in release versions of modern desktop and mobile browsers \(including Microsoft's Edge browser, although not Internet Explorer.\)

#### How do you create responsive images?

In this section, we'll look at the two problems illustrated above and show how to solve them using HTML's responsive image features. You should note that we will be focusing on the HTML [`<img>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img)s for this section, as seen in the content area of the example above — the image in the site header is only for decoration, and therefore implemented using CSS background images. [CSS arguably has better tools for responsive design](http://blog.cloudfour.com/responsive-images-101-part-8-css-images/) than HTML, and we'll talk about those in a future CSS module.

#### Resolution switching: Different sizes

So, what is the problem that we want to solve with resolution switching? We want to display identical image content, just larger or smaller depending on the device — this is the situation we have with the second content image in our example. The standard [`<img>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img) element traditionally only lets you point the browser to a single source file:

```text
<img src="elva-fairy-800w.jpg" alt="Elva dressed as a fairy">
```

We can however use two new attributes — `srcset` and `sizes` — to provide several additional source images along with hints to help the browser pick the right one. You can see an example of this in our [responsive.html](http://mdn.github.io/learning-area/html/multimedia-and-embedding/responsive-images/responsive.html) example on Github \(see also [the source code](https://github.com/mdn/learning-area/blob/master/html/multimedia-and-embedding/responsive-images/responsive.html)\):

```text
<img srcset="elva-fairy-320w.jpg 320w,
             elva-fairy-480w.jpg 480w,
             elva-fairy-800w.jpg 800w"
     sizes="(max-width: 320px) 280px,
            (max-width: 480px) 440px,
            800px"
     src="elva-fairy-800w.jpg" alt="Elva dressed as a fairy">
```

The `srcset` and `sizes` attributes look complicated, but they're not that bad to understand if you format them as shown above, with a different part of the attribute value on each line. Each value contains a comma-separated list. and each part of the lists are made up of three sub-parts. Let's run through the contents of each now:

**srcset** defines the set of images we will allow the browser to choose between, and what size each image is. Before each comma, we write:

1. An **image filename** \(`elva-fairy-480w.jpg`.\)
2. A space.
3. The image's **inherent width in pixels** \(`480w`\) — note that this uses the `w` unit, not `px` as you might expect. This is the image's real size, which can be found by inspecting the image file on your computer \(for example on a Mac you can select the image in Finder, and press Cmd + I to bring up the info screen.\)

**sizes** defines a set of media conditions \(e.g. screen widths\) and indicates what image size would be best to choose, when certain media conditions are true — these are the hints we talked about earlier. In this case, before each comma we write

1. a **media condition** \(`(max-width:480px)`\) — you'll learn more about these in the [CSS topic](https://developer.mozilla.org/en-US/docs/Learn/CSS), but for now let's just say that a media condition describes a possible state that the screen can be in. In this case, we are saying "when the viewport width is 480 pixels or less".
2. A space.
3. The **width of the slot** the image will fill when the media condition is true \(`440px`.\)

**Note**: For the slot width, you may provide an absolute length \(`px`, `em`\) or a relative length \(such as a percentage.\) You may have noticed that the last slot width has no media condition — this is the default that is chosen when none of the media conditions are true.\) The browser ignores everything after the first matching condition, so be careful how you order the media conditions.

So, with these attributes in place, the browser will:

1. Look at its device width.
2. Work out which media condition in the `sizes` list is the first one to be true.
3. Look at the slot size given to that media query.
4. Load the image referenced in the `srcset` list that most closely matches the chosen slot size.

And that's it! So at this point, if a supporting browser with a viewport width of 480px loads the page, the `(max-width: 480px)` media condition will be true, therefore the `440px` slot will be chosen, so the `elva-fairy-480w.jpg` will be loaded, as its inherent width \(`480w`\) is the closest to `440px`. The 800px picture is 128KB on disk whereas the 480px version is only 63KB — a saving of 65KB. Now imagine if this was a page that had many pictures on it. Using this technique could save mobile users a lot of bandwidth.

Older browsers that don't support these features will just ignore them, and go ahead and load the image referenced in the `src` attribute as normal.

**Note**: In the [`<head>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/head) of the document you'll find the line `<meta name="viewport" content="width=device-width">`: this forces mobile browsers to adopt their real viewport width for loading web pages \(some mobile browsers lie about their viewport width, and instead load pages at a larger viewport width then shrink the loaded page down, which is not very helpful for responsive images or design. We'll teach you more about this in a future module.\)

#### Useful developer tools

There are some useful [developer tools](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_are_browser_developer_tools) in browsers to help with working out the necessary slot widths, etc, that you need to use. When I was working them out, I first loaded up the non-responsive version of my example \(`not-responsive.html`\), then went into [Responsive Design View](https://developer.mozilla.org/en-US/docs/Tools/Responsive_Design_Mode) \(_Tools &gt; Web Developer &gt; Responsive Design View_\), which allows you to look at your web page layouts as if they were being viewed through a variety of different device screen sizes.

I set the viewport width to 320px then 480px; for each one I went into the [DOM Inspector](https://developer.mozilla.org/en-US/docs/Tools/Page_Inspector), clicked on the [`<img>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img) element we are interested in, then looked at its size in the Box Model view tab on the right hand side of the display. This should give you the inherent image widths you need.

![](https://mdn.mozillademos.org/files/12932/box-model-devtools.png)

Next, you can check whether the `srcset` is working by setting the viewport width to what you want \(set it to a narrow width, for example\), opening the Network Inspector \(_Tools &gt; Web Developer &gt; Network_\), then reloading the page. This should give you a list of the assets that were downloaded to make up the webpage, and here you can check which image file was chosen for download.

![](https://mdn.mozillademos.org/files/12934/network-devtools.png)

#### Resolution switching: Same size, different resolutions

If you're supporting multiple display resolutions, but everyone sees your image at the same real-world size on the screen, you can allow the browser to choose an appropriate resolution image by using `srcset` with x-descriptors and without `sizes` — a somewhat easier syntax! You can find an example of what this looks like in [srcset-resolutions.html](http://mdn.github.io/learning-area/html/multimedia-and-embedding/responsive-images/srcset-resolutions.html) \(see also [the source code](https://github.com/mdn/learning-area/blob/master/html/multimedia-and-embedding/responsive-images/srcset-resolutions.html)\):

```text
<img srcset="elva-fairy-320w.jpg,
             elva-fairy-480w.jpg 1.5x,
             elva-fairy-640w.jpg 2x"
     src="elva-fairy-640w.jpg" alt="Elva dressed as a fairy">
```

![](https://mdn.mozillademos.org/files/12942/resolution-example.png)

In this example, the following CSS is applied to the image so that it will have a width of 320 pixels on the screen \(also called CSS pixels\):

```text
img {
  width: 320px;
}
```

In this case, `sizes` is not needed — the browser simply works out what resolution the display is that it is being shown on, and serves the most appropriate image referenced in the `srcset`. So if the device accessing the page has a standard/low resolution display, with one device pixel representing each CSS pixel, the `elva-fairy-320w.jpg` image will be loaded \(the 1x is implied, so you don't need to include it.\) If the device has a high resolution of two device pixels per CSS pixel or more, the `elva-fairy-640w.jpg` image will be loaded. The 640px image is 93KB, whereas the 320px image is only 39KB.

#### Art direction

To recap, the **art direction problem** involves wanting to change the image displayed to suit different image display sizes. For example, if a large landscape shot with a person in the middle is shown on a website when viewed on a desktop browser, then shrunk down when the website is viewed on a mobile browser, it will look bad as the person will be really tiny and hard to see. It would probably be better to show a smaller, portrait image on mobile, which shows the person zoomed in. The [`<picture>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/picture) element allows us to implement just this kind of solution.

Returning to our original [not-responsive.html](http://mdn.github.io/learning-area/html/multimedia-and-embedding/responsive-images/not-responsive.html) example, we have an image that badly needs art direction:

```text
<img src="elva-800w.jpg" alt="Chris standing up holding his daughter Elva">
```

Let's fix this, with [`<picture>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/picture)! Like [`<video>`](https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Video_and_audio_content) and `<audio>`, The `<picture>` element is a wrapper containing several [`<source>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/source) elements that provide several different sources for the browser to choose between, followed by the all-important [`<img>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img) element. the code in [responsive.html](http://mdn.github.io/learning-area/html/multimedia-and-embedding/responsive-images/responsive.html) looks like so:

```text
<picture>
  <source media="(max-width: 799px)" srcset="elva-480w-close-portrait.jpg">
  <source media="(min-width: 800px)" srcset="elva-800w.jpg">
  <img src="elva-800w.jpg" alt="Chris standing up holding his daughter Elva">
</picture>
```

* The `<source>` elements include a `media` attribute that contains a media condition — as with the first `srcset` example, these conditions are tests that decide which image is shown — the first one that returns true will be displayed. In this case, If the viewport width is 799px wide or less, the first `<source>` element's image will be displayed. If the viewport width is 800px or more, it'll be the second one.
* The `srcset` attributes contain the path to the image to display. Note that just as we saw with `<img>` above, `<source>` can take a `srcset` attribute with multiple images referenced, and a `sizes` attribute too. So you could offer multiple images via a `<picture>` element, but then also offer multiple resolutions of each one too. Realistically, you probably won't want to do this kind of thing very often.
* In all cases, you must provide an `<img>` element, with `src` and `alt`, right before `</picture>`, otherwise no images will appear. This provides a default case that will apply when none of the media conditions return true \(you could actually remove the second `<source>` element in this example\), and a fallback for browsers that don't support the `<picture>` element.

This code allows us to display a suitable image on both wide screen and narrow screen displays, as shown below:

![](https://mdn.mozillademos.org/files/12940/picture-element-wide.png)![](https://mdn.mozillademos.org/files/12938/picture-element-narrow.png)

**Note**: You should use the `media` attribute only in art direction scenarios; when you do use `media`, don't also offer media conditions within the `sizes` attribute.

#### Why can't we just do this using CSS or JavaScript?

When the browser starts to load a page, it starts to download \(preload\) any images before the main parser has started to load and interpret the page's CSS and JavaScript. This is a useful technique, which on average has shaved 20% off page load times. However, it is not helpful for responsive images, hence the need to implement solutions like `srcset`. You couldn't for example load the [`<img>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img) element, then detect the viewport width with JavaScript and dynamically change the source image to a smaller one if desired. By then, the original image would already have been loaded, and you would load the small image as well, which is even worse in responsive image terms.

#### Use modern image formats boldly

There are several exciting new image formats \(such as WebP and JPEG-2000\) that can maintain a low file size and high quality at the same time. However, browser support is spotty.

`<picture>` lets us continue catering to older browsers. You can supply MIME types inside `type`attributes so the browser can immediately reject unsupported file types:

```text
<picture>
  <source type="image/svg+xml" srcset="pyramid.svg">
  <source type="image/webp" srcset="pyramid.webp"> 
  <img src="pyramid.png" alt="regular pyramid built from four equilateral triangles">
</picture>
```

* Do _not_ use the `media` attribute, unless you also need art direction.
* In a `<source>` element, you can only refer to images of the type declared in `type`.
* As before, you're welcome to use comma-separated lists with `srcset` and `sizes`, as needed.

