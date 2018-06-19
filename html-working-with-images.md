# HTML Working With Images

### How do we put an image on a webpage?

In order to put a simple image on a webpage, we use the [`<img>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img) element. This is an empty element \(meaning that it has no text content or closing tag\) that requires a minimum of one attribute to be useful — `src` \(pronounced _sarc_, sometimes spoken as its full title, _source_\). The `src`attribute contains a path pointing to the image you want to embed in the page, which can be a relative or absolute URL, in the same way as [`<a>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a) element `href` attribute values.

**Note**: You should read [A quick primer on URLs and paths](https://developer.mozilla.org/en-US/Learn/HTML/Introduction_to_HTML/Creating_hyperlinks#A_quick_primer_on_URLs_and_paths) to refresh your memory on relative and absolute URLs before continuing.

So for example, if your image is called `dinosaur.jpg`, and it sat in the same directory as your HTML page, you could embed the image like so:

```text
 <img src="dinosaur.jpg">
```

If the image was in an `images` subdirectory, which was inside the same directory as the HTML page \(which Google recommends for [SEO](https://developer.mozilla.org/en-US/docs/Glossary/SEO)/indexing purposes\), then you'd embed it like this:

```text
 <img src="images/dinosaur.jpg">
```

And so on.

**Note**: Search engines also read image filenames and count them towards SEO. Therefore, give your image a descriptive filename; `dinosaur.jpg` is better than `img835.png`.

You could embed the image using its absolute URL, for example:

```text
 <img src="https://www.example.com/images/dinosaur.jpg">
```

But this is pointless, as it just makes the browser do more work, looking up the IP address from the DNS server all over again, etc. You'll almost always keep the images for your web site on the same server as your HTML.

**Warning:** Most images are copyrighted. Do **not** display an image on your webpage unless:1\) you own the image2\) you have received explicit, written permission from the image's owner, or3\) you have ample proof that the image is, in fact, in the public domain.Copyright violations are illegal and unethical. In addition, **never** point your `src` attribute at an image hosted on someone else's website that you don't have permission to link to. This is called "hotlinking". Again, stealing someone's bandwidth is illegal. It also slows down your page, leaving you with no control over whether the image is removed or replaced with something embarrassing.

Our above code would give us the following result:

![](https://mdn.mozillademos.org/files/12700/basic-image.png)

**Note**: Elements like [`<img>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img) and [`<video>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/video) are sometimes referred to as **replaced elements**. This is because the element's content ,and size, is defined by an external resource \(like an image or video file\), not by the contents of the element itself.

**Note**: You can find the finished example from this section [running on Github](https://mdn.github.io/learning-area/html/multimedia-and-embedding/images-in-html/index.html) \(see the [source code](https://github.com/mdn/learning-area/blob/master/html/multimedia-and-embedding/images-in-html/index.html) too.\)

#### Alternative text

The next attribute we'll look at is `alt`. Its value is supposed to be a textual description of the image, for use in situations where the image cannot be seen/displayed. For example, our above code could be modified like so:

```text
 <img src="images/dinosaur.jpg"     alt="The head and torso of a dinosaur skeleton;          it has a large head with long sharp teeth">
```

The easiest way to test your `alt` text is to purposely misspell your filename. If for example our image name was spelt `dinosooooor.jpg`, the browser wouldn't display the image, and display the alt text instead:

![](https://mdn.mozillademos.org/files/12702/alt-text.png)

So, why would you ever see or need alt text? It can come in handy for a number of reasons:

* The user is visually impaired, and using a [screen reader](https://en.wikipedia.org/wiki/Screen_reader) to read the web out to them. In fact, having alt text available to describe images is useful to most users.
* As described above, you might have spelt the file or path name wrong.
* The browser doesn't support the image type. Some people still use text-only browsers, such as [Lynx](https://en.wikipedia.org/wiki/Lynx_%28web_browser%29), which alternatively displays the alt text of images.
* You may want to provide text for search engines to utilize. For example, search engines can match alt text with search queries.
* Users have turned off images to reduce data transfer volume and distractions. This is especially common on mobile phones, and in countries where bandwidth is limited and expensive.

What exactly should you write inside your `alt` attribute? It depends on _why_ the image is there in the first place. In other words, what you lose if your image doesn't show up:

* **Decoration.** If the image is just decoration and isn't part of the content, add a blank `alt="". F`or example, a screen reader doesn't waste time reading out content that is no core need to the user. Decorative images don't really belong in your HTML. [CSS background images](https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Images_in_HTML#CSS_background_images) should be used for inserting decoration, but if it is unavoidable, `alt=""` is the best way to go.
* **Content.** If your image provides significant information, provide the same information in a _brief_ `alt` text. Or even better, in the main text which everybody can see. Don't write redundant `alt` text. How annoying would it be for a sighted user if all paragraphs were written twice in the main content? If the image is described adequately by the main text body, you can just use `alt=""`.
* **Link.** If you put an image inside [`<a>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a) tags, to turn an image into a link, you still must provide [accessible link text](https://developer.mozilla.org/en-US/Learn/HTML/Introduction_to_HTML/Creating_hyperlinks#Use_clear_link_wording). In such cases you may, either, write it inside the same `<a>`element, or inside the image's `alt` attribute. Whatever works best in your case.
* **Text.** You should not put your text into images. If your main heading needs a drop shadow, for example, [use CSS](https://developer.mozilla.org/en-US/docs/Web/CSS/text-shadow) for that rather than putting the text into an image. However, If you _really can't avoid doing this_, you should supply the text inside the `alt` attribute.

Essentially, the key is to deliver a usable experience, even when the images can't be seen. This ensures all users are not missing any of the content. Try turning off images in your browser and see how things look. You'll soon realise how unhelpful alt text is if the image cannot be seen, such as "logo" or "my favourite place".

**Note**: For more information, see our guide to [Text Alternatives](https://developer.mozilla.org/en-US/docs/Learn/Accessibility/HTML#Text_alternatives).

#### Width and height

You can use the `width` and `height` attributes, to specify the width and height of your image. You can find your image's width and height in a number of ways. For example on the Mac you can use Cmd + I to get the info display up for the image file. Returning to our example, we could do this:

```text
 <img src="images/dinosaur.jpg"     alt="The head and torso of a dinosaur skeleton;          it has a large head with long sharp teeth"     width="400"     height="341">
```

This doesn't result in much difference to the display, under normal circumstances. But if the image isn't being displayed, for example, the user has just navigated to the page, and the image hasn't yet loaded, you'll notice the browser is leaving a space for the image to appear in:

![](https://mdn.mozillademos.org/files/12706/alt-text-with-width-height.png)

This is a good thing to do, resulting in the page loading quicker and more smoothly.

However, you shouldn't alter the size of your images using HTML attributes. If you set the image size too big, you'll end up with images that look grainy,fuzzy, or too small, and wasting bandwidth downloading an image that is not fitting the user's needs. The image may also end up looking distorted, if you don't maintain the correct [aspect ratio](https://en.wikipedia.org/wiki/Aspect_ratio_%28image%29). You should use an image editor, to put your image at the correct size, before putting it on your webpage.

**Note**: If you do need to alter an image's size, you should use [CSS](https://developer.mozilla.org/en-US/docs/Learn/CSS) instead.

#### Image titles

As [with links](https://developer.mozilla.org/en-US/Learn/HTML/Introduction_to_HTML/Creating_hyperlinks#Adding_supporting_information_with_%3Ctitle%3E), you can also add `title` attributes to images, to provide further supporting information if needed. In our example, we could do this:

```text
 <img src="images/dinosaur.jpg"     alt="The head and torso of a dinosaur skeleton;          it has a large head with long sharp teeth"     width="400"     height="341"     title="A T-Rex on display in the Manchester University Museum">
```

This gives us a tooltip, just like link titles:

![](https://mdn.mozillademos.org/files/12708/image-with-title.png)

Image titles aren't essential to include. It is often better to include such supporting information in the main article text, rather than attached to the image. However, they are useful in some circumstances; for example, in an image gallery when you have no space for captions.

#### Annotating images with figures and figure captions

Speaking of captions, there are a number of ways that you could add a caption to go with your image. For example, there would be nothing to stop you doing this:

```text
 <div class="figure">  <img src="images/dinosaur.jpg"       alt="The head and torso of a dinosaur skeleton;            it has a large head with long sharp teeth"       width="400"       height="341">​  <p>A T-Rex on display in the Manchester University Museum.</p></div>
```

This is ok. It contains the content you need, and is nicely stylable using CSS. But there is a problem here: there is nothing that semantically links the image to its caption, which can cause problems for screen readers. For example, when you have 50 images and captions, which caption goes with which image?

A better solution, is to use the HTML5 [`<figure>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/figure) and [`<figcaption`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/figcaption) elements. These are created for exactly this purpose: to provide a semantic container for figures, and clearly linking the figure to the caption. Our above example, could be rewritten like this:

```text
 <figure>  <img src="images/dinosaur.jpg"       alt="The head and torso of a dinosaur skeleton;            it has a large head with long sharp teeth"       width="400"       height="341">​  <figcaption>A T-Rex on display in the Manchester University Museum.</figcaption></figure>
```

The [`<figcaption>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/figcaption) element tells browsers, and assistive technology, that the caption describes the other content of the [`<figure>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/figure) element.

**Note**: From an accessibility viewpoint, captions and `alt` text have distinct roles. Captions benefit even people who can see the image, whereas `alt` text provides the same functionality as an absent image. Therefore, captions and `alt` text shouldn't just say the same thing, because they both appear when the image is gone. Try turning images off in your browser and see how it looks.

A figure doesn't have to be an image. It is an independent unit of content that:

* Expresses your meaning in a compact, easy-to-grasp way.
* Could go in several places in the page's linear flow.
* Provides essential information supporting the main text.

A figure could be several images, a code snippet, audio, video, equations, a table, or something else.

#### CSS Background Images

You can also use CSS to embed images into webpages \(and JavaScript, but that's another story entirely\). The CSS [`background-image`](https://developer.mozilla.org/en-US/docs/Web/CSS/background-image) property, and the other `background-*` properties, are used to control background image placement. For example, to place a background image on every paragraph on a page, you could do this:

```text
 p {  background-image: url("images/dinosaur.jpg");}
```

The resulting embedded image, is arguably easier to position and control than HTML images. So why bother with HTML images? As hinted to above, CSS background images are for decoration only. If you just want to add something pretty to your page to enhance the visuals, this is fine. Though, such images have no semantic meaning at all. They can't have any text equivalents, are invisible to screen readers, etc. This is HTML images time to shine!

Summing up: if an image has meaning, in terms of your content, you should use an HTML image. If an image is purely decoration, you should use CSS background images.

