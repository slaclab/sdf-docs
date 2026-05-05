# Claude Code

[Claude Code](https://docs.anthropic.com/en/docs/claude-code) is Anthropic's AI coding assistant. The S3DF OnDemand app lets you run Claude Code in a browser-based terminal — no local install, no SSH key management, no manual configuration required.

## What S3DF provides

- The OnDemand launch form, session management, and browser terminal
- A pre-built container image with Claude Code and all its dependencies installed
- Automatic version management — new releases appear in the version dropdown without any action from you
- Integration with SDF-Sage for facility-based LLM cost allocation (see [LLM providers](#llm-providers) below)

## What SLAC IT provides

Claude Code on S3DF routes all AI model calls through **SLAC IT-managed infrastructure**. S3DF does not operate these services:

| Service | What it does |
| --- | --- |
| `ai-api.slac.stanford.edu` | LiteLLM proxy that routes Bedrock API calls to AWS Claude models |
| `llm.sdf.slac.stanford.edu` | SDF-Sage facility allocation endpoint |
| AWS Bedrock (Claude models) | The underlying AI models, procured by SLAC IT via AWS |

?> If `ai-api.slac.stanford.edu` is unavailable, Claude Code sessions using the Bedrock provider will fail with API errors. This is an IT-managed service — check the [S3DF status page](changelog.md) or [contact us](contact-us.md) if you believe there is an outage.

## LLM providers

Two provider options are available at launch:

| Option | How it works | Who pays |
| --- | --- | --- |
| **Bedrock (personal API key)** | Routes calls through `ai-api.slac.stanford.edu` using your personal key | Your individual allocation |
| **SDF-Sage (facility allocation)** | Routes calls through `llm.sdf.slac.stanford.edu` using your experiment's Coact repo | Your facility/experiment |

?> **SDF-Sage is currently in limited availability.** Contact [us](contact-us.md) if you are unsure whether your facility has access.

## Before you start

### Bedrock: request a SLAC AI API key

You need a personal **SLAC AI API Key** before you can use the Bedrock provider. Request one via the SLAC IT ServiceNow portal:

[Request a SLAC AI API Bedrock Key](https://slacprod.servicenowservices.com/it_services?id=sc_cat_item&sys_id=515f28711b607110c5d320eae54bcb64&sysparm_category=d65827c46fd921009c4235af1e3ee434)

Allow a few business days if the key is not provisioned immediately. This is an IT ticketing process outside S3DF's control.

### SDF-Sage: know your facility and repo

SDF-Sage bills AI usage to your experiment's compute allocation. You do not need a personal API key — authentication happens automatically when the session starts via a browser device flow.

You will need to know your **facility** and **repo** names (e.g. `rubin:default`). Contact your experiment's computing coordinator if you are unsure.

## Launching Claude Code

1. Go to [OnDemand](https://s3df.slac.stanford.edu/ondemand) and log in.
2. Under **Interactive Apps**, select **Claude Code**.
3. Fill in the launch form (see [Form fields](#form-fields) below).
4. Click **Launch**.
5. Wait for the session to start — typically under 30 seconds on a warm node.
6. Click **Connect to Claude Code** when the button appears.

## Form fields

### LLM Provider

Selects which backend handles AI model calls for this session. See [LLM providers](#llm-providers) above.

### SLAC AI API Key _(Bedrock only)_

Your personal key from the IT ServiceNow portal. On launch, the key is written to `~/.claude/settings.json` and retained for future sessions. If you change your key, tick **Clear settings.json** before relaunching.

### Coact Repo _(SDF-Sage only)_

Your facility allocation in `facility:repo` format, for example `rubin:default`. If you enter only the facility name (e.g. `rubin`), `:default` is added automatically.

### Claude Code Version

The version of the Claude Code container to run. **Latest is recommended** for most users. Older versions are shown if you need to pin to a specific release.

### Run on Cluster

The interactive pool where the session runs. Claude Code has a light resource footprint (minimal CPU, under 1 GB RAM), so any interactive pool works. See [Interactive Pools](interactive-compute.md#interactive-pools) for the list of available pools.

### Working Directory

The directory where Claude Code starts. Leave blank to use your home directory. The path must exist and you must have read/write access to it.

### Additional Bind Mounts

Extra directories to make available inside the container, in addition to the default mounts.

**Default mounts — always available in every session:**

| Path | What it contains |
| --- | --- |
| `/sdf` | All S3DF persistent storage: home (`/sdf/home`), science data (`/sdf/data`), scratch (`/sdf/scratch`), software (`/sdf/sw`), group storage (`/sdf/group`) |
| `/fs` | Legacy file systems (AFS and similar) |
| `/lscratch` | Local node scratch — fast, not shared, contents are cleared when the session ends |

**Adding extra mounts** — enter a comma-separated list of paths:

```
/sdf/data/rubin:ro,/sdf/scratch/rubin
```

Each entry may include a mode suffix:

| Suffix | Meaning | When to use |
| --- | --- | --- |
| `:ro` | Read-only | Data directories where you only need to read — prevents accidental writes |
| `:rw` | Read-write | Directories you need to create or modify files in |
| _(none)_ | Read-write | Same as `:rw` |

?> Most users do not need extra mounts. `/sdf` already covers home, data, scratch, and group directories. Use this field when you need a path that is not under `/sdf` or `/fs`, or when you want to explicitly restrict a data directory to read-only access.

### Session Duration (hours)

How long to keep the session alive. Maximum is 168 hours (7 days). The session ends when the walltime expires, you click **Delete** in My Interactive Sessions, or the node is restarted.

### Clear settings.json

Deletes `~/.claude/settings.json` before starting. Use this when:

- You want to switch LLM providers
- Your API key has changed and the old one is cached in the settings file
- Your settings file is corrupt or in an unexpected state

A timestamped backup (`settings.json.bak.YYYYMMDD_HHMMSS`) is created automatically before deletion. All other customisations (permissions, keybindings, MCP server config) are lost after a clear, so use it only when needed.

## Reconnecting to a running session

Claude Code sessions continue running after you close the browser tab. To reconnect:

1. Go to [My Interactive Sessions](https://s3df.slac.stanford.edu/pun/sys/dashboard/batch_connect/sessions) in OnDemand.
2. Find your Claude Code session in the list.
3. Click **Connect to Claude Code**.

Any active Claude Code conversation continues exactly where you left it, for as long as the job is alive.

## Troubleshooting

### Claude Code shows API errors at startup

Your API key may be invalid or revoked. Relaunch with **Clear settings.json** checked and paste your current key into the form.

### Session fails to start

Click the **Session ID** link on [My Interactive Sessions](https://s3df.slac.stanford.edu/pun/sys/dashboard/batch_connect/sessions) and open `output.log` to see the error. Common causes: SIF image not found, invalid working directory, blank API key.

### SDF-Sage: authentication times out

The browser device flow gives you 5 minutes to authenticate. If it times out, delete the session and relaunch. Make sure you can reach the SLAC identity provider in your browser.

### A directory is not visible inside Claude Code

The path must be under `/sdf`, `/fs`, or `/lscratch`, or added as an [additional bind mount](#additional-bind-mounts). Note that `/lscratch` contents are local to the node — they differ between sessions on different nodes.
