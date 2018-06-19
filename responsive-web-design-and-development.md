# Responsive Web Design & Development

### Creating consistent design across multiple devices and media

#### Introduction to RWD

Responsive web design \(RWD\) is an approach toweb design aimed at crafting sites to provide anoptimal viewing and interaction experienceacross a wide range of devices.

**NB! Responsive web design is not when a website or appresponds to user interaction.**

Responsive was once called Liquid or Fluidlayout design.

#### Responsive Design & Media

Responsive design is not only used for multiple screen layouts and orientation, we can also control print, speech, projection, handheld and even tv media devices.

[https://www.w3.org/TR/CSS21/media.html\#at-media-rule](https://www.w3.org/TR/CSS21/media.html#at-media-rule)

#### The Meta Tag & Viewport

Before we begin adding media queries we need to ensure the browser knows our site ismeant to be responsive for this we use the following meta tag.

```text
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

We place this tag in the `<head>` area of our website to ensure the definition is read by

the browser.

We can also declare stylesheets per media type using the following `<link>` in the `<head>`.

```text
<link rel="stylesheet" media="mediatype and|not|only (media feature)" href="mystylesheet.css">
```

#### @media Queries Basics

Once we have prepared our document we can start declaring `@media` queries in ourCSS to ensure the page responds as we need it per device.

**Basic Syntax**

```text
@media not|only mediatype and (media feature) {
    Our CSS Rules;
}
```

Full list of media features: [http://www.w3schools.com/cssref/css3\_pr\_mediaquery.asp](http://www.w3schools.com/cssref/css3_pr_mediaquery.asp)

#### @media Queries Example

For our first basic example we will be making a `<div>` expand and shrink based on thescreen size - without using percentage sizing.

1\) Include the meta tag for viewport in your `<head>`2\) Create a `<div>` with class of “box” that has a blue background and width of 650px and height of 450px.

3\) Define `@media` queries that change the “box” to a smaller size when the “screen” media feature is max-widthof 768px and to a larger size when min-width is 1366px. Try changing the colour as well.

