# bugbounty-triage

> A skill that lets an AI agent (Claude Code, Codex, Cursor …) behave like a bug bounty triager and validate your report before you submit. Useful if you hunt for vulnerabilities with an AI agent: reduces noise for you and for the triage team that will receive your report.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Format: SKILL.md](https://img.shields.io/badge/format-SKILL.md-7c3aed.svg)](https://github.com/anthropics/skills)

## Why

AI-assisted hunting produces longer, prettier, more confident reports. The underlying bugs often don't survive a triager who actually re-runs the PoC. `bugbounty-triage` runs that triage for you, on your own report, before you submit. If it validates, your odds of a clean accept from a real triager go up. Not a guarantee.

Web2 only: HackerOne, YesWeHack, Bugcrowd, Intigriti, and self-hosted programs.

## What it does

When you ask "triage this", `bugbounty-triage`:

1. Checks scope against the live program pages.
2. Replays the PoC end-to-end (Burp MCP, curl, or headless browser) and captures the request and response.
3. Fact-checks the endpoints, parameters, status codes, and headers cited in the report against what the app actually does.
4. Challenges validity. Self-XSS, missing headers, and CORS on public APIs are auto-rejected.
5. Sets severity from the replay, not the claim.
6. Decides fix-worthiness.
7. For valid findings, adds an acceptance and duplicate-risk read with a SUBMIT / HOLD / REVISE call.

Output: a single `triage-<vuln>.md` file with the verdict, the captured replay log, a weaknesses panel (3-5 attackable claims a counter-triager could raise), a SUBMIT / HOLD / REVISE call for valid findings, and action items.

## Install

```bash
npx skills add gobelinor/bugbounty-triage
```

The skill auto-triggers on phrases like "triage this", "review this report", "is this valid", "should I submit this", "validate this finding". Works on any agent that supports the [SKILL.md format](https://github.com/anthropics/skills).

## License

[MIT](LICENSE).
