# Third-Party Notices

Shodh is distributed as a single file, `shodh.html`, which **embeds third-party
software**. When you redistribute `shodh.html` (for example, by publishing it in
your own repository, hosting it, or attaching it to a paper), you are also
redistributing that third-party software and must comply with its licence.

This file lists those components. It is provided in good faith; if you are
redistributing Shodh in a context with strict compliance requirements, confirm
the details against the upstream projects yourself.

---

## Mozilla PDF.js

- **Purpose in Shodh:** renders and extracts text from PDF files entirely inside
  the browser, so PDFs can be read and searched offline.
- **Project:** https://github.com/mozilla/pdf.js
- **Copyright:** © Mozilla Foundation and PDF.js contributors.
- **Licence:** Apache License, Version 2.0.

### Required attribution (Apache License 2.0)

```
Copyright Mozilla Foundation and contributors.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```

### What you should do when redistributing

The Apache 2.0 licence requires that you **retain this notice** and provide a
copy of the licence. To do that cleanly:

1. Keep this `THIRD_PARTY_NOTICES.md` file alongside `shodh.html`.
2. Add the full Apache License 2.0 text to your repository. You can download it
   from <https://www.apache.org/licenses/LICENSE-2.0.txt> and save it as, for
   example, `licenses/Apache-2.0.txt`, or copy `pdf.js`'s own `LICENSE` file
   from its repository.

> **Verify the exact PDF.js version.** Shodh embeds a specific build of PDF.js
> as a base64 blob inside `shodh.html`. If you need the precise version number
> and commit for a compliance record, extract it from the bundled library or
> from the build notes for your copy of Shodh, rather than relying on this
> document.

---

## Anything else?

If future versions of Shodh add other bundled libraries (fonts, parsers, UI
components), list them here with the same three items: what it is, where it
comes from, and under what licence.
