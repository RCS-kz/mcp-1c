# @rcs-kz/mcp-1c — License

Copyright © 2026 RCS (IP KVANT, IIN 871228350772) · licenses@rcs.kz · Astana, Kazakhstan

## Solo Tier (Free)

The free Solo tier of `@rcs-kz/mcp-1c` is granted to any person under the following terms:

- **Permitted use:** personal exploration, learning, evaluation, non-commercial pet projects
- **Limits:** 10 API calls/day per license key, 1 connected 1С database, read-only tools (`ping`, `execute_query`, `get_metadata`, `get_object`)
- **Forbidden:** commercial use, redistribution, sublicensing, removal of license-check code

## Pro/Team Tier (Commercial)

Paid tiers (Pro 9 900 ₸/month, Team 39 900 ₸/month) are governed by a separate Service Agreement, concluded on request via https://rcs.kz/product/mcp-1c, and include:

- Unlimited API calls (Pro: 1 database, Team: up to 5)
- Write tools: `execute_code`, `write_object`, `post_document`
- Right to use in commercial software development and operations
- 24-hour email support (Pro), 4-hour SLA on critical issues (Team)

## Source Code

The Node bootstrap `bin/mcp-1c.js` is readable so customers can verify how the server is launched. The Python server ships obfuscated (`python-protected/`, see NOTICE.md); the plain source is not distributed.

This is **not an open-source license**. Source visibility ≠ permission to fork, redistribute, or sublicense.

## MCPService 1C Extension

The companion `MCPService.cfe` 1С extension (downloadable from GitHub Releases) is provided **free of charge** under the same Solo Tier terms above. The extension itself is required to use any tier of this product.

## Disclaimer

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED. The maintainer (RCS) is not liable for any damages arising from use of this software. Customers are responsible for backing up their 1С databases before using write operations.

## Termination

License keys may be revoked in case of:
- Confirmed redistribution of paid features without authorization
- Use that violates the laws of the customer's jurisdiction or Kazakhstan
- Chargebacks or fraudulent payment activity

Revoked keys return `status: "revoked"` from the verification endpoint, and the client immediately blocks subsequent tool calls.

## Contact

For licensing questions, custom enterprise terms, or partnership inquiries:

📧 **licenses@rcs.kz** (24h response)
🌐 **https://rcs.kz**

---

By using `@rcs-kz/mcp-1c`, you agree to these terms.
