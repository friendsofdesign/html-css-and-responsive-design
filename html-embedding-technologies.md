# HTML Embedding Technologies

### A short history of embedding

A long time ago on the Web, it was popular to use **frames** to create websites — small parts of a website stored in individual HTML pages. These were embedded in a master document called a **frameset**, which allowed you to specify the area on the screen that each frame filled, rather like sizing the columns and rows of a table. These were considered the height of coolness in the mid to late 90s, and there was evidence that having a webpage split up into smaller chunks like this was better for download speeds — especially noticeable with network connections being so slow back then. They did however have many problems, which far outweighed any positives as network speeds got faster, so you don't see them being used anymore.

A little while later \(late 90s, early 2000s\), plugin technologies became very popular, such as [Java Applets](https://developer.mozilla.org/en-US/docs/Glossary/Java) and [Flash](https://developer.mozilla.org/en-US/docs/Glossary/Adobe_Flash) — these allowed web developers to embed rich content into webpages such as video and [animations](http://moodle.friendsofdesign.co.za/mod/folder/view.php?id=489), which just weren't available through HTML alone. Embedding these technologies was achieved through elements like [`<object>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/object), and the lesser-used [`<embed>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/embed), and they were very useful at the time. They have since fallen out of fashion due to many problems, including accessibility, security, file size, and more; these days most mobile devices don't support such plugins anymore, and desktop support is on the way out.

Finally, the [`<iframe>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe) element appeared \(along with other ways of embedding content, such as [`<canvas>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/canvas), [`<video>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/video), etc.\) This provides a way to embed an entire web document inside another one, as if it were an [`<img>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img) or other such element, and is used regularly today.

With the history lesson out of the way, let's move on and see how to use some of these.

#### Iframes in detail

So, that was easy and fun right? [`<iframe>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe) elements are designed to allow you to embed other web documents into the current document. This is great for incorporating third party content into your website that you might not have direct control over and don't want to have to implement your own version of — such as video from online video providers, commenting systems like [Disqus](https://disqus.com/), maps from online map providers, advertising banners, etc. The live editable examples you've been using through this course are implemented using `<iframe>`s.

There are some serious [Security concerns](https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Other_embedding_technologies#Security_concerns) to consider with `<iframe>`s, as we'll discuss below, but this doesn't mean that you shouldn't use them in your websites — it just requires some knowledge and careful thinking. Let's explore the code in a bit more detail. Say you wanted to include the MDN glossary on one of your webpages — you could try something like this:

```text
<iframe src="https://developer.mozilla.org/en-US/docs/Glossary"
        width="100%" height="500" frameborder="0"
        allowfullscreen sandbox>
  <p> <a href="https://developer.mozilla.org/en-US/docs/Glossary">
    Fallback link for browsers that don't support iframes
  </a> </p>
</iframe>
```

This example includes the basic essentials needed to use an `<iframe>`:

* **`allowfullscreen`**

  If set, the `<iframe>` is able to be placed in fullscreen mode using the [Full Screen API](https://developer.mozilla.org/en-US/docs/Web/Apps/Fundamentals/User_notifications/Full_screen_api) \(somewhat beyond scope for this article.\)

* **`frameborder`**

  If set to 1, this tells the browser to draw a border between this frame and other frames, which is the default behaviour. 0 removes the border. Using this isn't really recommended any more, as the same effect can be better achieved using [`border`](https://developer.mozilla.org/en-US/docs/Web/CSS/border)`: none;` in your [CSS](https://developer.mozilla.org/en-US/docs/Glossary/CSS).

* **`src`**

  This attribute, as with [\`\`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/video)/[\`\`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img), contains a path pointing to the URL of the document to be embedded.

* **`width` and `height`**

  These attributes specify the width and height you want the iframe to be.

* **Fallback content**

  In the same way as other similar elements like [\`\`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/video), you can include fallback content between the opening and closing `<iframe></iframe>` tags that will appear if the browser doesn't support the `<iframe>`. In this case we have included a link to the page instead. It is unlikely that you'll come across any browser that doesn't support `<iframe>`s these days.

* **`sandbox`**

  This attribute, which works in slightly more modern browsers than the rest of the `<iframe>`features \(e.g. IE 10 and above\) requests heightened security settings; we'll say more about this in the next section.

**Note**: In order to improve speed, It's a good idea to set the iframe's `src` attribute with JavaScript after the main content is done loading. This makes your page usable sooner and decreases your official page load time \(an important [SEO](https://developer.mozilla.org/en-US/docs/Glossary/SEO) metric.\)

#### Security concerns

Above we mentioned security concerns — let's go into this in a bit more detail now. We are not expecting you to understand all of this content perfectly the first time; we just want to make you aware of this concern, and provide a reference to come back to as you get more experienced and start considering using `<iframe>`s in your experiments and work. Also, there is no need to be scared and not use `<iframe>`s — you just need to be careful. Read on...

Browser makers and Web developers have learned the hard way that iframes are a common target \(official term: **attack vector**\) for bad people on the Web \(often termed **hackers**, or more accurately, **crackers**\) to attack if they are trying to maliciously modify your webpage, or trick people into doing something they don't want to do, such as reveal sensitive information like usernames and passwords. Because of this, spec engineers and browser developers have developed various security mechanisms for making `<iframe>`s more secure, and there are also best practices to consider — we'll cover some of these below.

[Clickjacking](https://en.wikipedia.org/wiki/Clickjacking) is one kind of common iframe attack where hackers embed an invisible iframe into your document \(or embed your document into their own malicious website\) and use it to capture users' interactions. This is a common way to mislead users or steal sensitive data.

A quick example first though — try loading the previous example we showed above into your browser — you can [find it live on Github](http://mdn.github.io/learning-area/html/multimedia-and-embedding/other-embedding-technologies/iframe-detail.html) \([see the source code](https://github.com/mdn/learning-area/blob/gh-pages/html/multimedia-and-embedding/other-embedding-technologies/iframe-detail.html) too.\) You won't actually see anything displayed on the page, and if you look at the _Console_ in the [browser developer tools](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_are_browser_developer_tools), you'll see a message telling you why. In Firefox, you'll get told _Load denied by X-Frame-Options:_ [_https://developer.mozilla.org/en-US/docs/Glossary_](https://developer.mozilla.org/en-US/docs/Glossary) _does not permit framing_. This is because the developers that built MDN have included a setting on the server that serves the website pages to disallow them from being embedded inside `<iframe>`s \(see [Configure CSP directives](https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Other_embedding_technologies#Configure_CSP_directives), below.\) This makes sense — an entire MDN page doesn't really make sense to be embedded in other pages, unless you want to do something like embed them on your site and claim them as your own — or attempt to steal data via clickjacking, which are both really bad things to do. Plus if everybody started to do this, all the additional bandwidth would start to cost Mozilla a lot of money.

**Only embed when necessary**

Sometimes it makes sense to embed third party content — like youtube videos and maps — but you can save yourself a lot of headaches if you only embed third party content when completely necessary. A good rule of thumb for web security is _"You can never be too cautious. If you made it, double-check it anyway. If someone else made it, assume it's dangerous until proven otherwise."_

Besides security, you should also be aware of intellectual property issues. Most content is copyrighted, offline and online, even content you might not expect \(for example, most images on [Wikimedia Commons](https://commons.wikimedia.org/wiki/Main_Page)\). Never display content on your webpage unless you own it or the owners have given you written, unequivocal permission. Penalties for copyright infringement are severe. Again, you can never be too cautious.

If the content is licensed, you must obey the license terms. For example, the content on MDN is [licensed under CC-BY-SA](https://developer.mozilla.org/en-US/docs/MDN/About#Copyrights_and_licenses). That means, you must [credit us properly](https://wiki.creativecommons.org/wiki/Best_practices_for_attribution) when you quote our content, even if you make substantial changes.

**Use HTTPS**

[HTTPS](https://developer.mozilla.org/en-US/docs/Glossary/HTTPS) is the encrypted version of [HTTP](https://developer.mozilla.org/en-US/docs/Glossary/HTTP). You should serve your websites using HTTPS whenever possible:

1. HTTPS reduces the chance that remote content has been tampered with in transit,
2. HTTPS prevents embedded content from accessing content in your parent document, and vice versa.

Using HTTPS requires a security certificate, which can be expensive \(although [Let's Encrypt](https://letsencrypt.org/) makes things easier\) — if you can't get one, you may serve your parent document with HTTP. However, because of the second benefit of HTTPS above, _no matter what the cost, you must never embed third-party content with HTTP._ \(In the best case scenario, your user's Web browser will give them a scary warning.\) All reputable companies that make content available for embedding via an `<iframe>` will make it available via HTTPS — look at the URLs inside the `<iframe>` `src`attribute when you are embedding content from Google Maps or Youtube, for example.

**Note**: [Github pages](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/Using_Github_pages) allows content to be served via HTTPS by default, so is useful for hosting content. If you are using different hosting and are not sure, ask your hosting provider about it.

**Always use the sandbox attribute**

You want to give attackers as little power as you can to do bad things on your website, therefore you should give embedded content _only the permissions needed for doing its job._ Of course, this applies to your own content, too. A container for code where it can be used appropriately — or for testing — but can't cause any harm to the rest of the codebase \(either accidental or malicious\) is called a [sandbox](https://en.wikipedia.org/wiki/Sandbox_%28computer_security%29).

Unsandboxed content can do way too much \(executing JavaScript, submitting forms, popup windows, etc.\) By default you should impose all available restrictions by using the `sandbox`attribute with no parameters, as shown in our previous example.

If absolutely required, you can add permissions back one by one \(inside the `sandbox=""`attribute value\) — see the `sandbox` reference entry for all the available options. One important note is that you should _never_ add both `allow-scripts` and `allow-same-origin` to your `sandbox`attribute — in that case the embedded content could bypass the same origin security policy that stops sites from executing scripts, and use JavaScript to turn off sandboxing altogether.

**Note**: Sandboxing provides no protection if attackers can fool people into visiting malicious content directly \(outside an `iframe`\). If there's any chance that certain content may be malicious \(e.g., user-generated content\), please serve it from a different [domain](https://developer.mozilla.org/en-US/docs/Glossary/domain) to your main site.

**Configure CSP directives**

[CSP](https://developer.mozilla.org/en-US/docs/Glossary/CSP) stands for **content security policy**, and provides [a set of HTTP Headers](https://developer.mozilla.org/en-US/docs/Web/Security/CSP/CSP_policy_directives) \(metadata sent along with your web pages when they are served from a web server\) designed to improve the security of your HTML document. When it comes to securing `<iframe>`s, you can _configure your server to send an appropriate X-Frame-Options header._ This can prevent other websites from embedding your content in their webpages \(which would enable [clickjacking](https://en.wikipedia.org/wiki/clickjacking) and a host of other attacks\), which is exactly what the MDN developers have done, as we saw earlier on.

**Note**: You can read Frederik Braun's post [On the X-Frame-Options Security Header](https://blog.mozilla.org/security/2013/12/12/on-the-x-frame-options-security-header/) for more background information on this topic. Obviously, it's rather out of scope for a full explanation in this article.

### The `<embed>` and `<object>`elements

The [`<embed>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/embed) and [`<object>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/object) elements serve a different function to [`<iframe>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe) — these elements are general purpose embedding tools for embedding multiple types of external content, which include plugin technologies like Java Applets and Flash, PDF \(which can be shown in a browser with a PDF plugin\), and even content like videos, SVG and images!

**Note**: A **plugin** is software that provides access to content the browser cannot read natively.

However, you are unlikely to use these elements very much — Applets haven't been used for years, Flash is no longer very popular, due to a number of reasons \(see [The case against plugins](https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Other_embedding_technologies#The_case_against_plugins), below\), PDFs tend to be be better linked to than embedded, and other content such as images and video have much better, easier elements to handle those. Plugins and these embedding methods are really a legacy technology, and we are mainly mentioning them in case you come across them in certain circumstances like intranets, or enterprise projects.

If you find yourself needing to embed plugin content, this is the kind of information you'll need, at a minimum:

|  | [`<embed>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/embed) | [`<object>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/object) |
| --- | --- | --- | --- | --- | --- |
| [URL](https://developer.mozilla.org/en-US/docs/Glossary/URL) of the embedded content | `src` | `data` |
| _accurate_ [media type](https://developer.mozilla.org/en-US/docs/Glossary/MIME_type) of the embedded content | `type` | `type` |
| height and width \(in CSS pixels\) of the box controlled by the plugin | ```height``width``` | ```height``width``` |
| names and values, to feed the plugin as parameters | ad hoc attributes with those names and values | single-tag [`<param>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/param) elements, contained within `<object>` |
| independent HTML content as fallback for an unavailable resource | not supported \(`<noembed>` is obsolete\) | contained within `<object>`, after `<param>` elements |

**Note**: `<object>` requires a `data` attribute, a `type` attribute, or both. If you use both, you may also use the `typemustmatch` attribute \(only implemented in Firefox, as of this writing\). `typemustmatch` keeps the embedded file from running unless the `type` attribute provides the correct media type. `typemustmatch`can therefore confer significant security benefits when you're embedding content from a different [origin](https://developer.mozilla.org/en-US/docs/Glossary/origin)\(it can keep attackers from running arbitrary scripts through the plugin\).

Here's an example that uses the [`<embed>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/embed) element to embed a Flash movie \(see this [live on Github](http://mdn.github.io/learning-area/html/multimedia-and-embedding/other-embedding-technologies/embed-flash.html), and [check the source code](https://github.com/mdn/learning-area/blob/gh-pages/html/multimedia-and-embedding/other-embedding-technologies/embed-flash.html) too\):

```text
<embed src="whoosh.swf" quality="medium"
       bgcolor="#ffffff" width="550" height="400"
       name="whoosh" align="middle" allowScriptAccess="sameDomain"
       allowFullScreen="false" type="application/x-shockwave-flash"
       pluginspage="http://www.macromedia.com/go/getflashplayer">
```

Pretty horrible, isn't it. The HTML generated by the Adobe Flash tool tended to be even worse, using an `<object>` element with an `<embed>` element embedded in it, to cover all bases \(check out an example.\) Flash was even used successfully as fallback content for HTML5 video, for a time, but this is increasingly being seen as not necessary.

Now let's look at an `<object>` example that embeds a PDF into a page \(see the [live example](http://mdn.github.io/learning-area/html/multimedia-and-embedding/other-embedding-technologies/object-pdf.html) and the [source code](https://github.com/mdn/learning-area/blob/gh-pages/html/multimedia-and-embedding/other-embedding-technologies/object-pdf.html)\):

```text
<object data="mypdf.pdf" type="application/pdf"
        width="800" height="1200" typemustmatch>
  <p>You don't have a PDF plugin, but you can <a href="myfile.pdf">download the PDF file.</a></p>
</object>
```

PDFs were a necessary stepping stone between paper and digital, but they pose many [accessibility challenges](http://webaim.org/techniques/acrobat/acrobat) and can be hard to read on small screens. They do still tend to be popular in some circles, but it is much better to link to them so they can be downloaded or read on a separate page, rather than embedding them in a webpage.

