---
title: Python Stuff
description: ""
published: false
categories:
    - Tech
type: pages
layout: pages
date: 2025-03-28T11:09:24.108Z
lastmod: 2025-04-16T00:12:54.309Z
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
  * [Standards of note](#standards-of-note)
* [Variants](#variants)
* [Tools](#tools)
  * [venv](#venv)
  * [vscode](#vscode)
* [Tricks](#tricks)
  * [Running python script from interactive shell](#running-python-script-from-interactive-shell)
* [Useful Snippets](#useful-snippets)
  * [Exit Handler](#exit-handler)
  * [Termination Signal Capture](#termination-signal-capture)
* [Quirks to remember](#quirks-to-remember)
* [Books](#books)
* [Resources of NOTE](#resources-of-note)
<!--- cSpell:enable --->

## Standards

> [!NOTE] Standards
> Not sure if 'standards' is the right heading here

<https://peps.python.org/>

### Standards of note

[PEP8](https://www.python.org/dev/peps/pep-0008/#imports) details how imports should be organized. This helps keep your code both readable and maintainable. Auto-sorting will structure your Python imports first by their source (e.g. standard library, third-party, local application) then alphabetically within those sections.\

## Variants

<https://micropython.org/> - lean version of python for microcontrollers, like arduino\
<https://circuitpython.org/> - beginner / easier to user version of the above for microcontrollers\

## Tools

See Regex Tools that cover Python in [Software Tools in Misc Tools](misc-tools.md#software-tools)

### venv

More info on activation: <https://docs.python.org/3/library/venv.html#how-venvs-work>

| Platform | Shell       | Command to activate virtual environment                               |
|----------|-------------|------------------------------------------------------------------------|
| POSIX    | bash/zsh    | `$ source <venv>/bin/activate`                                         |
| POSIX    | fish        | `$ source <venv>/bin/activate.fish`                                    |
| POSIX    | csh/tcsh    | `$ source <venv>/bin/activate.csh`                                     |
| POSIX    | pwsh        | `$ <venv>/bin/Activate.ps1`                                            |
| Windows  | cmd.exe     | `C:\> <venv>\Scripts\activate.bat`                                     |
| Windows  | PowerShell  | `PS C:\> <venv>\Scripts\Activate.ps1`                                  |

### vscode

<https://code.visualstudio.com/docs/python/debugging#_command-line-debugging>

Also look at remote debugging using debugpy module.

## Tricks

### Running python script from interactive shell

<https://stackoverflow.com/questions/17247471/how-to-run-a-python-script-from-idle-interactive-shell>

```bash
python3
exec(open('./app/filename.py').read())
```

## Useful Snippets

### Exit Handler

```python
import atexit

@atexit.register
def cleaup():
    print("Exiting via atexit...")
```

### Termination Signal Capture

```python
import signal

def handle_sigterm(signum, frame):
    print("Received SIGTERM. Shutting down gracefully...")
    sys.exit(0)

# Register the signal handler
signal.signal(signal.SIGTERM, handle_sigterm)

try: 
  something

except KeyboardInterrupt:
  print("Received KeyboardInterrupt. Exiting...")
  sys.exit(1)

finally:
  print("Exiting via finally...")
  sys.exit(0)
```

## Quirks to remember

`os.environ.get('ENVVAR', 'value if env missing)` always returns as a string object. Cast it as an int (or other type) if required. eg: `int(os.environ.get('ENVVAR', 'value if env missing))`

Yes this is a pertty basic concept but its here to more remember what 'os.environ.get()` returns as.

## Books

See [Python in Books](books.md#python)

## Resources of NOTE

The Python Package Index: <https://pypi.org/>
