# CSS Text Styling

### What is involved in styling text in CSS?

As you'll have already experienced in your work with HTML and CSS, text inside an element is laid out inside the element's content box. It starts at the top left of the content area \(or the top right, in the case of RTL language content\), and flows towards the end of the line. Once it reaches the end, it goes down to the next line and continues, then the next line, until all the content has been placed in the box. Text content effectively behaves like a series of inline elements, being laid out on lines adjacent to one another, and not creating line breaks until the end of the line is reached, or unless you force a line break manually using the [`<br>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/br) element.

**Note**: If the above paragraph leaves you feeling confused, then no matter — go back and review our [Box model](https://developer.mozilla.org/en-US/docs/Learn/CSS/Introduction_to_CSS/Box_model) article, to brush up on the box model theory, before carrying on.

The CSS properties used to style text generally fall into two categories, which we'll look at separately in this article:

* **Font styles**: Properties that affect the font that is applied to the text, affecting what font is applied, how big it is, whether it is bold, italic, etc.
* **Text layout styles**: Properties that affect the spacing and other layout features of the text, allowing manipulation of, for example, the space between lines and letters, and how the text is aligned within the content box.

**Note**: Bear in mind that the text inside an element is all affected as one single entity. You can't select and style subsections of text unless you wrap them in an appropriate element \(such as a [`<span>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/span) or [`<strong>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/strong)\), or use a text-specific pseudo-element like [::first-letter](https://developer.mozilla.org/en-US/docs/Web/CSS/::first-letter) \(selects the first letter of an element's text\), [::first-line](https://developer.mozilla.org/en-US/docs/Web/CSS/::first-line) \(selects the first line of an element's text\), or [::selection](https://developer.mozilla.org/en-US/docs/Web/CSS/::selection) \(selects the text currently highlighted by the cursor.\)

#### Fonts

Let's move straight on to look at properties for styling fonts. In this example we'll apply some different CSS properties to the same HTML sample, which looks like this:

```text
<h1>Tommy the cat</h1>
​
<p>I remember as if it were a meal ago...</p>
​
<p>Said Tommy the Cat as he reeled back to clear whatever foreign matter
 may have nestled its way into his mighty throat. Many a fat alley rat 
had met its demise while staring point blank down the cavernous barrel of
 this awesome prowling machine. Truly a wonder of nature this urban 
predator — Tommy the cat had many a story to tell. But it was a rare 
occasion such as this that he did.</p>
```

You can find the [finished example on Github](http://mdn.github.io/learning-area/css/styling-text/fundamentals/) \(see also [the source code](https://github.com/mdn/learning-area/blob/master/css/styling-text/fundamentals/index.html).\)

#### Color

The [`color`](https://developer.mozilla.org/en-US/docs/Web/CSS/color) property sets the color of the foreground content of the selected elements \(which is usually the text, but can also include a couple of other things, such as an underline or overline placed on text using the [`text-decoration`](https://developer.mozilla.org/en-US/docs/Web/CSS/text-decoration) property\).

`color` can accept any [CSS color unit](https://developer.mozilla.org/en-US/Learn/CSS/Introduction_to_CSS/Values_and_units#Colors), for example:

```text
p {
  color: red;
}
```

This will cause the paragraphs to become red, rather than the standard browser default black, like so:

#### Font families

To set a different font on your text, you use the [`font-family`](https://developer.mozilla.org/en-US/docs/Web/CSS/font-family) property — this allows you to specify a font \(or list of fonts\) for the browser to apply to the selected elements. The browser will only apply a font if it is available on the machine the website is being accessed on; if not, it will just use a browser [default font](https://developer.mozilla.org/en-US/docs/Learn/CSS/Styling_text/Fundamentals#Default_fonts). A simple example looks like so:

```text
p {
  font-family: arial;
}
```

This would make all paragraphs on a page adopt the arial font, which is found on any computer.

**Web safe fonts**

Speaking of font availability, there are only a certain number of fonts that are generally available across all systems, and can therefore be used without much worry. These are the so-called **web safe fonts**.

Most of the time, as web developers we want to have more specific control over the fonts used to display our text content. The problem is to find a way to know which font is available on the computer used to see our web pages. There is no way to know this in every case, but the web safe fonts are known to be available on nearly all instances of the most used operating systems \(Windows, Mac, the most common Linux distributions, Android, and iOS.\)

The list of actual web safe fonts will change as operating systems evolve, but it's okay to consider the following fonts web safe, at least for now \(many of them have been popularized thanks to the Microsoft _Core fonts for the Web_ initiative in the late 90s and early 2000s\):

| Name | Generic type | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| Arial | sans-serif | It's often considered best practice to also add _Helvetica_ as a preferred alternative to _Arial_ as, although their font faces are almost identical, _Helvetica_ is considered to have a nicer shape, even if _Arial_ is more broadly available. |
| Courier New | monospace | Some OSes have an alternative \(possibly older\) version of the _Courier New_ font called _Courier_. It's considered best practice to use both with _Courier New_ as the preferred alternative. |
| Georgia | serif |  |
| Times New Roman | serif | Some OSes have an alternative \(possibly older\) version of the _Times New Roman_ font called _Times_. It's considered best practice to use both with _Times New Roman_ as the preferred alternative. |
| Trebuchet MS | sans-serif | You should be careful with using this font — it isn't widely available on mobile OSes. |
| Verdana | sans-serif |  |

**Note**: Among various [resources](http://moodle.friendsofdesign.co.za/mod/page/view.php?id=577), the [cssfontstack.com](http://www.cssfontstack.com/) website maintains a list of web safe fonts available on Windows and Mac OS operating systems, which can help you make your decision about what you consider safe for your usage.

**Note**: There is a way to download a custom font along with a webpage, to allow you to customize your font usage in any way you want: **web fonts**. This is a little bit more complex, and we will be discussing this in a separate article later on in the module.

**Default fonts**

CSS defines five generic names for fonts: ```serif, ``sans-serif, ``monospace```, `cursive,and` `fantasy.`Those are very generic and the exact font face used when using those generic names is up to each browser and can vary for each operating system they are running on. It represents a _worst case scenario_ where the browser will try to do its best to provide at least a font that looks appropriate. `serif`, `sans-serif` and `monospace` are quite predictable and should provide something reasonable. On the other hand, `cursive` and `fantasy` are less predictable and we recommend using them very carefully, testing as you go.

The five names are defined as follows:

| Term | Definition | Example |
| --- | --- | --- | --- | --- | --- |
| `serif` | Fonts that have serifs \(the flourishes and other small details you see at the ends of the strokes in some typefaces\) | My big red elephant |
| `sans-serif` | Fonts that don't have serifs. | My big red elephant |
| `monospace` | Fonts where every character has the same width, typically used in code listings. | My big red elephant |
| `cursive` | Fonts that are intended to emulate handwriting, with flowing, connected strokes. | My big red elephant |
| `fantasy` | Fonts that are intended to be decorative. | My big red elephant |

**Font stacks**

Since you can't guarantee the availability of the fonts you want to use on your webpages \(even a web font _could_ fail for some reason\), you can supply a **font stack** so that the browser has multiple fonts it can choose from. This simply involves a `font-family` value consisting of multiple font names separated by commas, e.g.

```text
p {
  font-family: "Trebuchet MS", Verdana, sans-serif;
}
```

In such a case, the browser starts at the beginning of the list and looks to see if that font is available on the machine. If it is, it applies that font to the selected elements. If not, it moves on to the next font, and so on.

It is a good idea to provide a suitable generic font name at the end of the stack, so that if none of the listed fonts are available, the browser can at least provide something approximately suitable. To emphasise this point, paragraphs are given the browser's default serif font if no other option is available — which is usually Time New Roman — this is no good for a sans-serif font!

**Note**: Fonts names that have more than one word — like `Trebuchet MS` — need to be surrounded by quotes.

**A font-family example**

Lets add to our previous example, giving the paragraphs a sans-serif font:

```text
p {
  color: red;
  font-family: Helvetica, Arial, sans-serif;
}
```

This gives us the following result:

#### Font size

In our previous module's [CSS values and units](https://developer.mozilla.org/en-US/docs/Learn/CSS/Introduction_to_CSS/Values_and_units) article, we reviewed [length and size units](https://developer.mozilla.org/en-US/Learn/CSS/Introduction_to_CSS/Values_and_units#Length_and_size). Font size \(set with the [`font-size`](https://developer.mozilla.org/en-US/docs/Web/CSS/font-size) property\) can take values measured in most of these units \(and others, such as [percentages](https://developer.mozilla.org/en-US/Learn/CSS/Introduction_to_CSS/Values_and_units#Percentages)\), however the most common units you'll use to size text are:

* `px` \(pixels\): The number of pixels high you want the text to be. This is an absolute unit — it results in the same final computed value for the font on the page in pretty much any situation.
* `em`s: 1em is equal to the font size set on the parent element of the current element we are styling \(more specifically, the width of a capital letter M contained inside the parent element.\) This can become tricky to work out if you have a lot of nested elements with different font sizes set, but it is doable, as you'll see below. Why bother? It is quite natural once you get used to it, and you can use `em`s to size everything, not just text. You can have an entire website sized using ems, which makes maintenance easy.
* `rem`s: These work just like `em`s, except that 1`rem` is equal to the font size set on the root element of the document \(i.e. [`<html>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/html)\), not the parent element. This makes doing the maths to work out your font sizes much easier, but unfortunately `rem`s are not supported in Internet Explorer 8 and below. If you need to support older browsers with your project, you can either stick to using `em`s or `px`, or use a [polyfill](https://developer.mozilla.org/en-US/docs/Glossary/polyfill) such as [REM-unit-polyfill](https://github.com/chuckcarpenter/REM-unit-polyfill).

The `font-size` of an element is inherited from that element's parent element. This all starts with the root element of the entire document — [`<html>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/html) — the `font-size` of which is set to 16px as standard across browsers. Any paragraph \(or other element that doesn't have a different size set by the browser\) inside the root element will have a final size of 16px. Other elements may have different default sizes, for example an [`<h1>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/h1) element has a size of 2ems set by default, so will have a final size of 32px.

Things become more tricky when you start altering the font size of nested elements. For example, if you had an [`<article>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/article) element in your page, and set its font-size to `1.5em`s \(which would compute to 24px final size\), and then wanted the paragraphs inside the `<article>`elements to have a computed font size of 20px, what em value would you use?

