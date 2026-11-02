# Staged scanned-PDF set — the page-image workaround demo

**What this is:** a deliberately *image-only* PDF (no text layer — verified:
0 extractable characters) of the Incident Report Procedure, plus its two
page images. It exists to demonstrate, live, the scanned-document problem
found on the real Intelligence Core build (Oct 30, 2026) and the workaround
that fixed it.

**The failure it reproduces:** AnythingLLM's document collector tries to
OCR scanned PDFs with a bundled Ghostscript renderer. On the Core's
real scanned BOIR transcript, that renderer failed on every page, OCR read
0 pages, and the upload died with **"No text content found"** — silently,
unless you read the upload results. A client with a drawer of scanned
policies hits exactly this wall.

**The workaround (proven on the Core):** extract the document's page
images, upscale them 3×, and upload the images instead. The collector's
image OCR (tesseract.js — no Ghostscript involved) reads them, and the
content embeds and retrieves normally.

**Staged artifacts here:**

- `07-incident-report-procedure-SCANNED.pdf` — the image-only PDF. Upload
  this first and watch it fail.
- `Pages/07-incident-report-procedure-p1.png`, `…-p2.png` — the page
  images at 200 dpi, ready to upload as the workaround (equivalent to the
  extracted + upscaled pages in the Core fix).

**When to run it:** after the acceptance battery, never instead of it.
The 8 clean documents in `../documents/` are the gate set; this set is a
bonus demonstration. Delete the image documents from the workspace during
reset (see `../SETUP.md`).

**Honesty note:** the PDF was generated as images from the same text as
`../documents/07-incident-report-procedure.md` — it is a faithful stand-in
for a phone-scanner export, not a photograph of a physical page.
