# Use Met Museum Explorer with your assistant

Build a personal tour of The Met with collection records, gallery numbers and questions for close looking.

## ChatGPT and Codex

[Download the ChatGPT and Codex package](https://raw.githubusercontent.com/OpZero-sh/met-museum-explorer-plugin/downloads/met-museum-explorer.zip). It includes the product skills, remote connection and product icon.

For a publisher or developer setup, open the OpenAI developer dashboard, choose **Upload plugin**, upload the one-connection ZIP and connect the declared MCP endpoint. People with an existing directory listing can install it directly in ChatGPT. For an OAuth-protected service select OAuth and complete its browser sign-in. Choose no authentication for a public service. Rebuild the archives from a checkout with `python3 scripts/build_openai.py ../plugin-zips`.

[OpenAI package guide](https://developers.openai.com/plugins/build/plugins) · [Upload and connection setup](https://developers.openai.com/plugins/deploy/submission)

## Claude

In Claude Code run `/plugin marketplace add OpZero-sh/plugins`, then `/plugin install met-museum-explorer@opzero`. In Claude chat or Cowork, add the OpZero marketplace if available to your account and connect the services in the installed plugin’s **Connectors** tab.

## Grok Build

From a checkout of this repository, run `grok plugin validate .` and `grok plugin install .`. View installed capabilities with `grok plugin details met-museum-explorer`. Grok Build reads the Claude-compatible plugin, its skills and MCP configuration. [Grok Build plugins](https://docs.x.ai/build/features/skills-plugins-marketplaces)

## Grok API

Preview a request locally with Python 3. Add `XAI_API_KEY` in your environment and omit `--dry-run` to send it. Use `--model` to select a model enabled for your account. The example requests a focused set of product tools; its tool list is in [grok-servers.json](integrations/grok-servers.json).

```sh
python3 integrations/grok_example.py --dry-run 'Plan three stops around cats in Egyptian art. Pick works on view and give my six-year-old one thing to look for at each stop.'
```

[Remote MCP tools in the xAI API](https://docs.x.ai/developers/tools/remote-mcp)

## Muse Code

From the repository root, validate and install the native plugin. Approve its public MCP connections, then start a new Muse session.

```sh
muse plugins validate .
muse plugins install .
muse plugins approve met-museum-explorer
```

[Muse Code plugins](https://meta-models.github.io/muse-code-sdk/next/guides/plugins/reference/manifest/)
