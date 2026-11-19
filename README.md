# JobQuoteLab MCP server for ChatGPT and Claude

JobQuoteLab publishes no public API or developer documentation, and no official MCP server or ChatGPT or Claude connector was found on the Cotlet.dev page checked 17 November 2026. Cotlet.dev connects your AI agent to your signed-in JobQuoteLab Cloud Browser. The page describes 8 hosted workflows: 4 reads and 4 writes. Writes ask for confirmation by default. Saved quotes, public links, pricing profiles and widget workflows need JobQuoteLab Pro.

## What you can ask

> Read new leads from your website widget

> Price a job from area, soil level and costs

> Check the price clears your minimum fee and margin

> Save a quote with Good, Better and Best options

> Make the customer-safe quote link

> Print a bid for a site visit

## Connect in 2 minutes

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1/connect`, then sign in with Cotlet.dev. No API key needed.

### Claude

Settings > Connectors > Add custom connector: `https://cotlet.dev/mcp/v1/connect`. Sign in to Cotlet.dev.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Run it locally (stdio)

This repo is a real MCP server. It speaks MCP over stdio, lists its JobQuoteLab tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers":{"jobquotelab":{"command":"uvx","args":["--from","git+https://github.com/cotlet-connect/jobquotelab-mcp","jobquotelab-mcp"],"env":{"COTLET_API_KEY":"your-key"}}}}
```

Or with Docker:

```bash
docker build -t jobquotelab-mcp .
docker run -i --rm -e COTLET_API_KEY jobquotelab-mcp
```

Tools: `jobquotelab_guide`, `jobquotelab_status`, `jobquotelab_open`, `jobquotelab_read`, `jobquotelab_click`, `jobquotelab_type`, `jobquotelab_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. From this repository:

```bash
pip install git+https://github.com/cotlet-connect/jobquotelab-mcp
jobquotelab-mcp connect
```

Or straight from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 jobquotelab_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 jobquotelab_agent.py status    # is JobQuoteLab ready in your Cotlet.dev account
python3 jobquotelab_agent.py guide     # JobQuoteLab screens and sign-in link
python3 jobquotelab_agent.py read      # open JobQuoteLab, read the page, close the browser
python3 jobquotelab_agent.py tools     # list Cotlet.dev tools
python3 jobquotelab_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from JobQuoteLab users

**Does JobQuoteLab have an API or MCP server?**

According to the Cotlet.dev page checked 17 November 2026, JobQuoteLab publishes no public API or developer documentation. No official MCP server or ChatGPT or Claude connector was found.

**How do I connect JobQuoteLab to ChatGPT?**

Sign up at https://cotlet.dev/signup?app=jobquotelab, enable JobQuoteLab and sign in at jobquotelab.com/login in your Cloud Browser. Add https://cotlet.dev/mcp/v1/connect in ChatGPT and authenticate with OAuth.

**Can I use JobQuoteLab with Claude?**

Add https://cotlet.dev/mcp/v1/connect as a custom connector in Claude and sign in to Cotlet.dev.

**Which workflows need JobQuoteLab Pro?**

The calculator works on any account. Saved quotes, public quote links, pricing profiles and the website widget need Pro.

**Does sharing a quote link send it to the customer?**

The tool creates a public branded page and returns its link. Sending the link to a customer remains up to you or your next tool. Public quotes and print output hide internal cost, profit and margin.

**Is this an official JobQuoteLab server?**

No. Cotlet.dev is independent and not affiliated with JobQuoteLab.

## Live integration page

https://cotlet.dev/integrations/jobquotelab-api-mcp-server

---

More: https://cotlet.dev/integrations/jobquotelab-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=jobquotelab

Start free: https://cotlet.dev/signup?app=jobquotelab&utm_source=github&utm_medium=readme&utm_campaign=jobquotelab
