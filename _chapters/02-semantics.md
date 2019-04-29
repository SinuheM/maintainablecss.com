---
layout: chapter
title: Semántica
section: Background
permalink: /chapters/semantics/
description: Why naming something based on what it is, instead of how it looks or behaves is the foundation of well architected and maintainable CSS.
---

Semantic HTML isn't only about the elements we use. It's quite obvious that we should use `<a>` for links, `<table>` for tabular data and `<p>` for paragraphs etc. What's less obvious is the names we use for classes.

As Phil Karton says, “there are only two hard things in Computer Science: cache invalidation and **naming things**.” So spending an entire chapter talking about it seems like an appropriate thing to do.

Naming is quite frankly the most important aspect of writing maintainable CSS. There are two main approaches: the semantic approach and the non-semantic approach. Let's discuss what they are.

## Semantic vs non-semantic

	<!-- non semantic -->
	<div class="red pull-left pb3">
	<div class="grid row">
	<div class="col-xs-4">

	<!-- semantic -->
	<div class="basket">
	<div class="product">
	<div class="searchResults">

Non-semantic classes don't convey *what* an element represents. At best, they give us an idea of what an element *looks* like. Atomic, visual, behavioural and utility classes are all forms of non-semantic classes.

Semantic classes don't convey their styles, but that's okay. That's what CSS is for. Semantic classes mean something to HTML, CSS, Javascript and automated functional tests.

Reasons why semantic classes work better:

## 1. Because they are readable

Here's a real snippet of HTML using atomic classes:

	<div class="pb3 pb4-ns pt4 pt5-ns mt4 black-70 fl-l w-50-l">
	  <h1 class="f4 fw6 f1-ns lh-title measure mt0">Heading</h1>
	  <p class="f5 f4-ns fw4 b measure dib-m lh-copy">Tagline</p>
	</div>

- It's easier to read words than abbreviations.  Abbreviations have to be broken down and mapped cognitively, assuming we know what they mean in the first place.
- It's hard to read the large cluster of class names. That's why CSS has syntax. We need to wade through many classes to work out what's happening; which classes override which; and which apply at certain break points etc.
- These classes are ambiguous. For example, does `black-70` refer to the colour or the background? If we need the inspector to find out, this implies the class names are not readable.
- The content is obfuscated by the surrounding HTML.

Here's the same thing using semantic classes:

	<div class="hero">
	  <h1 class="hero-title">Heading</h1>
	  <p class="hero-tagline">Tagline</p>
	</div>

- These classes are easy to read. No mental mapping is required.
- The content is no longer obfuscated.
- We know where the module begins and ends.
- The HTML is half the size.
- It's easy to read the CSS (in the inspector or in the file) because it has dedicated language constructs that exist for this purpose already.

## 2. Because it's easier to build responsive sites

Imagine coding a two-column responsive grid whereby:

* each column has `20px` and `50px` padding on small and large screens;
* each column has `2em` and `3em` font-size on small and large screens; and
* the columns stack on small screens. Note that *column* is now a misleading class name.

With visual/utility classes it looks like this:

	<div class="grid clearfix">
	  <div class="col pd20 pd50 fs2 fs3">Column 1</div>
	  <div class="col pd20 pd50 fs2 fs3">Column 2</div>
	</div>

- There are 7 classes, some of which override each other.
- To make the columns actually responsive we would need a `fs3large` class etc. This means using a naming convention that recreates language constructs already found and standardised in CSS.
- At certain break points, the classes are misleading and redundant. For example `.clearfix` doesn't clear on small screens.

A quick evaluation shows significant pain already.

With semantic classes it looks like this:

	<div class="thing">
	  <div class="thing-thingA"></div>
	  <div class="thing-thingB"></div>
	</div>

- These classes are encapsulated to the module's design and content.
- It's easy to style elements without having to write a multitude of classes and changing the HTML again.
- These classes are meaningful in small and big screens.
- Media queries can be used to clear elements only when needed.

> Question: How valuable is a codified responsive grid system? A [layout should adapt to the content](http://adamsilver.io/articles/stop-using-device-breakpoints/), not the other way around.

## 3. Because they are easier to find

Searching for HTML with a non-semantic class yields many results. As semantic classes are unique, a search yields only one result, making it easy to track down the HTML.

## 4. Because they eliminate the risk of regression

Updating a visual class could cause regression across a multitude of elements. Updating a semantic class only applies to the module in question, eliminating regression altogether.

## 5. Because visual classes aren't worth it

In some respects we may as well inline styles. This is more explicit and reduces the CSS footprint to zero. Inline CSS is a problem though, because we can't use media queries for example. And placing CSS in HTML mixes concerns and removes the ability to cache it.

> Question: Isn't `.red` the exact same abstraction that CSS already gives us for free with `color: red`?

## 6. Because they provide hooks for automated tests

Automated functional tests work by searching for, and interacting with elements. This may include:

1. clicking a link
2. finding a text box
3. typing in text
4. submitting a form
5. verifying some criteria

We can't use non-semantic classes to target specific elements. And adding hooks specifically for tests is wasteful as the user has to download this stuff.

## 7. Because they provide hooks for Javascript

We can't use non-semantic classes to target specific elements in order to enhance them with Javascript.

## 8. Because they don't need maintaining

If we name a thing based on what it is, we won't have to update the HTML again e.g. a heading is always a heading, no matter what it *looks* like.

With visual classes, both the HTML and the CSS need updating (assuming there aren't any selectors available for use).

## 9. Because they are easier to debug

Inspecting an element with a multitude of atomic classes, means wading through many selectors. With a semantic class, there's only one, making it far easier to work with.

## 10. Because the standards recommend it

On using the class attribute, HTML5 specs say in 3.2.5.7:

> "[...] authors are encouraged to use values that describe the nature of the content, rather than values that describe the desired presentation of the content."

## 11. Because styling state is easier

Consider the following HTML:

	<a class="padding-left-20 red" href="#"></a>

Changing the padding and colour on hover is a difficult task. It's better to avoid having to fix self-induced problems like this.

## 12. Because they produce a small HTML footprint

As we've seen above, atomic classes bloat HTML. Semantic classes result in smaller HTML. And whilst the CSS may increase in size, it's cacheable.

## Final thought

Semantic classes are a corner stone of *MaintainableCSS*. Without them, everything else makes little sense. Name something based on what it is and everything else falls into place.