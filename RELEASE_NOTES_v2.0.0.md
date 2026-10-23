# v2.0.0 — Missing security layers

Second release of Selfhack. v1.0.0 covered the OWASP Top 10 (web, API, LLM) well but was built as a single heavy pass. v2 adds the layers that were missing and makes the default workflow lighter.

## What's new

**Lighter default + release gate**
- Three operational modes: `Quick scan` (small diffs), `Standard review` (new default), `Full assessment` (releases).
- Hard requirement: an **independent re-check** must sign off before any `RELEASE` or `CONDITIONAL RELEASE` verdict. One agent's confidence in its own work is no longer treated as evidence.

**Seven new web/API checks (WEB-21 through WEB-27)**
- **WEB-21 Token & JWT pitfalls** — `alg:none`, RS256↔HS256 confusion, `kid` traversal, weak HMAC secrets, `jwk` header trust, token storage.
- **WEB-22 HTTP-layer attacks** — request smuggling (CL.TE, TE.CL, TE.TE), web cache poisoning, host-header injection, open redirect beyond OAuth, `X-Forwarded-For` rate-limit bypass.
- **WEB-23 Deserialization & language injection** — SSTI (Jinja/Twig/EJS/Handlebars/Liquid), unsafe deserialization (pickle, YAML, PHP, .NET, Java gadgets), prototype pollution, ReDoS, timing-unsafe comparison.
- **WEB-24 Third-party frontend integrity** — SRI, CSP allowlists, Magecart-style tag-manager injection, `postMessage` origin validation.
- **WEB-25 DNS & email identity** — SPF/DKIM/DMARC, subdomain takeover (Vercel, Netlify, Heroku, S3, Azure), DNSSEC.
- **WEB-26 Shadow endpoints & exposure** — `.git`, `.env`, `.DS_Store`, source maps, framework debug flags, stale preview deployments with prod creds.
- **WEB-27 Account recovery hijack** — Gmail plus-aliasing, unicode confusables, SIM-swap, MFA enrollment during reset, support "login as user" audit.

**AI supply chain (§7a)**
Slopsquatting (hallucinated package names), generated-code auditing, model API key leakage in logs/bundles, embedding corpus poisoning via public PRs, prompt leakage via error paths.

**Privacy & data protection (§8a)**
Data subject rights (access, portability, deletion through backups, caches, indexes, embeddings, processors), DPAs with sub-processors, consent withdrawal propagation, DPIA for AI features, GDPR 72-hour breach clock.

**Mobile, desktop, and extension apps (§8b)**
- iOS/Android: Keychain/Keystore, biometric gating, deep-link validation, App Attest / Play Integrity, insecure IPC, WebView hardening.
- Electron/Tauri: context isolation, `nodeIntegration` off, signed auto-updater, protocol handler validation.
- Browser extensions: Manifest V3 minimum permissions, content-script isolation, sender verification.

**Stack-specific presets (§9a)**
Supabase (RLS, service_role, storage), Firebase (rules, App Check, custom claims), Next.js App Router (Server Actions, `NEXT_PUBLIC_*`, image optimizer SSRF), Vite/SPA (no `VITE_*` secrets), Vercel/Netlify (env separation, preview access control), Stripe (webhook sig, idempotency, PCI SAQ scope, replay window).

**Chatbot & automation (§9b)**
Meta/WhatsApp HMAC, Telegram secret_token, prompt injection via customer messages, cost caps (per-conversation + daily + account), PII retention in n8n/Make/Zapier, multi-tenant workflow isolation.

**Optional free tools (§9c)**
gitleaks, trufflehog, semgrep, bandit, brakeman, osv-scanner, OWASP ZAP, nuclei, trivy, grype, checkov, tfsec, subjack, dnstwist, testssl.sh, MobSF.

**References**
Added OWASP MASVS/MASTG for mobile.

## Install

```bash
npx skills add karim4551308/selfhack
```

Or download `selfhack.zip` below and upload it in Claude's Skills settings.

## Known limitations

Selfhack is instructions, not a scanner. It can miss files on big projects, and results vary between runs. It cannot certify an app as secure or replace a professional assessment. Still planned: field-testing on real apps, splitting `SKILL.md` into smaller reference files, deeper container/K8s/IaC coverage.

Feedback and PRs welcome.

---

Full file: [`skills/selfhack/SKILL.md`](https://github.com/karim4551308/selfhack/blob/v2.0.0/skills/selfhack/SKILL.md)
Changelog in file: §15.
