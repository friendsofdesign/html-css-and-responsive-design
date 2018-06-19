# CSS Debugging

### CSS and debugging

Just like HTML, CSS is _permissive_ \(read [permissive code](https://developer.mozilla.org/en-US/Learn/HTML/Introduction_to_HTML/Debugging_HTML#Permissive_code) before continuing.\) In CSS's case, if a declaration is invalid \(contains a syntax error, or the browser doesn't support that feature\), the browser just ignores it completely and moves on to the next one it finds.

If a selector is invalid, then it doesn't select anything, and the whole rule does nothing — again, the browser just moves on to the next rule.

This is great in a lot of ways — in most cases your content will be shown to your users, even if it isn't styled quite right. But this isn't very helpful when you are trying to debug the problem and you don't even get any kind of error message to help you find it. This is even more of a pain when the content isn't viewable by your users — perhaps a critical style isn't being applied, resulting in the layout going badly wrong?

Fortunately there are some tools available to help you. Let's look at these now.

#### Inspecting the DOM and CSS

Nowadays, all web browsers provide developer tools made to help you inspect and understand web pages. Among the various tools they provide, there are two that are available in all browsers: The DOM Inspector and the CSS Editor, which are available in Firefox in the [page inspector tool](https://developer.mozilla.org/en-US/docs/Tools/Page_Inspector). We already looked at the DOM Inspector in [Debugging HTML](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML/Debugging_HTML) and how it can be used to inspect HTML. Here we'll look at this _and_ the CSS Editor, and how to use them together to debug CSS problems.

**Note**: In the following example, we are using [Firefox](https://www.mozilla.org/firefox/new), but all browsers provide the same kind of tools — they might just be available in slightly different places. Read [Discover browser developer tools](https://developer.mozilla.org/en-US/docs/Learn/Discover_browser_developer_tools) to find more about accessing them in different browsers.

When going through this example, we'd first like you to open our [CSS debugging example](http://mdn.github.io/learning-area/css/introduction-to-css/debugging-css/) in a new browser tab. If you want to work through and fix the code problems to create a finished version of the example, we'd advise you to make a copy of the [HTML and CSS files](https://github.com/mdn/learning-area/tree/master/css/introduction-to-css/debugging-css), and implement the fixes locally.

It is meant to be a simple, clear one column web page containing a simple article:

![](https://mdn.mozillademos.org/files/12614/page-fixed.png)

At the moment however it is a bit of a mess:

![](https://mdn.mozillademos.org/files/12612/page-broken.png)

Let's start investigating the page with the page inspector's features. In Firefox you can open the page inspector using Cmd/Ctrl + I \(or by choosing _Tools &gt; Web Developer &gt; Inspector_ from the menu\), which will give you a set of tools open in a window on the bottom of the browser like so:

![](https://mdn.mozillademos.org/files/12604/page-inspector.png)

If you click on an element inside the DOM Inspector on the left, the CSS editor on the right will update to show all the CSS rules applied to that element. This is really useful, especially as any invalid properties appear with a line through them and a little warning symbol next to them. This will come in handy below!

![](https://mdn.mozillademos.org/files/12606/show-invalid-property.png)

**Note**: Each property also has a checkbox next to it, which can be checked/unchecked to allow you to enable/disable your CSS property by property. This is also very useful for figuring out what might be causing an error.

#### Active learning: find the errors!

So, with the tool basics outlined, let's try to find our errors. In each case, you should try clicking on the element where the fault is, to see what the applied CSS looks like.

1. The [`<header>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/header) and [`<footer>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/footer) elements are supposed have a background color, but no color appears.
2. The [`<h1>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/h1) and the [`<p>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/p) inside the footer are both too high up on the page — this is especially apparent on the `<h1>`, which is nearly off the screen! You could try clicking on the `<h1>` and unchecking the applied declarations to find out which one is causing the problem.
3. The [`<img>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img) is supposed to be floated down and to the right so it sits to the right of some of the text, but it isn't — it's directly above all of the text.
4. The text in the [`<main>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/main) content area is far too small — the paragraphs and list items should have a larger font-size applied to it, but it doesn't seem to have been applied to either. Hint: This one is a bit harder, as it is a problem with the selector rather than a property. You may have to study the source code to find this — you can find it in the [Style Editor](https://developer.mozilla.org/en-US/docs/Tools/Style_Editor) in Firefox's developer tools.

If you are stuck, you can look at the [fixed source code on Github](https://github.com/mdn/learning-area/blob/master/css/introduction-to-css/debugging-css-finished/style.css).

#### CSS validation

We already looked at the [W3C HTML Validator](https://validator.w3.org/), but they have a [CSS Validator](http://jigsaw.w3.org/css-validator/) available too. This works in the same way, allowing you to validate CSS at a [particular URL](http://jigsaw.w3.org/css-validator/#validate_by_uri), by [uploading a local file](http://jigsaw.w3.org/css-validator/#validate_by_upload), or by [direct CSS input](http://jigsaw.w3.org/css-validator/#validate_by_input).

![](https://mdn.mozillademos.org/files/12602/css-validator.png)

#### Active learning: Validating our CSS

Let's try feeding our CSS into the validator to see what it spits out.

1. Go to the CSS Validation Service [Validate by direct input](http://jigsaw.w3.org/css-validator/#validate_by_input) view.
2. Copy our error-filled CSS into the text area on the validation service.
3. Press the _Check_ button.

You will now be presented with a list of errors. Only two are returned:

![](https://mdn.mozillademos.org/files/12610/validator-results.png)

These are useful messages, especially as they include line numbers and what selector is in action in each case. Let's see how we can interpret these.

* _Property background-colour doesn't exist :_ _teal_ — simple; this is telling us that a property doesn't exist, which makes it clear what needs to be done.
* _Value Error : float attempt to find a semi-colon before the property name. add it_ — this is telling us that a semi-colon is missing. Looking at the line number of where this is occuring makes this easy to find.

You could argue that this is less useful than the browser developer tools — it doesn't allow you to look at the rendered code while referencing what is wrong, and it is no good for finding instances where the selector is incorrect, or the syntax is correct and you've simply chosen an incorrect value for your design. But we would argue that for a large stylesheet, it is worth running it through this service first to get rid of any basic syntax mistakes, before then relying on the browser developer tools to pinpoint other problems.

**Note**: [CSS Lint](http://csslint.net/) is a similar tool for validating CSS and uncovering errors, which can also present some useful hints and give interesting warnings.

