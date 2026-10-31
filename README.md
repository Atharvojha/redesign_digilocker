# DigiLocker — Redesign Concept

A UX case study: mapping where [DigiLocker](https://www.digilocker.gov.in/)'s user journey breaks, then redesigning it with modern interface principles.

> **Unofficial concept.** Not affiliated with MeitY or NeGD. Every document, name and number in the prototype is fictional.

**Run it:** open `index.html` in a browser. It's a single file with no build step.

---

## 1. Mapping the journey

We walked the live site twice: once as a first-time visitor, and once as a signed-in user with 17 issued documents. At every junction we asked: *what is the person trying to do, and what does the interface make them do instead?*

```
Discover → Browse → Sign in → Home → My documents → View → Get a new document → Share → Drive → Account
```

## 2. Pain points

| Junction | What we saw | Why it hurts |
|---|---|---|
| **Discover** | Auto-rotating carousel. "Become a Partner" gets the same weight as citizen login. | No clear first step for the 99% who are citizens. |
| **Browse** | A category opened to a blank screen, then *"No documents found"* + *"Failed to fetch states"*. | First impression is a broken page. |
| **Home** | 17 documents squeezed into a sideways scroller showing about 3½. Legal text in place of a greeting. | The user's own documents are the least visible thing. |
| **My documents** | 8 rows titled "Degree/Diploma Marksheet", told apart only by masked codes. Delete sits next to Share. | Unscannable, and one slip deletes a document. |
| **Get a document** | Searching "income certificate" returned **1,241 issuers**, not documents. | Users must know which department issues what. |
| **Fetch form** | Consent box **ticked in advance**. Dates typed as text. Errors say only "Please retry". | Dark pattern, error-prone input, dead ends. |
| **Share** | Only to another DigiLocker user by mobile number, with expiry typed as `dd/mm/yyyy`. | No QR or link, and no way to share *less*. |
| **Empty states** | An empty inbox also shows a yellow *"No data found"* warning. | "Nothing here yet" looks like an error. |

The full audits are in [`docs/`](docs/).

## 3. Principles → changes

| Principle | What changed |
|---|---|
| **Intent over org chart** | Search for documents, not issuers ("What do you need today?"). The state is pre-filled from documents you already hold. |
| **Your stuff first** | A wallet of cards grouped by category. 8 marksheets become one *stack* that opens to Semester 1–8. |
| **Documents find you** | A "Ready to add" strip suggests documents matched to what's already in your wallet, added in one tap. |
| **Trust you can see** | A foil "verified" seal on every card. The legal note appears once, in plain language. |
| **Share only what's needed** | QR, link or user. Field-level toggles (prove *"18+"* without revealing your birth date), expiry presets, a live preview of what the recipient sees, full-screen Present mode, and one-tap revoke. |
| **Honest forms** | Consent left unticked, a real date picker, "Show me where" points to the number on a sample certificate, and errors say exactly what didn't match. |
| **Safe by default** | Sensitive fields stay masked until you reveal them, then re-mask after 30s. Removing a document takes a 1.5s hold and can be undone. |
| **One flow, not two** | Login and Register merged into a single mobile + code step. |

### Motion with a purpose

| Rule | Applied to |
|---|---|
| Never animate high-frequency actions | ⌘K palette and filter chips are instant. |
| Spatial continuity | The tapped card flies into its detail sheet and back. Drill-in pushes, Back pops. |
| Physics for touch | Spring-driven sheets that follow the finger and use release velocity. |
| Feedback on every press | Pressed controls shrink to 97%. Loading labels morph into place instead of being swapped. |
| Exit faster than enter | Sheets open in 440ms and close in 280ms. |
| Respect the user | `prefers-reduced-motion`, reduced transparency, dark mode, 44pt touch targets, safe areas. |

## 4. Process

1. **Audit:** walked the live site and wrote a junction-by-junction pain-point map.
2. **v1 prototype:** fixed the structural problems ([`archive/v1.html`](archive/v1.html)).
3. **Two independent design reviews in parallel**, using two lenses:
   - [Emil Kowalski's design-engineering principles](docs/audit-emil.md): craft, easing, purposeful motion.
   - [Apple's fluid-interface principles](docs/audit-apple.md): springs, gestures, materials, typography.
4. **Merge:** the two reviews were combined into [one plan](docs/polish-plan.md). Where both lenses independently flagged the same issue, it became top priority.
5. **Polish and review:** implemented in three batches, then reviewed again in a live browser at 375px and 1440px, light and dark.

## Files

```
index.html          the redesigned prototype
archive/v1.html     first pass, before the polish
docs/               pain-point audits and the merged polish plan
```
