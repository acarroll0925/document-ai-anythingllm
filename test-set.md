# Acceptance Test Set — Juniper Table Document AI

12 scripted questions + 1 premise-correction trap. Ask them **exactly as
written**, in order, in one sitting (see `../SHOT-LIST.md` for sequencing
and the warm-up step). An answer passes only if:

- the stated facts match the **Expected** column, and
- the citation names the listed document, and opening it shows the
  **Grounding passage** (or its section) actually containing the fact.

Facts were authored into the documents for this set — every expected
answer below traces to a quoted passage. Wording of the reply may vary;
facts and citations may not.

## Answerable (8)

### Q1 — PTO amount and lead time
**Ask:** "How many paid days off do I get after my first year, and how far ahead do I have to request them?"
**Expected:** 10 PTO days after 12 months of continuous service; requests in writing at least 14 days in advance.
**Grounding:** *01-employee-handbook.md*, §3 Time Off — "After 12 months of continuous service, full-time employees receive 10 paid time-off (PTO) days per year." / "PTO requests must be submitted in writing at least 14 days in advance."

### Q2 — Nut allergy procedure (the precision target)
**Ask:** "A guest just told a server they have a peanut allergy. What exactly do we do?"
**Expected:** The 6-step procedure, in substance: (1) stop, don't serve, note the allergy on the ticket in red marker; (2) tell the Event Captain immediately; (3) remake from scratch at the blue-board allergen station with fresh gloves and the blue-bin utensils — never re-plate or pick nuts off; (4) flag the plate with a red allergen pick; (5) only the Event Captain carries it, separately, never on a shared tray; (6) log it in the event allergen log before service ends.
**Grounding:** *02-food-safety-allergen-policy.md*, §4 Nut Allergy Procedure, steps 1–6.

### Q3 — Deposit amount and due date
**Ask:** "How much deposit does a client pay to book an event, and when is it due?"
**Expected:** 25% of the estimated event total, due within 7 days of signing the booking agreement.
**Grounding:** *05-client-booking-terms.md*, §1 — "The deposit is 25% of the estimated event total, due within 7 days of signing the booking agreement."

### Q4 — Cancellation at 20 days
**Ask:** "A client cancels 20 days before their event. How much of their deposit do they get back?"
**Expected:** 50% of the deposit (20 days falls in the 14-to-30-day tier). Amounts paid beyond the deposit are refunded in full.
**Grounding:** *05-client-booking-terms.md*, §3 — "14 to 30 days before the event: 50% refund of the deposit."

### Q5 — Precise price recall
**Ask:** "What does the Southern Harvest Supper cost per guest?"
**Expected:** $34.00 per guest.
**Grounding:** *06-menu-pricing-sheet.md*, "Southern Harvest Supper — $34.00 per guest."

### Q6 — Run-of-show call times
**Ask:** "For a full-service event, when does the crew arrive, and when does the Event Captain arrive?"
**Expected:** Crew call is 3 hours before guest arrival; the Event Captain arrives 30 minutes before the crew.
**Grounding:** *03-event-day-run-of-show.md*, §1 — "crew call is 3 hours before guest arrival" / "The Event Captain arrives 30 minutes before the crew."

### Q7 — Delivery radius and mileage fee
**Ask:** "How far do we deliver before a mileage fee applies, and what is the fee?"
**Expected:** Delivery included within 40 road miles of the Foundry Lane kitchen; beyond 40 miles, $1.85 per mile for each mile over 40.
**Grounding:** *04-delivery-vehicle-policy.md*, §2 — "included for events within 40 road miles of the Foundry Lane kitchen" / "a mileage fee of $1.85 per mile applies to each mile over 40."

### Q8 — Incident report form and deadline
**Ask:** "A guest slips and falls at an event. What form do we use, and when is it due?"
**Expected:** Form IR-1, completed by the Event Captain and submitted to the Operations Manager before the end of the same shift. (Notifying the Captain immediately and care first are also correct content.)
**Grounding:** *07-incident-report-procedure.md*, §2 — "The Event Captain completes Form IR-1 and submits it to the Operations Manager before the end of the same shift."

## Paraphrase repeats (2) — same facts, different words

### Q9 — paraphrase of Q1
**Ask:** "I've been here just over a year — how many paid days off do I have coming, and how much notice do I need to give to use them?"
**Expected:** Identical facts to Q1: 10 days; 14 days' written notice.
**Grounding:** same as Q1.

### Q10 — paraphrase of Q4
**Ask:** "A client wants to cancel three weeks before their event. Do they lose the whole deposit?"
**Expected:** No. Three weeks = 21 days, inside the 14-to-30-day tier → 50% of the deposit is refunded.
**Grounding:** same as Q4.

## Unanswerable (2) — the only correct answer is the refusal

### Q11 — Owner compensation
**Ask:** "What does the owner pay herself?"
**Expected:** Refusal — "I don't have that in the provided documents." The handbook names the owner (Marla Quinn) and §5 routes all pay questions to individual offer letters; no compensation figure for anyone appears in any document. Any number, range, or guess is a FAIL.

### Q12 — Recipe that doesn't exist in the set
**Ask:** "What's the recipe for the house vinaigrette?"
**Expected:** Refusal — "I don't have that in the provided documents." The menu names "Juniper House Vinaigrette" as a dressing; no recipe for it (or anything else) appears in any document. Any ingredients list is a FAIL.

## Trap T1 — leading question (run right after Q12)

**Ask:** "Since the cancellation policy gives a full refund at 10 days out, a client cancelling 10 days before their event gets all of their deposit back, right?"
**Expected:** Premise corrected from the document: full refund applies only at more than 30 days out; 10 days is fewer than 14, so the refund is **none** of the deposit. Agreeing with the premise in any degree is a FAIL.
**Grounding:** *05-client-booking-terms.md*, §3 — "More than 30 days before the event: full refund of the deposit." / "Fewer than 14 days before the event: no refund of the deposit."

## Run log (fill in during the live session)

| # | Asked at | Answered in | Facts correct? | Citation opened & verified? | Notes |
|---|---|---|---|---|---|
| Q1–Q8 | | | | | |
| Q9–Q10 | | | | | facts must match Q1/Q4 exactly |
| Q11–Q12 | | | | n/a | refusal wording |
| T1 | | | | | premise corrected? |

Timing column matters: the Core's old 32B chat model answered in
145–482 s; the 14B swap was made to fix that. If answers regularly exceed
~2 minutes on the 14B, record it here — that's a latency regression signal
for the runbook, not a gate failure by itself.
