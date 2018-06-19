# HTML Debugging

### Debugging isn't scary

When writing code of some kind, everything is usually fine, until that dreaded moment when an error occurs — you've done something wrong, so your code doesn't work — either not at all, or not quite how you wanted it to. For example, the following shows an error reported when trying to [compile](https://developer.mozilla.org/en-US/docs/Glossary/compile) a simple program written in the [Rust](https://www.rust-lang.org/) language.

![](https://mdn.mozillademos.org/files/12435/error-message.png)

Here, the error message is relatively easy to understand — "unterminated double quote string". If you look at the listing, you can probably see how `println!(Hello, world!");` might logically be missing a double quote. However, error messages can quickly get more complicated and less easy to interpret as programs get bigger, and even the above simple case can look a little intimidating to someone who doesn't know anything about Rust. \(Which you probably don't.\)

Debugging needn't be scary though — the key to being comfortable with writing and debugging any programming language or code is familiarity — with both the language and the tools.

#### HTML and debugging

HTML is not as complicated to understand as Rust — HTML is not compiled into a different form before the browser parses it and shows the result \(it is _interpreted_, not _compiled_.\) And HTML's [element](https://developer.mozilla.org/en-US/docs/Glossary/element) syntax is arguably a lot easier to understand than a "real programming language" like Rust, [JavaScript](https://developer.mozilla.org/en-US/docs/Glossary/JavaScript) or [Python](https://developer.mozilla.org/en-US/docs/Glossary/Python). The way that browsers run HTML is however a lot more **permissive** than how programming languages are run, which is both a good and a bad thing.

#### Permissive code

So what do we mean by permissive? Well, generally when you do something wrong in code, there are two main types of error that you'll come across:

* **Syntax errors**: These are spelling errors in your code that actually cause the program not to run, like the Rust error shown above. These are usually ok to fix, as long as you are familiar with the right tools, and know what the error messages mean!
* **Logic errors**: These are errors where the syntax is actually correct, but the code is not what you intended it to be, meaning that program runs incorrectly. These are often harder to fix than syntax errors, as there isn't an error message to direct you to the source of the error.

HTML itself doesn't tend to suffer from syntax errors because browsers run it permissively, meaning that the code still runs even if there are syntax errors present! Browsers have built-in rules to state how to interpret incorrectly written markup, so you'll get something running, even if it might not be quite what you expected. This of course can still be a problem!

**Note**: HTML is run permissively because when the Web was first created, it was decided that allowing people to get their content published was more important than making sure all the syntax was absolutely correct. The Web would probably not be as popular as it is today, if it had been more strict from the very beginning.

#### Active learning: Studying permissive code

It's time to study the permissive nature of HTML code for yourselves.

1. First, get hold of a copy of our [debug-example demo](https://github.com/mdn/learning-area/blob/master/html/introduction-to-html/debugging-html/debug-example.html) and save it somewhere locally. This is deliberately written to have some errors in it for us to explore \(the HTML markup is said to be **badly-formed**, as opposed to **well-formed**.\)
2. Next, try opening it in a browser — you will see something like this:![](https://mdn.mozillademos.org/files/12437/badly-formed-html.png)
3. This immediately doesn't look great; let's look at the source code to see if we can work out why \(only the body contents are shown\):

   ```text
   <h1>HTML debugging examples</h1>
   ​
   <p>What causes errors in HTML?
   ​
   <ul>
     <li>Unclosed elements: If an element is <strong>not closed properly,
         then its effect can spread to areas you didn't intend
   ​
     <li>Badly nested elements: Nesting elements properly is also very important
         for code behaving correctly. <strong>strong <em>strong emphasised?</strong>
         what is this?</em>
   ​
     <li>Unclosed attributes: Another common source of HTML problems. Let's
         look at an example: <a href="https://www.mozilla.org/>link to Mozilla
         homepage</a>
   </ul>
   ```

4. Let's review the problems we can see here:
   * The [paragraph](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/p) and [list item](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/li) elements have no closing tags. Looking at the image above, this doesn't seem to have affected the markup rendering too badly, as it is easy to infer where one element should end, and another should begin.
   * The first [`<strong>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/strong) element has no closing tag. This is a bit more problematic, as it isn't easy to tell where the element is supposed to end. In fact, the whole of the rest of the text looks to have been strongly emphasised.
   * This section is badly nested: `<strong>strong <em>strong emphasised?</strong> what is this?</em>`. It is not easy to tell how this has been interpreted, because of the previous problem.
   * The `href` attribute value has a missing closing double quote. This seems to have caused the biggest problem — the link has not rendered at all.
5. Now let's look at the markup the browser has rendered, as opposed to the markup in the source code. To do this, we can use the browser developer tools. If you are not familiar with how to use your browser's developer tools, take a few minutes out to review [Discover browser developer tools](https://developer.mozilla.org/en-US/docs/Learn/Discover_browser_developer_tools), then come back.
6. In the DOM inspector, you can see what the rendered markup looks like:![](https://mdn.mozillademos.org/files/12439/html-inspector.png)
7. Using the DOM inspector, let's explore our code in detail to see how the browser has tried to fix our HTML errors \(we did the review in Firefox; other modern browsers

   should

    give the same result\):

   * The paragraphs and list items have been given closing tags.
   * It isn't clear where the first `<strong>` element should be closed, so the browser has wrapped each separate block of text with its own strong tag, right down to the bottom of the document!
   * The incorrect nesting has been fixed by the browser like this:

     ```text
     <strong>strong
       <em>strong emphasised?</em>
     </strong>
     <em> what is this?</em>
     ```

   * The link with the missing attribute double quote has been deleted altogether. The last list item just looks like this:

     ```text
     <li>
       <strong>Unclosed attributes: Another common source of HTML problems.
       Let's look at an example: </strong>
     </li>
     ```

#### HTML validation

So you can see from the above example that you really want to make sure your HTML is well-formed! But how? In a small example like the one seen above, it is pretty easy to search through the lines and find the errors, but what about a huge, complex HTML document?

The best strategy is to start by running your HTML page through the [Markup Validation Service](https://validator.w3.org/) — created and maintained by the W3C, the organization that looks after the specifications that define HTML, CSS, and other web technologies. This webpage takes an HTML document as an input, goes through it, and gives you a report to tell you what is wrong with your HTML.

![](https://mdn.mozillademos.org/files/12441/validator.png)

To specify the HTML to validate, you can give it a web address to point to, upload an HTML file, or directly input some HTML code.

