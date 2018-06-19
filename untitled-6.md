# CSS Selectors

### The basics

In the last article we explained general CSS syntax and terminology in detail. To recap, selectors are one part of a CSS rule and come just before CSS declaration blocks.

![](https://mdn.mozillademos.org/files/3668/css%20syntax%20-%20ruleset.png)

#### Different types of selector

Selectors can be divided into the following categories:

* **Simple selectors**: Match one or more elements based on element type, `class`, or `id`.
* **Attribute selectors**: Match one or more elements based on their attributes/attribute values.
* **Pseudo-classes**: Match one or more elements that exist in a certain state, such as an element that is being hovered over by the mouse pointer, or a checkbox that is currently disabled or checked, or an element that is the first child of its parent in the DOM tree.
* **Pseudo-elements**: Match one or more parts of content that are in a certain position in relation to an element, for example the first word of each paragraph, or generated content appearing just before an element.
* **Combinators**: These are not exactly selectors themselves, but ways of combining two or more selectors in useful ways for very specific selections. So for example, you could select only paragraphs that are direct descendants of divs, or paragraphs that come directly after headings.
* **Multiple selectors**: Again, these are not separate selectors; the idea is that you can put multiple selectors on the same CSS rule, separated by commas, to apply a single set of declarations to all the elements selected by those selectors.

#### Selectors article overview

The next four articles all explore different aspects of selectors — we've broken this information up because there is a lot of it, and we wanted to make it less intimidating and give you some clear points to take breaks mid-learning. The articles are as follows:

* Simple selectors
* Attribute selectors
* Pseudo-classes and pseudo-elements
* Combinators and multiple selectors

You are strongly advised to tackle simple selectors first, in case you miss any pertinent information.

