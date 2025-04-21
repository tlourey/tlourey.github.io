---
title: Markdown Tips
description: Flavor Flav says "GFM is da shiz yo"
published: true
categories:
    - Tech
type: pages
layout: pages
isdraft: false
date: 2025-01-17T13:40:00
lastmod: 2025-04-21T23:22:09.342Z
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
    * [Issues with Codeblocks after Alerts](#issues-with-codeblocks-after-alerts)
  * [Keyboard tags](#keyboard-tags)
  * [Github Pages](#github-pages)
  * [Wikis](#wikis)
* [Not important things to remember](#not-important-things-to-remember)
  * [Emojis in Markdown](#emojis-in-markdown)
  * [GFM Definition](#gfm-definition)
  * [Footnotes](#footnotes)
  * [Creating diagrams](#creating-diagrams)
  * [Collapsed Section](#collapsed-section)
    * [You can add a header](#you-can-add-a-header)
  * [Markdown Lint Exclusions](#markdown-lint-exclusions)
  * [Bug in Markdown all in one](#bug-in-markdown-all-in-one)
  * [VScode Underline](#vscode-underline)
  * [Extended Syntax](#extended-syntax)
  * [Useless by cool](#useless-by-cool)
    * [ASCII STL](#ascii-stl)
<!--- cSpell:enable --->

(TOC might be slightly weird)

> [!TIP] TIP
> **Bold** means highly used

## References

Super useful:\
**<https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax#styling-text>**\
<https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax>
<https://docs.github.com/en/get-started/writing-on-github>\

<https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/quickstart-for-writing-on-github> - i can't remember if the quick start was useful or not\
<https://github.com/github/markup/> - This library is the first step of a journey that every markup file in a repository goes on before it is rendered on GitHub.com\

Less useful but still good:

<https://github.github.com/gfm/> - Github Flavored Markdown. An older version of hte CommonMark Spec + Github Spec Extensions\
<https://spec.commonmark.org/current/> the standard\
<https://daringfireball.net/projects/markdown/>\
<https://en.wikipedia.org/wiki/Markdown>\
<https://markdown.github.io/> - is supposed to documents various implementations but I think this is actually dead

## Important things to remember

### Tables

```markdown
| First Header  | Second Header |
| ------------- | ------------- |
| Content Cell  | Content Cell  |
| Content Cell  | Content Cell  |
```

| First Header  | Second Header |
| ------------- | ------------- |
| Content Cell  | Content Cell  |
| Content Cell  | Content Cell  |

```markdown
| Left-aligned | Center-aligned | Right-aligned |
| :---         |     :---:      |          ---: |
| `git status`   | *git status*     | \|    |
| git diff     | git diff       | **git diff**      |
```

| Left-aligned | Center-aligned | Right-aligned |
| :---         |     :---:      |          ---: |
| `git status`   | *git status*     | \|    |
| git diff     | git diff       | **git diff**      |

<https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/organizing-information-with-tables>

### Code Blocks

From: <https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/creating-and-highlighting-code-blocks#syntax-highlighting>

> [!TIP] TIP
> When you create a fenced code block that you also want to have syntax highlighting on a GitHub Pages site, use lower-case language identifiers. For more information, see [About GitHub Pages and Jekyll](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll#syntax-highlighting).

> GitHub use [Linguist](https://github.com/github-linguist/linguist) to perform language detection and to select [third-party grammars](https://github.com/github-linguist/linguist/blob/main/vendor/README.md) for syntax highlighting. You can find out which keywords are valid in the [languages YAML file](https://github.com/github-linguist/linguist/blob/main/lib/linguist/languages.yml).

### Alerts

<https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax#alerts>

> [!IMPORTANT] IMPORTANT
> Alerts on Github pages: Alerts don't work on github pages but they do when reading readme.md in an github repo, but it doesn't seem they work when viewing various other markdown files.

#### Issue with Alert Titles

27/01/25: With absolutly 0 research, I think i've found a bug with Markdown alerts on Github (not github pages which won't render them unless you use a plugin).

An alert with no title gets rended in Github correctly.

> [!TIP]
> Here is a tip with no title

But an alert with a title does not get rended in github correctly.

> [!TIP] Alert with title
> An alert with a title doesn't get rended correctly.

~~But I think both are standards compliant.~~ 3/02/25: Its not. Read below.

3/0/25: Not a bug, just not a part of the 2 main specs (CommonMark and GFM) in use but does seem to have a lot of support and works in some extensions and some systems.

<https://github.com/orgs/community/discussions/16925> - where alerts first got introduced\
<https://github.com/orgs/community/discussions/48797>\
<https://github.com/orgs/community/discussions/103219>

#### Issues with Codeblocks after Alerts

22/04/25: With absolutly 0 research, if you have a codeblock **right** after an alert it doesn't seem to render in Jekyll (at least with cayman). This may be more of an issue with Jekyll & Cayman than markdown or github but I'm putting it here for now.

This code block doesn't render: <https://github.com/tlourey/tlourey.github.io/blob/ffcdcdc5d37ded1578c40316a725cd5427cd886f/pages/windows-commands.md?plain=1#L72> in Jekyll. Not sure if its cause its type of bat or because its right after a code block

### Keyboard tags

> *The \<kbd\> element represents user input (typically keyboard input, although it may also be used to represent other input, such as voice commands).*\
> \- <https://www.w3.org/TR/2017/REC-html52-20171214/textlevel-semantics.html#the-kbd-element>

Also: <https://developer.mozilla.org/en-US/docs/Web/HTML/Element/kbd>

```markdown
<kbd>CTRL</kbd> + <kbd>ALT</kbd> + <kbd>DEL</kbd> + <kbd>Left-Click</kbd>
```

<kbd>CTRL</kbd> + <kbd>ALT</kbd> + <kbd>DEL</kbd>

To describe an input comprised of multiple keystrokes, you can nest multiple \<kbd\> elements, with an outer \<kbd\> element representing the overall input and each individual keystroke or component of the input enclosed within its own <kbd>.

```markdown
You can also create a new document using the <kbd><kbd>Ctrl</kbd>+<kbd>N</kbd></kbd> keyboard shortcut.
```

You can also create a new document using the <kbd><kbd>Ctrl</kbd>+<kbd>N</kbd></kbd> keyboard shortcut.

<!-- markdownlint-disable MD033-->
Nesting a \<kbd\> element inside a \<samp\> element represents input that has been echoed back to the user by the system.

```markdown
<kbd><kbd><samp>File</samp></kbd>⇒<kbd><samp>New Document</samp></kbd></kbd>
```

<kbd><kbd><samp>File</samp></kbd>⇒<kbd><samp>New Document</samp></kbd></kbd>

[\<samp\>: The Sample Output element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/samp)
<!-- markdownlint-enable MD033-->

Want a whole Keyboard? copy from this comment <https://meta.stackexchange.com/a/311579>

### Github Pages

[Github Pages Documentation](https://docs.github.com/en/pages)

[Github Pages supported themes](https://pages.github.com/themes/)\
[Jekyll Plugins that are whitelisted at github pages](https://pages.github.com/versions/)\
[GitHub Pages plugins that are enabled by default and cannot be disabled](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll#:~:text=GitHub%20Pages%20uses%20plugins%20that%20are%20enabled%20by%20default%20and%20cannot%20be%20disabled)\
[Github pages configuration that cannot be changed](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll#:~:text=Some%20configuration%20settings%20cannot%20be%20changed%20for%20GitHub%20Pages%20sites)

Also something to consider: Changing your Markdown processor <https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/setting-a-markdown-processor-for-your-github-pages-site-using-jekyll>

For _config.yml

```YAML
markdown: kramdown
```

### Wikis

* Not all Github markdown is supported in wikis apparently[^1].

[^1]: <https://docs.github.com/en/enterprise-cloud@latest/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax#footnotes:~:text=Footnotes%20are%20not%20supported%20in%20wikis.>

## Not important things to remember

### Emojis in Markdown

<https://www.markdownguide.org/extended-syntax/#emoji>\
<https://gist.github.com/rxaviers/7360908> - random emoji shortcut reference

> [!TIP] Static Site Generator
> If you're using a static site generator (Jekyll, Hugo, etc), make sure you [encode HTML pages as UTF-8](https://www.w3.org/International/tutorials/tutorial-char-enc/).

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

> [!NOTE] NOTE
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

### Markdown Lint Exclusions

If you are using markdownlint package or extension, you may want to exclude some specific rules, or at last adjust them at times. Example, I want markdown lint to show me inline html but not if its just an underline.

We can see that at <https://github.com/DavidAnson/markdownlint/blob/main/doc/md033.md> that rule MD033 has a parameter for allowed elements.

for an example of this refer to [VSCode Settings and Extensions](vscode-settings-and-extensions.md#allow-some-inline-html)

### Bug in Markdown all in one

When using the [Markdown All in One](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one) extension in VS Code, and using the Table of Contents, it may do weird things if you have an intended code block inside an ordered list if the intending is not perfect.

<https://github.com/tlourey/tlourey.github.io/commit/1ce91e004eca6ccb70b683c0e50895acdb879ea2> shows the slight intending change of the code block fixing up the table of contents.

### VScode Underline

VSCode doesn't have a keyboard shortcut for underline, at least not for markdown. You can try my snippet and keyboard shortcut from [VSCode Settings and Extensions](vscode-settings-and-extensions.md#ctrlu-underline-in-markdown)

### Extended Syntax

<https://www.markdownguide.org/extended-syntax/> - not always supported

==highlighted== is sometimes `==highlighted==`\
H~2~O is sometimes `H~2~O`\

First Term
: This is the definition of the first term.

Second Term
: This is one definition of the second term.
: This is another definition of the second term.

```markdown
First Term
: This is the definition of the first term.

Second Term
: This is one definition of the second term.
: This is another definition of the second term.
```


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
