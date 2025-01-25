---
title: Markdown Tips
description: Flavor Flav says "GFM is da shiz yo"
published: true
categories:
  - Tech
type: pages
layout: pages
draft: true
date: 2025-01-17T13:40:00
lastmod: 2025-01-24T03:38:52.181Z
tags:
  - Language
  - References
---


<!--- cSpell:disable --->
* [References](#references)
* [Important things to remember](#important-things-to-remember)
  * [Tables](#tables)
  * [Code Blocks](#code-blocks)
  * [Alerts](#alerts)
* [Not important things to remember](#not-important-things-to-remember)
  * [Creating diagrams](#creating-diagrams)
  * [Collapsed Section](#collapsed-section)
    * [You can add a header](#you-can-add-a-header)
  * [Useless by cool](#useless-by-cool)
    * [ASCII STL](#ascii-stl)
<!--- cSpell:enable --->

(TOC might be slightly weird)

## References

Super useful:

<https://github.github.com/gfm/>\
<https://docs.github.com/en/get-started/writing-on-github>\
<https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax>\
<https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax#styling-text>

Less useful but still good:

<https://spec.commonmark.org/current/> the standard\
<https://markdown.github.io/> - documents various implementations\
<https://daringfireball.net/projects/markdown/>\
<https://en.wikipedia.org/wiki/Markdown>

## Important things to remember

### Tables

<https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/organizing-information-with-tables>

### Code Blocks

From: <https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/creating-and-highlighting-code-blocks#syntax-highlighting>

> [!TIP] Tip
> When you create a fenced code block that you also want to have syntax highlighting on a GitHub Pages site, use lower-case language identifiers. For more information, see [About GitHub Pages and Jekyll](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll#syntax-highlighting).

> GitHub use [Linguist](https://github.com/github-linguist/linguist) to perform language detection and to select [third-party grammars](https://github.com/github-linguist/linguist/blob/main/vendor/README.md) for syntax highlighting. You can find out which keywords are valid in the [languages YAML file](https://github.com/github-linguist/linguist/blob/main/lib/linguist/languages.yml).

### Alerts

<https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax#alerts>

> [!IMPORTANT] Alerts on Github pages
> Alerts don't work on github pages but they do in the github viewer

## Not important things to remember

### Creating diagrams

<https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/creating-diagrams>\
<https://asciiflow.com/>

### Collapsed Section

````markdown
<details>

<summary>Tips for collapsed sections</summary>

### You can add a header

You can add text within a collapsed section.

You can add an image or a code block, too.

```ruby
   puts "Hello World"
```

</details>
````

Looks like:

<details>

<summary>Tips for collapsed sections</summary>

#### You can add a header

You can add text within a collapsed section.

You can add an image or a code block, too.

```ruby
   puts "Hello World"
```

</details>

> [!NOTE] Theme
> the above may not render correctly depending on the Jekyll theme in use but if you view it via github itself, it does seem to render correctly.

<https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/organizing-information-with-collapsed-sections>

### Useless by cool

#### ASCII STL

<!--- cSpell:disable --->
````markdown
```stl
solid cube_corner
  facet normal 0.0 -1.0 0.0
    outer loop
      vertex 0.0 0.0 0.0
      vertex 1.0 0.0 0.0
      vertex 0.0 0.0 1.0
    endloop
  endfacet
  facet normal 0.0 0.0 -1.0
    outer loop
      vertex 0.0 0.0 0.0
      vertex 0.0 1.0 0.0
      vertex 1.0 0.0 0.0
    endloop
  endfacet
  facet normal -1.0 0.0 0.0
    outer loop
      vertex 0.0 0.0 0.0
      vertex 0.0 0.0 1.0
      vertex 0.0 1.0 0.0
    endloop
  endfacet
  facet normal 0.577 0.577 0.577
    outer loop
      vertex 1.0 0.0 0.0
      vertex 0.0 1.0 0.0
      vertex 0.0 0.0 1.0
    endloop
  endfacet
endsolid
```
````

```stl
solid cube_corner
  facet normal 0.0 -1.0 0.0
    outer loop
      vertex 0.0 0.0 0.0
      vertex 1.0 0.0 0.0
      vertex 0.0 0.0 1.0
    endloop
  endfacet
  facet normal 0.0 0.0 -1.0
    outer loop
      vertex 0.0 0.0 0.0
      vertex 0.0 1.0 0.0
      vertex 1.0 0.0 0.0
    endloop
  endfacet
  facet normal -1.0 0.0 0.0
    outer loop
      vertex 0.0 0.0 0.0
      vertex 0.0 0.0 1.0
      vertex 0.0 1.0 0.0
    endloop
  endfacet
  facet normal 0.577 0.577 0.577
    outer loop
      vertex 1.0 0.0 0.0
      vertex 0.0 1.0 0.0
      vertex 0.0 0.0 1.0
    endloop
  endfacet
endsolid
```
