# Workspace Configuration Spec — Demo 02

Mirror of the verified **Styn & Mas Intelligence Core** configuration
(AnythingLLM 1.19.0, built and tested Oct 30, 2026), with the two
follow-up rulings Styn delegated and Bria made the same day. Where a value
says "Core-verified," it ran in production on the Core this morning;
where it says "ruled," it is the decision that supersedes the as-built
value. Anything not listed here was not changed on the Core and is not
changed for the demo.

## Platform

| Setting | Value | Source |
|---|---|---|
| App | AnythingLLM Desktop **1.19.0** (same install as the Core) | Core-verified |
| Demo workspace name | `Juniper Table Catering — Demo` | this demo |
| Vector database | LanceDB (application default) | Core-verified |
| Chat mode | **Query** (answers only from workspace documents; refuses when nothing relevant is retrieved) | Core-verified (end-to-end tests ran in query mode) |
| Similarity topN | **10** | Core-verified — raised from the default 4 after a needed document ranked below top-6 in testing; do not lower for the demo |
| Chunk size / overlap | Application defaults — **no override** | Core build applied no custom chunk settings; the demo mirrors that. If the live session changes these, log it as a deviation |

## Models (via LM Studio, local)

| Role | Setting | Value | Source |
|---|---|---|---|
| LLM provider | LM Studio | base URL `http://127.0.0.1:1234/v1` | Core-verified |
| Chat model | `qwen3-14b` (Q4_K_M GGUF, fully resident in the RTX 5070 Ti's 16 GB VRAM) | **Ruled Oct 30** — replaces `qwen/qwen3-32b`, whose partial VRAM fit caused 145–482 s answer latency on the Core |
| Embedding provider | LM Studio | same base URL | Core-verified |
| Embedding model | `text-embedding-nomic-embed-text-v1.5` | Core-verified — **unchanged** by the chat-model ruling |

## Privacy

| Setting | Value | Source |
|---|---|---|
| AnythingLLM telemetry | **Disabled** | **Ruled Oct 30** — telemetry is ON by default in 1.19.0; turn it off in Settings before uploading any documents, on this demo and the Core alike |

## Workspace system prompt (paste verbatim)

```
You are the staff assistant for Juniper Table Catering Co. Answer ONLY
from the documents in this workspace. For every factual claim, cite the
document name and the section it came from. If the documents do not cover
the question, reply: "I don't have that in the provided documents." Do
not guess, estimate, or use outside knowledge. If a question states a
policy incorrectly, correct it from the documents. Keep answers short
and in plain language.
```

## Operating notes carried from the Core build

- **Warm the model first.** The Core's first cold-start chats failed
  outright before the model was loaded. Before the battery: confirm
  `qwen3-14b` is loaded in LM Studio and ask one throwaway question
  (not scored).
- **Expected latency on the 14B:** seconds to tens of seconds per answer
  once loaded — but the battery is still run as one batched sitting, in
  order, without assuming instant replies. Actual timings are recorded
  in the test log; they are part of the gate evidence.
- **Scanned PDFs:** the collector's bundled Ghostscript renderer can
  silently fail on image-only PDFs ("No text content found"). The proven
  fix is uploading extracted, upscaled page images instead — staged in
  `documents-scanned/` and sequenced in the shot list.
- **Retrieval is not the bottleneck.** On the Core, vector search
  returned the right passages for 11/11 test questions in <0.1 s each.
  If a demo answer is wrong, suspect the chat side (prompt, mode, topN)
  before the embeddings.
