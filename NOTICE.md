# Notice — @rcs-kz/mcp-1c

## Code protection

This npm package contains **PyArmor-obfuscated** Python code (`python-protected/`). The plain source (`python/server.py`) is NOT distributed:

- ❌ Not in npm artifact (excluded via `.npmignore`)
- ❌ Not in public GitHub repo (excluded via `.gitignore`)
- ❌ Not in any GitHub Release archive

The obfuscation includes:
- Multi-platform native runtime (`pyarmor_runtime_000000/`)
- Bytecode-level encryption (PyArmor v9)
- Anti-debug guards
- Online license check via Cloudflare Worker

This protects the maintainer's intellectual property while allowing transparent license verification.

## Why protect a Python package?

Python is interpreted — anyone with `cat` can read source. Without obfuscation:
- Solo (free) tier code is trivially extracted
- Pro/Team tools can be unlocked by removing license-check
- Custom paid features can be cloned

PyArmor obfuscation raises the bar from "5-second copy-paste" to "needs serious reverse-engineering effort". Combined with **online license verification** (Ed25519-signed JWT, server-side revocation), this provides commercially-viable IP protection.

## What you CAN audit

- `bin/mcp-1c.js` — Node bootstrap (open, readable)
- `README.md` — full feature list, pricing, FAQ
- `LICENSE.md` — terms and conditions
- Network behavior — server runs locally, only license-verify endpoint is contacted (`https://bitrix24-mcp-license.shahruh.workers.dev/verify`)
- 1C extension `MCPService.cfe` — readable BSL code (separate download, free)

## Reporting security issues

If you discover a security vulnerability, please email **licenses@rcs.kz** privately. Do not open a public GitHub issue.

## Reporting license-check bypass attempts

Sharing license-check bypasses or distributing patched binaries violates the license agreement and may result in:
1. Immediate revocation of all your license keys
2. Termination of subscription without refund
3. Legal action under applicable IP laws

## Maintainer

RCS · Almaty, Kazakhstan
licenses@rcs.kz
