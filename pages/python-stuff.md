---
title: Python Stuff
description: ""
published: false
categories:
    - Tech
type: pages
layout: pages
date: 2025-03-28T11:09:24.108Z
lastmod: 2025-04-13T07:22:00.774Z
tags:
    - Language
    - Python
isdraft: true
fmContentType: pages
mermaid: false
preview: ""
---

<!--- cSpell:disable --->
* [Standards](#standards)
* [Variants](#variants)
* [Tools](#tools)
* [Tricks](#tricks)
  * [Running python script from interactive shell](#running-python-script-from-interactive-shell)
* [Quirks to remember](#quirks-to-remember)
* [Books](#books)
* [Resources of NOTE](#resources-of-note)
<!--- cSpell:enable --->

## Standards

> [!NOTE] Standards
> Not sure if 'standards' is the right heading here

<https://peps.python.org/>

## Variants

<https://micropython.org/> - lean version of python for microcontrollers, like arduino\
<https://circuitpython.org/> - beginner / easier to user version of the above for microcontrollers\

## Tools

See Regex Tools that cover Python in [Software Tools in Misc Tools](misc-tools.md#software-tools)

## Tricks

### Running python script from interactive shell

<https://stackoverflow.com/questions/17247471/how-to-run-a-python-script-from-idle-interactive-shell>

```bash
python3
exec(open('./app/filename.py').read())
```

## Quirks to remember

`os.environ.get('ENVVAR', 'value if env missing)` always returns as a string object. Cast it as an int (or other type) if required. eg: `int(os.environ.get('ENVVAR', 'value if env missing))`

Yes this is a pertty basic concept but its here to more remember what 'os.environ.get()` returns as.

## Books

See [Python in Books](books.md#python)

## Resources of NOTE

The Python Package Index: <https://pypi.org/>
