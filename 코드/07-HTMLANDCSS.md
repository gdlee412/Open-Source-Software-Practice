# HTML & CSS

## Graphical User Interface (GUI)
The menu and stat commands we developed are command-line tools
- Command-line interface or CLI

Most modern user interfaces are graphical
- Graphical User Interface or GUI
- WIMP: Windows + Icons + Menu + Pointer

Benefits:
- Simplicity
- Learnable
- Easy interaction
- ...

## How to Develop?
No default programming language for GUI

There are popular combinations of PL & framework / library
- JavaScript & React (Web)
- TypeScript & React (web)
- Python & PyQt5
- Dart & Flutter
- C# & Universal Windows Platform

## Web based interfaces
Benefits:
- Cross-platform (desktop and mobile)
- Accessible (no installation)
- Easy to update
- versatile

Dev stack
- JavaScript
- HTML
- CSS

## Web frameworks
most modern development scenarios use frameworks
Framework: skeleton on which your application is built
- Your code is run by the framework
- Sometimes, the code borrows functions from a library

Types of frameworks:
- React
- Angular
- Vue
- Svelte
- ...

For this course:
- frameworks entirely change development patterns and may be confusing
- start with vanilla web development with no support; use only HTML, CSS, and JavaScript

## Big Picture
HTML: structure of a web page
CSS: style
JavaScript: interaction


# HyperText Markup Language or HTML
- standard markup language for documents designed to be displayed in a web browser

- .docx files are parsed and rendered by MS Word
- .html files are parsed and rendered by web browsers

- Human-readable
- Not a programming language

Prepend <view-source:> to a url to see the HTML code

## Tags
Tags: keywords that define how web browser will format and display the content

Tags are keywords inside angle brackets <>
- there are opening and closing tags. Closing tags always start with a slash </>
- Some tags do not have a closing. <img> is one of them
- you can nest tags (tag inside a tag)

## HTML 
HTML document must start with a doctype declaration
- <!DOCTYPE html>: HTML document is written in HTML 5 (the most recent version)

root tag must be <html>
Inside <html>, there must be the <head> and <body> tags

<head>: provides the metadata of the page, e.g., title, character set, styles, scripts,...
<body>: provides the content of the page. Tags in <body> are rendered on the screen

<!DOCTYPE html>
<html>
    <head>
        <title>Page Title</title>
        <style>
            /* CSS Code */
        </style>
    </head>
    <body>
        <!--HTML CODE -->
        <script>
            /* JS CODE */
        </script>
    </body>
</html>


##  Headings
<h1>: main heading
<h2> ... <h6>: sub headings / headings for sections


## Paragraphs, Emphasis, and Hyperlinks
<p>: paragraph (has a bottom margin by default)
<strong> and <em>: emphasize text (bold and italics respectively)
<a> : creates a hyperlink
    Set the "href" attribute to designate the url

<p>
    This is a <em>sample</em> <strong>paragraph</strong>.
    Click <a href="www.google.com">here</a> to go to Google.
</p>
<p>
    Second paragraph!
</p>

## Lists
<ul>: unordered lists
- like
- this
- one

<ol>: ordered lists
1. Like
2. This
3. One

<li>: specifies a list item

## Image
<img>: puts an image in a HTML document, set the size using width and height attributes

## Table
<table>: creates a table
<tr>: table row
<th>: table header cell
<td>: table cell

## Grouping
<div>: group or block of tags. By default, it does not affect the rendering (transparent)

apply CSS rules to layout the elements in <div> (e.g., flexbox)

<header>, <nav>, <section>,...: Same as <div>, but define the semantic of Tags

## Tags you must know
<a href="url">Click me</a>: hyperlink
<body> and <head>
<em>text</em> emphasizes text (italic by default)
<h1> to <h6> for titles
<img src="url to image"> includes an image
<ol> and <ul> for ordered and unordered lists
<li> represents a list item in <ol> or <ul>
<p> for paragraphs
<strong> defines text with strong importance (bold by default)


# CSS
Cascading Style Sheets or CSS: style sheet language used for describing the presentation of a document written in a markup language such as HTML
CSS file is a human-readable text fileS

## CSS Rule
CSS file consists of multiple CSS Rules
Rule = Selector + (Property and Value)

## CSS Selector
selector specifies which tags the following rule applies.
many selector types, but 3 most important for now: 
1. by tag name (for all tags with the tag type)
    e.g. <p>
        <style>
            p{}
2. by class name (used for only a couple of tags)
    e.g. <p class="targets">
        <p class="targets">
        <style>
            .targets{}
3. by id (used for only one tag)
    e.g. <p id="target">
        <style>
            #target{}

### Combining Selectors
#wrapper .content: select tags that have class name "content" under an element whose id is "wrapper"(notice the space between the two selectors)

p.highlight: select all p tags that have a class name "highlight"

#wrapper.bordered: selects an element whose id is "wrapper" and has a class name "bordered" (no space between selectors)

## CSS in HTML 
3 ways to use CSS in an HTML document:
1. Using a <link> tag
    - Create a separate CSS file
    - Add a <link> tag to the <body> tag
    <link rel="stylesheet" href="styles.css">
    (assuming the HTML and CSS files are in the same directory)
    
2. Using a <style> tag
    - Embed CSS rules in the <style> tag
    - can be placed anywhere, but usually in the <head> tag

3. Using the style attribute
    - Embed CSS rules for each HTML element using the style attribute
    - Inline style
    - Inline styles are very strong. They even override rules set by an id selector.

## Text Styling
color: <color code>
font-weight: normal/bold
text-decoration: none/underline
font-style: normal/italic
font-size: <size>
text-align: left/center/right

<span>: style only sections within a tag

## Defining a Size
When you need to define a size:
px: pixels
em: a unit of measurement, 1 em = current font size
rem: root em. same as em without inheritance
%: percentages

## Margin and Padding
Margin: outer spacing
Padding: inner spacing

Order:
    Margin
        Border
            Padding
                Content
            Padding
        Border
    Margin

<margin: auto>: aligns the wrapper to the center

## Selector Specificity
When two rules conflict, the more specific rule is applied

#id > .class > tag name

add !important to the style declaration to override

<p id="main" class="content welcome">abc</p>
#main {color:red;}
.content {color:blue;}
p {color:green !important;}

## Debuggin CSS
CSS rules sometimes don't apply

Menu -> Tools -> Developer Tool
If Chrome on Windows, press <F12>

In the "Elements" tab, you can see the HTML code that your browser is showing currently

Can change values or apply new styles applied to the element

Box model
- Margin and padding

Hierarchy
- html > body > div#wrapper

## Tips
Sometimes, your page does not update even though you changed the source code.
This can be a cache issue
Open DevTool -> Go to Network -> Check "Disable cache"
    - Works only when DevTool is open. So keep it open

# Summary: HTML & CSS
HTML: structure of a web page
CSS: style
JavaScript: interaction

HTML document consists of tags (hierarchy!)
    <html><head><body><p><ul><li><img><table>...

CSS Rule = selector + (property: value)
- ID selector: #id, class selector:.class, tag name selector: tag_name
- Properties: color, margin, padding, background, font-size,...
- Selector Specificity