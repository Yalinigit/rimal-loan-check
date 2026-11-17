# Rimal Bank Loan Check

**Built in 48 Hours #1 to #4 · "Why was I rejected?"**

Live demo: https://yalinigit.github.io/rimal-loan-check/

A demo of how a UAE bank could explain an automated loan decision to a customer, clearly and in their own language.

> Rimal Bank is fictional. The rules are simplified for a demo. This is not financial advice.

## The problem

When a loan application is declined, customers usually get a one-line "not approved" with no reason they can act on. For people new to the UAE, the cause is often something fixable, like a short credit history or too little time in a job. Nobody tells them that.

## What the app does

1. **You enter your numbers:** salary, existing monthly payments, loan amount, term, months in your job and months of credit history.
2. **Fixed rules make the decision.** Three transparent checks:
   - Debt ratio (all monthly repayments ÷ salary) of 50% or less
   - At least 6 months in your current job
   - At least 6 months of credit history
3. **You see why, and what to do next:** each check shows your figure next to the requirement. The next steps use your numbers, such as the largest loan that fits or the date you can re-apply.
4. **English or Arabic:** the explanation switches to Arabic with a right-to-left layout.

Three examples are built in: **Sara** (new to the UAE, declined), **Omar** (settled, approved) and **Layla** (passes the rules, but the risk model flags her, so a person decides).

## Product decisions

| Decision | Why |
|---|---|
| Rules decide, AI only explains | Lending decisions must be consistent and auditable. AI is used where it helps most: plain-language explanation. |
| Show "yours vs needed" for every check | Customers understand a gap faster than a paragraph. |
| Every reason comes with a next step | A decline without a path forward loses the customer. |
| Arabic from day one | Arabic is the official language of the UAE. |
| State which factors are never used | Builds trust: nationality, gender, religion and age are not inputs. |

## How it's built

- One `index.html` file: HTML, CSS and plain JavaScript, with no framework and no build step.
- Monthly payment uses a standard amortisation formula at an assumed 7% yearly rate.
- **AI explanation:** when opened inside claude.ai, the page asks Claude to write a personal explanation from the decision facts only. Anywhere else, such as this GitHub Pages version, the app shows a built-in standard explanation generated from the same rules.

## Run it locally

1. Open this folder in VS Code.
2. Install the **Live Server** extension.
3. Right-click `index.html` → **Open with Live Server**.

## Stage #3 · Open Finance + path to approval

A reason only helps if the customer can act on it. Stage #3 turns every reason into **reason → action → timeline**.

1. **Open Finance consent (simulated).** A thin-file customer can share 12 months of salary deposits, rent and bills. The consent screen covers who is asking, what data is read, what is *not* shared, why, and for how long. It is modelled on Al Tareq, the UAE Central Bank's Open Finance consent layer.
2. **Alternative data counts (demo policy).** 6+ months of on-time rent and bills counts as credit history. 6+ months of steady salary, even across a job change, counts as time in work. Affordability (the 50% debt ratio) is never waived.
3. **Your path to approval.** Each failed check and each model driver gets a concrete action, a date ("Today" or "By 15 Jan 2027") and its effect, such as "Model risk 3.7% → 2.7%" for bringing card usage under 30%.
4. **Try this plan.** One click applies the plan and re-runs the decision. Sara goes from 3 failed checks to approved.

| Decision | Why |
|---|---|
| Open Finance fills gaps, it never overrides affordability | It shows how someone pays; it does not make an unaffordable loan safe. |
| Consent says what is *not* shared | Trust depends on knowing the limits, not just the scope. |
| Every action has a date | "Improve your credit" is not actionable; "by 15 Jan" is. |
| Model what-ifs on the plan | Shows the customer which change matters most. |

## Stage #4 · Human review + audit trail

An automated decision is only ready for a bank when a person can step in and when someone can later prove what happened. Stage #4 adds both.

1. **Ask for a human review.** On any decline, the customer can ask a person to look at it, with a reason and a short note. They get a case reference and, later, the outcome and its reason in English or Arabic.
2. **Model flags go to a person.** When the rules pass but the risk model sees risk above appetite (Layla), the application is not approved automatically. It is held and sent to the review queue.
3. **Bank view.** A reviewer sees the queue, the case facts (checks, model drivers, Open Finance use, the customer's reason) and records an outcome with a reason code and a note.
4. **Guardrail on overrides.** A reviewer can overturn a time-in-job or credit-history decline with evidence. Nobody can approve above the 50% debt ratio.
5. **Audit trail.** Every decision, consent, explanation (the exact text shown), plan and review is logged in order, with who did it. Each entry stores a SHA-256 hash of its content plus the previous entry's hash, so a later edit breaks the chain. "Verify log" checks it, "Simulate tampering" shows it failing, and the log exports to CSV.

| Decision | Why |
|---|---|
| Two routes to a person: customer asks, or model disagrees with the rules | Human oversight should not depend on the customer knowing to complain. |
| Reason code required; note required to overturn | A human decision needs to be as explainable as the automated one. |
| Affordability cannot be overridden | Judgement belongs on evidence gaps, not on the limit that protects the customer. |
| Log the exact explanation text | "What did we tell the customer?" is the first question in a complaint. |
| Log consent scope, not bank transactions | An audit trail should not become a second copy of personal data. |
| Track "declines overturned" | A rising override rate is the signal that a rule or the model needs tuning. |

The design follows the principles in the UAE Central Bank's February 2026 guidance note on AI and machine learning in financial services: explainability, effective human oversight and accountability. It is a demo, not a compliance tool: cases and the log live in the browser tab and reset on refresh.

## What's next

- [x] Open Finance data for thin-file customers (#3)
- [x] Reason → action → timeline plan (#3)
- [x] Human review: a customer can ask a person to check the decision (#4)
- [x] Bank compliance view: an audit trail of every decision and explanation (#4)
- [ ] Second approver (four-eyes check) for overturned decisions
- [ ] Append-only storage and reviewer sign-in, so the log outlives the browser tab
- [ ] Short survey: would UAE residents trust an AI explanation from their bank?

## Limits

- This is a demo, not a real credit model. Real banks use many more factors.
- The 50% debt ratio reflects the UAE Central Bank's debt-burden cap for personal loans. Check current regulations before relying on it.
- The Arabic text should be reviewed by a native speaker.
- The reviewer, case references and service target (2 working days) are invented for the demo.

---

Built by **Yalini**, Technical Product Owner · Dubai
