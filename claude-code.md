# Claude Code

[Claude Code](https://docs.anthropic.com/en/docs/claude-code) is Anthropic's AI coding assistant. The S3DF OnDemand app lets you run Claude Code in a browser-based terminal — no local install, no SSH key management, no manual configuration required. We provide:

- The OnDemand launch form, session management, and browser terminal
- A pre-built container image with Claude Code and all its dependencies installed
- Automatic version management — new releases appear in the version dropdown without any action from you


Claude Code on S3DF routes all AI model calls through **SLAC IT-managed infrastructure**. S3DF does not operate these services. You will need to [request a SLAC AI API Bedrock Key](https://slacprod.servicenowservices.com/it_services?id=sc_cat_item&sys_id=515f28711b607110c5d320eae54bcb64&sysparm_category=d65827c46fd921009c4235af1e3ee434) before using this service. Allow a few business days if the key is not provisioned immediately. This is an IT ticketing process outside S3DF's control.


?> If `ai-api.slac.stanford.edu` is unavailable, Claude Code sessions using the Bedrock provider will fail with API errors. This is an IT-managed service — check the [S3DF status page](changelog.md) or [contact us](contact-us.md) if you believe there is an outage.

## Launching Claude Code

1. Go to [OnDemand](https://s3df.slac.stanford.edu/ondemand) and log in.
2. Under **Interactive Apps**, select **Claude Code**.
3. Fill in the launch form (see [Form fields](#form-fields) below).
4. Click **Launch**.
5. Wait for the session to start — typically under 30 seconds on a warm node.
6. Click **Connect to Claude Code** when the button appears.

## Form fields

### LLM Provider

Selects which backend handles AI model calls for this session. Currently the only supported provider is SLAC IT AI's Bedrock service. Your personal key from the IT ServiceNow portal. On launch, the key is written to `~/.claude/settings.json` and retained for future sessions.

### Claude Code Version

The version of the Claude Code container to run. **Latest is recommended** for most users. Older versions are shown if you need to pin to a specific release.

### Run on Cluster

The interactive pool where the session runs. Claude Code has a light resource footprint (minimal CPU, under 1 GB RAM), so any interactive pool works. See [Interactive Pools](interactive-compute.md#interactive-pools) for the list of available pools.

### Working Directory

The directory where Claude Code starts. Leave blank to use your home directory. The path must exist and you must have read/write access to it.

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

### A directory is not visible inside Claude Code

All S3DF storage under `/sdf` and legacy filesystems under `/fs` are automatically available. `/lscratch` is local node scratch — its contents differ between nodes and are cleared when the session ends.

