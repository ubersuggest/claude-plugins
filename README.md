# Ubersuggest plugins for Claude Code

A Claude Code plugin marketplace maintained by [Ubersuggest](https://neilpatel.com).

## Install

```
/plugin marketplace add ubersuggest/claude-plugins
/plugin install ubersuggest
```

Then restart Claude Code. Check the connection any time with `/mcp`.

## Plugins

| Plugin | What it does |
| --- | --- |
| [`ubersuggest`](plugins/ubersuggest) | Turns Claude into an SEO consultant backed by real Ubersuggest data — keyword research, competitor analysis, site audits, backlinks, content briefs, content planning and AI search visibility. |

## Accounts

The `ubersuggest` plugin connects to the Ubersuggest MCP server, which signs you
in with your own Ubersuggest account over OAuth on the first tool call — no API
key to paste and nothing to configure. Every tool works on a **free** account;
your plan changes how much data comes back, not which tools run.

One skill needs no account and makes no data calls at all:
`/ubersuggest:content-demand-finder`, which turns a business description into 50
content opportunities.

See the [plugin README](plugins/ubersuggest/README.md) for the full command list,
which tools require login, and how quotas work.

## Links

- Tool reference: https://ubersuggest-mcp.neilpatelapi.com/docs
- Machine-readable docs: https://ubersuggest-mcp.neilpatelapi.com/llms.md
- Pricing: https://app.neilpatel.com/en/pricing
- Support: https://ubersuggest.zendesk.com/hc/en-us/requests/new

## Licence

Apache-2.0. See [LICENSE](LICENSE).
