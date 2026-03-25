# Quick Reference

(python-venv)=
## Python and use of virtual environments

During the course of the hackathons you might need Python tools or develop your own application.
For security reasons and to leave your system libraries unaffected, we always recommend you develop your 
demo apps inside a Python virtual environment,
as it often wants to install libraries and execute code. Given below are some pointers on how to do that.


::::::{tabs}

:::{group-tab} uv

The following commands show how to initialize a virtual environment named `.venv`,
install packages to it and run executables from it.

```bash
uv init
uv add <package>
uv run <executable>
```

:::


:::{group-tab} Python's `venv` module in Windows

You might have a working Python installation and you do not wish to use `uv`. If so,

```bash
py -m venv .venv
.venv\Scripts\activate
python -m pip install <package>
<executable>
```

Use `deactivate` to leave the environment.
:::

:::{group-tab} Python's `venv` module in WSL/Linux/macOS

You might have a working Python installation and you do not wish to use `uv`. If so,

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install <package>
<executable>
```

Use `deactivate` to leave the environment.
:::


::::::


The `<executable>` can be `python` or even something provided by a package such as `gradio`. 

## Python scripts

A new way (PEP 723) of developing scripts without having to ensure dependencies is 
to add inline-script metadata which looks like this:

```py
# /// script
# requires-python = ">=3.11"
# dependencies = [
#   "pandas",
#   "seaborn",
# ]
# ///

import pandas as pd
import seaborn as sns

...
```

No virtual environments are needed for such scripts to work.
This can be executed using [`uv run`](https://docs.astral.sh/uv/guides/scripts/#creating-a-python-script)
command and [`pipx`](https://pipx.pypa.io/).
