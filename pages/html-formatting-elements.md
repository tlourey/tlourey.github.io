---
title: HTML Formatting Elements
description: TBA
published: false
categories:
    - Tech
type: pages
layout: pages
date: 2025-03-12T02:31:01.751Z
lastmod: 2025-03-12T06:21:52.982Z
tags:
    - Language
    - References
    - Tips
    - Writing
    - Communication
isdraft: true
fmContentType: pages
mermaid: false
preview: ""
---

<!--- cSpell:disable --->
* [Common Elements](#common-elements)
* [Italics](#italics)
* [Strong, Mark and Bold](#strong-mark-and-bold)
* [Underline](#underline)
* [Highlight](#highlight)
* [Small](#small)
* [Strikethrough](#strikethrough)
<!--- cSpell:enable --->

<!--<!-- markdownlint-disable-file MD033 -->

## Common Elements

Formatting elements were designed to display special types of text:

```html
<b> - Bold text
<strong> - Important text
<i> - Italic text
<em> - Emphasized text (italics?)
<mark> - Marked text (highlighted)
<small> - Smaller text
<del> - Deleted text (strike through)
<ins> - Inserted text (italics?)
<sub> - Subscript text
<sup> - Superscript text
```

## Italics

*Italics* is for emphasized text in a doc - `<em>` tag

## Strong, Mark and Bold

The `<strong>` tag is used to define text with **strong** importance. The content inside is *typically* displayed in **bold**.

> [!TIP] TIP
> Tip: Use the `<b>` tag to specify bold text without any extra importance!

> [!NOTE] NOTE
> According to the HTML5 specification, the `<b>` tag should be used as a <ins>LAST</ins> resort when no other tag is more appropriate. The specification states that headings should be denoted with the `<h1>` to `<h6>` tags, emphasized text should be denoted with the `<em>` tag, important text should be denoted with the `<strong>` tag, and marked/highlighted text should be denoted with the `<mark>` tag.

## Underline

The `<u>` tag represents some text that is unarticulated and styled differently from normal text, such as misspelled words or proper names in Chinese text. The content inside is typically displayed with an <ins>underline</ins>. You can change this with CSS (see example below).

Tip: Avoid using the `<u>` element where it could be confused for a hyperlink!

## Highlight

`<mark>` to <mark>highlight</mark>

## Small

This is what <small>small</small> looks like.

> [!NOTE]
> This doesn't seem to work in the github native markdown viewer

## Strikethrough

This is what <del>strikethrough</del> looks like.
