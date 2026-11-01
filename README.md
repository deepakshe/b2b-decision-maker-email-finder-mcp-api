# B2B Decision Maker Email Finder MCP Server & Python API

[![Apify Store](https://img.shields.io/badge/Apify_Store-Run_on_Apify-blue?style=for-the-badge&logo=apify)](https://apify.com/deepaksheoran172/b2b-decision-maker-email-finder)
[![MCP Server](https://img.shields.io/badge/MCP-Model_Context_Protocol-purple?style=for-the-badge)](https://modelcontextprotocol.io)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)
[![Hub](https://img.shields.io/badge/Live_Catalog-B2B_Scrapers_Hub-emerald?style=for-the-badge)](https://deepakshe.github.io/b2b-mcp-apify-scrapers-hub/)

> **Deterministic B2B decision-maker email finder & corporate domain pattern resolver. MCP Server, Python SDK & n8n workflow.**

---

## ⚡ Instant Normalized Output (Sample JSON)

```json
[
  {
    "firstName": "Satya",
    "lastName": "Nadella",
    "domain": "microsoft.com",
    "resolved_email": "satya.nadella@microsoft.com",
    "confidence_score": 98,
    "pattern_matched": "{first}.{last}@microsoft.com"
  }
]
```

---

## ⚡ The Problem vs. The Solution

Guessing executive email formats wastes outreach quotas. This engine tests all RFC pattern permutations ({first}.{last}, {first}, {f}{last}) against live MX mailservers to pinpoint the exact mailbox without false positives.

- **Zero-Proxy Architecture:** Pure asynchronous execution designed for extreme speed (<50MB RAM).
- **Multi-Interface Support:** Run via pure Python SDK, cURL, Node.js fetch, n8n / Make.com workflow, or Claude / Cursor MCP Agent.
- **Production Reliable:** Backed by Apify's serverless infrastructure with 99.9% uptime SLA.

---

## 🚀 Quickstart: 1-Line cURL (Test in 2 Seconds)

```bash
curl -X POST "https://api.apify.com/v2/acts/deepaksheoran172~b2b-decision-maker-email-finder/run-sync-get-dataset-items?token=YOUR_APIFY_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{\"contacts\": [{\"firstName\": \"Satya\", \"lastName\": \"Nadella\", \"domain\": \"microsoft.com\"}]}'
```

---

## 🚀 Quickstart: Pure Python (Zero-Dependency)

No third-party SDKs required. Run directly with Python standard library:

```python
import json
import os
import urllib.request

APIFY_TOKEN = os.getenv("APIFY_TOKEN", "YOUR_APIFY_TOKEN")
ACTOR_URL = "https://api.apify.com/v2/acts/deepaksheoran172~b2b-decision-maker-email-finder/run-sync-get-dataset-items?token=" + APIFY_TOKEN

payload = {
  "contacts": [
    {
      "firstName": "Satya",
      "lastName": "Nadella",
      "domain": "microsoft.com"
    }
  ]
}

req = urllib.request.Request(
    ACTOR_URL,
    data=json.dumps(payload).encode("utf-8"),
    headers={"Content-Type": "application/json"},
    method="POST"
)

with urllib.request.urlopen(req, timeout=120) as resp:
    results = json.loads(resp.read().decode("utf-8"))
    print(f"Retrieved {len(results)} items:")
    print(json.dumps(results[:2], indent=2))
```

---

## 🌐 Quickstart: Node.js / TypeScript

```javascript
const APIFY_TOKEN = process.env.APIFY_TOKEN || 'YOUR_APIFY_TOKEN';
const ACTOR_URL = `https://api.apify.com/v2/acts/deepaksheoran172~b2b-decision-maker-email-finder/run-sync-get-dataset-items?token=${APIFY_TOKEN}`;

const payload = {
  "contacts": [
    {
      "firstName": "Satya",
      "lastName": "Nadella",
      "domain": "microsoft.com"
    }
  ]
};

async function run() {
  const res = await fetch(ACTOR_URL, {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(payload)
  });
  const items = await res.json();
  console.log(`Received ${items.length} records:`, items.slice(0, 2));
}

run().catch(console.error);
```

---

## 🤖 Claude Desktop & Cursor MCP Server Setup

Add this actor to your `claude_desktop_config.json` to allow Claude / Cursor AI agents to execute it autonomously:

```json
{
  "mcpServers": {
    "b2b-decision-maker-email-finder": {
      "command": "npx",
      "args": ["-y", "@apify/actors-mcp-server"],
      "env": {
        "APIFY_TOKEN": "YOUR_APIFY_TOKEN",
        "ACTOR_NAME": "deepaksheoran172/b2b-decision-maker-email-finder"
      }
    }
  }
}
```

---

## 🔄 n8n & Make.com Automation

A fully configured production n8n workflow template is bundled in this repository as [`workflow.json`](./workflow.json).

1. In n8n, click **Workflow** -> **Import from File...** and select `workflow.json`.
2. Provide your `APIFY_TOKEN` in the environment variables or HTTP Request node.
3. Schedule it to run daily or trigger on demand from webhooks.

---

## 📊 Output Schema Highlights

Each returned item includes normalized, RFC-compliant fields:
- `firstName`
- `lastName`
- `domain`
- `resolved_email`
- `confidence_score`
- `pattern_matched`

---

## 🏷️ Pricing & 60% Launch Discount

- **Apify Store:** Available under pay-per-result pricing with a **60% Launch Discount**.
- **Run Online:** Test it instantly on the [Apify Store Console](https://apify.com/deepaksheoran172/b2b-decision-maker-email-finder).
- **Fleet Hub:** Explore all 62 enterprise scrapers and MCP servers at [b2b-mcp-apify-scrapers-hub](https://deepakshe.github.io/b2b-mcp-apify-scrapers-hub/).

---

## 🛡️ 100% Automated Self-Service & Zero-DM Guarantee

- **Pure Self-Service:** Runs autonomously via Apify Cloud API. No sales calls, manual configuration, or onboarding tickets needed.
- **Pay-Per-Result:** Only successful output items are billed. Zero-charge on failed executions.
- **API Documentation:** For key creation, webhooks, and concurrency settings, see [Apify Docs](https://docs.apify.com/platform/actors/running/api).

---

## 📄 License

MIT License. Free for personal, commercial, and enterprise integration.
