# OpenFirmList MCP Server

Official remote Model Context Protocol (MCP) server for [OpenFirmList](https://openfirmlist.com) — a global B2B company search engine indexing 3.1M+ manufacturers, suppliers, workshops, and industrial sites worldwide.

**Remote MCP Endpoint:** `https://openfirmlist.com/mcp`

## Available Tools

- **`search_companies`** — Search for companies that make, sell, or do something, optionally filtered by country, city, or radius (20 results per page). Searches can also narrow by 4-digit HS code (`hs_code`), certification, head count (`employees`), founding year, sector, company type, and production area.
- **`find_potential_buyers`** — Identify which industries buy a product, based on what its suppliers say about their customers, along with example companies.
- **`get_company`** — Retrieve a single company's full profile: products, services, certifications, export markets, and industries served.

> **Data notes:** Each result includes a `confidence` level (`high` when read from the company's own website, `medium` when placed in a sector, `low` when only listed) and `source_type` (`company_website` or `public_directory`). No phone numbers or email addresses are returned; each result links to its OpenFirmList profile page.

## Setup Instructions

### Claude, ChatGPT, and other apps (OAuth)

Add a custom connector with the MCP endpoint URL:

```
https://openfirmlist.com/mcp
```

The app opens an OpenFirmList sign-in flow; after you allow access, your AI assistant can use the tools directly without needing to copy an API key.

### Claude Code

Sign in at [OpenFirmList](https://openfirmlist.com/developers) to create an API key, then run:

```bash
claude mcp add --transport http openfirmlist https://openfirmlist.com/mcp \
  --header "Authorization: Bearer ofl_YOUR_KEY"
```

### Cursor and other tools with a configuration file

Add the following entry to your MCP configuration file:

```json
{
  "mcpServers": {
    "openfirmlist": {
      "url": "https://openfirmlist.com/mcp",
      "headers": {
        "Authorization": "Bearer ofl_YOUR_KEY"
      }
    }
  }
}
```

## Pricing & Rate Limits

- **Free Tier:** 1,000 queries per month (no credit card required).
- **Pro Tier:** 10,000 queries per month for US$29.
- **Rate Limit:** Up to 60 requests per minute per key or connected app.
- Every successful tool call counts as one query; failed calls are free. Monthly counts reset on the 1st of each month (UTC).

## Links

- [Developer Documentation & OpenAPI](https://openfirmlist.com/developers)
- [Pricing](https://openfirmlist.com/pricing)
- [OpenFirmList](https://openfirmlist.com)
