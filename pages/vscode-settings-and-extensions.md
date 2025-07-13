---
title: VSCode Settings and Extensions
description: TBC
published: true
categories:
    - Tech
type: pages
layout: pages
date: 2025-02-02T03:50:07.720Z
lastmod: 2025-05-13T10:09:15.200Z
tags:
    - VSCode
    - Tools
isdraft: true
fmContentType: pages
preview: ""
---

<!-- cSpell:ignore ignoreword,ignorewords,yzhang Anson -->

<!--- cSpell:disable --->
* [Settings](#settings)
* [Shortcuts often forgotten](#shortcuts-often-forgotten)
* [Custom Keyboard Shortcuts](#custom-keyboard-shortcuts)
  * [CTRL+U: Underline in Markdown](#ctrlu-underline-in-markdown)
  * [References](#references)
* [Extensions](#extensions)
  * [vscode-spell-checker](#vscode-spell-checker)
    * [vscode-spell-checker Commands](#vscode-spell-checker-commands)
    * [vscode-spell-checker Notes](#vscode-spell-checker-notes)
    * [vscode-spell-checker Tips](#vscode-spell-checker-tips)
      * [vscode-spell-checker Tips for Markdown](#vscode-spell-checker-tips-for-markdown)
    * [vscode-spell-checker References](#vscode-spell-checker-references)
  * [Markdown all in one](#markdown-all-in-one)
    * [Markdown all in one Commands](#markdown-all-in-one-commands)
    * [Markdown all in one Notes](#markdown-all-in-one-notes)
      * [Bug in Markdown all in one](#bug-in-markdown-all-in-one)
    * [Markdown all in one Tips](#markdown-all-in-one-tips)
    * [Markdown all in one References](#markdown-all-in-one-references)
* [markdownlint](#markdownlint)
  * [markdownlint Commands](#markdownlint-commands)
  * [markdownlint Notes](#markdownlint-notes)
    * [Ignore Rules](#ignore-rules)
    * [Rules with Parameter](#rules-with-parameter)
  * [markdownlint Tips](#markdownlint-tips)
    * [Allow some inline HTML](#allow-some-inline-html)
  * [markdownlint References](#markdownlint-references)
<!--- cSpell:enable --->

## Settings

`"editor.renderWhitespace": "all",` \
`"editor.renderControlCharacters": true,`: useful for rendering UNICODE Characters that sometimes are not good including invisible characters\
`"files.eol": "\n"`: set end of line format aka CRLF or LF aka part of the Unix/Windows format (from [How to set default line endings in Visual Studio Code?](https://stackoverflow.com/questions/71240918/how-to-set-default-line-endings-in-visual-studio-code))

> [!TIP] Check git settings
> Git also has CRLF settings that matter, esp. if working between windows and non-windows machines. the setting is `autocrlf`. See [autocrlf in Git Commands](git-commands.md#autocrlf)

## Shortcuts often forgotten

<kbd>CTRL</kbd>+<kbd>R</kbd>: Open different repo\
<kbd>CTRL</kbd>+<kbd>Shift</kbd>+<kbd>O</kbd>: show outline/symbol list\
<kbd>F1</kbd> then <kbd>Backspace</kbd>: search current repo/workspace files\
<kbd>F1</kbd> then <kbd>Backspace</kbd> then <kbd>%</kbd>: search for text in files in current repo/workspace

## Custom Keyboard Shortcuts

### CTRL+U: Underline in Markdown

Based off: <https://stackoverflow.com/questions/39333639/visual-studio-code-snippet-as-keyboard-shortcut-key/43604034#43604034>

markdown.json (user snippet):

```json
    "underline": {
        "prefix": "underline",
        "body": [
            "<ins>$TM_SELECTED_TEXT${1:}</ins>"
        ],
        "description": "Encloses selected text in <ins></ins> tags"
    }

```

keybindings.json:

```json
{
    "key": "cmd+u",
    "command": "editor.action.insertSnippet",
    "args": { "name": "underline" },
    "when": "editorTextFocus && editorLangId == markdown"
}

```

### References

[Windows PDF](https://go.microsoft.com/fwlink/?linkid=832145)\
[macOS PDF](https://go.microsoft.com/fwlink/?linkid=832143)\
[Linux PDF](https://go.microsoft.com/fwlink/?linkid=832144)

[when clause contexts for keyboard shortcuts](https://code.visualstudio.com/api/references/when-clause-contexts)

## Extensions

### vscode-spell-checker

<https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker>\
<https://streetsidesoftware.com/vscode-spell-checker/>\
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

##### vscode-spell-checker Tips for Markdown

Consider configuring cspell to ignore codeblocks and any text between backticks \` for markdown

```json
    "cSpell.languageSettings": [
        {
            // use with Markdown files
            "languageId": "markdown",
            // Exclude code.
            "ignoreRegExpList": [
                "/^\\s*```[\\s\\S]*?^\\s*```/gm",
                "`[^`]*`"
            ]
        }
    ],
```

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

## markdownlint

<https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint>\
<vscode:extension/DavidAnson.vscode-markdownlint>

### markdownlint Commands

Consider setting markdownlint.focusMode - only valid at user level, not workspace

```json
{
    "editor.someSetting": true,
    "markdownlint.focusMode": true
}
```

To ignore issues on the N lines above and below the cursor, set focusMode to a positive integer representing the number of lines to ignore in each direction:

```json
{
    "editor.someSetting": true,
    "markdownlint.focusMode": 2
}
```

More settings are here: <https://github.com/DavidAnson/vscode-markdownlint>

### markdownlint Notes

#### Ignore Rules

You can use ignore lines inside of files where you can disable markdown lint or a specific rule for the whole file, the next line or just a section (where it can then be re-enabled), such as:

```html
<!-- markdownlint-disable MD000 -->
<!-- markdownlint-enable MD000 -->
<!-- markdownlint-disable-next-line MD000 -->
<!-- markdownlint-disable-file MD000 -->
```

You can also configure the markdown lint settings to ignore this.

#### Rules with Parameter

Some rules may have parameters so you can customise how they are evaluated. See example in tips. Find the rules with Parameters in the rules link in references.

### markdownlint Tips

#### Allow some inline HTML

```json
 "markdownlint.config": {
    "MD033": {
      "allowed_elements": [
        "details",
        "summary",
        "ins",
        "kbd"
      ]
    },
 }
```

### markdownlint References

<https://github.com/DavidAnson/markdownlint/> - Contains rules
