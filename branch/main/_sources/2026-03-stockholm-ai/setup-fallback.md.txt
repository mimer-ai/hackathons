(fallback-installation)=
# Fallback installation with bring-your-own LLM provider

:::{important}
If you managed to install using the instructions in the section {ref}`standard-installation`, you can skip this section.
:::

For illustrative purposes we show how to locally install **MCP servers** and **agent skills** in the following agentic harnesses: OpenCode, Mistral Vibe and Claude Code.

:::{prereq}
Here we assume that you have
- installed the agentic harness of your choice, and
- connected or authenticated to an LLM that you have access to (in OpenCode using `/connect`, in Mistral Vibe with `vibe --setup` and in Claude Code using `/login`).
:::

:::::::{tabs}

::::{group-tab} OpenCode

[Local MCP servers](https://opencode.ai/docs/mcp-servers/#local) are configured by editing the 
global configuration `~/.config/opencode/opencode.jsonc`:

:::{tip}
For a local configuration use a directory `.opencode` in your current path instead of `~/.config/opencode`
:::

```json
{
  "$schema": "https://opencode.ai/config.json",
  // Other settings ...
  "mcp": {
    "scb_opendata_mcp": {
      "type": "local",
      "command": ["uvx", "scb_opendata_mcp", "--transport", "stdio"],
      "enabled": true
    },
    "swemo-mcp": {
      "type": "local",
      "command": ["uvx", "--with", "mcp==1.6.0", "swemo-mcp"],
      "enabled": true
    }
  }
}
```

and [skills](https://opencode.ai/docs/skills/) can be added by running the commands:

```console
$ mkdir -p ~/.config/opencode/skills

$ git clone https://github.com/ashwinvis/scb-opendata-skills
$ cp -r scb-opendata-skills/skills/*  ~/.config/opencode/skills/  # Global configuration
```
::::

::::{group-tab} Mistral Vibe

[Local MCP servers](https://docs.mistral.ai/mistral-vibe/introduction/configuration#mcp-server-configuration)
are configured by editing the global configuration `~/.vibe/config.toml`:

:::{tip}
For a custom agent configuration use a file say `~/.vibe/agents/mimer.toml` instead of the above, and later open with 

```sh
vibe --agent mimer
```
:::

```toml
[[mcp_servers]]
name = "scb_opendata_mcp"
transport = "stdio"
commmand = "uvx"
args = ["scb_opendata_mcp", "--transport", "stdio"],
      
[[mcp_servers]]
name = "swemo-mcp"
transport = "stdio"
command = "uvx" 
args = ["--with", "mcp==1.6.0", "swemo-mcp"],
```

and [skills](https://docs.mistral.ai/mistral-vibe/agents-skills) can be added by running the commands:

```console
$ mkdir -p ~/.vibe/skills

$ git clone https://github.com/ashwinvis/scb-opendata-skills
$ cp -r scb-opendata-skills/skills/*  ~/.vibe/skills/  # Global configuration
```

:::{tip}
If you are using a custom agent configuration say `~/.vibe/agents/mimer.toml`, instead of copying with `cp -r`, you can also let skills be discovered:

```toml
skill_paths = ["/path/to/cloned/repo/scb-opendata-skills/skills/"]
enabled_skills = ["scb-*"]
```
:::

::::

::::{group-tab} Claude Code

[Local MCP servers](https://code.claude.com/docs/en/mcp#option-3-add-a-local-stdio-server) are configured by executing:

```console
$ claude mcp add --scope user --transport stdio scb_opendata_mcp -- uvx scb_opendata_mcp --transport stdio
$ claude mcp add --scope user --transport stdio swemo-mcp -- uvx --with mcp==1.6.0 swemo-mcp
```

and [skills](https://code.claude.com/docs/en/skills) can be added by running the commands:


```console
$ mkdir -p ~/.claude/skills

$ git clone https://github.com/ashwinvis/scb-opendata-skills
$ cp -r scb-opendata-skills/skills/* ~/.claude/skills/  # Global configuration
```

::::
:::::::
