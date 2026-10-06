# OpenCode

[OpenCode](https://opencode.ai) is an open-source AI coding assistant with a terminal UI that supports multiple LLM providers. The S3DF OnDemand app lets you run OpenCode in a browser-based terminal with no local install or manual configuration. We provide:

- The OnDemand launch form, session management, and browser terminal
- A pre-built container image with OpenCode and all its dependencies installed
- Automatic version management — new releases appear in the version dropdown without any action from you

OpenCode and [Claude Code](claude-code.md) serve similar purposes. The main differences:

| | Claude Code | OpenCode |
| --- | --- | --- |
| Origin | Anthropic (official product) | Open-source community project |
| Provider support | Claude models only | Multiple LLM providers |
| Config file | `~/.claude/settings.json` | `~/.config/opencode/opencode.json` |

Both apps use the same two LLM provider options and the same interactive node infrastructure.

OpenCode on S3DF routes all AI model calls through the same SLAC IT-managed infrastructure as Claude Code. See [Claude Code — What SLAC IT provides](claude-code.md#what-slac-it-provides) for details and IT dependency notes. S3DF does not operate these services. You will need to [request a SLAC AI API Bedrock Key](https://slacprod.servicenowservices.com/it_services?id=sc_cat_item&sys_id=515f28711b607110c5d320eae54bcb64&sysparm_category=d65827c46fd921009c4235af1e3ee434) before using this service. Allow a few business days if the key is not provisioned immediately. This is an IT ticketing process outside S3DF's control.

## Launching OpenCode

1. Go to [OnDemand](https://s3df.slac.stanford.edu/ondemand) and log in.
2. Under **Interactive Apps**, select **OpenCode**.
3. Fill in the launch form (see [Form fields](#form-fields) below).
4. Click **Launch**.
5. Click **Connect to OpenCode** when the button appears.

## Form fields

### LLM Provider

Your personal SLAC AI API key. On launch, the key is written into `~/.config/opencode/opencode.json`. Unlike Claude Code, there is no **Clear settings.json** checkbox — to reset OpenCode's configuration, delete `~/.config/opencode/opencode.json` from a terminal before relaunching.

### OpenCode Version

The version of the OpenCode container to run. **Latest is recommended.**

### Run on Cluster

The interactive pool where the session runs. See [Interactive Pools](interactive-compute.md#interactive-pools) for available pools.

### Working Directory

The directory where OpenCode starts. Leave blank for your home directory.

### Session Duration (hours)

How long to keep the session alive. Maximum is 168 hours (7 days).

**Available storage paths** — the following paths are always mounted in the container:

| Path | What it contains |
| --- | --- |
| `/sdf` | All S3DF persistent storage: home, science data, scratch, software, group storage |
| `/fs` | Legacy file systems (AFS and similar) |
| `/lscratch` | Local node scratch — fast, not shared, cleared when the session ends |

## Reconnecting to a running session

See [Claude Code — Reconnecting to a running session](claude-code.md#reconnecting-to-a-running-session). The process is identical.

## Troubleshooting

Troubleshooting steps are the same as for Claude Code — see [Claude Code — Troubleshooting](claude-code.md#troubleshooting).

OpenCode's configuration file is `~/.config/opencode/opencode.json`. If the configuration is invalid or the wrong provider is written, delete the file and relaunch.

