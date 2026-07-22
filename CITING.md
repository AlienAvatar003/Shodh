# How to cite Shodh

If you use Shodh to conduct or screen a review that appears in a thesis, paper, preprint, or report, please cite it. Two things make a review reproducible and honest: describing the *method* and crediting the *tools*. This page helps you do both.

> **Please read this first.** The citation entries below contain **placeholders in `<ANGLE BRACKETS>`**. You must replace them with real values before you paste a citation into a manuscript. Do not submit a reference that still says `<YEAR>` or `<AUTHOR>`. If you are unsure what to put, see [What to fill in](#what-to-fill-in) at the bottom.
>
> There is **no pre-assigned DOI** for Shodh. If a journal or your institution requires a citable DOI, you can mint one yourself in a few minutes — see [Getting a DOI with Zenodo](#getting-a-doi-with-zenodo). Do not invent a DOI.

---

## Contents

1. [The short version](#the-short-version)
2. [Reference-list entries](#reference-list-entries)
3. [A methods-section sentence you can adapt](#a-methods-section-sentence-you-can-adapt)
4. [Getting a DOI with Zenodo](#getting-a-doi-with-zenodo)
5. [What to fill in](#what-to-fill-in)

---

## The short version

Cite Shodh as a **software** item. A software citation normally has: the author(s), the year of the version you used, the software name and version, a note that it is software, and a URL (or DOI). Cite the **version you actually used** — you can see it in the app and set it in `CITATION.cff`.

GitHub can generate a citation for you automatically: on the repository page, the **"Cite this repository"** button reads the `CITATION.cff` file. That only works once you have filled in the placeholders in `CITATION.cff`, so do that first.

---

## Reference-list entries

Pick the style your target journal uses. **Replace every `<PLACEHOLDER>`.** These are templates, not a finished citation for any specific person — the author and year are deliberately left blank because only you know the correct values for your release.

### APA (7th edition) style

```
<Author, A. A.> (<Year>). Shodh: An offline literature-review desk for
systematic reviews (Version <x.y.z>) [Computer software].
https://github.com/<OWNER>/<REPO>
```

If you have minted a DOI, end with the DOI instead of the URL:

```
<Author, A. A.> (<Year>). Shodh: An offline literature-review desk for
systematic reviews (Version <x.y.z>) [Computer software].
https://doi.org/<10.5281/zenodo.XXXXXXX>
```

### Vancouver / numbered style (common in medicine and many STEM journals)

```
<Author AA>. Shodh: An offline literature-review desk for systematic reviews.
Version <x.y.z>. <Year>. Available from: https://github.com/<OWNER>/<REPO>
```

### BibTeX

```bibtex
@software{shodh<Year>,
  author  = {<Family, Given>},
  title   = {{Shodh: An offline literature-review desk for systematic reviews}},
  version = {<x.y.z>},
  year    = {<Year>},
  url      = {https://github.com/<OWNER>/<REPO>}
  % doi   = {<10.5281/zenodo.XXXXXXX>}   % uncomment if you have one
}
```

> **Note on the author field.** Shodh was built by its author(s); this repository does not assert who that is on your behalf. Put the name(s) that should receive credit — normally you, if you are the person who created or released this copy, or whoever you agreed should be credited. If you are unsure, that is a question for you and your collaborators, not something a citation template can decide.

---

## A methods-section sentence you can adapt

It is good practice to name your screening tool in the methods, alongside how you used it. Here is a neutral template. **Edit it to match what you actually did** — do not claim steps you did not perform.

> *Records were imported and de-duplicated, then screened in two stages (title/abstract, followed by full text) using Shodh (version `<x.y.z>`), a free, offline, browser-based systematic-review tool [ref]. Title/abstract and full-text decisions were recorded within the tool, and a PRISMA 2020 flow diagram and decision log were exported. [If applicable: Two reviewers screened independently and disagreements were adjudicated using the tool's conflict view.]*

A few honesty checks before you use that sentence:

- If only one reviewer screened, **delete the two-reviewer clause.** Do not imply independent double-screening that did not happen.
- The PRISMA counts Shodh produces are **working aids.** State that you verified them against your records (and actually verify them). See the note in the [README](../README.md#honest-limitations).
- If you used the **"Ask"** feature, remember it is **BM25 keyword retrieval**, not semantic search, and — unless you separately ran a local model — it does not "read" or "understand" the literature. Describe it accurately (e.g., "keyword-based retrieval over abstract and full-text passages") rather than as an AI literature analysis.

---

## Getting a DOI with Zenodo

A DOI gives your software a permanent, citable identifier and an archived copy. It is free through **Zenodo** (operated by CERN), which integrates directly with GitHub. Outline of the process (verify the exact steps on Zenodo's own site, as their interface changes over time):

1. Push this repository to GitHub (see the repository's publishing instructions).
2. Sign in to **[zenodo.org](https://zenodo.org)** and connect your GitHub account.
3. In Zenodo's GitHub settings, **toggle this repository on.**
4. Back on GitHub, create a **release** (e.g., tag `v1.0.0`). Zenodo detects the release and archives a snapshot.
5. Zenodo issues a **DOI** for that release (and a "concept DOI" that always points to the latest version).
6. Copy the DOI into `CITATION.cff` (the `doi:` line) and into your reference entry above.

> I can't confirm Zenodo's current screens or limits from here — treat the steps above as a guide and follow the live instructions on Zenodo. The GitHub–Zenodo integration is well established, but details (button names, settings location) may have moved.

---

## What to fill in

Before publishing or citing, replace these everywhere they appear:

| Placeholder | What it means | Where it lives |
|-------------|---------------|----------------|
| `<AUTHOR>` / `<Family, Given>` | The name(s) that should be credited | `CITATION.cff`, `LICENSE`, citations above |
| `<Year>` | The year of the release you are citing | citations above, `CITATION.cff` (`date-released`) |
| `<x.y.z>` | The version you used | the app, `CITATION.cff` (`version`), citations above |
| `<OWNER>/<REPO>` | Your GitHub username and repository name | `CITATION.cff`, docs, URLs |
| `<10.5281/zenodo.XXXXXXX>` | A DOI — **only if** you mint one via Zenodo | `CITATION.cff`, citations above |

If a value doesn't apply to you (for example, you have no DOI), **remove that line** rather than leaving a placeholder in place.
