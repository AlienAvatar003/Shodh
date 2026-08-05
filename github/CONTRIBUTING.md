# Contributing to Shodh

Thanks for your interest in improving Shodh. It's a small, self-contained
project, and contributions — bug reports, documentation fixes, and code — are
welcome.

> **A note before you dig in.** Almost the entire application is a *single*
> HTML file (`shodh.html`), and a large portion of that file is a bundled
> third-party library (Mozilla PDF.js) encoded as base64 data. That makes the
> file big and unusual to work with. Please read the sections below before
> proposing large changes.

---

## Ways to contribute

- **Report a bug.** Open an issue using the bug-report template. Include your
  operating system, browser and version, what you did, what you expected, and
  what happened. **Do not paste confidential or unpublished records** into a
  public issue — describe the problem with a minimal, non-sensitive example.
- **Suggest a feature.** Open an issue using the feature-request template.
  Explain the research problem it solves, not just the mechanism — that helps
  keep Shodh focused and simple.
- **Improve the docs.** Corrections and clarifications to the manual, FAQ, or
  install guide are genuinely valuable and easy to review.
- **Submit code.** For anything beyond a small fix, please open an issue first
  so we can agree on the approach before you spend time on it.

---

## Licence for contributions

Shodh is released under the **Apache License 2.0** (SPDX: `Apache-2.0`).
By submitting a pull request or any other contribution, you agree that your
contribution is made under the same licence. This is the standard Apache 2.0
inbound = outbound model — there is no separate Contributor Licence Agreement.

**Why Apache 2.0?** Shodh bundles Mozilla PDF.js, which is also Apache 2.0.
Aligning the wrapper to the same licence keeps everything under one consistent
licence, adds an explicit patent grant (Section 3 of [LICENSE](LICENSE)), and
meets institutional and corporate adoption requirements more cleanly than MIT.

---

## Working with the source

- The app is `shodh.html`. Application logic is human-readable at the top and
  bottom of the file; the large block in the middle is base64-encoded **PDF.js**
  (Mozilla, Apache-2.0) and should not be hand-edited. If PDF.js needs
  updating, replace the encoded blob from an official PDF.js release rather than
  editing it, and update [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md) and
  [NOTICE](NOTICE) with the new version number.
- There is no build step and no framework: it is designed to run by opening the
  file. Please keep it that way unless there is a strong reason not to — the
  zero-install, single-file property is a core feature, not an accident.
- Test in more than one browser before submitting a pull request (at minimum a
  Chromium-based browser and Firefox), because storage and PDF behaviour can
  differ between implementations.

---

## Pull-request checklist

- [ ] The app still opens and works by double-clicking the file (no server,
      no build required).
- [ ] You tested the affected feature in at least two browsers.
- [ ] You did **not** introduce any network calls that transmit user data.
      Shodh's offline, local-only behaviour is a promise to its users; a
      change that silently breaks it will be rejected.
- [ ] If you changed or added a third-party dependency, you updated
      [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md) and [NOTICE](NOTICE).
- [ ] If you changed user-facing behaviour, you updated the relevant docs and
      [CHANGELOG.md](CHANGELOG.md).
- [ ] You did not add fabricated data, invented citations, or placeholder DOIs
      anywhere in code or documentation.
- [ ] The Apache 2.0 licence header at the top of `shodh.html` still reads
      correctly (it should not reference MIT).

---

## Reporting a security or privacy issue

If you find a problem that could expose users' data or transmit it off-device,
please **do not** open a public issue with the details. See
[SECURITY.md](SECURITY.md) for the private reporting path so the issue can
be addressed before it is publicly known.
