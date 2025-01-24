---
title: Markdown Tips
description: Flavor Flav says "GFM is da shiz yo"
published: true
categories:
    - References
    - Language
type: pages
layout: pages
draft: true
date: 2025-01-17T13:40:00
lastmod: 2025-01-24T03:38:52.181Z
---


<!--- cSpell:disable --->
* [References](#references)
* [Important things to remember](#important-things-to-remember)
  * [Tables](#tables)
* [Not important things to remember](#not-important-things-to-remember)
  * [Collapsed Section](#collapsed-section)
  * [You can add a header](#you-can-add-a-header)
<!--- cSpell:enable --->

(TOC might be slightly weird)

## References

Super useful:

<https://github.github.com/gfm/>\
<https://docs.github.com/en/get-started/writing-on-github>

Less useful but still good:

<https://spec.commonmark.org/current/> the standard\
<https://markdown.github.io/> - documents various implementations\
<https://daringfireball.net/projects/markdown/>\
<https://en.wikipedia.org/wiki/Markdown>

## Important things to remember

### Tables

<https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/organizing-information-with-tables>

## Not important things to remember

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

### You can add a header

You can add text within a collapsed section.

You can add an image or a code block, too.

```ruby
   puts "Hello World"
```

</details>

<https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/organizing-information-with-collapsed-sections>
