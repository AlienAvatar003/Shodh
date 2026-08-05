# Shodh — User Manual

This manual walks through Shodh from first launch to final export. It describes
what each part of the application does and, where relevant, what it does **not**
do, so you can rely on it appropriately in a real review.

> Throughout, remember the core idea: **Shodh runs on your machine and keeps
> your data on your machine.** That is a feature, but it also means *you* are
> responsible for backups. Export a JSON backup regularly (see
> [Backups](#backups-and-restore)).

## Contents

1. [Launching Shodh](#launching-shodh)
2. [The Desk (projects)](#the-desk-projects)
3. [How your data is stored](#how-your-data-is-stored)
4. [Import](#import)
5. [Duplicates](#duplicates)
6. [Stage 1 — Title/abstract screening](#stage-1--titleabstract-screening)
7. [Conflicts (multi-reviewer)](#conflicts-multi-reviewer)
8. [Stage 2 — Full-text screening](#stage-2--full-text-screening)
9. [Ask (offline retrieval)](#ask-offline-retrieval)
10. [Export](#export)
11. [Backups and restore](#backups-and-restore)
12. [Keyboard shortcuts](#keyboard-shortcuts)
13. [Recommended workflow](#recommended-workflow)
14. [Troubleshooting](#troubleshooting)

---

## Launching Shodh

Open `shodh.html` in a modern web browser (Chrome, Edge, Firefox, or Safari).
Nothing installs; the page *is* the application. Platform-specific launch notes,
including the optional desktop apps, are in [INSTALL.md](INSTALL.md).

The top of the window shows the **Shodh** wordmark, the current review name (or
"no project"), and — once you are inside a review — an **Export** button. Below
that is a row of tabs that form the workflow, left to right.

---

## The Desk (projects)

The **Desk** tab is your home base. From here you:

- **Create a review.** Give it a name and a topic. You will also be asked for a
  **reviewer name** — this identifies your decisions and matters if more than one
  person will screen (see [Conflicts](#conflicts-multi-reviewer)).
- **Switch between reviews.** Shodh supports multiple independent projects; each
  keeps its own references, decisions, PDFs, and notes.
- **See progress at a glance.** Counts for imported, screened, included, and
  excluded records help you track where a review stands.
- **Delete a review.** This removes the review and its screening decisions.
  (PDFs that are shared with other reviews are kept.) Deletion cannot be undone,
  so back up first if you are unsure.

The tabs to the right of Desk stay disabled until a review is selected, because
they act *on* the current review.

---

## How your data is stored

This section is important; please read it before you put real work into Shodh.

Shodh saves everything **locally, in your browser**, using a storage priority
order:

1. **IndexedDB** — the browser's durable local database. This is the normal
   case and it can store your PDFs as well as records and decisions.
2. **A host-provided storage API** — used only in certain embedded/hosted
   contexts. This is session-oriented and does **not** durably store large PDF
   blobs.
3. **In-memory** — a last-resort fallback that lasts only until you close the
   tab. If Shodh is running in memory-only mode, treat everything as temporary
   and export often.

Practical consequences:

- **Your review is tied to one browser profile and one origin.** If you open
  Shodh in a different browser, on a different computer, in a private/incognito
  window, or (for the desktop builds) from a different local address or port,
  you will not see reviews created elsewhere.
- **Clearing browser data can delete your reviews.** "Clear browsing data",
  "clear site data", or aggressive privacy settings can wipe IndexedDB.
- **The fix is simple: export JSON backups.** A JSON backup is portable — you
  can restore it in another browser or on another machine. See
  [Backups](#backups-and-restore).

None of your data is sent anywhere by Shodh itself. The only feature that can
reach out is the *optional* Ollama integration on the Ask tab, and only if you
choose to enable it and have Ollama running locally.

---

## Import

The **Import** tab is where references enter a review. Shodh accepts:

- **RIS** (`.ris`) — exported by most databases and reference managers.
- **BibTeX** (`.bib`) — common from Google Scholar, Zotero, and LaTeX workflows.
- **CSV** (`.csv`) — exported from databases like Scopus, Web of Science, and
  spreadsheets.
- **PDF** (`.pdf`) — attach the full text of a paper to a record.

**How fields are read.** Shodh maps common field names to a shared record shape
(title, authors, year, journal, DOI, abstract, keywords). For CSV, it recognises
many header aliases (for example `Title`, `Article Title`, or `Document Title`
all map to the title). If a CSV has no recognisable title column, Shodh tells you
which columns it *did* find so you can fix the export.

**Authors** are split on the conventional separators (`and` in BibTeX, `;` in
many CSVs) so that each author is stored separately.

**Tips**

- Export from your database in RIS or BibTeX when you can; those formats carry
  abstracts and keywords more reliably than a generic CSV.
- You can import several files into the same review; Shodh appends records. Use
  the [Duplicates](#duplicates) tab afterwards to clean up overlaps.
- The abstract you import here is the same text shown during
  [Stage 2](#stage-2--full-text-screening) and searched by [Ask](#ask-offline-retrieval),
  so complete abstracts improve later stages.

---

## Duplicates

Importing from multiple databases produces overlaps. The **Duplicates** tab finds
likely duplicate records so you can remove them before screening — and record the
count for your PRISMA diagram.

Shodh detects duplicates three ways:

- **Exact DOI match** — the most reliable signal.
- **Identical title** — after light normalisation (case, spacing).
- **Fuzzy title match** — near-identical titles, which catches things like
  British/American spelling differences or minor punctuation changes.

**Review before you remove.** Fuzzy matching is a heuristic. Two genuinely
different papers can occasionally have very similar titles, and conference-vs-
journal versions of the same work are a judgement call. Look at each suggested
pair before confirming removal. Removed duplicates are recorded so they can
appear in your decision log and PRISMA counts.

---

## Stage 1 — Title/abstract screening

**Stage 1** is fast, first-pass screening. You see one record at a time — its
title, authors, and journal — and decide whether it is potentially relevant.

Make decisions with the keyboard for speed:

- **`I`** — Include (send it forward to full-text screening)
- **`E`** — Exclude
- **`M`** — Maybe (revisit later)
- **Undo** — reverse the last decision if you mis-key

The point of Stage 1 is triage, not final judgement: include anything that might
qualify, and leave definitive calls to Stage 2 where you have the full text. Your
running progress is shown so you know how much of the set remains.

---

## Conflicts (multi-reviewer)

Systematic reviews often require **two independent reviewers**. Shodh supports
this: reviewers screen independently (each under their own reviewer name), and the
**Conflicts** tab surfaces records where their decisions disagree so they can be
**adjudicated** (resolved), optionally by a third person.

**An honest caveat about independence.** Shodh implements this by *convention* on
a single machine — it distinguishes decisions by reviewer name and shows you the
disagreements. It does **not** enforce reviewer separation the way a hosted,
multi-account server would. If your protocol demands strict blinding, organise
your process to achieve it (for example, reviewers work on separate copies and you
merge via JSON), and describe honestly in your methods how independence was
maintained.

---

## Stage 2 — Full-text screening

**Stage 2** is where records that survived Stage 1 get a considered decision
against the full text. The screen is split:

- **Left panel:** the record's **title**, **authors — journal**, and the
  **abstract** imported from your reference file. The attached PDF is available
  here for reading.
- **Right panel:** a **keyword rule engine**. You type inclusion and/or exclusion
  keywords, and Shodh can apply them across the set to **bulk include or exclude**
  records that match — or you can decide one record at a time. As in Stage 1, the
  **`I`** and **`E`** keys make single decisions quickly.

The keyword engine searches the fields you choose (title, abstract, keywords, and
the extracted PDF text). It supports "match any" vs "match all" of your inclusion
terms, and exclusion terms that veto a match.

**Use keyword rules as assistance, not authority.** Bulk keyword decisions are a
huge time-saver, but keywords are blunt. Spot-check what a rule includes and
excludes before you commit it, especially for exclusion — it is easy to
accidentally drop relevant papers whose authors used different terminology.

---

## Ask (offline retrieval)

The **Ask** tab lets you ask a question and get back the passages from your
library most relevant to it. This is a study aid — a way to find where in your
imported abstracts and PDFs a topic is discussed.

**How it works, precisely:**

- Retrieval uses **BM25**, a classical keyword-ranking algorithm, over your
  abstracts and extracted PDF text. It is fast and fully offline, but it matches
  on **words**, not meaning. If a passage discusses your topic using different
  vocabulary, BM25 may not surface it. This is a real limitation — do not treat
  Ask as an exhaustive search.
- **Optional AI synthesis via Ollama.** If you have [Ollama](https://ollama.com)
  installed and running locally, Shodh can use a local language model to
  summarise the retrieved passages into a readable answer. This is optional; if
  Ollama is not present, you still get the ranked passages. Because the model runs
  on your own computer, this remains local — but any language model can be wrong
  or can misread a source, so verify claims against the passages themselves.

**No OCR.** Ask can only search text that exists. If your PDFs are scans (images
of pages) with no text layer, there is nothing for BM25 to match.

---

## Export

The **Export** tab produces everything you need to move forward or to document
your process:

- **Reference-manager files** — export your **selected** references as
  **BibTeX**, **RIS**, or **CSV** and import them into Zotero, Mendeley, EndNote,
  or similar.
- **PRISMA 2020 flow diagram** — a flow diagram (as an image) summarising records
  identified, duplicates removed, records screened, and so on. **Treat the numbers
  as a draft to verify**, not as an authoritative count; the diagram itself notes
  that counts should be checked before submission.
- **Decision log** — an audit trail of what happened to each record (imported,
  de-duplicated, included, excluded), useful for transparency and for a methods
  appendix.
- **Notes** — if you selected text and made annotated notes during screening, you
  can export them (as `.txt`).
- **JSON backup** — the whole project, portable and restorable. See below.

---

## Backups and restore

Because your data lives in one browser profile, **back it up.**

- **Export a JSON backup** of the project from the app. Keep it somewhere you
  trust (cloud drive, institutional storage, a second disk).
- **Restore** by importing that JSON back into Shodh — in the same browser after
  clearing data, or in a *different* browser or on a *different* machine. This is
  also how you move a review between computers or hand it to a colleague.

A good habit: export a JSON backup at the end of every working session, and again
before deleting anything or clearing browser data.

---

## Keyboard shortcuts

| Key | Where | Action |
|-----|-------|--------|
| `I` | Stage 1 & Stage 2 | Include the current record |
| `E` | Stage 1 & Stage 2 | Exclude the current record |
| `M` | Stage 1 | Mark the current record as "Maybe" |
| Undo control | Stage 1 | Reverse your last decision |

Keyboard screening is the fastest way to work through a large set. Keep your hand
on `I` / `E` and let the record advance.

---

## Recommended workflow

A typical review in Shodh:

1. **Desk** — create the review, enter your reviewer name, define the topic.
2. **Import** — bring in RIS/BibTeX/CSV from each database; attach PDFs as you
   obtain them.
3. **Duplicates** — review and remove duplicates; note the count.
4. **Stage 1** — screen titles/abstracts quickly with `I` / `E` / `M`.
5. **Conflicts** — if screening with a partner, adjudicate disagreements.
6. **Stage 2** — screen full text; use keyword rules to accelerate, spot-checking
   as you go.
7. **Ask** — interrogate your library while writing, remembering it is keyword
   retrieval.
8. **Export** — pull selected references into your reference manager; export the
   PRISMA diagram and decision log for your manuscript; **verify all counts.**
9. **Back up** — export a JSON backup and store it safely.

---

## Troubleshooting

**My review disappeared.** You are almost certainly looking in a different
browser, profile, machine, or (desktop builds) local address/port than the one
you created it in — or browser data was cleared. Restore from your JSON backup.
This is why frequent backups matter. See
[How your data is stored](#how-your-data-is-stored).

**My CSV imported with no titles / wrong fields.** Shodh reports which columns it
found. Re-export from the database with a clearer header, or rename the column to
a recognised alias such as `Title`. RIS or BibTeX often import more cleanly.

**A scanned PDF has no searchable text / doesn't appear in Ask.** Shodh does not
perform OCR. Obtain a text-based PDF, or OCR it in another tool first.

**Ask missed an obviously relevant paper.** BM25 matches words, not meaning.
Rephrase your query using terms the source is likely to use, or browse the
records directly. Do not rely on Ask as a complete search.

**Bulk keyword include/exclude did something I didn't expect.** Review the terms
and the fields being searched; broaden or narrow the rule; and spot-check results
before committing. Keyword rules are assistance, not a substitute for judgement.

**Something looks like a genuine bug.** Please open an issue — see
[CONTRIBUTING.md](../CONTRIBUTING.md). Include your browser and operating system,
what you did, what you expected, and what happened.
