<div align="center">

# Shodh · शोध

**A free, offline literature-review desk for systematic reviews.**

Import references → remove duplicates → screen titles/abstracts → resolve reviewer conflicts → screen full text with PDFs → export to your reference manager. Runs entirely in your browser. No account, no server, no data leaves your machine.

</div>

---

> **Note on this README.** The description below reflects what the application actually does, based on its source. Where a feature has limits (retrieval quality, PDF handling, how "offline" it really is), those limits are stated plainly rather than glossed over — see [Honest limitations](#honest-limitations). Please verify any claim that matters for your own publication.

## What it is

Shodh ("शोध", Hindi/Sanskrit for *research / inquiry*) is a self-contained workbench for running a **systematic literature review** end to end. It implements a two-stage, PRISMA-2020-aligned screening workflow and keeps every record, decision, and PDF on your own device.

The entire application is a **single HTML file** (`shodh.html`). You open it in a web browser and it works — on Windows, macOS, or Linux — with nothing to install.

## Why you might want it

- **It's free and self-hosted.** No subscription, no seat licences, no vendor lock-in.
- **Your data stays local.** Records and PDFs are stored in your browser's own storage; nothing is uploaded. This is useful for unpublished data and for institutions with data-handling constraints. (Read [How your data is stored](docs/USER_MANUAL.md#how-your-data-is-stored) so you understand the trade-offs.)
- **It works offline.** Once the file is on your machine, you don't need a connection.
- **It's auditable.** You can export a decision log and a PRISMA flow diagram to document your process.

If you already have a tool your team is happy with, you may not need this. Shodh is aimed at individual researchers and small teams who want a transparent, no-cost, local workflow.

## Features

| Stage | What Shodh does |
|-------|-----------------|
| **Import** | Load references from **RIS**, **BibTeX**, or **CSV**; attach **PDF** files. |
| **Duplicates** | Detect duplicates by DOI, by identical title, and by fuzzy title match; review before removing. |
| **Stage 1 — Title/abstract screening** | Screen on title, authors, and journal with fast `I` / `E` / `M` (Include / Exclude / Maybe) keyboard shortcuts and undo. |
| **Conflicts** | For multi-reviewer reviews, compare independent decisions and adjudicate disagreements. |
| **Stage 2 — Full-text screening** | Split view: title / authors / journal / abstract on the left, a **keyword rule engine** for bulk or one-by-one include/exclude on the right, with the attached PDF available. |
| **Ask** | An **offline** question box that retrieves the most relevant abstracts and PDF text using **BM25 keyword search**, with *optional* local AI synthesis via **[Ollama](https://ollama.com)** if you have it installed. |
| **Export** | Export selected references as **BibTeX / RIS / CSV** for Zotero, Mendeley, EndNote, etc.; export a **PRISMA 2020 flow diagram** and a **decision log**; save annotated **notes**; back up and restore the whole project as **JSON**. |

## Quick start (30 seconds)

1. Download **`shodh.html`** from this repository (or from the [Releases](../../releases) page).
2. Double-click it. It opens in your default browser.
3. On the **Desk** tab, create a review, enter a reviewer name, and go to **Import**.

That's it. Full step-by-step instructions are in the [User Manual](docs/USER_MANUAL.md), and platform-specific notes (including how to publish it for others) are in [INSTALL](docs/INSTALL.md).

## Documentation

- **[Guided walkthrough](shodh-guide.html)** — an animated eight-step tour of the whole workflow. Open it in a browser like any other page; it works offline. **Start here if you are new.**
- **[User Manual](docs/USER_MANUAL.md)** — a complete walkthrough of every tab and feature.
- **[Installation & platforms](docs/INSTALL.md)** — Windows, macOS, Linux, and hosting for a whole lab.
- **[How to cite Shodh](docs/CITING.md)** — what to put in your paper's methods and references. **Please read this if you use Shodh in published work.**
- **[FAQ](docs/FAQ.md)** — common questions and troubleshooting.

## Honest limitations

Shodh is a genuinely useful tool, but it is not magic. Please keep these in mind:

- **The "Ask" tab is keyword retrieval, not semantic understanding.** It ranks passages with BM25 (a classical keyword-matching algorithm). It does **not** use semantic embeddings, so it can miss relevant text that uses different wording. Treat its answers as a starting point, not a conclusion.
- **No OCR.** Text is extracted from PDFs that already contain a text layer. **Scanned / image-only PDFs will yield little or no searchable text.**
- **Multi-reviewer blinding is by convention, on one machine.** Shodh supports independent screening and conflict adjudication, but it does not enforce reviewer separation the way a multi-user server would. For methods that require true independence, use it accordingly and document your process.
- **PRISMA counts are working aids.** The generated numbers and diagram are meant to help you draft your flow — **verify every count against your records before submitting.**
- **Deduplication is heuristic.** DOI/title/fuzzy matching is convenient but imperfect. **Review suggested duplicates before removing them.**
- **Your data lives in one browser profile.** Reviews are tied to the browser and origin you created them in. Clearing browser data, switching browsers or machines, or (for the desktop builds) changing the local port can make a review disappear. **Export a JSON backup regularly.** See [How your data is stored](docs/USER_MANUAL.md#how-your-data-is-stored).

## Contributing

Issues and pull requests are welcome. Please read [CONTRIBUTING.md](CONTRIBUTING.md)
before opening a PR, and the [Code of Conduct](CODE_OF_CONDUCT.md) for the
expected standards of interaction. To report a security or privacy issue
privately, see [SECURITY.md](SECURITY.md).


## Licence and third-party code

Shodh is released under the **Apache License 2.0** (see [LICENSE](LICENSE)). This is a permissive open-source licence: you may use, modify, and redistribute Shodh freely, including in commercial or closed-source products, provided you retain the copyright and licence notices. It also includes an explicit patent grant that the MIT Licence does not.

Shodh **bundles Mozilla's [PDF.js](https://github.com/mozilla/pdf.js)**, which is licenced under the same Apache License 2.0. Both the wrapper and the bundled library therefore carry identical licence obligations. See [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md) for attribution details and the [NOTICE](NOTICE) file for the attribution notices that must be reproduced on redistribution.
