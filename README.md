# Selfhack

**Hack your own app first, before someone else does.**

Selfhack is an AI agent skill that turns your coding agent (Claude, Codex, Antigravity, Claude Code and other tools that support `SKILL.md` skills) into a careful security reviewer for **your own** web apps, APIs and AI features. It is built for vibe-coded and fast-shipped projects that need a real check before going live.

By **Karim** · MIT License · Version 1.0.0 (early release)

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

This is an early release. Planned improvements:

- A lighter default mode and a quick scan for small changes (the current default is thorough and can be slow).
- Stack-specific checks for common vibe-coding stacks.
- Coverage for chatbots and automation platforms.
- A required independent re-check before release verdicts.
- Mobile and desktop apps are not covered.

Feedback and pull requests are welcome. Please open an issue if the skill missed something on a real project.

## License

[MIT](LICENSE) © 2026 Karim. You can use, modify and share it; keep the copyright notice.
