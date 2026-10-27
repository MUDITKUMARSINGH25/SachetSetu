# SachetSetu — Scam Check & Recovery Guide

**Theme:** Digital Safety & Cyber Fraud Awareness (with Digital Inclusion and Elderly Care)

**Tagline:** Stop. Check. Secure.

SachetSetu is an offline-first, multilingual public-awareness prototype for people in India. It helps a user (1) inspect a suspicious SMS/chat/email for explainable warning signs, (2) understand why each signal matters, (3) select what has already happened and see a stage-appropriate response checklist, and (4) practise safer reactions through a short family-friendly quiz.

## What makes this proposal different from a generic “scam detector”

- **Before and after:** It does more than label a message. Its incident-response mode adapts to whether the user ignored it, clicked a link, exposed credentials, gave remote access, or sent money.
- **Explainable:** Every triggered heuristic displays its reason. The score is a warning indicator, not a probability.
- **Local-first:** The analysis uses JavaScript in the browser. No text is sent to a server or external AI API; no user account is needed.
- **Local-language access:** English, Hindi, and Punjabi UI, examples, explanations, and response guidance.
- **Designed for family/community use:** A short practice quiz and a printable safety card support awareness sessions.
- **Low deployment barrier:** No paid APIs, database, cloud account, or special hardware are required.

## Run the prototype

### Option A — Local web server (recommended)

Requires Python 3, already installed on many computers. No dependencies need to be installed.

```bash
cd SachetSetu_Hackathon_Pack
python3 -m http.server 8000
```

Open `http://localhost:8000` in a browser. Stop the server with `Ctrl+C`.

### Option B — Node tests

Requires Node.js 18+ (no npm packages are downloaded).

```bash
npm test
```

The tests exercise example classifications, a low-signal message, multilingual detection, and the incident checklists.

### Offline/PWA behaviour

The app has no external runtime dependencies. When served over localhost or HTTPS, the service worker caches the interface files for subsequent offline use. A browser can also open the local files, but module restrictions vary by browser; the local web-server method is the recommended demonstration path.

## Architecture

```text
index.html + styles.css
        |
        v
src/app.js  ---- language selector / checker / quiz / incident response UI
        |
        v
src/scam-engine.js ---- local transparent rules + example messages + response plans
        |
        v
Browser only — no message upload, telemetry, user profile, or cloud model
```

### Rule engine

The engine uses a small set of readable regular-expression rules for warning patterns such as credential requests, urgency/threats, payment or refund tricks, links, impersonated authority, remote-access requests, unexpected prizes, and secrecy pressure. A message may trigger multiple rules. The displayed score is the sum of heuristic points capped at 100, bucketed into high (55+), check carefully (25–54), or few known signals (0–24).

**Important:** These thresholds are prototype heuristics. They have not been calibrated on a representative corpus. A low score does not establish that a message is safe, and a high score does not establish that it is fraudulent. False positives and false negatives are expected. Never use this prototype as the sole basis for a financial or safety decision.

## Emergency guidance

For suspected financial cyber fraud in India, the app points users to **1930** and the official National Cyber Crime Reporting Portal: <https://cybercrime.gov.in/>. The app does not submit a complaint, contact a bank, trace a transaction, or promise that money can be recovered. Use the official directions and the bank/payment provider’s contact details obtained independently.

## Test status

Run `npm test` to execute the included Node test suite. The current tests are smoke tests over hand-authored synthetic examples, not an accuracy evaluation. No real victims’ messages or personal data are used.

## File map

- `index.html` — interface and accessible form structure
- `styles.css` — responsive visual design and print styles
- `src/app.js` — UI, language switching, quiz, and view state
- `src/scam-engine.js` — transparent heuristics, sample messages, and incident plans
- `tests/engine.test.js` — automated smoke tests
- `data_test_cases.json` — synthetic message examples and expected signal coverage
- `docs/problem_statement.md` — localized problem framing and target beneficiaries
- `docs/validation_plan.md` — proposed pilot and metrics; no fabricated impact claims
- `docs/demo_script.md` — 3–5 minute prototype narration and shot plan
- `docs/demo_narration.md` — narration for the optional synthesized demo-video draft
- `docs/GITHUB_PUBLISHING.md` — steps to create the public repo before uploading the source
- `docs/AI_disclosure.md` — draft disclosure to reconcile with the final submission
- `docs/submission_checklist.md` — submission and eligibility checklist
- `presentation/SachetSetu_HSC_Official_Template_NEEDS_TEAMID_AND_REPO.pdf` — seven-slide official-template draft; replace the Team ID and public repository URL before submission

## Open-source license

MIT. See `LICENSE`.

## Authoritative references

1. MY Bharat, “Hack for Social Cause — Youth Tech Challenge 2027”: <https://mybharat.gov.in/pages/hack-for-social-cause>
2. National Cyber Crime Reporting Portal: <https://cybercrime.gov.in/>
3. Government of India, Ministry of Home Affairs, information on 1930 financial cyber-fraud reporting: <https://www.mha.gov.in/>

The MY Bharat page currently displays inconsistent submission dates in different sections. Confirm the live portal’s submission state and any official updates before assuming an entry can still be submitted.
