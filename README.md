# 📊 E-Commerce Risk Register — GRC Portfolio Project

![Status](https://img.shields.io/badge/status-complete-brightgreen)
![Type](https://img.shields.io/badge/type-GRC%20%2F%20Risk%20Management-blue)
![Tool](https://img.shields.io/badge/built%20with-Excel-217346)
![License](https://img.shields.io/badge/license-MIT-lightgrey)

> A full enterprise risk register I built from scratch for BRIGHTLEAF, a mid-sized e-commerce company, covering the complete methodology from risk identification through executive reporting. I built this as a hands-on demonstration of core GRC skills.

---

## 📑 Table of Contents

- [Why This Project Exists](#why-this-project-exists)
- [The Business Case](#the-business-case)
- [What's Included](#whats-included)
- [Methodology](#methodology)
- [Where the Risks Actually Came From](#where-the-risks-actually-came-from)
- [Scoring Model](#scoring-model)
- [Repository Structure](#repository-structure)
- [Sample Output](#sample-output)
- [Key Findings](#key-findings)
- [A Note on Scope: What Made the Cut and What Didn't](#a-note-on-scope-what-made-the-cut-and-what-didnt)
- [Skills Demonstrated](#skills-demonstrated)
- [How to Use This Repo](#how-to-use-this-repo)
- [Lessons Learned](#lessons-learned)
- [Future Improvements](#future-improvements)
- [About This Project](#about-this-project)

---

## Why This Project Exists

Most people learning GRC read about risk registers. I wanted to build one, the way it would actually be built on the job that would involve scoping the business, identifying risk across categories most people forget to check, scoring it defensibly instead of by gut feel, and then translating the whole thing into something a non-technical executive would actually approve budget against.

This repo is the full trail: the workbook, the raw methodology, the reasoning behind every risk score, and the executive-facing writeup. It is detailed.

---

## The Business Case

The register is built around a realistic profile: a mid-sized e-commerce company (~200 employees) selling physical goods online, processing customer payments (bringing PCI DSS into scope), storing customer PII, and depending on third-party vendors for hosting, logistics, and payment processing. Every risk in the register is derived directly from a specific fact about how this kind of business actually operates.

---

## What's Included

| File | Description |
|---|---|
| `risk_register.xlsx` | The full working register — live formulas, conditional formatting, data validation, and a legend tab explaining every scoring decision |
| `risk_register_raw_data.pdf` | Every risk broken out field-by-field, for anyone who wants to rebuild the register from scratch in their own format |
| `docs/executive_walkthrough.md` | A full narrative of how this would be presented to a leadership team, including anticipated pushback questions and how I'd answer them |
| `docs/methodology_notes.md` | Extended notes on where each risk, control, and score actually came from |

---

## Methodology

The register was built following a 10-step process:

1. **Define scope** — core e-commerce operation: payments, customer data, vendor/hosting dependencies, day-to-day operations
2. **Identify risks** across six categories: Cybersecurity, Third-Party/Vendor, Compliance, Operational, Financial, Reputational
3. **Write clear, specific risk descriptions** — avoiding vague statements like "cybersecurity risk"
4. **Define likelihood and impact scales in writing before scoring anything**
5. **Score inherent risk** (Likelihood × Impact, no controls considered)
6. **Document existing controls** for each risk
7. **Score residual risk** (Likelihood × Impact, controls considered)
8. **Select a treatment strategy** — Mitigate, Transfer, Avoid, or Accept
9. **Assign an owner and target date** for every open risk
10. **Define a review cadence** — quarterly, with per-risk review dates built in

---

## Where the Risks Actually Came From

This is the part most portfolio projects skip, and it's the part I think matters most. I didn't just formulate the risks. I had to understand how to come up with important risks so that nothing salient is left out. Every risk here traces back to one of four real sources:

- **The business model itself** — online payments imply payment fraud risk; a single overseas supplier implies shipping-delay risk; one DevOps engineer with no backup implies key-person risk.
- **Documented real-world incidents** — the business email compromise risk is modeled directly on a real, publicly reported case that cost a company over $46 million through employee impersonation alone, no hacking involved.
- **Regulatory obligation** — accepting card payments brings PCI DSS into scope automatically, which is where the compliance risk comes from.
- **Standard threat catalogs** — cross-checked against common risk categories from frameworks like ISO/IEC 27005 and NIST SP 800-30, so the list isn't limited to whatever happened to come to mind.

I also added a risk after the initial build — a DDoS attack against the checkout system. This was specifically to show the register is a living document, not a one-time exercise. Full reasoning for that addition, including why the remediation deadline was deliberately set ahead of the holiday shopping season, is in `docs/methodology_notes.md`.

---

## Scoring Model

Likelihood and Impact are each scored 1–5, multiplied for a score of 1–25, and grouped into four bands:

| Score Range | Level | Response |
|---|---|---|
| 1–4 | 🟢 Low | Monitor; accept or address at routine review |
| 5–9 | 🟡 Medium | Assign owner and treatment plan within normal planning cycle |
| 10–14 | 🟠 High | Prioritize treatment; report to management |
| 15–25 | 🔴 Critical | Immediate action required; escalate to leadership |

Impact thresholds are anchored to concrete dollar figures (e.g., "Major" = $250K–$1M impact) rather than vague labels, so scoring is repeatable and defensible rather than a matter of individual opinion. Full scale definitions are in the workbook's **Instructions & Legend** tab.

---

## Repository Structure

```
ecommerce-risk-register/
│
├── README.md                          <- you are here
├── risk_register.xlsx                 <- the full risk register workbook
├── risk_register_raw_data.pdf         <- field-by-field data for manual rebuilds
│
├── docs/
│   ├── executive_walkthrough.md       <- narrative for presenting to leadership
│   └── methodology_notes.md           <- extended notes on scoring rationale
│
├── screenshots/
│   ├── legend_tab.png
│   ├── risk_register_tab.png
│   └── risk_matrix_tab.png
│
└── LICENSE
```

---

## Sample Output

| Risk ID | Category | Description | Inherent Score | Inherent Level | Residual Score | Residual Level |
|---|---|---|---|---|---|---|
| R-001 | Cybersecurity | Unauthorized access to payment data via broad access permissions | 15 | 🔴 Critical | 10 | 🟠 High |
| R-002 | Cybersecurity / Fraud | BEC scam tricking Finance into fraudulent wire transfer | 16 | 🔴 Critical | 8 | 🟡 Medium |
| R-010 | HR / Cybersecurity | Social engineering due to limited security awareness training | 12 | 🟠 High | 6 | 🟡 Medium |
| R-011 | Cybersecurity / Availability | DDoS attack causing checkout downtime | 12 | 🟠 High | 4 | 🟢 Low |

*(Full 11-row register, live formulas, and conditional formatting visible in the workbook.)*

---

## Key Findings

- **Three risks scored Critical on an inherent basis** — unauthorized payment data access, BEC-style fraud, and an unpatched vulnerability exposing customer PII.
- **One risk remained High even after existing controls** — employee susceptibility to social engineering, because the only current control was a single onboarding session rather than ongoing training.
- **Existing controls consistently reduced likelihood more than impact** — a pattern worth calling out on its own, since it shows controls were shifting *probability* down without necessarily reducing *severity* if something still went wrong.
- **Remediation timing was tied to the business calendar, not just severity** — the DDoS mitigation deadline was deliberately set before the holiday shopping season, since the same attack carries very different stakes depending on when it happens.

---

## A Note on Scope: What Made the Cut and What Didn't

Part of doing this well is knowing what *doesn't* belong on a GRC risk register, not just what does. While building this out, I considered adding "low SEO ranking" as a risk and deliberately didn't, for a specific reason: it doesn't have a security or compliance trigger event behind it, which is what a GRC register is built around. Where it's genuinely relevant, it shows up as a *consequence* inside an existing risk instead — for example, a security incident leading to search engine blacklisting is noted as part of that risk's impact, not treated as a standalone line item. That distinction is a judgment call I think is worth documenting, since knowing what to leave out is as much a part of the skill as knowing what to include.

---

## Skills Demonstrated

- Risk identification and categorization across multiple domains (not just cybersecurity)
- Quantitative risk scoring methodology (Likelihood × Impact)
- Distinguishing inherent vs. residual risk
- Control mapping and treatment planning (Mitigate / Transfer / Avoid / Accept)
- Building a usable, non-technical deliverable (formulas, conditional formatting, data validation in Excel)
- Translating technical risk analysis into a narrative for a non-technical executive audience
- Judgment on risk register scope — recognizing what belongs on a GRC register versus what belongs elsewhere
- Familiarity with underlying frameworks: NIST RMF, NIST SP 800-30, ISO 27005, ISO 31000, PCI DSS, COBIT

---

## How to Use This Repo

1. Download `risk_register.xlsx`
2. Start with the **Instructions & Legend** tab to understand the scoring model
3. Review the **Risk Register** tab — yellow cells are editable inputs, all scores/levels calculate automatically
4. Use the **Risk Matrix (Reference)** tab as a quick visual reference for any Likelihood × Impact combination
5. Read `docs/executive_walkthrough.md` for the full narrative of how this would be presented to leadership
6. Use `risk_register_raw_data.pdf` if you want to rebuild the register from scratch in your own format, as practice

---

## Lessons Learned

- Defining the likelihood and impact scales *before* scoring anything was the single most important step as it's what makes the scores defensible rather than subjective.
- Separating inherent and residual risk changes the entire conversation with leadership. It shows the value of existing controls instead of just presenting a flat list of dangers.
- A risk register is only useful if someone owns each line item. Risks without an assigned owner and date tend to just sit there.
- Knowing what *not* to include is as much a skill as knowing what to include. Not every business concern belongs on a GRC risk register.

---

## Future Improvements
These are recommendations I'd consider:
- [ ] Add a live dashboard (Power BI or a simple Python/matplotlib script) visualizing risk distribution by category and level
- [ ] Expand to a second company in a different industry, to practice adapting the impact scale to a different risk appetite
- [ ] Add a simple risk trend log to show how residual risk scores change over multiple quarterly reviews
- [ ] Map each risk to specific ISO 27001 Annex A / NIST CSF controls for a fuller GRC-framework tie-in

---

## About This Project

Built as part of a self-directed 2026 GRC learning journey, documenting hands-on practice with core GRC deliverables alongside relevant frameworks and certifications (CGRC, CRISC, ISO 27001).



---

## License

This project is released under the [MIT License](LICENSE) — feel free to fork, adapt, and use this template for your own GRC practice projects.
