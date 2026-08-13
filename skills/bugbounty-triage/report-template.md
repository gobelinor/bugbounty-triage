# Triage Report Template

Read this file only when writing the final `triage-<vuln-name>.md`, after all gates are complete.

````markdown
# Triage Report: <vulnerability title>

**Report file:** <path to the original report>
**Date:** <today>
**Triager verdict:** <VERDICT>
**Assessed severity:** <Critical / High / Medium / Low / Informational>
**Reporter severity:** <what they claimed>

---

## Scope Check
<In scope / Out of scope. Which asset, which scope rule. Note the live-fetch date for the program pages.>

## Replay Log
<MANDATORY. The exact request(s) sent, the exact response(s) observed, the tool used, the date.>

```http
POST /api/v2/transfer HTTP/1.1
Host: target.example.com
Cookie: session=...REDACTED...
Content-Type: application/json

{"to": "attacker", "amount": 1, "from_account_id": 999}
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{"status": "ok", "transferred": 1, "from": "victim_user_42"}
```

<Tool: Burp Repeater (mcp__burp__create_repeater_tab) on YYYY-MM-DD. Two test accounts created via signup flow. Cross-tenant transfer confirmed.>

## Replay Assessment
<Did the replay match the report's claims? What was different? If you couldn't replay, what blocked you and what would unblock?>

## Validity Assessment
<Is this a real vulnerability? Direct challenge of the claims using the replay evidence. Don't speculate beyond what you observed.>

## Impact Assessment
<What's the real damage based on the replay? Severity justification. If downgraded from the reporter's claim, explain why with reference to the captured evidence.>

## Fix-Worthiness
<Worth developer time? Precedent implications?>

## Weaknesses Panel (mandatory even on VALID verdicts)
<Enumerate 3-5 concrete weaknesses a counter-triager could legitimately raise against this report. Specific attackable claims, not "could be better" bromides. Examples: "PoC uses test account A but cross-tenant access to user B is implied, not shown", "stored XSS payload only fires on the reporter's own profile page, not on a feed shared with others", "claimed CSRF chain depends on the victim staying logged in for 30+ minutes — not stated", "report quotes a `Server: nginx/1.18` header but the actual response shows `nginx/1.24`". If you cannot name 3 weaknesses, reread the report — every real report has them.>

<Also list LLM-slop signals present (length disproportionate to finding, template symmetry, repeated impact restatement, rhetorical dates, self-validation phrases, synthetic-looking logs). If two or more are present, note the slop-rejection risk.>

## Verdict

<2-3 sentences. The decision and the primary reason. No hedging.>

## Acceptance Risk Analysis
<Mandatory for VALID and VALID_DOWNGRADED verdicts. Skip only when an earlier gate returned a rejection verdict (INFORMATIVE, NOT_APPLICABLE, NEEDS_MORE_INFO, OUT_OF_SCOPE, DUPLICATE).>

### Acceptance risk
<Top 2-3 rejection / downgrade arguments the program could make, with probability bands. Include the steelman rejection.>

### Duplicate risk
<Low / medium / high with the signals that drove the call.>

### Recommendation
<SUBMIT / HOLD / REVISE with one sentence of reasoning.>

## Action Items
- <What happens next — e.g., "Accept and assign to security team", "Request PoC showing actual XSS execution in a current browser", "Close as informative, comment with explanation">
````
