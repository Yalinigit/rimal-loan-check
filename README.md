# Rimal Bank Loan Check

**Built in 48 Hours #1 · "Why was I rejected?"**

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

Two examples are built in: **Sara** (new to the UAE, declined) and **Omar** (settled, approved).

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

## What's next

- [ ] Human review: let a customer ask a person to check the decision
- [ ] Bank compliance view: an audit trail of every decision and explanation
- [ ] Short survey: would UAE residents trust an AI explanation from their bank?

## Limits

- This is a demo, not a real credit model. Real banks use many more factors.
- The 50% debt ratio reflects the UAE Central Bank's debt-burden cap for personal loans. Check current regulations before relying on it.
- The Arabic text should be reviewed by a native speaker.

---

Built by **Yalini**, Technical Product Owner · Dubai
