# HTML Head

### What is HTML head?

Let's revisit the simple HTML document we covered in the previous chapter:

```text
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>My test page</title>
  </head>
  <body>
    <p>This is my page</p>
  </body>
</html>
```

The HTML head is the contents of the [`<head>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/head) element — unlike the contents of the [`<body>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/body)element \(which are displayed on the page when loaded in a browser\), the head's content is not displayed on the page. Instead, the head's job is to contain [metadata](https://developer.mozilla.org/en-US/docs/Glossary/Metadata) about the document. In the above example, the head is quite small:

```text
<head>
  <meta charset="utf-8">
  <title>My test page</title>
</head>
```

In larger pages however, the head can get quite full of items — try going to some of your favourite web sites and using the [developer tools](https://developer.mozilla.org/en-US/docs/Learn/Discover_browser_developer_tools) to check out their head contents. Our aim here is not to show you how to use everything that can possibly be put in the head, but rather to teach you how to use the most obvious things you'll want to include in the head, and give you some familiarity. Let's get started.

#### Adding a title

We've already seen the [`<title>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/title) element in action — this can be used to add a title to the document. This however can get confused with the [`<h1>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/h1) element, which is used to add a top level heading to your body content — this is also sometimes referred to as the page title. But they are different things!

* The [`<h1>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/h1) element appears on the page when loaded in the browser — generally this should be used once per page, to mark up the title of your page content \(the story title, or news headline, or whatever is appropriate to your usage.\)
* The [`<title>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/title) element is metadata that represents the title of the overall HTML document \(not the document's content.\)

#### Active learning: Inspecting a simple example

1. To start off this active learning, we'd like you to go to our Github repo and download a copy of our title-example.html page. To do this, either
   1. Copy and paste the code out of the page and into a new text file in your code editor, then save it in a sensible place.
   2. Press the "Raw" button on the page, choose _File &gt; Save Page As..._ in your browser's menu, then choose a place to save the file.
2. Now open the file in your browser. You should see something like this:

   ![](https://mdn.mozillademos.org/files/12323/title-example.png)

3. It should now be completely obvious where the `<h1>` content appears, and where the `<title>` content appears!
4. You should also try opening the code up in your code editor, editing the contents of these elements, then refreshing the page in your browser. Have some fun with it.

The `<title>` element contents are also used in other ways. For example, if you try bookmarking the page \(_Bookmarks &gt; Bookmark This Page_, in Firefox\), you will see the `<title>` contents filled in as the suggested bookmark name.

![](https://mdn.mozillademos.org/files/12337/bookmark-example.png)

The `<title>` contents are also used in search results, as you'll see below.

#### Metadata: the `<meta>` element

Metadata is data that describes data, and HTML has an "official" way of adding metadata to a document — the [`<meta>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/meta) element. Of course, the other stuff we are talking about in this article could also be thought of as metadata too. There are a lot of different types of `<meta>` element that can be included in your page's `<head>`, but we won't try to explain them all at this stage, as it would just get too confusing. Instead, we'll explain a few things that you might commonly see, just to give you an idea.

#### Specifying your document's character encoding

In the example we saw above, this line was included:

```text
<meta charset="utf-8">
```

This element simply specifies the document's character encoding — the character set that the document is permitted to use. `utf-8` is a universal character set that includes pretty much any character from any human language. This means that your web page will be able to handle displaying any language; it's therefore a good idea to set this on every web page you create! For example, your page could handle English and Japanese just fine:

![](https://mdn.mozillademos.org/files/12343/correct-encoding.png)

If you set your character encoding to `ISO-8859-1`, for example \(the character set for the Latin alphabet\), your page rendering would be all messed up:

![](https://mdn.mozillademos.org/files/12341/bad-encoding.png)

#### Active learning: Experiment with character encoding

To try this out, revisit the simple HTML template you obtained in the previous section on `<title>` \(the [title-example.html page](https://github.com/mdn/learning-area/blob/master/html/introduction-to-html/the-html-head/title-example.html)\), try changing the meta charset value to `ISO-8859-1`, and add the Japanese to your page. This is the code we used:

```text
<p>Japanese example: ご飯が熱い。</p>
```

#### Adding an author and description

Many `<meta>` elements include `name` and `content` attributes:

* `name` specifies the type of meta element it is; what type of information it contains.
* `content` specifies the actual meta content.

Two such meta elements that are useful to include on your page define the author of the page, and provide a concise description of the page. Let's look at an example:

```text
<meta name="author" content="Chris Mills">
<meta name="description" content="The MDN Learning Area aims to provide
complete beginners to the Web with all they need to know to get
started with developing web sites and applications.">
```

Specifying an author is useful in a few ways: it is useful to be able to work out who wrote the page, if you want to contact them with questions about the content. Some content management systems have facilities to automatically extract page author information and make it available for such purposes.

Specifying a description that includes keywords relating to the content of your page is useful as it has the potential to make your page appear higher in relevant searches performed in search engines \(such activities are termed [Search Engine Optimization](https://developer.mozilla.org/en-US/docs/Glossary/SEO), or [SEO](https://developer.mozilla.org/en-US/docs/Glossary/SEO).\)

#### Active learning: The description's use in search engines

The description is also used on search engine result pages. Let's go through an exercise to explore this

1. Go to the [front page of The Mozilla Developer Network](https://developer.mozilla.org/en-US/).
2. View the page's source \(Right/Ctrl + click on the page, choose _View Page Source_ from the context menu.\)
3. Find the description meta tag. It will look like this:

   ```text
   <meta name="description" content="The Mozilla Developer Network (MDN) provides
   information about Open Web technologies including HTML, CSS, and APIs for both
   Web sites and HTML5 Apps. It also documents Mozilla products, like Firefox OS.">
   ```

4. Now search for "Mozilla Developer Network" in your favourite search engine \(We used Yahoo.\) You'll notice the description `<meta>` and `<title>` element content used in the search result — definitely worth having!

   ![](https://mdn.mozillademos.org/files/12347/search-result.png)

**Note**: In Google, you will see some relevant subpages of MDN listed below the main MDN homepage link — these are called sitelinks, and are configurable in [Google's webmaster tools](http://www.google.com/webmasters/tools/) — a way to make your site's search results better in the Google search engine.

**Note**: Many `<meta>` features just aren't used any more. For example, the keyword `<meta>` element — which is supposed to provide keywords for search engines to determine relevance of that page for different search terms — is ignored by search engines, because spammers were just filling the keyword list with hundreds of keywords, biasing results.

#### Other types of metadata

As you trawl around the Web, you'll find other types of metadata, too. A lot of the features you'll see on websites are proprietary creations, designed to provide certain sites \(such as social networking sites\) with specific pieces of information they can use.

For example, [Open Graph Data](http://ogp.me/) is a metadata protocol that Facebook invented to provide richer metadata for websites. In the MDN sourcecode, you'll find this:

```text
<meta property="og:image" content="https://developer.cdn.mozilla.net/static/img/opengraph-logo.dc4e08e2f6af.png">
<meta property="og:description" content="The Mozilla Developer Network (MDN) provides
information about Open Web technologies including HTML, CSS, and APIs for both Web sites
and HTML5 Apps. It also documents Mozilla products, like Firefox OS.">
<meta property="og:title" content="Mozilla Developer Network">
```

One effect of this is that when you link to MDN on facebook, the link appears along with an image and description: a richer experience for users.

![](https://mdn.mozillademos.org/files/12349/facebook-output.png)

Twitter also has its own similar proprietary metadata, which has a similar effect when the site's URL is displayed on twitter.com. For example:

```text
<meta name="twitter:title" content="Mozilla Developer Network">
```

#### Adding custom icons to your site

To further enrich your site design, you can add references to custom icons in your metadata, and these will be displayed in certain contexts.

The humble favicon, which has been around for many, many years, was the first icon of this type, a 16 x 16 pixel icon used in multiple places. The favicon can be added to your page by:

1. Saving it in the same directory as the site's index page, saved in `.ico` format \(most browsers will support favicons in more common formats like `.gif` or `.png`, but using the ICO format will ensure it works as far back as Internet Explorer 6.\)
2. Adding the following line into your HTML `<head>` to reference it:

   ```text
   <link rel="shortcut icon" href="favicon.ico" type="image/x-icon">
   ```

Modern browsers use favicons in various places, such as in the tab the page is open in, and in the bookmarks panel when you bookmark the page:

![](https://mdn.mozillademos.org/files/12351/bookmark-favicon.png)

There are lots of other icon types to consider these days as well. For example, you'll find this in the source code of the MDN homepage:

```text
<!-- third-generation iPad with high-resolution Retina display: -->
<link rel="apple-touch-icon-precomposed" sizes="144x144" href="https://developer.cdn.mozilla.net/static/img/favicon144.a6e4162070f4.png">
<!-- iPhone with high-resolution Retina display: -->
<link rel="apple-touch-icon-precomposed" sizes="114x114" href="https://developer.cdn.mozilla.net/static/img/favicon114.0e9fabd44f85.png">
<!-- first- and second-generation iPad: -->
<link rel="apple-touch-icon-precomposed" sizes="72x72" href="https://developer.cdn.mozilla.net/static/img/favicon72.8ff9d87c82a0.png">
<!-- non-Retina iPhone, iPod Touch, and Android 2.1+ devices: -->
<link rel="apple-touch-icon-precomposed" href="https://developer.cdn.mozilla.net/static/img/favicon57.a2490b9a2d76.png">
<!-- basic favicon -->
<link rel="shortcut icon" href="https://developer.cdn.mozilla.net/static/img/favicon32.e02854fdcf73.png">
```

The comments explain what each icon is used for — these elements cover things like providing a nice high resolution icon to use when the website is saved to an iPad's home screen.

Don't worry too much about implementing all these types of icon right now — this is a fairly advanced feature, and you won't be expected to have knowledge of this to progress through the course. The main purpose here is to let you know what such things are, in case you come across them while browsing other web sites' source code.

#### Applying CSS and JavaScript to HTML

Just about all websites you'll use in the modern day will employ [CSS](https://developer.mozilla.org/en-US/docs/Glossary/CSS) to make them look cool, and [JavaScript](https://developer.mozilla.org/en-US/docs/Glossary/JavaScript) to power interactive functionality, such as video players, maps, games, and more. These are most commonly applied to a web page using the [`<link>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/link) element and the [`<script>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/script)element, respectively.

* The [`<link>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/link) element always goes inside the head of your document. This takes two attributes, rel="stylesheet", which indicates that it is the document's stylesheet, and href, which contains the path to the stylesheet file:

  ```text
  <link rel="stylesheet" href="my-css-file.css">
  ```

* The [`<script>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/script) element does not have to go in the head; in fact, often it is better to put it at the bottom of the document body \(just before the closing `</body>` tag\), to make sure that all the HTML content has been read by the browser before it tries to apply JavaScript to it \(if JavaScript tries to access an element that doesn't yet exist, the browser will throw an error.\)

  ```text
  <script src="my-js-file.js"></script>
  ```

  **Note**: The `<script>` element may look like an empty element, but it's not, and so needs a closing tag. Instead of pointing to an external script file, you can also choose to put your script inside the `<script>` element.

#### Active learning: applying CSS and JavaScript to a page

1. To start this active learning, grab a copy of our [meta-example.html](https://github.com/mdn/learning-area/blob/master/html/introduction-to-html/the-html-head/meta-example.html), [script.js](https://github.com/mdn/learning-area/blob/master/html/introduction-to-html/the-html-head/script.js) and [style.css](https://github.com/mdn/learning-area/blob/master/html/introduction-to-html/the-html-head/style.css) files, and save them on your local computer in the same directory. Make sure they are saved with the correct names and file extensions.
2. Open the HTML file in both your browser, and your text editor.
3. By following the information given above, add [`<link>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/link) and [`<script>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/script) elements to your HTML, so that your CSS and JavaScript are applied to your HTML.

If done correctly, when you save your HTML and refresh your browser you'll see that things have changed:

![](https://mdn.mozillademos.org/files/12359/js-and-css.png)

* The JavaScript has added an empty list to the page. Now when you click anywhere on the list, a dialog box will pop up asking you to enter some text for a new list item. when you press the OK button, a new list item will be added to the list containing the text. When you click on an existing list item, a dialog box will pop up allowing you to change the item's text.
* The CSS has caused the background to go green, and the text to become bigger. It has also styled some of the content that the JavaScript has added to the page \(the red bar with the black border is the styling the CSS has added to the JS-generated list.\)

**Note**: If you get stuck in this exercise and can't get the CSS/JS to apply, try checking out our [css-and-js.html](https://github.com/mdn/learning-area/blob/master/html/introduction-to-html/the-html-head/css-and-js.html) example page.

#### Setting the primary language of the document

Finally, it's worth mentioning that you can \(and really should\) set the language of your page. This can be done by adding the [lang attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/lang) to the opening HTML tag \(as seen in the [meta-example.html](https://github.com/mdn/learning-area/blob/master/html/introduction-to-html/the-html-head/meta-example.html) and shown below.\)

```text
<html lang="en-US">
```

This is useful in many ways. Your HTML document will be indexed more effectively by search engines if its language is set \(allowing it to appear correctly in language-specific results, for example\), and it is useful to people with visual impairments using screen readers \(for example, the word "six" exists in both French and English, but is pronounced differently.\)

You can also set sub sections of your document to be recognised as different languages. For example, we could set our Japanese language section to be recognised as Japanese, like so:

```text
<p>Japanese example: <span lang="jp">ご飯が熱い。</span>.</p>
```

These codes are defined by the [ISO 639-1](https://en.wikipedia.org/wiki/ISO_639-1) standard. You can find more about them in [Language tags in HTML and XML](https://www.w3.org/International/articles/language-tags/).

