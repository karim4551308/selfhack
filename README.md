# Selfhack

**Hack your own app first, before someone else does.**

Selfhack is an AI agent skill that turns your coding agent (Claude, Codex, Antigravity, Claude Code and other tools that support `SKILL.md` skills) into a careful security reviewer for **your own** web apps, APIs and AI features. It is built for vibe-coded and fast-shipped projects that need a real check before going live.

By **Karim** · MIT License · Version 2.0.0

---

> [!WARNING]
> **Early release, and not a certification.** Selfhack helps an AI agent find likely and demonstrated security problems, fix them, and verify the fixes. It cannot prove an app is secure, compliant, or "hack-proof". A `RELEASE` verdict means "no known blockers within what was tested", nothing more. Review its findings yourself, and get a professional assessment for high-risk or sensitive systems.

> [!IMPORTANT]
> **Only use it on systems you own or are explicitly authorized to test.** Installing or invoking the skill does not grant permission to scan any website, API or third-party service. The skill is designed to start with read-only review and to ask before any active testing.

---

## What it does

- **Threat model** your app: assets, users, roles, data flows and trust boundaries.
- **Test realistic failures** safely with synthetic data: broken access control, leaked secrets, injection, unsafe webhooks, business-logic abuse, AI prompt injection and more.
- **Report with evidence**: every PASS needs proof; anything only reviewed is labeled "review-only"; skipped checks never count as passed.
- **Fix and verify**: small fixes at the right layer, plus regression tests.
- **Give an honest verdict**: `RELEASE`, `CONDITIONAL RELEASE`, `HOLD`, or `INSUFFICIENT EVIDENCE`.

It maps its checks to current OWASP references: Top 10:2025 (web), API Security Top 10:2023, LLM Top 10:2025, and ASVS 5.0.0.

## What's new in v2.0.0

- **Assessment modes** — `Quick scan` for small diffs, `Standard review` as the new default, `Full assessment` for releases.
- **7 new web/API checks (WEB-21–27)** — JWT pitfalls, HTTP-layer attacks (request smuggling, cache poisoning, host-header injection), deserialization and language injection (SSTI, pickle, prototype pollution, ReDoS), third-party frontend integrity (SRI, CSP, Magecart), DNS and email identity (SPF/DKIM/DMARC, subdomain takeover), shadow endpoints and exposure, account recovery hijack.
- **AI supply chain** — slopsquatting, generated-code auditing, model API key leakage, embedding corpus poisoning, prompt leakage via error paths.
- **Privacy and data protection** — data subject rights, processors, consent, DPIA for AI features, breach notification.
- **Mobile, desktop, and extension apps** — iOS/Android, Electron/Tauri, Manifest V3 extensions.
- **Stack-specific presets** — Supabase, Firebase, Next.js, Vite, Vercel/Netlify, Stripe.
- **Chatbot and automation** — Meta/WhatsApp, Telegram, n8n, Make, Zapier with cost caps and PII retention.
- **Independent re-check required** before any `RELEASE` or `CONDITIONAL RELEASE` verdict.
- **Optional free tools** list (gitleaks, semgrep, OSV-Scanner, ZAP, trivy, checkov, etc.).

See the full changelog in [§15 of `SKILL.md`](skills/selfhack/SKILL.md).

## Install

The skill lives in [`skills/selfhack/SKILL.md`](skills/selfhack/SKILL.md). Every install method below just puts that folder where your tool looks for skills.

### Any tool (one command)

If you have Node.js:

```bash
npx skills add karim4551308/selfhack
```

### Claude (claude.ai and the desktop app)

1. Download [`dist/selfhack.zip`](https://github.com/karim4551308/selfhack/raw/main/dist/selfhack.zip).
2. Upload it in Claude's settings, in the Skills section. Don't unzip it first.

### Claude Code

Copy the `skills/selfhack` folder to:

- All projects: `~/.claude/skills/selfhack/`
- One project: `<your-project>/.claude/skills/selfhack/`

### Codex (OpenAI)

Copy the `skills/selfhack` folder to:

- All projects: `~/.agents/skills/selfhack/`
- One project: `<your-project>/.agents/skills/selfhack/`

### Antigravity (Google)

Copy the `skills/selfhack` folder to:

- All workspaces: `~/.gemini/config/skills/selfhack/`
- One workspace: `<your-workspace>/.agents/skills/selfhack/`

Restart your tool after installing.

### Browser app builders (Lovable, Bolt, Replit, etc.)

These usually don't support skill folders and can't run real tests. Export or sync your project to GitHub, open it in one of the tools above, and run Selfhack there.

## Use it

Start with a read-only review:

```text
Use the selfhack skill on this project. Start with a read-only repository
review and threat model. Recommend an assessment profile, identify trust
boundaries, and create a prioritized test matrix. Ask only for missing scope
needed before active testing. Report evidence, untested areas, and release
blockers.
```

Before a launch:

```text
Run the release assessment using selfhack. Assess the exact release commit and
deployment configuration, produce the coverage and findings reports, verify
remediation, and recommend RELEASE, CONDITIONAL RELEASE, HOLD, or
INSUFFICIENT EVIDENCE. Do not deploy without authorization.
```

More example prompts are at the top of [`SKILL.md`](skills/selfhack/SKILL.md).

### For the best results

- Use your tool's **agent mode**, so it can read files and run tests.
- Open the **whole project folder**.
- Test against a **local or staging copy**, not production.
- If your app has logins, prepare **two test accounts**, so it can check whether one user can see another's data.

## Known limitations

Selfhack is instructions, not a scanner. On large projects the agent may skip files, and results can vary between runs. It cannot certify an app as secure, prove compliance, or replace a professional assessment for high-risk or sensitive systems. Treat its verdicts as a starting point, not a guarantee.

Still planned:

- Splitting `SKILL.md` into smaller reference files so agents follow it more reliably.
- Field-testing on real apps and recording what the skill catches versus misses.
- Deeper coverage for container, Kubernetes, and IaC-heavy stacks.

Feedback and pull requests are welcome. Please open an issue if the skill missed something on a real project.

## License

[MIT](LICENSE) © 2026 Karim. You can use, modify and share it; keep the copyright notice.
