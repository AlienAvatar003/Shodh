# Frequently asked questions

Short, honest answers. For step-by-step detail, see the [User Manual](USER_MANUAL.md) and [Installation guide](INSTALL.md).

---

## General

**What is Shodh, in one line?**
A free, offline, single-file web app for running a systematic literature review — import, de-duplicate, screen in two stages, resolve reviewer conflicts, and export — with all data kept on your own machine.

**Do I need an account or internet connection?**
No account, ever. You need a connection only to *download* the file (and, optionally, to use a local AI model or to publish the tool for others). Once `shodh.html` is on your computer, screening works with the connection off.

**Is it really free? What's the catch?**
It's free and released under an open-source licence. The honest "catch" is that it's a lightweight local tool, not a hosted commercial platform: there's no support desk, no cloud sync, and no one backing up your data but you. That's the trade-off for privacy and zero cost.

**Which operating systems does it work on?**
Any that runs a modern browser — Windows, macOS, Linux, ChromeOS. See [INSTALL](INSTALL.md) for per-platform notes.

**Is my data sent anywhere?**
No. Records and PDFs stay in your browser's local storage on your device. Nothing is uploaded. The flip side is that **the tool cannot recover your data for you** — read [How your data is stored](USER_MANUAL.md#how-your-data-is-stored) and keep JSON backups.

---

## Data and safety

**Where exactly is my review stored?**
In your browser's storage (IndexedDB) for the specific browser and origin you opened the file from. It is not a file you can email. To move or safeguard a review, use **Export → JSON backup**. Details: [How your data is stored](USER_MANUAL.md#how-your-data-is-stored).

**Will I lose my work if I close the tab or restart my computer?**
Normally no — the data persists in browser storage. You *can* lose it by clearing browser data, using private/incognito mode, switching browsers or machines, or (for desktop builds) changing the local port. **Export a JSON backup regularly** so a lost browser profile doesn't mean a lost review.

**Can I move a review to another computer?**
Yes: export a JSON backup on the first machine, open Shodh on the second, and restore it. See [Backups and restore](USER_MANUAL.md#backups-and-restore).

**Can my whole team share one review?**
Not automatically — there is no central server. Teams typically screen on their own machines and exchange JSON backups, or one person consolidates. Multi-reviewer conflict adjudication is supported, but reviewer independence is **by convention on one machine**, not enforced by a server. Plan and document your process accordingly.

---

## Importing and PDFs

**What import formats are supported?**
RIS, BibTeX, and CSV for references, and PDF files for full text. Most databases and reference managers (Zotero, Mendeley, EndNote, PubMed, Scopus, Web of Science) can export at least one of these.

**My PDF text isn't searchable in "Ask". Why?**
Shodh extracts text from PDFs that already contain a text layer. **Scanned or image-only PDFs have no text layer**, and Shodh does **not** perform OCR, so little or no text will be searchable. If you need scanned documents searchable, OCR them first with a separate tool, then re-attach.

**Does deduplication catch everything?**
No — it's heuristic (DOI match, identical title, fuzzy title). It's a strong first pass but will miss some duplicates and may flag near-matches that aren't. **Review suggestions before removing anything.**

---

## The "Ask" tab and AI

**Is Shodh an "AI literature review" tool?**
Not by default. The "Ask" tab uses **BM25**, a classical keyword-ranking method, to find the most relevant abstract and PDF passages. That is retrieval, not comprehension. It will miss relevant text phrased in different words, and it does not summarise or reason on its own.

**So what does the "optional AI" do?**
If you install **[Ollama](https://ollama.com)** and a local model, Shodh can pass retrieved passages to that model to draft a synthesis — still entirely on your machine. This is optional and off unless you set it up. Any model output should be checked against the sources; treat it as a draft, not a citable finding.

**Should I cite the "Ask" output in my paper?**
Cite the underlying sources, not the tool's synthesis. If you describe using the feature in your methods, describe it accurately (keyword retrieval, optional local model) rather than as authoritative AI analysis.

---

## PRISMA and reporting

**Can I trust the PRISMA numbers and diagram?**
Use them as a **drafting aid, and verify every count against your own records** before you submit. They reflect the actions you took in the tool, which is helpful, but the responsibility for correct reporting is yours.

**Does Shodh guarantee my review is PRISMA-compliant?**
No tool can. Shodh is *aligned with* the PRISMA 2020 two-stage flow and helps you produce the artefacts, but compliance depends on how you conduct and report the review.

---

## Citing and licence

**How do I cite Shodh in my paper?**
See [How to cite Shodh](CITING.md). Use the version you actually used, and fill in the placeholders. There is no built-in DOI, but you can mint one free via Zenodo (instructions in that document).

**What licence is Shodh under, and can I modify it?**
It's released under the MIT Licence (see [LICENSE](../LICENSE)) — permissive, so you may use, modify, and redistribute it, keeping the licence and attribution. Note that Shodh **bundles Mozilla PDF.js (Apache-2.0)**; if you redistribute the file you must keep PDF.js's attribution — see [THIRD_PARTY_NOTICES](../THIRD_PARTY_NOTICES.md).

---

## Something's wrong

**A tab is blank, or an action didn't work.**
Try reloading the file. If it persists, check [Troubleshooting](USER_MANUAL.md#troubleshooting) in the manual. If you think it's a bug, please open an issue (see the repository's issue templates) with your browser, operating system, and the steps that reproduce it — but **never attach confidential or unpublished records** to a public issue.

**Windows warned me the app is unsafe / SmartScreen blocked it.**
That warning appears for unsigned downloaded programs and is expected for the desktop `.exe` builds; it is not a sign of a virus. The details and options are in [INSTALL](INSTALL.md). The single `shodh.html` file avoids this entirely, since it just opens in your browser.
