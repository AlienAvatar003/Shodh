# Installation & Platforms

Shodh is a single HTML file that runs in a web browser. That makes it genuinely
cross-platform: **the same `shodh.html` works on Windows, macOS, Linux, and
ChromeOS.** There is no installer to run and no runtime to manage.

This guide covers the simple universal method, per-platform notes, an optional
"install as an app" step, the separate desktop builds, and how to publish Shodh
so an entire lab can use it.

## Contents

1. [The universal method (all platforms)](#the-universal-method-all-platforms)
2. [Windows](#windows)
3. [macOS](#macos)
4. [Linux / ChromeOS](#linux--chromeos)
5. [Install it as an app (optional)](#install-it-as-an-app-optional)
6. [Optional desktop builds](#optional-desktop-builds)
7. [Publish it for others (GitHub Pages, shared drive)](#publish-it-for-others)
8. [Optional: the Ollama integration](#optional-the-ollama-integration)

---

## The universal method (all platforms)

1. Download **`shodh.html`** from this repository or from the
   [Releases](../../releases) page.
2. Save it somewhere permanent (not your Downloads folder, which you might empty).
3. **Double-click it.** It opens in your default browser and is ready to use.

Because your reviews are stored per browser and per file location (see
[How your data is stored](USER_MANUAL.md#how-your-data-is-stored)), pick a home
for `shodh.html` and open it the same way each time. If you move the file, keep
using the same browser so your reviews remain visible — and keep JSON backups
regardless.

---

## Windows

- Double-clicking `shodh.html` opens it in your default browser (Edge, Chrome,
  Firefox).
- If you keep the file on OneDrive or a network drive, make sure it is actually
  downloaded/available offline before relying on it.
- No SmartScreen warning appears for the plain HTML file — SmartScreen warnings
  are associated with downloaded **executables**, which the browser method avoids
  entirely. (See [Optional desktop builds](#optional-desktop-builds) for the
  `.exe` case.)

## macOS

- Double-clicking `shodh.html` opens it in Safari or your default browser.
- If a browser ever refuses to open a local file directly, right-click the file →
  **Open With** → your browser, or drag the file onto the browser icon.

## Linux / ChromeOS

- Double-click, or run `xdg-open shodh.html`, or drag the file into a browser
  window.
- On ChromeOS, place the file in a location the browser can access and open it
  from the Files app.

---

## Install it as an app (optional)

Modern browsers can give `shodh.html` its own window and icon, so it feels like a
desktop application while still being the same file:

- **Chrome / Edge:** open `shodh.html`, then use the browser menu →
  **Save and share** / **Apps** → **Install this site as an app** (wording varies
  by version). You get a standalone window and a launcher/desktop icon.
- This is a convenience wrapper only; your data is still stored in that browser's
  storage for that origin.

---

## Optional desktop builds

In addition to the browser method, Shodh has been packaged as **native desktop
apps** in earlier development:

- **macOS:** a Python launcher using `pywebview` to show Shodh in a native window,
  with a fallback to opening it in a browser.
- **Windows:** a small **Go** server that serves `shodh.html` locally and opens it
  in a window, cross-compiled to self-contained executables
  (e.g. `Shodh.exe` for x64 and an ARM64 build) with no runtime dependencies.

> **Not included in this repository snapshot.** The source for those launchers
> was produced in separate build sessions and is **not part of this upload**,
> which contains `shodh.html` only. If you want them in the repo, add those
> launcher files from that earlier work (or re-supply them) under, for example,
> `desktop/macos/` and `desktop/windows/`, and document their build steps here.
> Please don't ship reconstructed launcher code you haven't tested.

**Two honest caveats for the desktop route**, carried over from that work:

- **Windows SmartScreen.** Distributing an unsigned `.exe` directly is free but
  will trigger a Microsoft Defender SmartScreen warning for downloaders until the
  binary builds reputation. Eliminating the warning generally requires a paid
  code-signing certificate. Microsoft Store distribution is another path, but its
  registration terms and any fees change over time — **verify current Microsoft
  terms before relying on this**, as they may have changed since this was written.
- **Port/origin storage.** The desktop servers run on a local address and port
  (for example `127.0.0.1:<port>`). Reviews are stored against that origin in the
  browser profile the window uses, so changing the port or the access method can
  make a review appear to vanish. Keep JSON backups.

For most people, **the plain `shodh.html` browser method is the simplest and most
portable option**, and it is the one this repository is built around.

---

## Publish it for others

You said you want researchers to be able to use Shodh. Here are three ways to
distribute it.

### A. Let people download the file (simplest)

Publish `shodh.html` in this repository and point people to it, or attach it to a
GitHub **Release** so there is a stable download link and a version number.

### B. Host it on GitHub Pages (a URL anyone can open)

GitHub Pages can serve `shodh.html` as a live web page, so anyone with the link
runs Shodh in their browser — nothing to download.

1. Push this repository to GitHub.
2. In the repository, go to **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to *Deploy from a branch*,
   choose your default branch (e.g. `main`) and the `/ (root)` folder, and save.
4. Wait for the build, then visit the published URL. This repository includes a
   small **`index.html`** at the root that redirects to `shodh.html`, so the base
   URL opens the app directly. (You can also link straight to
   `https://<owner>.github.io/<repo>/shodh.html`.)

> **Data note for hosted use.** Even when Shodh is served from a URL, each visitor's
> reviews are still stored **in their own browser**, not on any server. Two people
> visiting the same URL do not share data. This preserves privacy but means users
> must keep their own JSON backups.

### C. Put it on a shared or institutional drive

Drop `shodh.html` on a shared network drive or a lab wiki. Each person opens their
own copy; each person's data stays in their own browser. This keeps everything
inside your institution's storage.

---

## Optional: the Ollama integration

The **Ask** tab can optionally use a **local** language model via
[Ollama](https://ollama.com) to summarise retrieved passages. This is entirely
optional — Shodh works without it.

1. Install Ollama from <https://ollama.com> for your operating system.
2. Pull a model (for example, a small general model) following Ollama's own
   instructions.
3. Make sure Ollama is running locally, then use the Ask tab.

Everything stays on your machine: Shodh talks to Ollama on your own computer, and
no library content is sent to a third party. As with any language model, verify
its summaries against the underlying passages.
