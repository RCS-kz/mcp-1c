# mcp-1c

> **Production MCP server for 1C:Enterprise.** Connect Claude Desktop, Cursor, Cline, Continue to your 1С database — read invoices, contracts, partners; create documents; conduct postings — all through AI conversations.

**Install:**

```bash
npm install -g @rcs-kz/mcp-1c
```

**Get free Solo license:**

```bash
curl -X POST https://bitrix24-mcp-license.shahruh.workers.dev/freemium \
  -H "Content-Type: application/json" \
  -d '{"email":"you@company.com","product":"mcp-1c"}'
```

**Add to Claude Desktop config**, install [MCPService.cfe](releases/latest) into your 1С database — and you're set.

Full docs: [npmjs.com/package/@rcs-kz/mcp-1c](https://www.npmjs.com/package/@rcs-kz/mcp-1c)

---

## Pricing

| Tier | Price | What you get |
|---|---|---|
| Solo | **$0/forever** | 10 calls/day, read-only (4 tools), personal use |
| Pro | $20/month | Unlimited, write enabled, 1 database, 24h support |
| Team | $80/month | 5 databases, custom tools, 4h SLA |

[Start 14-day Pro trial →](https://rcs-kz.lemonsqueezy.com)

---

## Source code

This repository contains documentation, install guides, and the MCPService 1C extension (`.cfe` source).

**The Python MCP server source is NOT in this repository.** The runtime ships only via npm (`@rcs-kz/mcp-1c`) as PyArmor-obfuscated bytecode. This protects the maintainer's IP while allowing transparent license verification (server runs locally, only checks license online).

For security audit, threat model, and trust questions — see [NOTICE.md in the npm package](https://www.npmjs.com/package/@rcs-kz/mcp-1c?activeTab=code).

## Issues & Support

- 🐛 **Bug reports:** [open an issue](issues/new?template=bug_report.md)
- 💡 **Feature requests:** [open an issue](issues/new?template=feature_request.md)
- 💬 **Questions:** [GitHub Discussions](discussions)
- 📧 **Email:** licenses@rcs.kz (24h response)

## Related products

- [@rcs-kz/bitrix24-mcp](https://github.com/rcs-kz/bitrix24-mcp) — MCP server for Bitrix24 CRM (45 tools)

Use both together for full 1C+CRM AI workflows.

## Maintainer

[RCS](https://rcs.kz) · Bitrix24 partner agency · Almaty, Kazakhstan

---

© 2026 RCS · Commercial software with free Solo tier · See LICENSE.md
