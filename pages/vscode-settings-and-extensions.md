---
title: VSCode Settings and Extensions
description: ""
published: false
categories:
    - Tech
type: pages
layout: pages
date: 2025-02-02T03:50:07.720Z
lastmod: 2025-02-27T11:22:49.169Z
tags:
    - VSCode
draft: true
fmContentType: pages
preview: ""
---


<!-- cSpell:ignore ignoreword,ignorewords,yzhang -->

<!--- cSpell:disable --->
* [Settings](#settings)
* [Extensions](#extensions)
  * [vscode-spell-checker](#vscode-spell-checker)
    * [vscode-spell-checker Commands](#vscode-spell-checker-commands)
    * [vscode-spell-checker Notes](#vscode-spell-checker-notes)
    * [vscode-spell-checker Tips](#vscode-spell-checker-tips)
    * [vscode-spell-checker References](#vscode-spell-checker-references)
  * [Markdown all in one](#markdown-all-in-one)
    * [Markdown all in one Commands](#markdown-all-in-one-commands)
    * [Markdown all in one Notes](#markdown-all-in-one-notes)
      * [Bug in Markdown all in one](#bug-in-markdown-all-in-one)
    * [Markdown all in one Tips](#markdown-all-in-one-tips)
    * [Markdown all in one References](#markdown-all-in-one-references)
<!--- cSpell:enable --->

## Settings

`"editor.renderWhitespace": "all",` \
`"editor.renderControlCharacters": true,`: useful for rendering UNICODE Characters that sometimes are not good including invisible characters

## Extensions

### vscode-spell-checker

<https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker>\
<https://streetsidesoftware.com/vscode-spell-checker/>
<https://cspell.org/>

#### vscode-spell-checker Commands

#### vscode-spell-checker Notes

* cspell.ignorewords: Ignore that specific combination or letters
* cspell.words: mark the word as correct and use as a suggestion
* cspell.flagWords - list of words to be always considered incorrect. This is useful for offensive words and common spelling errors. For example "hte" should be "the"

* [ ] determine when best to use a custom dictionary at both user level and repo level (is it really just to reduce space)

#### vscode-spell-checker Tips

* Install your native language dictionary addon if it isn't in the [supported languages list](https://streetsidesoftware.com/vscode-spell-checker/#supported-languages): <https://streetsidesoftware.com/vscode-spell-checker/#language-dictionaries>
* Install your technical / coding language plugin: <https://streetsidesoftware.com/vscode-spell-checker/#technical-dictionaries>
* Ensure vscode-spell-checker uses it. You should make sure this is specifically enabled. eg:

  ```json
  "cSpell.dictionaries": [
    "markdown"
  ],
  ```

* Consider what is a ignoreword for yourself vs the project/repo - also consider that an ignoreword doesn't check checked for plurals
* Consider what is a valid word to use as a suggestion for yourself vs the project/repo
  * If you are the only one who makes that error and you make it in multiple repos, it may be best in your settings so it applies to all your workspaces
* Consider if it only applies to a line, section, whole file, the whole repo, or just you personally: <https://streetsidesoftware.com/vscode-spell-checker/#enable--disable-checking-sections-of-code>
* While I don't do this, there is some mention of creating a cspell.json in your repo with some of the settings. This allows other IDEs that use cspell to get the correct dictionaries, language, settings, etc - even if they don't use VSCode.
* Spend some time configuring parts of vscode-spell-checker at both user and repo level things like
  * Disable programming languages/supported filetypes at user level that you don't use `cSpell.enableFiletypes`

#### vscode-spell-checker References

<https://cspell.org/configuration/>\
<https://streetsidesoftware.com/vscode-spell-checker/docs/configuration>\
<https://github.com/streetsidesoftware/cspell-dicts/tree/main/dictionaries> - list of all available dictionaries.\
<https://cspell.org/configuration/document-settings/#inline-document-settings> - inline comments to control cspell

### Markdown all in one

<https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one>\
<vscode:extension/yzhang.markdown-all-in-one>

#### Markdown all in one Commands

[Full list here](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one#available-commands) but my fav *manual* ones are:

* Markdown All in One: Create Table of Contents
* Markdown All in One: Update Table of Contents

#### Markdown all in one Notes

* Does a lot of things itself which helps.

##### Bug in Markdown all in one

When using the [Markdown All in One](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one) extension in VS Code, and using the Table of Contents, it may do weird things if you have an intended code block inside an ordered list if the intending is not perfect.

<https://github.com/tlourey/tlourey.github.io/commit/1ce91e004eca6ccb70b683c0e50895acdb879ea2> shows the slight intending change of the code block fixing up the table of contents.

#### Markdown all in one Tips

Useful settings:

* `"markdown.extension.toc.unorderedList.marker": "*",`: Gives a preference\
* `"markdown.extension.toc.levels": "2..6",`: makes any markdown table of contents exclude the title\
* `"markdown.extension.completion.enabled": true,`: helps markdown snippets behave more.\
* `"markdown.extension.preview.autoShowPreviewToSide": false,`: Sometimes, given a particular workflow, task or repo, this could be useful\

#### Markdown all in one References

Full settings on marketplace base:<https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one#supported-settings>