```text
<!-- document base font-size is 16px -->
<article> <!-- If my font-size is 1.5em -->
  <p>My paragraph</p> <!-- How do I compute to 20px font-size? -->
</article>
```

You would need to set its em value to 20/24, or `0.83333333em`s. The maths can be complicated, so you need to be careful about how you style things. It is best to use rems where you can, to keep things simple, and avoid setting the font-size of container elements where possible.

**A simple sizing example**

When sizing your text, it is usually a good idea to set the base `font-size` of the document to 10px, so that then the maths is a lot easier to work out — required \(r\)em values are then the pixel font size divided by 10, not 16. After doing that, you can easily size the different types if text in your document to what you want. It is a good idea to list all your `font-size` rulesets in a designated area in your stylesheet, so they are easy to find.

Our new result is like so:

```text
html {
  font-size: 10px;
}
​
h1 {
  font-size: 2.6rem;
}
​
p {
  font-size: 1.4rem;
  color: red;
  font-family: Helvetica, Arial, sans-serif;
}
```

#### Font style, font weight, text transform, and text decoration

CSS provides four common properties to alter the visual weight/emphasis of text:

* `font-style`

  : Used to turn italic text on and off. Possible values are as follows \(you'll rarely use this, unless you want to turn some italic styling off for some reason\):

  * `normal`: Sets text to normal font \(turns existing italics off.\)
  * `italic`: Sets text to use the _italic version of the font_ if available; if not available, it will simulate italics with oblique instead.
  * `oblique`: Sets text to use a simulated version of an italic font, created by slanting the normal version.

* `font-weight`: Sets how bold the text is. This has many available values available in case you have many font variants available \(such as -light, -normal, -bold, -extrabold, -black, etc.\), but realistically you'll rarely use any of them except for `normal` and `bold`:
  * `normal`, `bold`: Normal and **bold** font weight
  * `lighter`, `bolder`: Sets the current element's boldness to be one step lighter or heavier than its parent element's boldness.
  * `100`–`900`: Numeric boldness values that provide finer grained control than the above keywords, if needed.
* `text-transform`: Allows you to set your font to be transformed. Values include:
  * `none`: Prevents any transformation.
  * `uppercase`: Transforms ALL TEXT TO CAPITALS.
  * `lowercase`: Transforms all text to lower case.
  * `capitalize`: Transforms all words to Have The First Letter Capitalized.
  * `full-width`: Transforms all glyphs to be written inside a fixed-width square, similar to a monospace font, allowing aligning of e.g. latin characters along with asian language glyphs \(like Chinese, Japanese, Korean.\)
* `text-decoration`: Sets/unsets text decorations on fonts \(you'll mainly use this to unset the default underline on links when styling them.\) Available values are:

  * `none`: Unsets any text decorations already present.
  * `underline`: Underlines the text.
  * `overline`: Gives the text an overline.
  * `line-through`: Puts a strikethrough over the text.

  You should note that `text-decoration` can accept multiple values at once, if you want to add multiple decorations simultaneously, for example `text-decoration: underline overline`. Also note that `text-decoration` is a shorthand property for `text-decoration-line`, `text-decoration-style`, and `text-decoration-color`. You can use combinations of these property values to create interesting effects, for example `text-decoration: line-through red wavy`.

Let's look at adding a couple of these properties to our example:

Our new result is like so:

```text
html {
  font-size: 10px;
}
​
h1 {
  font-size: 2.6rem;
  text-transform: capitalize;
}
​
h1 + p {
  font-weight: bold;
}
​
p {
  font-size: 1.4rem;
  color: red;
  font-family: Helvetica, Arial, sans-serif;
}
```

#### Text drop shadows

You can apply drop shadows to your text using the [`text-shadow`](https://developer.mozilla.org/en-US/docs/Web/CSS/text-shadow) property. This takes up to four values, as shown in the example below:

```text
text-shadow: 4px 4px 5px red;
```

The four properties are as follows:

1. The horizontal offset of the shadow from the original text — this can take most available CSS [length and size units](https://developer.mozilla.org/en-US/Learn/CSS/Introduction_to_CSS/Values_and_units#Length_and_size), but you'll most comonly use px. This value has to be included.
2. The vertical offset of the shadow from the original text; behaves basically just like the horizontal offset, except that it moves the shadow up/down, not left/right. This value has to be included.
3. The blur radius — a higher value means the shadow is dispersed more widely. If this value is not included, it defaults to 0, which means no blur. This can take most available CSS [length and size units](https://developer.mozilla.org/en-US/Learn/CSS/Introduction_to_CSS/Values_and_units#Length_and_size).
4. The base color of the shadow, which can take any [CSS color unit](https://developer.mozilla.org/en-US/Learn/CSS/Introduction_to_CSS/Values_and_units#Colors). If not included, it defaults to `black`.

**Note**: Positive offset values move the shadow right and down, but you can also use negative offset vaues to move the shadow left and up, for example `-1px -1px`.

**Multiple shadows**

You can apply multiple shadows to the same text by including multiple shadow values separated by commas, for example:

```text
text-shadow: -1px -1px 1px #aaa,
             0px 4px 1px rgba(0,0,0,0.5),
             4px 4px 5px rgba(0,0,0,0.7),
             0px 0px 7px rgba(0,0,0,0.4);
```

If we applied this to the [`<h1>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/h1) element in our Tommy the cat example, we'd end up with this:

**Note**: You can see more interesting examples of `text-shadow` usage in the Sitepoint article [Moonlighting with CSS text-shadow](http://www.sitepoint.com/moonlighting-css-text-shadow/).

#### Text layout

With basic font properties out the way, let's now have a look at properties we can use to affect text layout.

#### Text alignment

The [`text-align`](https://developer.mozilla.org/en-US/docs/Web/CSS/text-align) property is used to control how text is aligned within its containing content box. The available values are as follows, and work in pretty much the same way as they do in a regular word processor application:

* `left`: Left justifies the text.
* `right`: Right justifies the text.
* `center`: Centers the text.
* `justify`: Makes the text spread out, varying the gaps in between the words so that all lines of text are the same width. You need to use this carefully — it can look terrible, especially when applied to a paragraph with lots of long words in it. If you are going to use this, you should also think about using something else along with it, such as [`hyphens`](https://developer.mozilla.org/en-US/docs/Web/CSS/hyphens), to break some of the longer words across lines.

If we applied `text-align: center;` to the [`<h1>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/h1) in our example, we'd end up with this:

#### Line height

The [`line-height`](https://developer.mozilla.org/en-US/docs/Web/CSS/line-height) property sets the height of each line of text — this can take most [length and size units](https://developer.mozilla.org/en-US/Learn/CSS/Introduction_to_CSS/Values_and_units#Length_and_size), but can also take a unitless value, which acts as a multiplier and is generally considered the best option — the [`font-size`](https://developer.mozilla.org/en-US/docs/Web/CSS/font-size) is multiplied to get the `line-height`. Body text generally looks nicer and is easier to read when the lines are spaced apart; the recommended line height is around 1.5–2 \(double spaced.\) So to set our lines of text to 1.5 times the height of the font, you'd use this:

```text
line-height: 1.5;
```

Applying this to the [`<p>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/p) elements in our example would give us this result:

#### Letter and word spacing

The [`letter-spacing`](https://developer.mozilla.org/en-US/docs/Web/CSS/letter-spacing) and [`word-spacing`](https://developer.mozilla.org/en-US/docs/Web/CSS/word-spacing) properties allow you to set the spacing between letters and words in your text. You won't use these very often, but might find use for them to get a certain look, or to improve the legibility of a particularly dense font. They can take most [length and size units](https://developer.mozilla.org/en-US/Learn/CSS/Introduction_to_CSS/Values_and_units#Length_and_size).

So as an example, if we applied the following to the first line of the [`<p>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/p) elements in our example:

```text
p::first-line {
  letter-spacing: 2px;
  word-spacing: 4px;
}
```

We'd get the following:

#### Other properties worth looking at

The above properties give you an idea of how to start styling text on a webpage, but there are many more properties you could use. We just wanted to cover the most important ones here. Once you've become used to using the above, you should also explore the following:

Font styles:

* [`font-variant`](https://developer.mozilla.org/en-US/docs/Web/CSS/font-variant): Switch between small caps and normal font alternatives.
* [`font-kerning`](https://developer.mozilla.org/en-US/docs/Web/CSS/font-kerning): Switch font kerning options on and off.
* [`font-feature-settings`](https://developer.mozilla.org/en-US/docs/Web/CSS/font-feature-settings): Switch various [OpenType](https://en.wikipedia.org/wiki/OpenType) font features on and off.
* [`font-variant-alternates`](https://developer.mozilla.org/en-US/docs/Web/CSS/font-variant-alternates): Control the use of alternate glyphs for a given font-face.
* [`font-variant-caps`](https://developer.mozilla.org/en-US/docs/Web/CSS/font-variant-caps): Control the use of alternate capital glyphs.
* [`font-variant-east-asian`](https://developer.mozilla.org/en-US/docs/Web/CSS/font-variant-east-asian): Control the usage of alternate glyphs for East Asian scripts, like Japanese and Chinese.
* [`font-variant-ligatures`](https://developer.mozilla.org/en-US/docs/Web/CSS/font-variant-ligatures): Control which ligatures and contextual forms are used in text.
* [`font-variant-numeric`](https://developer.mozilla.org/en-US/docs/Web/CSS/font-variant-numeric): Control the usage of alternate glyphs for numbers, fractions, and ordinal markers.
* [`font-variant-position`](https://developer.mozilla.org/en-US/docs/Web/CSS/font-variant-position): Control the usage of alternate glyphs of smaller sizes positioned as superscript or subscript.
* [`font-size-adjust`](https://developer.mozilla.org/en-US/docs/Web/CSS/font-size-adjust): Adjust the visual size of the font independently of its actual font size.
* [`font-stretch`](https://developer.mozilla.org/en-US/docs/Web/CSS/font-stretch): Switch between possible alternative stretched versions of a given font.
* [`text-underline-position`](https://developer.mozilla.org/en-US/docs/Web/CSS/text-underline-position): Specify the position of underlines set using the `text-decoration-line` property `underline` value.
* [`text-rendering`](https://developer.mozilla.org/en-US/docs/Web/CSS/text-rendering): Try to perform some text rendering optimization.

Text layout styles

* [`text-indent`](https://developer.mozilla.org/en-US/docs/Web/CSS/text-indent): Specify how much horizontal space should be left before the beginning of the first line of the text content.
* [`text-overflow`](https://developer.mozilla.org/en-US/docs/Web/CSS/text-overflow): Define how overflowed content that is not displayed is signaled to users.
* [`white-space`](https://developer.mozilla.org/en-US/docs/Web/CSS/white-space): Define how whitespace and associated line breaks inside the element are handled.
* [`word-break`](https://developer.mozilla.org/en-US/docs/Web/CSS/word-break): Specify whether to break lines within words.
* [`direction`](https://developer.mozilla.org/en-US/docs/Web/CSS/direction): Define the text direction \(This depends on the language and usually it's better to let HTML handle that part as it is tied to the text content.\)
* [`hyphens`](https://developer.mozilla.org/en-US/docs/Web/CSS/hyphens): Switch on and off hyphenation for supported languages.
* [`line-break`](https://developer.mozilla.org/en-US/docs/Web/CSS/line-break): Relax or strengthen line breaking for Asian languages.
* [`text-align-last`](https://developer.mozilla.org/en-US/docs/Web/CSS/text-align-last): Define how the last line of a block or a line, right before a forced line break, is aligned.
* [`text-orientation`](https://developer.mozilla.org/en-US/docs/Web/CSS/text-orientation): Define the orientation of the text in a line.
* [`word-wrap`](https://developer.mozilla.org/en-US/docs/Web/CSS/word-wrap): Specify whether or not the browser may break lines within words in order to prevent overflow.
* [`writing-mode`](https://developer.mozilla.org/en-US/docs/Web/CSS/writing-mode): Define whether lines of text are laid out horizontally or vertically and the direction in which subsequent lines flow.

#### Font shorthand

Many font properties can also be set through the shorthand property [`font`](https://developer.mozilla.org/en-US/docs/Web/CSS/font). These are written in the following order: [`font-style`](https://developer.mozilla.org/en-US/docs/Web/CSS/font-style), [`font-variant`](https://developer.mozilla.org/en-US/docs/Web/CSS/font-variant), [`font-weight`](https://developer.mozilla.org/en-US/docs/Web/CSS/font-weight), [`font-stretch`](https://developer.mozilla.org/en-US/docs/Web/CSS/font-stretch), [`font-size`](https://developer.mozilla.org/en-US/docs/Web/CSS/font-size), [`line-height`](https://developer.mozilla.org/en-US/docs/Web/CSS/line-height), and [`font-family`](https://developer.mozilla.org/en-US/docs/Web/CSS/font-family).

Among all those properties, only `font-size` and `font-family` are required when using the `font`shorthand property.

A forward slash has to be put in between the [`font-size`](https://developer.mozilla.org/en-US/docs/Web/CSS/font-size) and [`line-height`](https://developer.mozilla.org/en-US/docs/Web/CSS/line-height) properties.

A full example would look like this:

```text
font: italic normal bold normal 3em/1.5 Helvetica, Arial, sans-serif;
```

#### Active learning: Playing with styling text

In this active learning session, we don't have any specific exercises for you to do: we'd just like you to have a good play with some font/text layout properties, and see what you can produce! You can either do this using offline HTML/CSS files, or enter your code into the live editable example below.

If you make a mistake, you can always reset it using the _Reset_ button.

\[WE WILL HAVE TO INCLUDE A \(LINK TO A\) LIVE EXAMPLE HERE\]

