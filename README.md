# Document AI with Citations — an AnythingLLM workspace that won't invent your policies

A chat workspace loaded with one company's handbook, safety policies,
booking terms, and pricing. Staff ask plain-English questions and get
answers **with the source cited** — document and section, every time.
Ask something the documents don't cover and it refuses, plainly, instead
of inventing a policy.

Demo project. The company (Juniper Table Catering Co.) and every document
in it are fictional; the workspace configuration, guardrail prompt, and
test method are the real deliverable pattern.

## Quick start

1. Install AnythingLLM and point it at a local or hosted model —
   exact settings in `workspace-config.md`.
2. Create a workspace, set **Query** mode, topN **10**, and paste the
   guardrail system prompt (in `workspace-config.md`).
3. Upload the 8 documents from `documents/`; confirm all 8 are indexed.
4. Run the battery in `test-set.md` — 12 questions + 1 trap — and check
   every citation against the quoted passage.

Full click-by-click: `SETUP.md`. What it answers and what it won't:
`can-cant-answer.md`.

## What it guarantees

- **Cited or refused** — every factual answer names its document and
  section; anything outside the documents gets "I don't have that in
  the provided documents."
- **Premise correction** — a question that misstates a policy gets
  corrected from the document, not agreed with (test trap T1).
- **Consistency** — the same question asked two ways returns the same
  facts (test Q9/Q10 vs Q1/Q4).
- **Local-first** — the reference build runs entirely on a local model
  (LM Studio); the documents never leave the machine.

## Files

| Path | Contents |
|---|---|
| `documents/` | The 8 fictional company documents (the knowledge base) |
| `documents-scanned/` | Staged image-only PDF + page images demonstrating the scanned-document workaround |
| `workspace-config.md` | Exact provider, model, topN, prompt, and privacy settings |
| `SETUP.md` | The setup runbook — build, test, and reset the workspace |
| `test-set.md` | 12 questions + trap, expected answers, grounding passages, run log |
| `can-cant-answer.md` | The one-page scope sheet that ships with a delivery |

## Using it on your documents

Swap `documents/` for the client's set (up to ~50 documents at the
entry tier), keep the guardrail prompt, re-run the same battery shape
with questions keyed to *their* facts, and fill in their
can/can't-answer sheet. Scanned PDFs are handled with the page-image
method in `documents-scanned/README.md`. That's the client version of
this demo — fixed price, runbook included.
