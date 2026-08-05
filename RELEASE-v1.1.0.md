# Shodh v1.1.0

**Release date:** 2026-08-05  
**DOI:** https://doi.org/10.5281/zenodo.21499303  
**Author:** Tanuj Namboodri, University of Miskolc

---

## What's new in v1.1.0

### Text selection → notes (Stage 2 & Ask)
Select any text from a paper abstract in Stage 2, or from a source excerpt in the Ask tab, and a floating **+ Note** button appears above the selection. Click it and the selected text is pre-filled in the note editor — press Save immediately to keep it as a highlight, or edit it before saving. Previously notes had to be typed from scratch.

Selection also works on decided papers in both the Stage 1 and Stage 2 reviewed lists (abstracts are now shown inline in those rows), so you can go back to any decided paper and annotate it without resetting it first.

### Searchable decided lists (Stage 1 & Stage 2)
Both the "Your Stage 1 decisions" panel and the "Decided at full text" panel now have a live search box. Type any part of a title, author surname, journal, year, or DOI and the list filters instantly. Multi-word queries narrow further (all terms must match). Up to 60 rows are drawn at a time with a count indicator; keep typing to narrow large lists. Tested against a 1,196-record review at under 10 ms per keystroke.

### Stage 1 exclusion recovery
A new **"Your Stage 1 decisions"** panel appears at the bottom of the Stage 1 tab — both while you are still screening and after the queue is empty. It shows every record you have voted on with a Reset button. If you excluded a paper by mistake, search for it and click Reset to put it back in your queue immediately. Only your own votes are shown to preserve blind dual-reviewer screening.

### Version stamp in masthead
The application masthead now shows **v1.1.0** so you always know which version is running. This is particularly important when distributing the Mac or Windows app, where a stale server could silently serve an older build.

---

## Mac app fixes

These are Mac-specific stability fixes that do not affect the standalone HTML file.

**Stale build served after update.** The Mac launcher compared server instances by checking truthiness of the probe result, but the probe now returns a `(bool, build_string)` tuple — always truthy in Python. This caused the new `.app` to connect to whatever old server was still running instead of starting fresh. Fixed: the launcher now correctly unpacks the tuple and compares build strings.

**Old server not killed on update.** Graceful `/quit` requests fail on servers older than v1.0.x (no endpoint). Added force-kill fallback: `lsof` on macOS to find the PID and send SIGTERM, with `pkill -f shodh_server.py` as a secondary fallback.

**WKWebView serving cached old page.** Added `?v=1.1.0` query parameter to the window URL so WKWebView treats each new version as a distinct resource and cannot serve a stale cached copy.

**All responses sent with `Cache-Control: no-store`** to prevent future caching issues.

---

## Files

| File | Description |
|------|-------------|
| `shodh.html` | Standalone single-file app — open in any modern browser, fully offline |
| `Shodh-Mac-v1.1.0.zip` | Native macOS window (pywebview), includes Save As bridge for exports |
| `Shodh-Windows-v1.1.0.zip` | Native Windows window (Go + Edge), ~6 MB |

---

## Upgrading from v1.0.x

**Browser (shodh.html):** Replace the file and reload. Your data is in browser IndexedDB and is unaffected.

**Mac app:** Quit the running Shodh window (Cmd+Q), replace `Shodh.app` with the new one, then launch. The new app detects any old server still running and replaces it automatically. The masthead should show **v1.1.0** within a second of launch.

**Windows app:** Replace `shodh.html` next to the `.exe` (the exe loads the loose file in preference to its embedded copy). Your data is preserved.

**Data migration is not required.** IndexedDB data is tied to `127.0.0.1:8503` and persists across version upgrades as long as the port does not change (Mac) or the browser profile is not cleared (HTML/Windows).

---

## Known limitations (unchanged from v1.0.x)

- No OCR; keyword-based retrieval only (no semantic search without Ollama)
- Single-machine reviewer blinding — two reviewers must use separate browser sessions or user accounts
- PDFs are not included in JSON backups; reattach after restoring from a backup
- Unsigned app warnings on macOS (Gatekeeper) and Windows (SmartScreen) — right-click → Open to bypass
- PRISMA flow counts are a working aid; verify against your final inclusion/exclusion numbers before submission
