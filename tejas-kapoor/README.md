# Phishing Email Pattern Detector

> A rule-based phishing email detector that flags suspicious emails using weighted indicators, with no machine learning involved.

**Track:** Cybersecurity
**Candidate:** Tejas Kapoor
**Github Username**: TejasKapoor0353
**Phone Number**: Not provided
**Email ID**: bondtejas03@gmail.com

---

## 1. Overview

### What & Why
[Write 2-3 sentences in your own words: what phishing detection problem you're solving, and why you picked this project from the Cybersecurity track.]

### Expected Outcome
A detector that can classify an email as phishing or legitimate by scoring it against known phishing patterns (spoofed domains, suspicious links, urgency language, credential requests, risky attachments), with a transparent explanation of why each verdict was reached.

---

## 2. Requirements

### Hardware
Not applicable — this is a software-only project.

### Software
| Tool / Library | Version | Purpose |
|---|---|---|
| Python | 3.9+ | Core language, no external dependencies |
| `http.server` (standard library) | built-in | Local web server for the UI |
| `email` (standard library) | built-in | Parsing raw email text |

**Constraints:** No machine learning allowed; must use rule-based pattern matching only.

---

## 3. Design

### System Overview
An email (sender, subject, body, attachments) is passed into the detector. Each rule checks for one indicator — e.g. a look-alike sender domain, a mismatched link, urgent language, a request for credentials, or a risky attachment. Every indicator that fires adds weighted points to a score. If the total score crosses a threshold (5), the email is classified as PHISHING; otherwise LEGITIMATE.

[Add a diagram here if you want — `./docs/images/system-overview.png` — otherwise you can delete the image line below.]

![System Diagram](./docs/images/system-overview.png)

### Key Decisions
[Write in your own words: why weighted scoring instead of simple keyword counting; why whole-word matching was needed; why warning phrases like "never share your OTP" had to be excluded from triggering credential-request rules.]

---

## 4. Implementation

- `src/phishing_detector/detector.py` — the scoring engine: domain look-alike detection, link/href mismatch checks, URL shortener and raw-IP detection, urgency/threat/credential/lure keyword lists, attachment checks
- `src/phishing_detector/samples.py` — 5 known phishing emails and 5 known legitimate emails used for the demonstration
- `src/server.py` — local Python HTTP server exposing `/api/demo` and `/api/analyze` as a JSON API, and serving the website
- `src/web/index.html` — the website showing the demonstration results and a live analyzer for pasted emails
- `src/demo.py` — command-line version of the same demonstration
- `tests/test_detector.py` — unit tests covering the demo set and two specific bug fixes

[Add 2-3 sentences on anything you changed or added yourself.]

---

## 5. Demonstration

**Requirement: Test against 5 known phishing and 5 known legitimate emails, show correct classifications, report false positives/negatives, explain indicators.**

Run locally:
```bash
python src/demo.py
```
or start the website:
```bash
python src/server.py
# open http://127.0.0.1:8000
```

Both show, for all 10 emails: predicted verdict vs. actual label, the score, every indicator that fired, and a summary of correct classifications, false positives, and false negatives.

[Insert your demo video link here, e.g. an unlisted YouTube video showing `python demo.py` running and the website working.]

---

## 6. Final Result

### Working
- Correctly classifies all 5 phishing and 5 legitimate demo emails (10/10, 0 false positives, 0 false negatives)
- Website with live analyzer — paste any
