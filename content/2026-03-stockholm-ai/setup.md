# Setup

:::{admonition} TLDR; The Endpoints
:class: hint

While we provide instructions below for several tools (`npm`, `uv`, `opencode` etc.). If you are in a hurry, here are the information about the **inference and MCP endpoints**
for your reference.

- Endpoint for the model:  <http://mimer-aif-hackathon.icedc.se/v1>
- Endpoint for Riksbanken MCP: <http://mimer-aif-hackathon.icedc.se/swemo/sse>
- Endpoint for SCB/Statistics Sweden MCP: <http://mimer-aif-hackathon.icedc.se/scb/mcp>

We have also added a skills repo for the SCB MCP available here: <https://github.com/ashwinvis/scb-opendata-skills>

In this hackathon, we execute MistralAI's Devstral 2 Small (256K, 24B) in H100 GPUs, served through multiple instances of vLLM. The model was chosen as it fits consumer hardware and therefore can simulating a home development for those who never did it.
:::

## Recommended Tools

The following tools are often useful for either installing MCP servers or building the final application for your hackathon.

- Node.js via `npm` and `npx` commands: Follow instructions at <https://nodejs.org/en/download>
- Python via `uv` and `uvx` commands: Follow instructions at <https://docs.astral.sh/uv/getting-started/installation/> 
- **(Optional, but convenient to have)** Git for cloning skill repositories instead of downloading. We use `git clone` command in instructions below. Follow instructions at <https://git-scm.com/> to get `git`.

::::::::{admonition} Python and use of virtual environments
:class: tip

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


The `<executable>` can be `python` or even something provided by a package such as `gradio`.
::::::

:::::::::

(standard-installation)=
## Standard installation with open-weights LLM from Mimer



For this Hackathon, we support the usage of OpenCode as it is a free and opensource tool that do not require any third-party account. 
If you want to use other tools (Claude Code, Mistral Vibe, etc), you can directly refer to their documentation and configuration of custom endpoints.

:::::::{tabs}

::::{group-tab} Windows

:::{important}
Please notice that while there are instructions for Windows, we strongly support using Windows Subsystem for Linux (see **WSL** in the next tab) as the development environment is more robust and secure (i.e., it is easier to administrate Python environments). 
:::

1. Download the OpenCode at its official [download webpage](https://opencode.ai/download).
2. Open OpenCode once, and close it.
3. On Windows Explorer, open `%USERPROFILE%\.config\opencode`
4. Create a file named `opencode.jsonc`, and insert the JSON configuration **given below**, replacing the entire content, if the file was not empty:
5. Now reopen OpenCode.

::::

::::{group-tab} WSL / Linux / Mac

1. In your terminal, download OpenCode by running[^link-to-install-script]

```sh
curl -fsSL https://opencode.ai/install | bash
```

2. Run `opencode`, and then type `exit` and hit <kbd>Enter</kbd>.
3. Execute the following to prepare the configuration file
```sh
mkdir -p ~/.config/opencode/  # create the directory if it doesn't exist
cd ~/.config/opencode/
touch opencode.jsonc  # create the configuration file if it doesn't exist
``` 
4. Then use your favourite text editor to replace the contents of `opencode.jsonc`,
   with the JSON configuration **given below**.
5. Run `opencode` and start using it! 

**(Optional)**: you can also run `opencode web --port 4096 --hostname 0.0.0.0` and start a web instance of it in your browser, 
which will then be available on `http://localhost:4096`. 

::::
::::::::

[^link-to-install-script]: It is good practice to the read the install script and verify it. Click here <https://opencode.ai/install> and read it. Alternatively, you may also use `npm i -g opencode-ai` if you have a Node.js installlation.


::::::{callout} OpenCode JSON configuration
```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "mimer": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "Mimer AI",
      "options": {
        "baseURL": "http://mimer-aif-hackathon.icedc.se/v1"
      },
      "models": {
        "mistralai/Devstral-Small-2-24B-Instruct-2512": {
          "name": "Devstral 2 Small (256k)",
          "limit": {
            "context": 262144,
            "output": 262144
          }
        },
      }
    }
  },
  "model": "mistralai/Devstral-Small-2-24B-Instruct-2512",
  "mcp": {
    "scb_opendata_mcp": {
      "type": "remote",
      "url": "http://mimer-aif-hackathon.icedc.se/scb/mcp",
      "enabled": true
    },
    "swemo-mcp": {
      "type": "remote",
      "url": "http://mimer-aif-hackathon.icedc.se/swemo/sse",
      "enabled": true
    }
  }
}
```
::::::

Use `Ctrl+P` to access menus and switch the models and/or the MCPs. You can also use slash commands like `/models` and `/mcps`. You should now be able to select the model **(Devstral 2 Small (256k))**.


### Skills

Agent [skills](https://opencode.ai/docs/skills/) can be added by running the commands:

:::::::{tabs}

::::{group-tab} Windows with Git Bash

Launch Git bash from the start menu. It should [look like this](https://gitforwindows.org/img/gw1.png). Then run the following commands.

```console
$ mkdir -p $USERPROFILE/.config/opencode/skills

$ git clone https://github.com/ashwinvis/scb-opendata-skills
$ cp -r scb-opendata-skills/skills/*  $USERPROFILE/.config/opencode/skills/  # Global configuration
```
::::

::::{group-tab} WSL/Linux/MacOS
```console
$ mkdir -p ~/.config/opencode/skills

$ git clone https://github.com/ashwinvis/scb-opendata-skills
$ cp -r scb-opendata-skills/skills/*  ~/.config/opencode/skills/  # Global configuration
```
::::

:::::::

Happy coding 🥳!
