# mcp-1c

> **Production MCP server for 1C:Enterprise.** Connect Claude Desktop, Cursor, Cline, Continue to your 1С database — read invoices, contracts, partners; create documents; conduct postings — all through AI conversations.

**Install (0.1.4):**

```bash
npm install -g https://github.com/RCS-kz/mcp-1c/releases/download/v0.1.4/rcs-kz-mcp-1c-0.1.4.tgz
```

`npm install -g @rcs-kz/mcp-1c` still installs 0.1.0 from npm (Python 3.10 only) until 0.1.4 is published there.

**Get free Solo license:**

```bash
curl -X POST https://bitrix24-mcp-license.shahruh.workers.dev/freemium \
  -H "Content-Type: application/json" \
  -d '{"email":"you@company.com","product":"mcp-1c"}'
```

**Requires Python 3.10, 3.11, 3.12 or 3.13** on Linux (x86_64, ARM64), macOS (Intel, Apple Silicon) or Windows x86_64 — version 0.1.4.

**Add to Claude Desktop config**, install [MCPService.cfe](https://github.com/RCS-kz/mcp-1c/releases/latest) into your 1С database — and you're set.

Full docs: [npmjs.com/package/@rcs-kz/mcp-1c](https://www.npmjs.com/package/@rcs-kz/mcp-1c)

---

## Pricing

| Tier | Price | What you get |
|---|---|---|
| **Solo** | **0 ₸ / forever** | 10 calls/day · read-only (4 tools) · personal use |
| **Pro** | **9 900 ₸/mo** | Unlimited · write enabled (7 tools) · 1 database · 24h support · commercial use |
| **Team** | **39 900 ₸/mo** | 5 databases · custom tools · 4h SLA · priority support |

**Pro or Team:** [request on rcs.kz](https://rcs.kz/request-promo?utm_source=github&utm_medium=readme&utm_campaign=mcp-1c) — monthly billing under contract. Details: [rcs.kz/product/mcp-1c](https://rcs.kz/product/mcp-1c)

**🆓 Free Solo activation (5 seconds, no credit card):**

```bash
curl -X POST https://bitrix24-mcp-license.shahruh.workers.dev/freemium \
  -H "Content-Type: application/json" \
  -d '{"email":"you@company.com","product":"mcp-1c"}'
```


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

[RCS](https://rcs.kz) (IP KVANT, IIN 871228350772) · 1C partner in Kazakhstan since 2009 · Astana, Kazakhstan

---

© 2026 RCS · Commercial software with free Solo tier · See LICENSE.md
