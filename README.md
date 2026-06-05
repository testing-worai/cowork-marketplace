# wor-training — Cowork Operator Training Plugin

Interactive Claude Cowork operator training by [Work On Referrals, Inc.](https://workonreferrals.com)

`wor-training` is a paid plugin that turns Claude Cowork into a structured curriculum for learning the Cowork product. The plugin itself is a thin connector: it ships a skill file plus an `.mcp.json` pointing at our remote MCP server, which serves curriculum content one segment at a time.

## Installation

In Claude Cowork:

1. Open **Customize → Browse Plugins**
2. Add this marketplace: `testing-worai/cowork-marketplace`
3. Install **wor-training**
4. Say *"train me"* to start

You will be prompted for a license key on first use. Licenses are issued via a standalone Stripe Payment Link; the key is emailed to you within a minute of checkout.

## What's in this repository

- `.claude-plugin/marketplace.json` — marketplace manifest
- `plugins/wor-training/` — the plugin source
  - `.claude-plugin/plugin.json` — plugin manifest
  - `.mcp.json` — MCP server connection (remote, Streamable HTTP)
  - `skills/train-05-06-2026/SKILL.md` — pedagogical orchestration

This repository is **plugin source only**. The MCP server backend, curriculum content, and infrastructure live in a private Work On Referrals repository.

## Privacy Policy

`wor-training` collects only the minimum data required to deliver training content and process payments: your license key, name, email, and Stripe billing metadata. We do not log Claude conversation content, prompt text, or response text. No personal data is sold or shared with third parties beyond Stripe (billing) and Resend (license-email delivery).

Full policy: **[workonreferrals.com/privacy](https://workonreferrals.com/privacy/)**. Subprocessor list: **[workonreferrals.com/subprocessors](https://workonreferrals.com/subprocessors)**.

For data-handling questions, contact [operations@workonreferrals.com](mailto:operations@workonreferrals.com).

## Security

Found a security issue? See [SECURITY.md](SECURITY.md) for our disclosure policy. Reports go to [operations@workonreferrals.com](mailto:operations@workonreferrals.com).

## Support

Email: [operations@workonreferrals.com](mailto:operations@workonreferrals.com)

## License

[MIT](LICENSE) — see the LICENSE file for the full text.

The MIT license applies to plugin code in this repository. Curriculum content delivered by the remote MCP server is proprietary and is not redistributable independent of an active paid license.
