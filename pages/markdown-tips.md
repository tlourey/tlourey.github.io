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
lastmod: 2025-01-27T12:28:25.088Z
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
    * [Issue with Alert Titles](#issue-with-alert-titles)
  * [Github Pages](#github-pages)
  * [Wikis](#wikis)
* [Not important things to remember](#not-important-things-to-remember)
  * [GFM Definition](#gfm-definition)
  * [Footnotes](#footnotes)
  * [Creating diagrams](#creating-diagrams)
  * [Collapsed Section](#collapsed-section)
    * [You can add a header](#you-can-add-a-header)
  * [Bug in Markdown all in one](#bug-in-markdown-all-in-one)
  * [Useless by cool](#useless-by-cool)
    * [ASCII STL](#ascii-stl)
<!--- cSpell:enable --->

(TOC might be slightly weird)

## References

Super useful:

<https://github.github.com/gfm/>\
<https://docs.github.com/en/get-started/writing-on-github>\
**<https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax>**\
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

> [!TIP]
> When you create a fenced code block that you also want to have syntax highlighting on a GitHub Pages site, use lower-case language identifiers. For more information, see [About GitHub Pages and Jekyll](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll#syntax-highlighting).

> GitHub use [Linguist](https://github.com/github-linguist/linguist) to perform language detection and to select [third-party grammars](https://github.com/github-linguist/linguist/blob/main/vendor/README.md) for syntax highlighting. You can find out which keywords are valid in the [languages YAML file](https://github.com/github-linguist/linguist/blob/main/lib/linguist/languages.yml).

### Alerts

<https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax#alerts>

> [!IMPORTANT]
> Alerts on Github pages: Alerts don't work on github pages but they do when reading readme.md in an github repo, but it doesn't seem they work when viewing various other markdown files.

#### Issue with Alert Titles

27/01/25: With absolute 0 research, I think i've found a bug with Markdown alerts on Github (not github pages which won't render them unless you use a plugin).

An alert with no title gets rended in Github correctly.

> [!TIP]
> Here is a tip with no title

But an alert with a title does not get rended in github correctly.

> [!TIP] Alert with title
> An alert with a title doesn't get rended correctly.

But I think both are standards compliant.

### Github Pages

[Github Pages supported themes](https://pages.github.com/themes/)\
[Jekyll Plugins that are whitelisted at github pages](https://pages.github.com/versions/)\
[GitHub Pages plugins that are enabled by default and cannot be disabled](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll#:~:text=GitHub%20Pages%20uses%20plugins%20that%20are%20enabled%20by%20default%20and%20cannot%20be%20disabled)\
[Github pages configuration that cannot be changed](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll#:~:text=Some%20configuration%20settings%20cannot%20be%20changed%20for%20GitHub%20Pages%20sites)

### Wikis

* Not all Github markdown is supported in wikis apparently[^1].

[^1]: <https://docs.github.com/en/enterprise-cloud@latest/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax#footnotes:~:text=Footnotes%20are%20not%20supported%20in%20wikis.>

## Not important things to remember

### GFM Definition

> GitHub Flavored Markdown, often shortened as GFM, is the dialect of Markdown that is currently supported for user content on GitHub.com and GitHub Enterprise.
>
> This formal specification, based on the CommonMark Spec, defines the syntax and semantics of this dialect.
>
> GFM is a strict superset of CommonMark. All the features which are supported in GitHub user content and that are not specified on the original CommonMark Spec are hence known as extensions, and highlighted as such.
>
> While GFM supports a wide range of inputs, it's worth noting that GitHub.com and GitHub Enterprise perform additional post-processing and sanitization after GFM is converted to HTML to ensure security and consistency of the website.

### Footnotes

<https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax#footnotes>

```markdown
Here is a simple footnote[^1].

A footnote can also have multiple lines[^2].

[^1]: My reference.
[^2]: To add line breaks within a footnote, prefix new lines with 2 spaces.
  This is a second line.
```

> [!NOTE]
> The position of a footnote in your Markdown does not influence where the footnote will be rendered. You can write a footnote right after your reference to the footnote, and the footnote will still render at the bottom of the Markdown. Footnotes are not supported in wikis.

### Creating diagrams

<https://asciiflow.com/>\
<https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/creating-diagrams>

* Mermaid only works in Github not github pages unless you make your own action to build the site

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

### Bug in Markdown all in one

When using the [Markdown All in One](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one) extension in VS Code, and using the Table of Contents, it may do weird things if you have an intended code block inside an ordered list if the intending is not perfect.

<https://github.com/tlourey/tlourey.github.io/commit/1ce91e004eca6ccb70b683c0e50895acdb879ea2> shows the slight intending change of the code block fixing up the table of contents.

### Useless by cool

#### ASCII STL

This gets rendered by GitHub but not Github pages

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
