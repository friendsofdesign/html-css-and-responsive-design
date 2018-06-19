# HTML Advanced Tables

### Adding a caption to your table with `<caption>`

You can give your table a caption by putting it inside a [`<caption>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/caption) element and nesting that inside the [`<table>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/table) element. You should put it just below the opening `<table>` tag.

```text
<table>
  <caption>Dinosaurs in the Jurassic period</caption>
​
  ...
</table>
```

As you can infer from the brief example above, the caption is meant to contain a description of the table contents. This is useful for all readers wishing to get a quick idea of whether the table is useful to them as they scan the page, but particularly for blind users. Rather than have a screenreader read out the contents of many cells just to find out what the table is about, he or she can rely on a caption and then decide whether or not to read the table in greater detail.

A caption is placed directly beneath the **`<table>`** tag.

**Note**: The `summary` attribute can also be used on the `<table>` tag to provide a description — this is also read out by screenreaders. We'd recommend using the `<caption>` element instead, however, as `summary`is [deprecated](https://developer.mozilla.org/en-US/docs/Glossary/deprecated) by the HTML5 spec, and can't be read by sighted users \(it doesn't appear on the page.\)

**Active learning: Adding a caption**

Let's try this out, revisiting an example we first met in the previous article.

1. Open up your language teacher's school timetable from the end of [HTML Table Basics](https://developer.mozilla.org/en-US/docs/Learn/HTML/Tables/Basics#Active_learning_colgroup_and_col), or make a local copy of our [timetable-fixed.html](https://github.com/mdn/learning-area/blob/master/html/tables/basic/timetable-fixed.html) file.
2. Add a suitable caption for the table.
3. Save your code and open it in a browser to see what it looks like.

**Note**: You can find our version on GitHub — see [timetable-caption.html](https://github.com/mdn/learning-area/blob/master/html/tables/advanced/timetable-caption.html) \([see it live also](http://mdn.github.io/learning-area/html/tables/advanced/timetable-caption.html)\).

#### Adding structure with `<thead>`, `<tfoot>`, and `<tbody>`

As your tables get a bit more complex in structure, it is useful to give them more structural definition. One clear way to do this is by using ,`<thead>` , `<tfoot>` and `<tbody>`, which allow you to mark up a header, footer, and body section for the table.

These elements don't make the table any more accessible to screenreader users, and don't result in any visual enhancement on their own. They are however very useful for styling and layout — acting as useful hooks for adding CSS to your table. To give you some interesting examples, in the case of a long table you could make the table header and footer repeat on every printed page, and you could make the table body display on a single page and have the contents available by scrolling up and down.

To use them:

* The `<thead>` element needs to wrap the part of the table that is the header — this will commonly be the first row containing the column headings, but this is not necessarily always the case. if you are using `<col>`/`<colgroup>` element, the table header should come just below those.
* The `<tfoot>` element needs to wrap the part of the table that is the footer — this might be a final row with items in the previous rows summed, for example. You can include the table footer right at the bottom of the table as you'd expect, or just below the table header \(the browser will still render it at the bottom of the table\).
* The `<tbody>` element needs to wrap the other parts of the table content that aren't in the table header or footer. It will appear below the table header or sometimes footer, depending on how you decided to structure it \(see the notes above\).

**Note**: `<tbody>` is always included in every table, implicitly if you don't specify it in your code. To check this, open up one of your previous examples that doesn't include `<tbody>` and look at the HTML code in your [browser developer tools](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_are_browser_developer_tools) — you will see that the brower has added this tag for you. You might wonder why you ought to bother including it at all — you should, because it gives you more control over your table structure and styling.

**Active learning: Adding table structure**

Let's put these new elements into action.

1. First of all, make a local copy of [spending-record.html](https://github.com/mdn/learning-area/blob/master/html/tables/advanced/spending-record.html) and [minimal-table.css](https://github.com/mdn/learning-area/blob/master/html/tables/advanced/minimal-table.css) in a new folder.
2. Try opening it in a browser — You'll see that it looks OK, but it could stand to be improved. The "SUM" row that contains a summation of the spent amounts seems to be in the wrong place, and there are some details missing from the code.
3. Put the obvious headers row inside a `<thead>` element, the "SUM" row inside a `<tfoot>`element, and the rest of the content inside a `<tbody>` element.
4. Save and refresh, and you'll see that adding the `<tfoot>` element has caused the "SUM" row to go down to the bottom of the table.
5. Next, add a `colspan` attribute to make the "SUM" cell span across the first four columns, so the actual number appears at the bottom of the "Cost" column.
6. Let's add some simple extra styling to the table, to give you an idea of how useful these elements are for applying CSS. Inside the head of your HTML document, you'll see an empty `<style>` element. Inside this element, add the following lines of CSS code:

   ```text
   tbody {
     font-size: 90%;
     font-style: italic;
   }
   ​
   tfoot {
     font-weight: bold;
   }
   ```

7. Save and refresh, and have a look at the result. If the `<tbody>` and `<tfoot>` elements weren't in place, you'd have to write much more complicated selectors/rules to apply the same styling.

**Note**: We don't expect you to fully understand the CSS right now. You'll learn more about this when you go through our CSS modules \([Introduction to CSS](https://developer.mozilla.org/en-US/docs/Learn/CSS/Introduction_to_CSS) is a good place to start; we also have an article specifically on [styling tables](https://developer.mozilla.org/en-US/docs/Learn/CSS/Styling_boxes/Styling_tables)\).

Your finished table should look something like the following:

\[TABLE IMG\]

**Note**: You can also find it on Github as [spending-record-finished.html](https://github.com/mdn/learning-area/blob/master/html/tables/advanced/spending-record-finished.html) \([see it live also](http://mdn.github.io/learning-area/html/tables/advanced/spending-record-finished.html)\).

#### Nesting Tables

It is possible to nest a table inside another one, as long as you include the complete structure, including the `<table>` element. This is generally not really advised, as it makes the markup more confusing and less accessible to screenreader users, and in many cases you might as well just insert extra cells/rows/columns into the existing table. It is however sometimes necessary, for example if you want to import content easily from other sources.

The following markup shows a simple nested table:

```text
<table id="table1">
  <tr>
    <th>title1</th>
    <th>title2</th>
    <th>title3</th>
  </tr>
  <tr>
    <td id="nested">
      <table id="table2">
        <tr>
          <td>cell1</td>
          <td>cell2</td>
          <td>cell3</td>
        </tr>
      </table>
    </td>
    <td>cell2</td>
    <td>cell3</td>
  </tr>
  <tr>
    <td>cell4</td>
    <td>cell5</td>
    <td>cell6</td>
  </tr>
</table>
```

The output of which looks something like this:

\[TABLE IMG\]

#### Tables for visually impaired users

Let's recap briefly on how we use data tables. A table can be a handy tool, for giving us quick access to data and allowing us to look up different values. For example, It takes only a short glance at the table below to find out how many rings were sold in Gent last August. To understand its information we make visual associations between the data in this table and its column and/or row headers.

**Items Sold August 2016**

\[TABLE\]

But what if you cannot make those visual associations? How then can you read a table like the above? Visually impaired people often use a screenreader that reads out information on web pages to them. This is no problem when you're reading plain text but interpreting a table can be quite a challenge for a blind person. Nevertheless, with the proper markup we can replace visual associations by programmatic ones.

This section of the article provides further techniques for making tables as accessible as possible.

#### Using column and row headers

Screenreaders will identify all headers and use them to make programmatic associations between those headers and the cells they relate to. The combination of column and row headers will identify and interpret the data in each cell so that screenreader user can interpret the table similarly to how a sighted user does.

We already covered headers in our previous article — see [Adding headers with `<th>` elements](https://developer.mozilla.org/en-US/docs/Learn/HTML/Tables/Basics#Adding_headers_with_%3Cth%3E_elements).

#### The scope attribute

A new topic for this article is the `scope` attribute, which can be added to the `<th>` element to tell screenreaders exactly what cells the header is a header for — is it a header for the row it is in, or the column, for example? Looking back to our spending record example from earlier on, you could unambiguously define the column headers as column headers like this:

```text
<thead>
  <tr>
    <th scope="col">Purchase</th>
    <th scope="col">Location</th>
    <th scope="col">Date</th>
    <th scope="col">Evaluation</th>
    <th scope="col">Cost (€)</th>
  </tr>
</thead>
```

And each row could have a header defined like this \(if we added row headers as well as column headers\):

```text
<tr>
  <th scope="row">Haircut</th>
  <td>Hairdresser</td>
  <td>12/09</td>
  <td>Great idea</td>
  <td>30</td>
</tr>
```

Screenreaders will recognize markup structured like this, and allow their users to read out the entire column or row at once, for example.

`scope` has two more possible values — `colgroup` and `rowgroup`. these are used for headings that sit over the top of multiple columns or rows. If you look back at the "Items sold..." table at the start of this section of the article, you'll see that the "Clothes" cell sits above the "Trousers", "Skirts", and "Dresses" cells. All of these cells should be marked up as headers \(`<th>`\), but "Clothes" is a heading that sits over the top and defines the other three subheadings. "Clothes" therefore should get an attribute of `scope="colgroup"`, whereas the others would get an attribute of `scope="col"`.

#### The id and headers attributes

An alternative to using the `scope` attribute is to use `id` and `headers` attributes to create associations between headers and cells. The way they are used is as follows:

1. You add a unique `id` to each `<th>` element.
2. You add a `headers` attribute to each `<td>` element. Each `headers` attribute has to contain a list of the `id`s of all the `<th>` elements that act as a header for that cell, separated by spaces.

This gives your HTML table an explicit definition of the position of each cell in the table, defined by the header\(s\) for each column and row it is part of, kind of like a spreadsheet. For it to work well, the table really needs both column and row headers.

Returning to our spending costs example, the previous two snippets could be rewritten like this:

```text
<thead>
  <tr>
    <th id="purchase">Purchase</th>
    <th id="location">Location</th>
    <th id="date">Date</th>
    <th id="evaluation">Evaluation</th>
    <th id="cost">Cost (€)</th>
  </tr>
</thead>
<tbody>
<tr>
  <th id="haircut">Haircut</th>
  <td headers="location haircut">Hairdresser</td>
  <td headers="date haircut">12/09</td>
  <td headers="evaluation haircut">Great idea</td>
  <td headers="cost haircut">30</td>
</tr>
​
  ...
​
</tbody>
```

**Note**: This method creates very precise associations between headers and data cells but it uses **a lot** more markup and does not leave any room for errors. The `scope` approach is usually enough for most tables.

