# @rcs-kz/mcp-1c — License

Copyright © 2026 RCS (IP KVANT, IIN 871228350772) · licenses@rcs.kz · Astana, Kazakhstan

Edition of 21 November 2026. Applies to license keys issued on or after this date.

## Trial

A trial license key is issued on request via https://rcs.kz/product/mcp-1c for the period stated when the key is issued.

- **Permitted use:** evaluation of the software on your own 1С databases
- **Forbidden:** redistribution, sublicensing, removal or circumvention of license-check code
- After the trial period the key stops working; continued use requires a Pro or Team subscription

There is no free tier. Solo keys issued before 21 November 2026 remain valid until their stated expiry under the terms in force when they were issued.

## Pro/Team Tier (Commercial)

Paid tiers (Pro 14 900 ₸/month, Team 44 900 ₸/month) are governed by a separate Service Agreement, concluded on request via https://rcs.kz/product/mcp-1c, and include:

- Unlimited API calls (Pro: 1 database, Team: up to 5)
- Write tools: `execute_code`, `write_object`, `post_document`
- Right to use in commercial software development and operations
- 24-hour email support (Pro), 4-hour SLA on critical issues (Team)

## Source Code

The Node bootstrap `bin/mcp-1c.js` is readable so customers can verify how the server is launched. The Python server ships in compiled form (see NOTICE.md); the plain source is not distributed.

This is **not an open-source license**. Source visibility ≠ permission to fork, redistribute, or sublicense.

## MCPService 1C Extension

The companion `MCPService.cfe` 1С extension (downloadable from GitHub Releases) is provided **free of charge** for use together with a valid trial or paid license key of this product. The extension itself is required to use the product.

## Disclaimer

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED. The maintainer (RCS) is not liable for any damages arising from use of this software. Customers are responsible for backing up their 1С databases before using write operations.

## Termination

License keys may be revoked in case of:
- Confirmed redistribution of paid features without authorization
- Use that violates the laws of the customer's jurisdiction or Kazakhstan
- Chargebacks or fraudulent payment activity

Revoked keys return `status: "revoked"` from the verification endpoint, and the client immediately blocks subsequent tool calls.

## Governing Law

These terms are governed by the laws of the Republic of Kazakhstan. A written claim is required before going to court; the response period is 15 calendar days. Disputes that cannot be settled are resolved by the Specialized Inter-District Economic Court of Astana.

## Changes to These Terms

New editions are published in this repository. A new edition applies to keys issued after its publication; existing paid subscriptions move to it on renewal, and material changes are announced by email at least 30 days in advance.

## Contact

For licensing questions, custom enterprise terms, or partnership inquiries:

📧 **licenses@rcs.kz** (24h response)
🌐 **https://rcs.kz**

---

By using `@rcs-kz/mcp-1c`, you agree to these terms.
