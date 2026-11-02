# Setup Runbook — Demo 02 Document AI Workspace

Build, test, and reset the Juniper Table demo workspace on the same
AnythingLLM install as the Intelligence Core. Written for AnythingLLM
Desktop 1.19.0 + LM Studio. Every step here is a **live-session (Styn)
step** — nothing in this runbook has been run against the PC yet; the
gate closes only when the acceptance battery below passes in the live
workspace.

Budget: ~30 min to build, one sitting for the battery, ≤15 min to
re-create from scratch (that re-creation *is* the reset proof).

## 0. Before you start

- [ ] Skim the 8 documents in `documents/` — flag anything that reads
      like a real business you know. (SPEC privacy step; all content is
      authored fiction, but your eyes are the last check.)
- [ ] LM Studio is running with **`qwen3-14b`** loaded and
      `text-embedding-nomic-embed-text-v1.5` available. Ask the model
      one throwaway question in LM Studio to warm it — cold starts on
      this stack can fail outright (Core build log, Oct 30).

## 1. Privacy first

- [ ] AnythingLLM → Settings → disable **telemetry** (it is ON by
      default in 1.19.0). Ruled Oct 30: off — demo and Core alike.

## 2. Create the workspace

- [ ] New workspace named **`Juniper Table Catering — Demo`**.
- [ ] Workspace chat settings (mirror `workspace-config.md`):
  - LLM provider: **LM Studio**, base `http://127.0.0.1:1234/v1`,
    chat model **`qwen3-14b`**
  - Embedder: **LM Studio**, same base, model
    **`text-embedding-nomic-embed-text-v1.5`**
  - Vector DB: **LanceDB** (default)
  - Chat mode: **Query**
  - Similarity topN: **10**
  - System prompt: paste verbatim from `workspace-config.md`
- [ ] Confirm AnythingLLM's global LLM/embedder preferences match the
      same values (the Core uses them; don't fork the stack).

## 3. Upload the documents

- [ ] Upload all 8 files from `documents/` (01–08, Markdown).
- [ ] Move them into the workspace and save/embed.
- [ ] **Verify the document count is exactly 8** and every file shows
      as embedded. A silent embed failure invalidates everything after
      this step — check before chatting.

## 4. Run the acceptance battery

- [ ] Open `test-set.md`. Ask Q1–Q12 then trap T1, **exactly as
      written, in order, in one sitting**. Record times in the run log.
- [ ] For each answerable question: open the citation and confirm the
      quoted grounding passage is really there.
- [ ] Pass bar (SPEC): 8/8 citations verified · Q9/Q10 facts identical
      to Q1/Q4 · Q11 and Q12 refused · T1's premise corrected.
- Latency expectation on the 14B: seconds to tens of seconds once warm.
  Answers regularly over ~2 min = note it in the run log (regression
  signal), keep going.

## 5. Bonus: the scanned-PDF workaround (after the battery)

- [ ] Upload `documents-scanned/07-incident-report-procedure-SCANNED.pdf`
      → expected result: **fails with "No text content found"** (the
      collector's Ghostscript renderer can't read image-only PDFs —
      the same failure the Core hit on its BOIR scan).
- [ ] Upload `documents-scanned/pages/*.png` (the extracted page images)
      → these embed via image OCR. Ask "What form do we use for an
      incident, and when is it due?" and confirm it can now answer
      from the scanned content.
- [ ] Delete the two image documents from the workspace afterward —
      the clean 07 Markdown is the gate copy.

## 6. Reset (one step, and the re-creation proof)

- [ ] Delete the **`Juniper Table Catering — Demo`** workspace.
      **Only that workspace.** The `Styn & Mas Intelligence Core`
      workspace is production — never touch it in a demo reset.
- [ ] Clean state = workspace gone, no demo documents left in the
      document library. Re-creating from §1–§3 in ≤15 minutes is the
      documented reset; the runbook is the reset.

## Swapping in a client's documents (delivery pattern)

Replace `documents/` with the client's set, keep the prompt, topN, and
Query mode, and rebuild the battery from *their* facts (prices,
deadlines, procedures) in the `test-set.md` shape. Fill in their
`can-cant-answer.md`. Scanned client PDFs go through §5's page-image
method as a matter of routine, not exception.
