# Contributing to Shodh

Thanks for your interest in improving Shodh. It's a small, self-contained project, and contributions — bug reports, documentation fixes, and code — are welcome.

> **A note before you dig in.** Almost the entire application is a *single* HTML file (`shodh.html`), and a large portion of that file is a bundled third-party library (Mozilla PDF.js) encoded as data. That makes the file big and unusual to work with. Please read the sections below before proposing large changes.

---

## Ways to contribute

- **Report a bug.** Open an issue using the bug-report template. Include your operating system, browser and version, what you did, what you expected, and what happened. **Do not paste confidential or unpublished records** into a public issue — describe the problem with a minimal, non-sensitive example.
- **Suggest a feature.** Open an issue using the feature-request template. Explain the research problem it solves, not just the mechanism — that helps keep Shodh focused.
- **Improve the docs.** Corrections and clarifications to the manual, FAQ, or install guide are genuinely valuable and easy to review.
- **Submit code.** For anything beyond a small fix, please open an issue first so we can agree on the approach before you spend time on it.

---

## Working with the source

- The app is `shodh.html`. Application logic is human-readable at the top and bottom of the file; the large block in the middle is base64-encoded **PDF.js** (Mozilla, Apache-2.0) and should not be hand-edited. If PDF.js needs updating, replace it from an official PDF.js build rather than editing the encoded blob, and update [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md) accordingly.
- There is no build step and no framework: it's meant to run by opening the file. Please keep it that way unless there's a strong reason not to — the zero-install, single-file property is a core feature, not an accident.
- Test in more than one browser before submitting (at minimum a Chromium-based browser and Firefox), because storage and PDF behaviour can differ.

## Pull-request checklist

- [ ] The app still opens and works by double-clicking the file (no server, no build required).
- [ ] You tested the affected feature in at least two browsers.
- [ ] You did **not** introduce any network calls that send user data off the machine. Shodh's offline, local-only behaviour is a promise to its users; a change that quietly breaks it will be rejected.
- [ ] If you changed or added a third-party dependency, you updated `THIRD_PARTY_NOTICES.md`.
- [ ] If you changed user-facing behaviour, you updated the relevant docs and `CHANGELOG.md`.
- [ ] You did not add fabricated data, fake citations, or placeholder DOIs anywhere in the code or docs.

## Reporting a security or privacy issue

If you find a problem that could expose users' data or send it off-device, please **do not** open a public issue with the details. Contact the maintainer privately (see the repository owner's profile) so it can be fixed before it's widely known.

---

## Choosing a licence

*This section is here because the README links to it, and because picking a licence is a decision the project owner should make deliberately — not just accept a default.*

Shodh currently ships under the **MIT Licence**. That is a reasonable default for a tool meant to be used and adapted freely by researchers, but it is **your choice as the project owner**, and it's worth understanding the trade-offs. This is a plain-language summary, **not legal advice** — if the decision has real stakes for you or your institution, confirm it with someone qualified.

A quick, honest comparison of the three licences people most often consider for a project like this:

| Licence | In plain terms | Good fit when… | Trade-off |
|---------|----------------|----------------|-----------|
| **MIT** (current) | "Do almost anything, just keep my copyright and licence notice." Very short, very permissive. | You want the widest possible reuse, including in closed-source or commercial tools, with minimal friction. | Someone can take your code, modify it, and release their version without sharing their changes back. |
| **Apache-2.0** | Like MIT, permissive, but longer and with an explicit patent grant and clearer contribution terms. | You want permissive reuse **and** explicit patent protection / clearer legal wording, e.g. for institutional or corporate adoption. | Slightly heavier to read; per-file notice conventions. (Note: Shodh already includes Apache-2.0 code via PDF.js, so this licence is already in the picture for the bundled component.) |
| **GPL-3.0** | "You can use and modify it, but if you distribute a modified version, you must release your source under the same terms." Copyleft. | You want to guarantee that improvements stay open and can't be folded into a closed product. | Discourages some commercial/closed adoption; imposes obligations on redistributors that can deter reuse. |

Two practical points specific to Shodh:

1. **You are redistributing PDF.js (Apache-2.0) either way.** Whatever licence you choose for *your* code, you must keep PDF.js's attribution when you distribute the file. See [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md). MIT and Apache-2.0 combine with that cleanly; if you were ever to choose a copyleft licence, check compatibility carefully.
2. **Change it deliberately and early.** Re-licensing after other people have contributed is awkward, because contributions come in under whatever licence was in force. If you want a different licence than MIT, decide **before** you accept outside contributions.

If MIT suits you, you don't need to do anything — just fill in your name in [LICENSE](LICENSE). If you want to switch, replace the `LICENSE` file with the full text of your chosen licence (from [choosealicense.com](https://choosealicense.com) or the licence's official source) and update the "Licence" section of the README and the `license:` field in `CITATION.cff` to match.
