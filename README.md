# Person LinkedIn URL Resolver MCP Server

[![Smithery](https://smithery.ai/badge/mambabuilt/mcp-person-linkedin-url-resolver)](https://smithery.ai/servers/mambabuilt/mcp-person-linkedin-url-resolver) [![Glama score](https://glama.ai/mcp/servers/mambalabsdev/mcp-person-linkedin-url-resolver/badges/score.svg)](https://glama.ai/mcp/servers/mambalabsdev/mcp-person-linkedin-url-resolver) [![MCP Registry](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fregistry.modelcontextprotocol.io%2Fv0%2Fservers%3Fsearch%3Dcom.mambabuilt%252Fmcp-person-linkedin-url-resolver%26limit%3D1&query=%24.servers%5B0%5D._meta%5B%22io.modelcontextprotocol.registry%2Fofficial%22%5D.status&label=mcp%20registry&color=blue)](https://registry.modelcontextprotocol.io/v0/servers?search=com.mambabuilt/mcp-person-linkedin-url-resolver&limit=1) [![npm version](https://img.shields.io/npm/v/@mambalabsdev/mcp-person-linkedin-url-resolver)](https://www.npmjs.com/package/@mambalabsdev/mcp-person-linkedin-url-resolver) [![npm downloads](https://img.shields.io/npm/dm/@mambalabsdev/mcp-person-linkedin-url-resolver)](https://www.npmjs.com/package/@mambalabsdev/mcp-person-linkedin-url-resolver) [![license](https://img.shields.io/github/license/mambalabsdev/mcp-person-linkedin-url-resolver)](https://github.com/mambalabsdev/mcp-person-linkedin-url-resolver/blob/main/LICENSE) [![mcpservers.org](https://img.shields.io/badge/mcpservers.org-listed-blue)](https://mcpservers.org/servers/mambalabsdev/mcp-person-linkedin-url-resolver)

<a href="https://mcprush.com/to/person-linkedin-url-resolver-mcp?ref=badge"><img width="380" height="200" src="https://mcprush.com/badge/person-linkedin-url-resolver-mcp/card.svg" alt="Person LinkedIn URL Resolver MCP server" /></a>

Give it a person's name and company domain (or company name). Each run reads Google result pages through the Apify Google SERP proxy and returns one row per person with the LinkedIn profile URL, the headline and follower count Google shows, and a match confidence. It never opens LinkedIn and needs no LinkedIn account.

## What's Inside

- [What it does](#what-it-does)
- [Quick start](#quick-start)
- [Prerequisites](#prerequisites)
- [Example prompts](#example-prompts)
- [Tool](#tool)
- [Inputs](#inputs)
- [Pricing](#pricing)
- [Your keys](#your-keys)
- [Full actor documentation](#full-actor-documentation)
- [License](#license)

## What it does

- `match_status` is `found` at a confidence of 0.8 or more with a clear lead over every other profile, `ambiguous` (the likely URL), `not_found`, or `blocked`.
- `company_match` says whether the company is `current` (headline or a present role), `former` (marked prev, ex, or former), or only `mentioned`.
- Posts, articles, and directory pages are dropped; only `/in/` profile URLs are returned.

All of the work runs on Apify. This package is a thin client that starts the actor run, waits for it, and hands back the dataset rows.

## Quick start

You need Node.js 18 or newer and an Apify account with an API token.

Add this to your Claude Desktop config (`claude_desktop_config.json`), Cursor, or any MCP client:

```json
{
  "mcpServers": {
    "mamba-person-linkedin-url-resolver": {
      "command": "npx",
      "args": [
        "-y",
        "@mambalabsdev/mcp-person-linkedin-url-resolver"
      ],
      "env": {
        "APIFY_TOKEN": "your-apify-token"
      }
    }
  }
}
```

Restart the client. The `resolve_person_linkedin_url` tool appears.

## Prerequisites

- Node.js 18 or newer.
- An Apify API token from [console.apify.com/account/integrations](https://console.apify.com/account/integrations), set as `APIFY_TOKEN`. The server lists its tool without a token; a call needs one.

## Example prompts

- "Find the LinkedIn profile of Armon Dadgar at hashicorp.com."
- "Here are 20 names and company domains from my CRM. Find each LinkedIn URL and tell me which ones are certain."

## Tool

`resolve_person_linkedin_url`. One tool. Example arguments:

```json
{ "full_name": "Armon Dadgar", "company_domain": "hashicorp.com" }
```

## Inputs

Every buyer facing input of the actor, unchanged. Omitted inputs take the actor's own defaults.

| Input | Type | Description |
|---|---|---|
| `full_name` | string | First and last name |
| `company_domain` | string | The company domain; give this or `company_name` |
| `company_name` | string | Optional company name |
| `job_title` | string | Optional; a small boost when the headline agrees |
| `location` | string | Optional; a small boost when the snippet agrees |
| `keywords` | string | Optional extra query words |
| `persons` | array | Up to 500 lines as `Full Name \| company.com \| job title` |
| `country` | string | Google country code. Default us |
| `allow_name_only` | string | true searches without a company; never `found` |
| `max_charge_usd` | string | Optional cost cap for the run |

## Pricing

Pay per event on Apify, billed to your Apify account. Prices in USD.

| Event | Free plan | Bronze | Silver | Gold |
|---|---|---|---|---|
| `person-searched`, per input person | $0.035 | $0.03325 | $0.0315 | $0.02975 |
| `apify-actor-start`, per run start | $0.0005 | $0.0005 | $0.0005 | $0.0005 |

`found`, `ambiguous`, and `not_found` rows each cost one `person-searched`. `blocked` and `error` rows are free. The actor reads at most 2 Google result pages per person.

## Your keys

The actor needs no key and holds none. Mamba Labs pays the platform costs of the run, Google SERP proxy traffic included.

## Full actor documentation

[apify.com/mambalabs/person-linkedin-url-resolver](https://apify.com/mambalabs/person-linkedin-url-resolver)

## License

MIT. See [LICENSE](LICENSE).
