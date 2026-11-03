# OKZest plugin for Claude Code

Personalised image templates for email, social and automation, through the OKZest MCP server. OKZest is a template tool, not an AI image generator.

> STUB: final copy comes from OKZ-605.

## Install

```
claude plugin marketplace add KevinUK/okzest-skill
claude plugin install okzest@okzest
```

## Set your key

Create an API key at Settings, API Keys on https://okzest.com and set it before starting Claude Code:

```
export OKZEST_API_KEY=your-key
```

## Fallback without the plugin's MCP config

```
claude mcp add --transport http okzest https://api.okzest.com/mcp --header "x-api-key: $OKZEST_API_KEY"
```

More: https://docs.okzest.com and https://okzest.com
