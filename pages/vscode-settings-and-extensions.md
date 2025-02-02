---
title: VSCode Settings and Extensions
description: ""
published: false
categories:
    - Tech
type: pages
layout: pages
date: 2025-02-02T03:50:07.720Z
lastmod: 2025-02-02T04:45:46.508Z
tags:
    - VSCode
draft: true
fmContentType: pages
preview: ""
---


<!-- cSpell:ignore ignoreword,ignorewords -->

<!--- cSpell:disable --->
* [vscode-spell-checker](#vscode-spell-checker)
  * [vscode-spell-checker Commands](#vscode-spell-checker-commands)
  * [vscode-spell-checker Notes](#vscode-spell-checker-notes)
  * [vscode-spell-checker Tips](#vscode-spell-checker-tips)
  * [vscode-spell-checker References](#vscode-spell-checker-references)
<!--- cSpell:enable --->

## vscode-spell-checker

<https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker>\
<https://streetsidesoftware.com/vscode-spell-checker/>
<https://cspell.org/>

### vscode-spell-checker Commands

### vscode-spell-checker Notes

* cspell.ignorewords: Ignore that specific combination or letters
* cspell.words: mark the word as correct and use as a suggestion

### vscode-spell-checker Tips

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
* Consider if it only applies to a line, section, file or the whole repo: <https://streetsidesoftware.com/vscode-spell-checker/#enable--disable-checking-sections-of-code>

### vscode-spell-checker References

<https://cspell.org/configuration/>
