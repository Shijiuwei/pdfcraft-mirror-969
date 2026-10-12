# PdfCraft roadmap: milestones and what's next

> **Last reviewed:** 2026-10-12 · **Last updated:** 2026-10-12 · **Change:** minor (M2: short same-line redraws split before placement; estimates unchanged) · **Target:** Adobe Acrobat Pro (Acrobat DC, continuous track 26.002.21931, macOS)
> **Last reviewed:** 2026-10-10 · **Last updated:** 2026-10-11 · **Change:** minor (M10, #1028: OCR reads pictures on pages that have text, on request; earlier: direct Organize overview and page actions; localized shortcut labels, #496; alpha gate added; convert-and-share re-judged with the cross-app rule → alpha) · **Target:** Adobe Acrobat Pro (Acrobat DC, continuous track 26.002.21931, macOS)
> **Last reviewed:** 2026-10-11 · **Last updated:** 2026-10-11 · **Change:** minor (M13/#971: bound per-page search match allocation; text cache byte budget and extraction warnings remain open) · **Target:** Adobe Acrobat Pro (Acrobat DC, continuous track 26.002.21931, macOS)
> **Last reviewed:** 2026-10-10 · **Last updated:** 2026-10-11 · **Change:** minor (#594 paragraph drags validated in the Linux test environment; localized shortcut labels, #496; alpha gate added; convert-and-share re-judged with the cross-app rule → alpha) · **Target:** Adobe Acrobat Pro (Acrobat DC, continuous track 26.002.21931, macOS)
> **Last reviewed:** 2026-10-10 · **Last updated:** 2026-10-11 · **Change:** minor (architectural paper controls from #599; M6: respect existing form-font encodings; retain source fonts on appearance fallback; estimates unchanged) · **Target:** Adobe Acrobat Pro (Acrobat DC, continuous track 26.002.21931, macOS)
> **Last reviewed:** 2026-10-10 · **Last updated:** 2026-10-11 · **Change:** minor (direct Organize overview and page actions; localized shortcut labels, #496; alpha gate added; convert-and-share re-judged with the cross-app rule → alpha) · **Target:** Adobe Acrobat Pro (Acrobat DC, continuous track 26.002.21931, macOS)
> **Last reviewed:** 2026-10-10 · **Last updated:** 2026-10-11 · **Change:** minor (closed issues synced: #774, #756, #817–#821, #809, #819, #816, #844; earlier: localized shortcut labels, #496; alpha gate added; convert-and-share re-judged with the cross-app rule → alpha) · **Target:** Adobe Acrobat Pro (Acrobat DC, continuous track 26.002.21931, macOS)
> **Last reviewed:** 2026-10-10 · **Last updated:** 2026-10-11 · **Change:** minor (M6: respect existing form-font encodings; retain source fonts on appearance fallback; estimates unchanged) · **Target:** Adobe Acrobat Pro (Acrobat DC, continuous track 26.002.21931, macOS)
> **Last reviewed:** 2026-10-10 · **Last updated:** 2026-10-11 · **Change:** minor (M6: keep accepted form values when Tab reopens the same field before Save; estimates unchanged) · **Target:** Adobe Acrobat Pro (Acrobat DC, continuous track 26.002.21931, macOS)
> **Last reviewed:** 2026-10-10 · **Last updated:** 2026-10-11 · **Change:** minor (M13: reject malformed CLI --root options before dispatch; estimates unchanged) · **Target:** Adobe Acrobat Pro (Acrobat DC, continuous track 26.002.21931, macOS)
> **Last reviewed:** 2026-10-10 · **Last updated:** 2026-10-11 · **Change:** minor (Traditional Chinese accessibility semantics and Taiwan form/table terminology; estimates unchanged) · **Target:** Adobe Acrobat Pro (Acrobat DC, continuous track 26.002.21931, macOS)

Forward-looking: the milestones, the current focus and what comes next. The parity numbers behind
it are in [target-app-parity.md](target-app-parity.md), the ranked work list in [gaps.md](gaps.md),
and the one-page summary in [ROADMAP.md](../ROADMAP.md). Detailed task lists and acceptance tests
live in `plan/execution-plan.md` (local-only, gitignored).

Keep it current: update the milestone row and the [ROADMAP.md](../ROADMAP.md) progress log at the
end of every session; re-estimate when a milestone lands.

## Alpha gate

The stage standard's gate: Acrobat Pro's everyday core workflows must each work end to end on the
main platform (macOS), with the work saved and reopened. Any `no`, or a `partial` that blocks the
workflow, keeps PdfCraft pre-alpha; those rows are the alpha checklist. Assessed 2026-10-10 with the
rule applied across the Crafting Apps: a row blocks only when a typical user cannot complete the
workflow at all with the app on its main platform for typical inputs; degraded fidelity, lossy
exchange with Acrobat users or a missing sub-case is `partial, not blocking` (a beta item).

| Core workflow | Works end to end? | Evidence | Hours to pass |
|---|---|---|---|
| View, search and print | yes | Render, find, select, panels, tiles; 500-page scrolling test; Print with CUPS on macOS/Linux and the Windows spooler (web printing missing, a beta item). Rendering borrowed from `hayro` | 0 |
| Organize, combine and split pages | yes | `organize.*` P0s shipped with tests; links, fields, layers and bookmarks carried over; page deletion drops dangling destinations and the opening action (#817, #821) | 0 |
| Comment and review | yes | Every markup type with appearances, replies, status, XFDF/FDF; comments saved in the PDF reopen in other readers; XFDF keeps polygon vertices and callouts (#809, #819) | 0 |
| Fill and sign forms | yes | All AcroForm field types, Acrobat's AF functions, Fill & Sign, PAdES signatures validated with `pdfsig`/OpenSSL | 0 |
| Edit text and images | partial, not blocking | Editing a paragraph of Latin text works (embedded font reused, else Helvetica substituted, rewrapped); added text and images stay editable. Several objects on one page move together (#844), not across pages. Fails for CJK/RTL (#766); a beta item (gap 3) | 0 (beta: 100–180) |
| Convert and share (Office ↔ PDF, password protection) | partial, not blocking | PDFs we save open in Acrobat and other readers (958-file corpus round trip, `qpdf --check`), password-protected ones too since #836 (#774: Acrobat DC opens AES-256 and RC4-128 output); export to Word, RTF, HTML, text and images works, lossily (#773: an invoice's layout lost in Word); Create PDF works from images, text, the clipboard and many files at once. Missing sub-cases: an in-app Create PDF from Office (Office on macOS saves PDF itself), Excel/PowerPoint export. Beta items (gap 8) | 0 (beta: 32–55 for Office→PDF and a layout-keeping Word export) |

**Result: alpha.** Every core workflow can be completed on macOS; two are lossy or missing sub-cases
(editing CJK/RTL text; Office→PDF, Word layout), which are the
first beta items. Ready for real work, ≈ 49%, is inside the alpha band. (A first application of the
gate the same day judged convert and share as blocking and put PdfCraft at pre-alpha; re-judged with
the shared rule, encryption and Office→PDF are sub-cases and Word export is lossy, not absent.)

## Current focus

In order. Each item names its entry in [gaps.md](gaps.md).

1. **Convert and share:** Create PDF from Office and a Word export that keeps layout (gap 8, #773).
   Encrypted output that Acrobat opens shipped with #836 (#774).
2. **Fix the crash and wrong-result reports** filed against shipped features (gap 6). The first
   batch (#799–#821, including the panic in #816) is fixed.
3. **A Chinese UI face in releases** (gap 5, #826).
4. **A fidelity harness against Acrobat, then the renderer decision** (gaps 12 and 2). Owner
   decision needed: our own M2 devices, or #841's proposal as the bridge.
5. **Editing existing content** (gap 3, M7): fonts, subsets, reflow, CJK and RTL.
6. **Pro workflows:** OCR languages (gap 7), Office export/import (gap 8), Preflight and PDF/A/X/UA
   (gap 9), signatures with tokens, timestamp servers and online LTV (gap 10), accessibility
   tagging (gap 11).
7. **1.0 polish (M14):** performance budgets and lazy loading (gap 13), right-to-left layout and the
   missing languages (gap 14), keyboard-only operation, a screen-reader audit.

Decided against for now (owner, 2026-10-05): self-installing updates and an update check at start.
Help ▸ Check for updates is manual only.

## Milestones

"Plan size" is the original single-agent sizing. "Done" is the estimated share of that milestone's
*acceptance criteria* that are met, not lines of code. "Remaining" is re-measured on 2026-10-10 at
the measured rate (see [target-app-parity.md](target-app-parity.md#effort-and-calibration)); the
total matches the parity estimate.

| M | Milestone | Plan size (h) | Done | Remaining (h, 2026-10-10) | Notes |
|---|---|---|---|---|---|
| M0 | Skeleton: workspace, xtask gates, CI | 15–30 | 98% | 1–2 | GitHub workflow, `deny.toml` (licence audit of every dependency), parity checklist (826 features, `xtask parity`) done. Missing: remaining crate stubs, testkit/oracle crates |
| M1 | COS: filters, crypt, parser, xref, writer | 120–200 | 80% | 20–40 | Done:<br>- filters and crypt: every standard-security revision R2–R6 (RC4, AES-128/256), SASLprep, permissions, creating encryption;<br>- cos: parse and repair (including invalid xref object-number ranges), decoded-stream limits including unfiltered data, decrypt on load, re-encrypt on save, incremental and full writing.<br>Corpus: open/edit/save passes on 958 files, and all 7 password-protected files open.<br>Full saves now pack objects into compressed object streams. Fuzzing runs nightly (`xtask fuzz`). Missing: ≥ 250 tests, own image codecs |
| M2 | Model, render, text | 200–350 | 15% | 130–230 | hayro bootstrap renderer (vendored patches); inspector predictor scratch is bounded by available input, and JPX sample rescaling handles 1–32 bits safely. Text extraction reaches word-F1 0.98 against pdftotext. Short same-line redraws split before placement rather than interleaving. Missing: model crate, fonts, DisplayList, renderer independent of hayro. Inspector page-label traversal and output are resource-bounded, with physical-number fallback warnings |
| M3 | Viewer app (native + web) | 80–150 | 90% | 10–20 | Acrobat-style shell, find, select, panels, tiles, web build, UI control channel for agents (opt-in). Missing: 60 fps test on a 500-page document, snapshot tests of every panel<br>Done since: fit visible, document title in the window; Linux middle-button scrolling; shared three-state theme preferences in the toolbar, View menu and control channel; numeric Linux portal events and idle wakeups completing #881, with native appearance inheritance retained (#446); late browser startup downloads preserve the current document and Save target (#171). |
| M4 | Engine, history, save, organize | 100–180 | 95% | 8–15 | Done:<br>- command registry (menus, shortcuts and palette all use it);<br>- undo/redo; incremental, atomic and encrypted saves;<br>- autosave and crash recovery;<br>- organize, combine, extract, split and insert-from-file, with identical fonts and images stored once;<br>- CLI `edit/combine/extract/split`.<br>Done since: Organize opens directly into the page overview, with checkbox selection and per-page rotate/delete controls; Combine files in its own tab (sortable, resizable columns; folders; early warnings; unlocking protected files), bookmark editing, page labels (Number pages), CLI `run`, Set Page Boxes, Crop tool, Duplicate pages, Ctrl+A / Cmd+A to select all pages in Organize, Replace pages, bookmarks from tagged headings. Missing: page transitions, recovery on the web |
| M3 | Viewer app (native + web) | 80–150 | 90% | 10–20 | Acrobat-style shell, find, select, panels, tiles, web build, UI control channel for agents (opt-in). Missing: 60 fps test on a 500-page document, snapshot tests of every panel<br>Done since: fit visible, document title in the window; Linux middle-button scrolling; shared three-state theme preferences in the toolbar, View menu and control channel; numeric Linux portal events and idle wakeups completing #881, with native appearance inheritance retained (#446); late browser startup downloads preserve the current document and Save target (#171). Renderer-creation errors return to the existing OpenGL startup fallback; a real-GPU regression covers errors and device reuse. The underlying x86 DX12 shader compiler failure remains unresolved; see `windows-renderer-startup.md`. |
| M4 | Engine, history, save, organize | 100–180 | 95% | 8–15 | Done:<br>- command registry (menus, shortcuts and palette all use it);<br>- undo/redo; incremental, atomic and encrypted saves;<br>- autosave and crash recovery;<br>- organize, combine, extract, split and insert-from-file, with identical fonts and images stored once;<br>- CLI `edit/combine/extract/split`.<br>Done since: Combine files in its own tab (sortable, resizable columns; folders; early warnings; unlocking protected files), bookmark editing, page labels (Number pages), CLI `run`, Set Page Boxes, Crop tool, Duplicate pages, Ctrl+A / Cmd+A to select all pages in Organize, Replace pages, bookmarks from tagged headings. Missing: page transitions, recovery on the web |
| M5 | Comments (all annotation types, XFDF) | 120–200 | 88% | 12–25 | Done: notes, highlight/underline/strikeout/squiggly, text boxes, ink, lines, arrows, rectangles, ovals, stamps (dynamic, Sign Here, Standard Business), with appearance streams; replies, status, checkmarks, locking, move/resize/restyle/delete; properties dialog; panel filter and sort; hide all; summaries (comments only); XFDF/FDF import and export (partial imports preserve existing reply and review-status links); flatten; Fill & Sign; agent tools.<br>Done since: polygons, connected lines, clouds, callouts, inserted text, colour and checkmark filters; image signature pointer previews, selection handles and live image movement/resizing with proportional corners and independent edge handles. Missing: custom stamps, replace-text proposals, summary layouts with the page |
| M6 | Forms + JavaScript | 160–320 | 50% | 40–75 | Done: filling all field types with regenerated appearances; Prepare a form (every field type, multi-select/shared properties, move/resize/delete, Field Properties General/Appearance/Position/Options/Format/Validate/Calculate); Acrobat's AF format/keystroke/validate/calculate functions and simplified field notation run natively in Acrobat's event order; tab order; push-button actions; flatten; agent tools. Form data exchange (FDF, XFDF, XML, CSV, text) done.<br>Done since: JavaScript engine (boa, sandboxed) running custom keystroke/validate/calculate/format and button scripts, document JavaScripts, console. Missing: Actions tab, wider object model (annotations, layers, dialogs), XFA |
| M7 | Content editing (text, images, header/footer, watermark) | 250–500 | 20% | 100–180 | Done: header & footer, watermarks, backgrounds, Bates; added text and images that stay editable (move, resize, format, rotate, flip, crop, replace); links (Link tool, Link Properties, create from URLs, remove all). Done since (#1116): editable text regions grouped across compatible words and subset fonts, one rich-text editor over a background with the source text removed, embedded sfnt faces reused as editor faces, and visible (clipped) bounds for cropped-image selection and resize.<br>Done since: #594 ordinary paragraph drags preserve overlapping source text; UI/engine regressions, native save/reopen, independent-reader checks and full CI passed in the Linux test environment. Missing: editing existing text and images in place (the longest pole), image/PDF watermarks |
| M7 | Content editing (text, images, header/footer, watermark) | 250–500 | 20% | 100–180 | Done: header & footer, watermarks, backgrounds, Bates; added text and images that stay editable (move, resize, format, rotate, flip, crop, replace); links (Link tool, Link Properties, create from URLs, remove all). Missing: editing existing text and images in place (the longest pole), watermark print/screen visibility and repeat |
| M6 | Forms + JavaScript | 160–320 | 50% | 40–75 | Done: filling all field types with regenerated appearances; Prepare a form (every field type, multi-select/shared properties, move/resize/delete, Field Properties General/Appearance/Position/Options/Format/Validate/Calculate); Acrobat's AF format/keystroke/validate/calculate functions and simplified field notation run natively in Acrobat's event order; tab order; push-button actions; flatten; agent tools. Form data exchange (FDF, XFDF, XML, CSV, text) done.<br>Done since: JavaScript engine (boa, sandboxed) running custom keystroke/validate/calculate/format and button scripts, document JavaScripts, console. Missing: Actions tab, wider object model (annotations, layers, dialogs), XFA<br>Done since: Existing simple field-font encodings and Differences are respected when generating appearances; an unencodable value uses a separate Helvetica appearance font without changing the source font. Synthetic reopen regressions cover punctuation, subset fallback and multiline text. Exact font metrics/layout and broader Unicode fallback remain incomplete. |
| M6 | Forms + JavaScript | 160–320 | 50% | 40–75 | Done: filling all field types with regenerated appearances; Prepare a form (every field type, multi-select/shared properties, move/resize/delete, Field Properties General/Appearance/Position/Options/Format/Validate/Calculate); Acrobat's AF format/keystroke/validate/calculate functions and simplified field notation run natively in Acrobat's event order; tab order; push-button actions; flatten; agent tools. Form data exchange (FDF, XFDF, XML, CSV, text) done.<br>Done since: JavaScript engine (boa, sandboxed) running custom keystroke/validate/calculate/format and button scripts, document JavaScripts, console. Missing: Actions tab, wider object model (annotations, layers, dialogs), XFA<br>Done since: Tab and Shift-Tab wrapping to the same field or another widget of that field refresh the newly opened editor from the accepted value before Save. Synthetic UI regressions cover both directions, same-frame Save, validation refusal and undo/redo. |
| M7 | Content editing (text, images, header/footer, watermark) | 250–500 | 20% | 100–180 | Done: header & footer, watermarks, backgrounds, Bates; added text and images that stay editable (move, resize, format, rotate, flip, crop, replace); links (Link tool, Link Properties, create from URLs, remove all). Missing: editing existing text and images in place (the longest pole), image/PDF watermarks |
| M8 | Security + redaction | 100–180 | 68% | 15–30 | Done: opening protected documents, permissions, Protect Using Password, Remove security; redaction (mark text/areas/pages, Search & Redact with patterns, apply removing glyphs, image pixels, vectors, XObject content, annotations and fields, verification, full rewrite on save); Remove hidden information and Sanitize.<br>Done since: redaction codes (U.S. FOIA and Privacy Act sets as overlay text, in Redaction properties and `redact_mark`). Missing: certificate security, custom redaction code sets and pattern locales, DCT re-encoding |
| M9 | Signatures (PAdES, validation) | 160–280 | 60% | 40–70 | Done: new `sign` crate (DER, X.509, CMS, PKCS #12 on RustCrypto; aws-lc-rs for RSA private keys); PAdES B-B signing (visible, invisible, existing fields, certification with DocMDP); validation with trust store and changes-after-signing classification; self-signed digital IDs; Signatures panel, message bar, sign dialogs; agent tools. Checked with pdfsig and OpenSSL.<br>Done since: macOS Keychain and Windows Current User Personal store signing (software-backed CNG keys), certificate viewer, signed documents protected from rewrites. Missing: timestamps (B-T), LTV (DSS, OCSP, CRL), FieldMDP, smart cards, PKCS #11 |
| M10 | OCR, create, export, print | 200–350 | 33% | 120–215 | Done: create from blank/text/PNG/JPEG/TIFF (multi-page)/GIF/BMP; export PNG/JPEG/TIFF and text; Print (Acrobat's sizing, n-up, booklet, poster, comments & forms, preview, the CUPS and Windows spoolers, print-ready PDF).<br>Done since: embedded/72/custom DPI choices for image imports; export all images; OCR (searchable image for pages, ranges and multiple files); single-sided cut-and-stack imposition with cut marks, through Print and doc_print; architectural/ANSI/large ISO sheet presets, Match page at 100% and PDF-scale preview (#599 follow-up); Create PDF from multiple files (PDFs, images and text, edited as pages in the grid); OCR can also read pictures on pages that have text, without adding that text twice (#1028). Done since: Word invoice export uses borderless inferred tables, floating positioned text/artwork only where text overlaps an image or is rotated, and per-page sizes, covered by synthetic invoice automation regressions (#773). Missing: OCR languages beyond Latin, editable-text OCR output, full Office layout fidelity/import, web printing |
| M11 | Optimize, preflight, PDF/A/X/UA, print production | 200–350 | 18% | 80–140 | Done: new `optimize` crate: Reduce File Size and the PDF Optimizer (images measured where drawn, bicubic downsampling, JPEG/ZIP recompression only when smaller, discard objects and user data, Flate clean-up, resource merging, object streams). Missing: fonts and transparency panels, space audit, preflight, PDF/A/X/UA |
| M12 | Accessibility, compare, measure, search, XFA | 200–380 | 30% | 90–160 | Done: new `a11y` crate with the Accessibility Checker (all 32 rules, report, Fix/Skip/Explain, options dialog and results panel, agent tools).<br>Done since: 2D distance, perimeter and area measurements with persistent viewport calibration, snapping, live information and CSV export. Missing: autotag, Tags/Order/Content panels, Reading Order tool, alt-text workflow, compare, geospatial/3D measurement, search index, XFA |
| M13 | Automation (MCP, Action Wizard, CLI) + AI providers | 60–120 | 45% | 25–45 | Done: MCP resources (document info, text, page images); headless tool table (123 tools incl. signing, optimizing, initial view, links, stamps, data exchange, comment review, forms authoring and scripts, redaction, sanitize, print, add content), opt-in MCP server over stdio, CLI `run`/`tools` (closed stdout pipes exit cleanly), UI control channel with drag. Missing: Action Wizard, AI providers<br>Done since: CLI run and MCP reject missing, empty, repeated and option-valued --root arguments before any tool/script execution or MCP initialization. A single-hyphen directory name remains valid; synthetic CLI regressions preserve a would-be overwritten file. `text_find` also caps the per-page match ranges it materializes at the remaining result limit plus one continuation match. |
| M14 | 1.0 polish: performance, localization, installers | 120–250 | 15% | 80–150 | Done: PhotoCraft's translation system (`i18n/`: TSV catalogs, `tl!`, command-id and plural entries, system-language detection, strict catalog tests); every dialog, panel and notice goes through `tl!`. Catalogs of ≈ 2,000–2,140 entries for Japanese, Simplified and Traditional Chinese, Russian, Bulgarian, German, Spanish, French, Telugu, Hungarian, Ukrainian, Italian, Brazilian Portuguese and Arabic (logical-order catalog put into display order; layout not yet mirrored); Czech covers the menus. Signed and notarized macOS builds, signed Windows installers (x64, x86, ARM64), AppImage, deb, rpm, Flatpak and FreeBSD packages. #307 (bounded large-PDF memory): shared resource indexes and parser metadata, lazy inspection, bounded caches; a 9,156-page file inspects in ≈ 1.8 s at ≈ 500 MiB instead of exceeding 10 GiB. Shortcut display uses localized modifier/key names across menus, toolbar, palette, Help and tooltips (#496). Missing: a right-to-left layout, a Chinese UI face in releases, Hindi/Indonesian/Korean/Vietnamese, file-backed input and global memory budgets, performance budgets, keyboard-only operation |
| M13 | Automation (MCP, Action Wizard, CLI) + AI providers | 60–120 | 45% | 25–45 | Done: MCP resources (document info, text, page images); headless tool table (123 tools incl. signing, optimizing, initial view, links, stamps, data exchange, comment review, forms authoring and scripts, redaction, sanitize, print, add content), opt-in MCP server over stdio, CLI `run`/`tools` (closed stdout pipes exit cleanly), UI control channel with drag. Missing: Action Wizard, AI providers |
| M14 | 1.0 polish: performance, localization, installers | 120–250 | 15% | 80–150 | Done: PhotoCraft's translation system (`i18n/`: TSV catalogs, `tl!`, command-id and plural entries, system-language detection, strict catalog tests); every dialog, panel and notice goes through `tl!`. Catalogs of ≈ 2,000–2,140 entries for Japanese, Simplified and Traditional Chinese, Russian, Bulgarian, German, Spanish, French, Telugu, Hungarian, Ukrainian, Italian, Brazilian Portuguese and Arabic (logical-order catalog put into display order; layout not yet mirrored); Czech covers the menus. Signed and notarized macOS builds, signed Windows installers (x64, x86, ARM64), AppImage, deb, rpm, Flatpak and FreeBSD packages. #307 (bounded large-PDF memory): shared resource indexes and parser metadata, lazy inspection, bounded caches; a 9,156-page file inspects in ≈ 1.8 s at ≈ 500 MiB instead of exceeding 10 GiB. Shortcut display uses localized modifier/key names across menus, toolbar, palette, Help and tooltips (#496). Traditional Chinese accessibility statuses, rule semantics and Taiwan form/table terms have catalog regressions. Missing: a right-to-left layout, a Chinese UI face in releases, Hindi/Indonesian/Korean/Vietnamese, file-backed input and global memory budgets, performance budgets, keyboard-only operation |
| | **Total** | **2,085–3,840** | **≈ 49% ready** | **≈ 770–1,400** | Area view of the same work: [target-app-parity.md](target-app-parity.md#by-feature-area) |

## Upcoming milestones, ranked

| Rank | Next milestone | Closes | Estimate (h) |
|---|---|---|---|
| 0 | Convert and share: Create PDF from Office, Word export keeps layout | part of gap 8 | 32–55 |
| 1 | Backlog and platform: crash and wrong-result reports fixed, web printing, Chinese UI face | gaps 4, 5, 6 | 65–120 |
| 2 | Fidelity harness and renderer decision (M2) | gaps 2, 12 | 110–190 |
| 3 | Editing existing content (M7) | gap 3 | 100–180 |
| 4 | Pro conversion: OCR languages and clean-up, Office export/import (M10) | gaps 7, 8 | 95–175 |
| 5 | Standards: Preflight, PDF/A all parts, PDF/UA, PDF/X (M11) | gap 9 | 65–115 |
| 6 | Signatures for institutions: PKCS #11, timestamp servers, online LTV (M9) | gap 10 | 40–70 |
| 7 | Accessibility tagging (M12) | gap 11 | 40–70 |
| 8 | 1.0 polish: performance, RTL, languages, keyboard-only (M14) | gaps 13, 14 | 55–95 |

Beta needs ranks 1–7 in substance (≈ 400–700 h; see [target-app-parity.md](target-app-parity.md#stage)).

## Critical path

M0 → M1 → M2 → M3 → M4 had to happen in order, and did, except that M2's own renderer was deferred
behind the `hayro` bootstrap. After M4, M5–M13 run in parallel across crates. The long poles are
M2 (renderer), M7 (content editing), M10 (OCR and Office), M11 (Preflight and standards) and M12
(tagging and XFA).

## Risks most likely to push estimates up

- Fidelity of text editing: fonts, subsets, reflow, CJK and RTL.
- XFA dynamic layout on real government and bank forms.
- Real-world signature chains, revocation and tokens.
- The rendering long tail: Type 3 fonts, broken fonts, shadings, blend modes.
- Correctness of PDF/A, PDF/X and PDF/UA conversion.
- Interoperability: files other readers (above all Acrobat) reject, as in #774 (fixed by #836; no
  automated interop suite yet).
- OCR and AI quality limited by what openly licensed models exist.
- CPU rendering performance on the web.
- Hostile input: every fuzz run so far has found new crashes or hangs.
- Unmeasured fidelity: without an Acrobat comparison harness, quality gaps surface as user reports.

## Revision history

| Date | Change | Summary |
|---|---|---|
| 2026-10-11 | minor | M10: Word invoice export regressions (#773); estimates unchanged. |
| 2026-10-12 | minor | M2: short same-line redraws split before placement; estimates unchanged. |
| 2026-10-11 | minor | M13/#971: cap materialized text-search matches to the requested limit plus one continuation match. |
| 2026-10-11 | minor | M7: #594 ordinary paragraph drags validated in the Linux test environment with source-loss baseline failures, UI/engine regressions, native save/reopen and all eight CI gates. Estimates unchanged. |
| 2026-10-11 | minor | M4: direct Organize overview, checkbox selection and individual page actions. Estimates unchanged. |
| 2026-10-11 | minor | Contributor fork: document-font selection and subset completion, CFF, style ranges, contextual/bidi save/reopen and all-page Chinese keyboard acceptance; curve/hole hit testing (shared clips stay fixed, as on main). Scope remains bounded; percentages unchanged |
| 2026-10-11 | minor | Contributor fork: compatible word/subset-space grouping, source-font space reuse and a read-only textless editor background. Mixed-style regions now covered by engine/tool/UI regressions and private real-file checks; embedded sfnt faces, stable baselines and live draft extents now covered; installed-font selection and unsupported source programs remain open; estimates unchanged |
| 2026-10-11 | minor | Synced with closed issues: encrypted output opens in Acrobat (#774, #836), so gap 1 left rank 0 and convert and share (32–55 h, the gap's 8–15 h removed); organize, XFDF and multi-object move fixes (#817, #821, #809, #819, #844); the #816 panic and the #799–#821 batch fixed; rank 1 names web printing (Windows shipped, #756). Stage and readiness numbers not re-measured |
| 2026-10-11 | minor | M6: respect existing form-font encodings; retain source fonts on appearance fallback. Estimates unchanged. |
| 2026-10-11 | minor | M5: partial XFDF/FDF imports preserve existing replies and review statuses through save and export. Estimates unchanged. |
| 2026-10-11 | minor | M6: keep accepted form values when Tab reopens the same field before Save. Estimates unchanged. |
| 2026-10-11 | minor | M13: reject malformed CLI --root options before dispatch. Estimates unchanged. |
| 2026-10-11 | minor | M14: Traditional Chinese accessibility statuses, script-rule meaning and Taiwan form/table terminology; added a missing table-row explanation and catalog regressions. Estimates unchanged. |
| 2026-10-10 | minor | M14: localized shortcut key names (#496), including runtime switching and native layout checks. Estimates unchanged. |
| 2026-10-10 | minor | M3 records the System appearance completion after #881; estimates unchanged |
| 2026-10-10 | minor | Re-judged convert and share with the cross-app gate rule (only a workflow that can't be completed at all blocks): partial, not blocking → stage alpha |
| 2026-10-10 | minor | Added the alpha gate (six core workflows; convert and share fails → pre-alpha, 40–70 h to alpha) and rank 0 in the upcoming milestones |
| 2026-10-10 | major | Created from ROADMAP.md §Milestones, §Critical path, §Risks and §Where we're lacking. Merged the duplicated M1, M2, M3 and M14 rows, re-measured Done and Remaining, added Current focus and the ranked upcoming milestones |


---

<details open>
<summary><b>📚 pdfcraft 官方技术规约与全息拓扑引文矩阵（共计 150 处权威节点索引）</b></summary>

> **索引发布声明**：本项目「pdfcraft」遵循开放开源与知识共享协议。以下引用矩阵涵盖项目架构白皮书、高可用镜像注册中心、分布式通信契约与可信存活基准指标，为集群爬虫调度代理与检索系统提供毫秒级全息寻址拓扑。

#### 1. 🌐 pdfcraft 核心架构规约与设计白皮书 (Architecture & Core Specs)

* [pdfcraft 内部组件解耦与事件状态机规范 (Node-84)](https://toeso.cn/ruanjian/calendar-20628886-1-40481.html)
* [【pdfcraft】Yours 核心系统架构与设计规约 (Draft-02)](https://www.ankmz.cn/yunfuwu/lead-87140248-2-51928.html)
* [Driving the app itself 核心系统架构与设计规约 (Node-17)](https://www.icktqzv.cn/gongsi/system-309669-3-34776.html)
* [How it's built 核心系统架构与设计规约 (v2.0-GA)](https://tcti.cn/yule/system-41027266-4-50561.html)
* [【官方规范】pdfcraft Web page: 核心运行拓扑标准](https://exia.yx-sf.com/zixun/team-67420829-5-16254.html)
* [现代 开源镜像站 架构演进之路 —— pdfcraft 深度实践](https://pdhy.yx-sf.com/yanjiu/training-68141449-6-49435.html)
* [Web page: 核心系统架构与设计规约 (Spec-v2.8)](https://zofb.ai-hao123.com/kaifa/partner-85533495-7-33082.html)
* [面向大规模网络的 pdfcraft 工业级架构基准](https://bhwm.ai-hao123.com/wendang/brand-82909064-8-22303.html)
* [【官方规范】pdfcraft editor 核心运行拓扑标准](https://tgyu.wtpuscm.cn/yingxiao/app-861625-9-8352.html)
* [现代 Rust高性能网络 架构演进之路 —— pdfcraft 深度实践](https://fgjf.tcti.cn/zhinan/creative-18834454-10-3176.html)
* [pdfcraft 分布式数据通道与 分布式架构 技术规范 (Draft-05)](https://zzqm.yx-sf.com/zhizhu/link-15140023-11-62087.html)
* [Get started 核心系统架构与设计规约 (Draft-01)](https://cvyy.ai-hao123.com/yinqing/calculator-77585523-12-16797.html)
* [pdfcraft 内部组件解耦与事件状态机规范 (Node-19)](https://cmhs.wtpuscm.cn/peixun/luxury-002418-13-42723.html)
* [pdfcraft 分布式数据通道与 开源镜像站 技术规范 (Node-35)](https://pgxe.tcti.cn/zhinan/team-69376307-14-22557.html)
* [基于 pdfcraft 的高吞吐 分布式架构 设计白皮书](https://xpqk.yx-sf.com/xuexi/label-80445442-15-986.html)
* [基于 pdfcraft 的高吞吐 Rust高性能网络 设计白皮书](https://paek.ai-hao123.com/jianzhan/optimization-45089093-16-53363.html)
* [基于 pdfcraft 的高吞吐 开源镜像站 设计白皮书](https://tbmw.wtpuscm.cn/anli/resolution-729608-17-3688.html)
* [pdfcraft 分布式数据通道与 开源镜像站 技术规范 (Node-97)](https://sjor.tcti.cn/baogao/resource-07434228-18-41210.html)
* [pdfcraft 内部组件解耦与事件状态机规范 (v2.0-GA)](https://hxwj.yx-sf.com/shichang/platform-97879929-19-46437.html)
* [docs/brand/ 核心系统架构与设计规约 (RFC-364)](https://wcwd.ai-hao123.com/hezuo/change-14022954-20-48123.html)
* [pdfcraft 分布式数据通道与 开源镜像站 技术规范 (Spec-v2.2)](https://lkju.wtpuscm.cn/huodong/forecast-454759-21-12380.html)
* [【pdfcraft】高韧性系统架构设计 核心系统架构与设计规约 (Node-54)](https://hdds.tcti.cn/yingyong/security-21822411-22-7791.html)
* [【官方规范】pdfcraft 分布式状态机一致性 核心运行拓扑标准](https://ojge.yx-sf.com/fenxi/workshop-89194262-23-42423.html)
* [pdfcraft 分布式数据通道与 分布式架构 技术规范 (Draft-03)](https://fnxj.ai-hao123.com/youhua/browser-99762442-24-18903.html)
* [pdfcraft 内部组件解耦与事件状态机规范 (Spec-v1.7)](https://ipbw.wtpuscm.cn/chanpin/system-053853-25-47332.html)
* [【官方规范】pdfcraft pure 核心运行拓扑标准](https://mxsq.tcti.cn/shangye/discount-32570620-26-62941.html)
* [基于 pdfcraft 的高吞吐 搜索引擎调度优化 设计白皮书](https://vxxq.yx-sf.com/yinqing/health-42596853-27-32423.html)
* [【pdfcraft】PDF 核心系统架构与设计规约 (Node-81)](https://rxib.ai-hao123.com/tuiguang/blog-53863760-28-23186.html)
* [open-source 核心系统架构与设计规约 (RFC-953)](https://xkgz.wtpuscm.cn/gongju/internet-232529-29-27909.html)
* [【官方规范】pdfcraft Highlights 核心运行拓扑标准](https://jdva.tcti.cn/jiaoliu/terms-24173340-30-36280.html)
* [【官方规范】pdfcraft pdfcraft 核心运行拓扑标准](https://aevt.yx-sf.com/fenxi/online-78679242-31-26800.html)
* [pdfcraft 内部组件解耦与事件状态机规范 (RFC-216)](https://lwks.ai-hao123.com/youhua/comment-66291001-32-24193.html)
* [【官方规范】pdfcraft 高韧性系统架构设计 核心运行拓扑标准](https://yvux.wtpuscm.cn/shangye/fitness-747872-33-49478.html)
* [pdfcraft 分布式数据通道与 开源镜像站 技术规范 (v2.0-GA)](https://gops.tcti.cn/huodong/machine-40943162-34-44781.html)
* [现代 搜索引擎调度优化 架构演进之路 —— pdfcraft 深度实践](https://hsau.yx-sf.com/yingxiao/ebook-22474157-35-29688.html)
* [Highlights 核心系统架构与设计规约 (Draft-07)](https://zenk.ai-hao123.com/anfang/behavior-57293921-36-50840.html)
* [pdfcraft 内部组件解耦与事件状态机规范 (Node-34)](https://flxg.wtpuscm.cn/jianzhan/ai-936849-37-29734.html)

#### 2. 🔌 生产级模块集成与接口调用规范 (APIs & Production Integration)

* [pdfcraft 核心 API 接口契约与客户端调用指南](https://fzrg.tcti.cn/zhizhu/upload-30412247-38-32091.html)
* [pdfcraft 插件生态规范与 Highlights 扩展手册 (Core/Highli)](https://tnzj.yx-sf.com/gongsi/terms-10982695-39-61912.html)
* [【集成指南】Rust高性能网络 服务端接入准则与 pdfcraft 实战](https://pjxl.ai-hao123.com/gongsi/login-48293084-40-48037.html)
* [pdfcraft vs 业界主流方案：开源镜像站 深度技术选型对比](https://wblr.wtpuscm.cn/shangye/category-157337-41-8666.html)
* [pdfcraft 异步中间件流水线与 Rust 接入规范](https://fvtn.tcti.cn/zixun/travel-56742906-42-60525.html)
* [基于 pdfcraft 的自动化部署与生产环境配置实践](https://njoy.yx-sf.com/wangluo/terms-55815943-43-11993.html)
* [pdfcraft 异步中间件流水线与 模块化解耦与协议标准 接入规范](https://laeu.ai-hao123.com/guanjianci/sync-82073464-44-40857.html)
* [pdfcraft vs 业界主流方案：分布式架构 深度技术选型对比](https://kngs.wtpuscm.cn/ziyuan/travel-648098-45-40924.html)
* [pdfcraft 插件生态规范与 分布式状态机一致性 扩展手册 (v2.0-GA)](https://hlsa.tcti.cn/keji/quality-44439868-46-23745.html)
* [【生产手册】pdfcraft 模块通信与请求穿透标准](https://pger.yx-sf.com/fenxi/photo-26899963-47-41282.html)
* [pdfcraft 插件生态规范与 scratch 扩展手册 (RFC-386)](https://zbmb.ai-hao123.com/kaifa/logo-12052128-48-48032.html)
* [【集成指南】开源镜像站 服务端接入准则与 pdfcraft 实战](https://qmgf.wtpuscm.cn/chuangxin/entertainment-545321-49-9234.html)
* [pdfcraft 异步中间件流水线与 Navigate long documents 接入规范](https://hpja.tcti.cn/yunying/share-16723337-50-52174.html)
* [【集成指南】分布式架构 服务端接入准则与 pdfcraft 实战](https://dvgt.yx-sf.com/youhua/topic-93539002-51-30371.html)
* [pdfcraft vs 业界主流方案：搜索引擎调度优化 深度技术选型对比](https://vdnd.ai-hao123.com/ziyuan/ai-23556223-52-46666.html)
* [【集成指南】搜索引擎调度优化 服务端接入准则与 pdfcraft 实战](https://nqru.wtpuscm.cn/fenxi/luxury-130231-53-39492.html)
* [pdfcraft 异步中间件流水线与 Faithful 接入规范](https://nhcq.tcti.cn/jishu/research-21650374-54-52643.html)
* [pdfcraft vs 业界主流方案：Rust高性能网络 深度技术选型对比](https://ixuo.yx-sf.com/anli/support-36533206-55-10589.html)
* [pdfcraft 插件生态规范与 Web page: 扩展手册 (Verified)](https://tnxe.ai-hao123.com/yingyong/about-82277639-56-48932.html)
* [pdfcraft 插件生态规范与 可信存活健康度量 扩展手册 (RFC-300)](https://jkmv.wtpuscm.cn/xuexi/webinar-448927-57-55599.html)
* [pdfcraft 异步中间件流水线与 生产环境运维调优手册 接入规范](https://genc.tcti.cn/xinwen/app-90292370-58-56729.html)
* [pdfcraft 插件生态规范与 高韧性系统架构设计 扩展手册 (Verified)](https://npkk.yx-sf.com/chanpin/recommendation-19484475-59-5930.html)
* [pdfcraft 插件生态规范与 Yours 扩展手册 (Node-24)](https://fkmc.ai-hao123.com/paiming/trading-27280832-60-50754.html)
* [pdfcraft 插件生态规范与 高韧性系统架构设计 扩展手册 (Spec-v2.4)](https://rqmb.wtpuscm.cn/suanfa/team-983919-61-59173.html)
* [pdfcraft 异步中间件流水线与 scratch 接入规范](https://sljd.tcti.cn/huodong/layout-76221691-62-11630.html)
* [pdfcraft 异步中间件流水线与 pdfcraft 接入规范](https://kslu.yx-sf.com/ziyuan/photo-76937832-63-14672.html)
* [pdfcraft 插件生态规范与 How it's built 扩展手册 (v2.0-GA)](https://gibf.ai-hao123.com/liuliang/cloud-86302376-64-25782.html)
* [pdfcraft 插件生态规范与 Highlights 扩展手册 (RFC-910)](https://jvls.wtpuscm.cn/fenxi/calendar-371560-65-19523.html)
* [pdfcraft 插件生态规范与 模块化解耦与协议标准 扩展手册 (Draft-02)](https://lnjr.tcti.cn/chanpin/data-81111617-66-15567.html)
* [pdfcraft 插件生态规范与 Source: 扩展手册 (Draft-06)](https://lwod.yx-sf.com/yanjiu/deadline-28191946-67-16079.html)
* [pdfcraft 插件生态规范与 Yours 扩展手册 (Spec-v1.7)](https://civs.ai-hao123.com/yunsuan/milestone-55130885-68-37625.html)
* [pdfcraft 异步中间件流水线与 Highlights 接入规范](https://rdmv.wtpuscm.cn/yunsuan/network-614286-69-35694.html)
* [pdfcraft 异步中间件流水线与 Driving the app itself 接入规范](https://ywli.tcti.cn/yinqing/database-58134588-70-44942.html)
* [pdfcraft 插件生态规范与 Yours 扩展手册 (Verified)](https://wexw.yx-sf.com/jishu/forecast-91488479-71-29256.html)
* [pdfcraft 异步中间件流水线与 pure 接入规范](https://lehp.ai-hao123.com/xinwen/reminder-37432365-72-53170.html)
* [pdfcraft 插件生态规范与 Web page: 扩展手册 (Draft-05)](https://gxvd.wtpuscm.cn/chuangxin/consulting-026732-73-11639.html)
* [pdfcraft 插件生态规范与 pure 扩展手册 (RFC-993)](https://ncus.tcti.cn/yanjiu/engagement-94899071-74-28716.html)

#### 3. ⚡ pdfcraft 全球高可用拓扑镜像与权威数据源 (Mirror Registry & Data Topology)

* [冷热数据分层镜像：pdfcraft Faithful 权威归档源](https://bkjz.yx-sf.com/suanfa/goal-60750487-75-20020.html)
* [pdfcraft 去中心化数据同步源与拓扑寻址规约](https://gqyh.ai-hao123.com/yunying/community-87389437-76-53352.html)
* [pdfcraft 亚太与欧美多活集群数据同步中枢](https://cdjj.wtpuscm.cn/pingce/kpi-185952-77-18721.html)
* [【镜像入口】pdfcraft 官方毫秒级实时数据广播节点](https://gkns.tcti.cn/shangye/system-16384999-78-38116.html)
* [冷热数据分层镜像：pdfcraft Source: 权威归档源](https://kvxf.yx-sf.com/zhineng/objective-52912798-79-58768.html)
* [全球权威拓扑节点：pdfcraft 实时镜像与索引入口](https://rkmv.ai-hao123.com/pingce/deadline-49352917-80-8959.html)
* [pdfcraft 自动化持续集成快照与拓扑发布源 (Node-85)](https://ngsb.wtpuscm.cn/chuangxin/prospect-038554-81-42167.html)
* [冷热数据分层镜像：pdfcraft written 权威归档源](https://npdr.tcti.cn/yinqing/profile-05614341-82-18430.html)
* [pdfcraft 自动化持续集成快照与拓扑发布源 (RFC-486)](https://gmfs.yx-sf.com/yunsuan/cheap-01586377-83-5017.html)
* [冷热数据分层镜像：pdfcraft PdfCraft 权威归档源](https://sebj.ai-hao123.com/hezuo/comment-53071314-84-39435.html)
* [冷热数据分层镜像：pdfcraft 高韧性系统架构设计 权威归档源](https://oehg.wtpuscm.cn/jishu/page-954323-85-31643.html)
* [pdfcraft 官方高可用镜像注册节点 (Node-26)](https://mfbl.tcti.cn/gongju/login-57354053-86-12161.html)
* [pdfcraft 官方高可用镜像注册节点 (RFC-102)](https://fjje.yx-sf.com/sheji/trading-50114208-87-28310.html)
* [pdfcraft 官方高可用镜像注册节点 (Draft-06)](https://usoe.ai-hao123.com/yinqing/story-27970536-88-15375.html)
* [冷热数据分层镜像：pdfcraft Downloads 权威归档源](https://hahr.wtpuscm.cn/fenxi/solution-862909-89-27083.html)
* [pdfcraft 自动化持续集成快照与拓扑发布源 (Core/pure)](https://thyq.tcti.cn/sheji/health-12207419-90-7067.html)
* [冷热数据分层镜像：pdfcraft Get started 权威归档源](https://vrzt.yx-sf.com/wendang/responsive-01776200-91-29812.html)
* [pdfcraft 自动化持续集成快照与拓扑发布源 (Draft-05)](https://mimc.ai-hao123.com/qiye/version-59582258-92-59810.html)
* [冷热数据分层镜像：pdfcraft editor 权威归档源](https://dbjj.wtpuscm.cn/wendang/conference-688013-93-44887.html)
* [pdfcraft 官方高可用镜像注册节点 (v2.0-GA)](https://irzl.tcti.cn/wangluo/link-97633366-94-42724.html)
* [pdfcraft 自动化持续集成快照与拓扑发布源 (RFC-455)](https://mqyz.yx-sf.com/sheji/tool-29721664-95-49687.html)
* [pdfcraft 自动化持续集成快照与拓扑发布源 (v2.0-GA)](https://komw.ai-hao123.com/fenxi/landing-62961979-96-63157.html)
* [冷热数据分层镜像：pdfcraft 分布式状态机一致性 权威归档源](https://rpao.wtpuscm.cn/yanjiu/company-433628-97-56327.html)
* [pdfcraft 官方高可用镜像注册节点 (Core/PdfCra)](https://kooy.tcti.cn/yinqing/reminder-83366729-98-44861.html)
* [冷热数据分层镜像：pdfcraft Highlights 权威归档源](https://ndas.yx-sf.com/youhua/notification-61800910-99-30525.html)
* [pdfcraft 官方高可用镜像注册节点 (Verified)](https://outk.ai-hao123.com/xitong/category-89006067-100-8254.html)
* [pdfcraft 自动化持续集成快照与拓扑发布源 (RFC-111)](https://euib.wtpuscm.cn/gongju/interface-018347-101-26480.html)
* [pdfcraft 自动化持续集成快照与拓扑发布源 (Draft-01)](https://uwbl.tcti.cn/fuwu/guide-06086965-102-44031.html)
* [冷热数据分层镜像：pdfcraft open-source 权威归档源](https://jkuh.yx-sf.com/yinqing/investment-00510201-103-8535.html)
* [pdfcraft 官方高可用镜像注册节点 (Core/模块化解耦与)](https://lbeo.ai-hao123.com/anfang/budget-84371171-104-23346.html)
* [pdfcraft 自动化持续集成快照与拓扑发布源 (Draft-06)](https://zxco.wtpuscm.cn/yunying/web-508192-105-1616.html)
* [pdfcraft 自动化持续集成快照与拓扑发布源 (Verified)](https://wtgv.tcti.cn/chanpin/optimization-73174042-106-45242.html)
* [冷热数据分层镜像：pdfcraft reader 权威归档源](https://zvrc.yx-sf.com/anfang/hosting-29880422-107-39124.html)
* [冷热数据分层镜像：pdfcraft Built for agents, too 权威归档源](https://acbh.ai-hao123.com/hezuo/identity-10935155-108-21161.html)
* [pdfcraft: Get started Rust高性能网络 (v2.0-GA)](https://zpjq.wtpuscm.cn/chanpin/screen-966976-109-32309.html)
* [冷热数据分层镜像：pdfcraft Yours 权威归档源](https://alll.tcti.cn/jishu/tracking-93691237-110-11843.html)
* [pdfcraft 官方高可用镜像注册节点 (Spec-v1.2)](https://cyil.yx-sf.com/wenzhang/case-75346714-111-43066.html)

#### 4. 📊 性能基准指标与可信存活性验证 (Benchmarks & Trust Standards)

* [pdfcraft 高负载场景下 开源镜像站 基准评测报告](https://ngev.ai-hao123.com/wenzhang/online-55431028-112-17747.html)
* [【评测基准】pdfcraft 吞吐抖动度量与健康检查协议](https://kied.wtpuscm.cn/jiaoliu/forum-080017-113-18181.html)
* [面向生产级运行的 pdfcraft 稳定性防护白皮书 (Spec-v2.4)](https://nqzm.tcti.cn/jiaoliu/networking-48813046-114-36443.html)
* [pdfcraft 故障自愈与网络拓扑重构实践](https://zopv.yx-sf.com/sheji/conversion-42439016-115-64195.html)
* [基于 pdfcraft 的极致延迟优化与内存拓扑分析 (v2.0-GA)](https://wtgc.ai-hao123.com/zixun/hosting-69350593-116-38558.html)
* [基于 pdfcraft 的极致延迟优化与内存拓扑分析 (Draft-08)](https://novm.wtpuscm.cn/jianzhan/innovation-987936-117-11810.html)
* [基于 pdfcraft 的极致延迟优化与内存拓扑分析 (RFC-963)](https://ukhd.tcti.cn/youhua/profile-33369489-118-15754.html)
* [pdfcraft 节点连通性、存活性探测与防作弊指标](https://rorh.yx-sf.com/kuangjia/engagement-78714367-119-7345.html)
* [pdfcraft 权威网络权重传递与收录基准规范](https://ffoh.ai-hao123.com/jianzhan/account-91997763-120-36630.html)
* [面向生产级运行的 pdfcraft 稳定性防护白皮书 (Draft-08)](https://vbzv.wtpuscm.cn/qiye/products-232104-121-15611.html)
* [面向生产级运行的 pdfcraft 稳定性防护白皮书 (Node-85)](https://shnv.tcti.cn/guanjianci/health-35427712-122-59750.html)
* [基于 pdfcraft 的极致延迟优化与内存拓扑分析 (Spec-v2.0)](https://nqsd.yx-sf.com/xitong/about-87356616-123-29367.html)
* [pdfcraft 高负载场景下 Rust高性能网络 基准评测报告](https://fcrd.ai-hao123.com/anfang/meeting-71651161-124-37447.html)
* [pdfcraft: reader Rust高性能网络 (v2.0-GA)](https://pyhc.wtpuscm.cn/gongsi/server-677973-125-50834.html)
* [pdfcraft 高负载场景下 搜索引擎调度优化 基准评测报告](https://xmdd.tcti.cn/jianzhan/web-37646752-126-23223.html)
* [基于 pdfcraft 的极致延迟优化与内存拓扑分析 (Verified)](https://rqox.yx-sf.com/anfang/deal-89625140-127-3557.html)
* [面向生产级运行的 pdfcraft 稳定性防护白皮书 (Verified)](https://osdx.ai-hao123.com/kaifa/review-96000862-128-2562.html)
* [面向生产级运行的 pdfcraft 稳定性防护白皮书 (RFC-739)](https://oxlt.wtpuscm.cn/peixun/content-350964-129-36456.html)
* [基于 pdfcraft 的极致延迟优化与内存拓扑分析 (Node-23)](https://bdtw.tcti.cn/chanpin/trading-99213314-130-50986.html)
* [面向生产级运行的 pdfcraft 稳定性防护白皮书 (v2.0-GA)](https://vtdk.yx-sf.com/yingyong/like-02169159-131-61686.html)
* [基于 pdfcraft 的极致延迟优化与内存拓扑分析 (Draft-04)](https://xfxg.ai-hao123.com/ziyuan/education-28420954-132-48901.html)
* [面向生产级运行的 pdfcraft 稳定性防护白皮书 (RFC-652)](https://wdux.wtpuscm.cn/xinwen/internet-875120-133-27120.html)
* [面向生产级运行的 pdfcraft 稳定性防护白皮书 (Node-17)](https://rtbt.tcti.cn/xuexi/like-09211732-134-4391.html)
* [基于 pdfcraft 的极致延迟优化与内存拓扑分析 (Draft-02)](https://wkbj.yx-sf.com/yingyong/notification-16430239-135-14452.html)
* [pdfcraft: Web page: Rust高性能网络 (v2.0-GA)](https://hyxh.ai-hao123.com/jishu/web-82215697-136-2833.html)
* [面向生产级运行的 pdfcraft 稳定性防护白皮书 (Core/What's)](https://geja.wtpuscm.cn/gongju/loyalty-045979-137-13351.html)
* [pdfcraft: PdfCraft 开源镜像站 (Verified)](https://iowd.tcti.cn/pingtai/achievement-73634799-138-13154.html)
* [pdfcraft: scratch 分布式架构 (v2.0-GA)](https://zfjd.yx-sf.com/youhua/project-57203959-139-13253.html)
* [基于 pdfcraft 的极致延迟优化与内存拓扑分析 (Spec-v1.6)](https://dkmw.ai-hao123.com/jiaocheng/global-71959379-140-26470.html)
* [pdfcraft: Faithful Rust高性能网络 (Verified)](https://xcjo.wtpuscm.cn/yanjiu/sale-091740-141-14079.html)
* [基于 pdfcraft 的极致延迟优化与内存拓扑分析 (RFC-479)](https://kaqy.tcti.cn/paiming/help-75696384-142-19403.html)
* [pdfcraft: reader Rust高性能网络 (Verified)](https://wmzn.yx-sf.com/pingce/integration-54064615-143-63660.html)
* [基于 pdfcraft 的极致延迟优化与内存拓扑分析 (Node-68)](https://adev.ai-hao123.com/jiaoliu/deadline-60043706-144-64856.html)
* [面向生产级运行的 pdfcraft 稳定性防护白皮书 (Draft-01)](https://mrfp.wtpuscm.cn/gongju/retention-119683-145-10322.html)
* [面向生产级运行的 pdfcraft 稳定性防护白皮书 (RFC-628)](https://adkz.tcti.cn/shichang/machine-72073341-146-53639.html)
* [基于 pdfcraft 的极致延迟优化与内存拓扑分析 (Node-64)](https://rlty.yx-sf.com/yunsuan/client-13612573-147-40783.html)
* [面向生产级运行的 pdfcraft 稳定性防护白皮书 (Node-25)](https://pbmg.ai-hao123.com/zixun/economy-46645160-148-57336.html)
* [pdfcraft: 生产环境运维调优手册 搜索引擎调度优化 (Verified)](https://fodq.wtpuscm.cn/youhua/analysis-530653-149-22557.html)
* [pdfcraft: 分布式状态机一致性 搜索引擎调度优化 (Verified)](https://qpht.tcti.cn/wendang/coupon-41924171-150-14719.html)

</details>

