# PdfCraft parity with Adobe Acrobat Pro

> **Last reviewed:** 2026-10-10 · **Last updated:** 2026-10-11 · **Change:** minor (document-font subset completion, source styles and curved/shared image clips in the contributor fork; closed issues synced, scores not re-judged: #774, #756, #740, #759, #799–#821, #825, #844; earlier: readiness table with hours per audience; full number restated as the standard's additive weighted sum, 47% → 49%; earlier: second look: cross-cutting double count removed, mainstream-practitioner number added, core-workflow gate applied → alpha) · **Target:** Adobe Acrobat Pro (Acrobat DC, continuous track 26.002.21931, macOS)

The authoritative assessment of how close PdfCraft is to Acrobat Pro. [ROADMAP.md](../ROADMAP.md)
summarizes it; [gaps.md](gaps.md) lists every shortfall one by one; the deep-dive checklists are
[pdf-spec-parity.md](pdf-spec-parity.md), [file-format-parity.md](file-format-parity.md),
[ui-parity.md](ui-parity.md), [hardware-parity.md](hardware-parity.md) and
[localization-parity.md](localization-parity.md).

**Scope.** Parity means the *offline* feature set of Acrobat Pro. Adobe's cloud services (Document
Cloud storage, Acrobat Sign requests, shared review, the AI Assistant, Adobe Express, the Adobe
Approved Trust List) are out of scope: 23 such features are tracked as `na` in
`parity/acrobat-features.toml` and excluded from every percentage.

## Headline

| | Value | Kind |
|---|---|---|
| **Feature breadth**, tier-weighted | **≈ 67%** | measured (checklist; weights below) |
| Feature breadth, unweighted | 56.9% (423 shipped + 74 partial of 808) | measured (`cargo xtask parity` arithmetic) |
| Must-have (P0) features | 94.2% (226 + 23 partial of 252) | measured |
| Feature breadth, mainstream practitioner | ≈ 70% tier-weighted (63.2% unweighted: 292 + 44 partial of 497; P0 95.3%) | measured ([split below](#mainstream-practitioner-vs-full-acrobat-pro)) |
| **Ready for real work**, full Acrobat Pro | **≈ 49%** (range 45–53%) | estimated (weighted sum over dimensions, [below](#by-dimension)) |
| **Ready for real work**, mainstream practitioner | **≈ 55%** (range 50–60%) | estimated ([split below](#mainstream-practitioner-vs-full-acrobat-pro)) |
| **Ready for real work**, essentials user | **≈ 66%** (range 60–70%) | estimated ([below](#essentials-user)) |
| **Stage** | **alpha** (passes the core-workflow gate) | see [Stage](#stage) |
| Remaining to beta | ≈ 400–700 Opus 5.5 agent-hours | estimated |
| Remaining to full parity | ≈ 780–1,400 Opus 5.5 agent-hours | estimated |

### Readiness by audience

| Audience | Ready | Opus 5.5 agent-hours to ≈ 95% | Work that dominates |
|---|---|---|---|
| Full Acrobat Pro (ready for real work) | ≈ 49% | ≈ 780–1,400 h (≈ 300–550 h wall clock with 3–5 agents; 60–70% parallelizes) | Own renderer and fidelity harness, editing existing content, OCR and Office conversion, Preflight and PDF/A/X/UA, accessibility tagging, signatures for institutions |
| Mainstream practitioner | ≈ 55% | ≈ 500–900 h (≈ 200–400 h wall clock; ≈ 60% parallelizes) | Rendering fidelity, editing existing text (CJK, RTL, subsets), conversion (Word layout, Excel, PowerPoint, Office→PDF), OCR languages, the bug backlog |
| Essentials user | ≈ 66% | ≈ 180–330 h (≈ 90–180 h wall clock; ≈ 50% parallelizes) | Rendering fidelity on everyday files, launch and GPU stability, simple text fixes, Word export layout, Chinese UI glyphs |

Hours are calibrated as in [Effort and calibration](#effort-and-calibration) (≈ 1k kept lines per agent-hour for new features, 3–10× slower for hardening and fidelity). The audiences are nested subsets, so essentials ≤ mainstream ≤ full.

The gap between the numbers is the story of this release: most of what an Acrobat user reaches
for *exists*, but much of it is shallower than Acrobat's, rendering is still borrowed, quality has
never been measured side by side with Acrobat, and the first public releases (0.4.0, 0.5.0) drew
245 open issues in two days, including one that made our encrypted files unreadable in Acrobat
([#774](https://npkk.yx-sf.com/chanpin/recommendation-19484475.html), fixed by #836).

## How this was measured

- **Target identified from the installed app.** `/Applications/Adobe Acrobat DC/Adobe Acrobat.app`,
  `CFBundleShortVersionString` 26.002.21931. Inspected without launching it and without opening
  anything inside `Contents/Resources/JavaScripts/` (clean-room rules, `AGENTS.md` §2): the
  `Info.plist` `CFBundleDocumentTypes` (the formats it opens: see
  [file-format-parity.md](file-format-parity.md)), the `.lproj` folder names (24 localizations,
  plus the MEA/MEH/NAF Middle East and North Africa editions named in `Resources/Sequences/`), the
  names in `Contents/Plugins/` (Accessibility, AcroForm, Checkers, Comments, DigSig, EScript,
  MakeAccessible, PPKLite, ReadOutLoud, Reflow, SaveAsRTF, Search, Spelling, WebLink, …),
  `Contents/Frameworks/` (AdobeJP2K, Adobe3D, AdobeCoolType, AdobeLinguistic, the OCR-capable
  `OnDeviceIntelligence_SDK`, …) and the `PDF Optimizer` and `Sequences` (Action Wizard) folders.
  Names and listings only.
- **Feature breadth from the checklist.** `parity/acrobat-features.toml` tracks 831 Acrobat Pro
  features (808 in scope). `cargo xtask parity` (in `xtask ci`) rejects any `shipped` claim whose
  command, automation tool or cited test does not exist. The numbers here were computed from the
  file on `origin/main` at 5d590604 (2026-10-10) with the same arithmetic as the tool (partial
  counts half). The checklist itself was written from Acrobat's public documentation, not diffed
  against a menu dump, so it can miss features; that risk is one of the gaps.
- **Ready for real work by judgement, from evidence:** the code (152k lines of Rust in `crates/`,
  `apps/` and `xtask`, 1,765 tests, 184 registered commands, 141 automation tools); the vendored
  renderer's patch list (`vendor/README.md`); user reports on GitHub (245 open, 107 closed issues on
  2026-10-10); release packaging (`.github/workflows/release.yml`); and knowledge of Acrobat Pro's
  feature set from Adobe's public documentation.
- **Not measured, and the largest uncertainty:** no side-by-side comparison of rendering, text
  extraction or form behaviour against Acrobat exists yet. Every "ready" figure below is an
  estimate.

### Weights

Feature breadth weights the checklist's tiers by how much Acrobat users rely on them: **P0 50%,
P1 30%, P2 15%, P3 5%** → 0.50 × 94.2 + 0.30 × 61.0 + 0.15 × 12.0 + 0.05 × 2.3 ≈ **67%**.

Ready for real work weights the areas by how often an Acrobat Pro user reaches for them (judgement:
Adobe publishes no usage data): view 16%, comment 12%, edit 12%, organize 10%, forms 10%,
create/export 9%, sign 7%, protect 5%, print 5%, OCR 4%, core 3%, optimize/standards 3%,
accessibility 2%, automation/preferences 2%. That gives the Features dimension, ≈ 49%.

The **full ready-for-real-work number is an additive weighted sum over the dimensions** (standard
method; weights by what decides whether a professional can switch): features 40%, file formats and
conversion 12%, UI/UX 10%, PDF specification 8%, stability 8%, performance 6%, localization 5%,
platforms 5%, hardware 4%, ecosystem 1%, AI 1%:
0.40 × 49 + 0.12 × 40 + 0.10 × 55 + 0.08 × 60 + 0.08 × 50 + 0.06 × 40 + 0.05 × 59 + 0.05 × 70 +
0.04 × 35 + 0.01 × 30 + 0.01 × 0 = 49.25 → **≈ 49%**.

History: the first version of this file subtracted 9 points from the area figure for cross-cutting
shortfalls (40%); the second look found that a double count (Windows printing, encrypted-output
interop and Chinese glyphs were already scored in their areas) and used a 2-point deduction (47%);
this version replaces the deduction with the standard's weighted sum over dimensions (49%). Method
aligned with the standard, no new evidence. Multiplicative discounts are used only for the
mainstream and essentials numbers.

## Mainstream practitioner vs full Acrobat Pro

The checklist covers all of Acrobat Pro, including surfaces a typical practitioner rarely opens.
Splitting it (measured from `parity/acrobat-features.toml`):

| Slice | Features | Shipped | Partial | Unweighted | Tier-weighted | P0 |
|---|---|---|---|---|---|---|
| Mainstream: view, comment (without measuring), edit, organize, forms (without XFA and JavaScript tooling), protect and redact, OCR, create and export, compress (Reduce File Size, Optimizer), print (without print production) | 497 | 292 | 44 | 63.2% | ≈ 70% | 95.3% (193) |
| Specialist: core internals, digital-signature PKI, accessibility remediation, automation and preferences, Preflight and PDF/A/X/UA, print production, measuring, XFA and JavaScript tooling | 311 | 131 | 30 | 46.9% | ≈ 63% | 90.7% (59) |
| All | 808 | 423 | 74 | 56.9% | ≈ 67% | 94.2% (252) |

So the checklist is **not** dominated by niche surface (38% of rows), and the P0 tier, which is
mostly mainstream, is at 94–95% in both slices. What holds the mainstream number down is P1 depth
(69%) and the P2 long tail (13%: rulers, loupe, portfolios, spell check, Bates across files).

**Ready for real work, mainstream practitioner ≈ 55%**, weighting the mainstream areas by use and
scoring only their mainstream features: view 20% × 60, comment 15% × 70, edit 15% × 35,
organize 12% × 75, fill and sign 12% × 70, convert 10% × 30, protect and redact 6% × 55,
OCR 4% × 20, compress 3% × 60, print 3% × 50 = 55.6%. Read-only, review, form-filling and page
workflows are close to Acrobat; editing existing content, conversion and OCR are not.

### Essentials user

Someone who uses Acrobat for the everyday basics and never opens the rest. Scored on those features
only, by depth, then discounted for what such a user actually runs into. Advanced options, Pro
workflows, exchange edge cases and everything outside the mainstream slice are excluded.

| Core feature | Weight | Depth | Evidence |
|---|---|---|---|
| Open the PDFs people send and read them (render, zoom, scroll, page through) | 20% | 80% | Repair of damaged files, 958-file corpus; rendering borrowed but broadly right (#794 is a TikZ pattern) |
| Find, select and copy text | 8% | 85% | Find, options, results list; word-F1 0.98 |
| Print | 8% | 55% | Good on macOS and Linux; Windows prints since #847 (#756), not yet re-scored |
| Highlight, sticky notes, text comments | 12% | 85% | All markup types, replies, properties |
| Fill in forms | 10% | 85% | Every AcroForm field type, Acrobat's formatting and calculations |
| Fill & Sign: typed, drawn or image signature | 10% | 85% | Fill & Sign tools; flatten on save |
| Rotate, delete, reorder and extract pages | 8% | 85% | Organize grid, drag reorder, thumbnails |
| Combine files | 6% | 85% | Combine tab with bookmarks per file |
| Fix a typo in existing text | 5% | 40% | Latin paragraphs only; font may be substituted |
| Export to Word or images | 5% | 45% | Images good; Word loses layout (#773) |
| Reduce file size | 3% | 75% | Reduce File Size, Optimizer |
| Protect with a password | 3% | 30% | Works in PdfCraft; Acrobat DC opens the output since #836 (#774), not yet re-scored |
| Undo, save, autosave | 2% | 90% | Undo after save, atomic saves, crash recovery |

Weighted depth: **≈ 75%**. Discounts an essentials user hits: launch and stability (54 issues about
installing, launching, GPU and windows; OpenGL fallback) −5 points; discoverability and clarity
(an Acrobat-like shell with Home and All tools, but tool-mode friction such as #721; #825 is fixed) −2;
opening what people send (Chinese UI glyph boxes #826, CJK documents #758) −2.
**Essentials user ≈ 66%** (60–70%).

### User sentiment (second look, 2026-10-10)

Practitioners' praise is real and consistent with these numbers:

- **Adoption:** 7,595 GitHub stars, 2,661 forks; release downloads 177,301 (v0.4.0) and 39,447
  (v0.5.0, its first day).
- **Praise:** 23 of 359 issues written by users carry explicit praise ("amazing bit of software"
  #693, "ridiculously fast and awesome PDF editor" #320, "brilliant" #542, "fantastic and very useful"
  #369, "Gigantic stuff… I love it" #449). Switching reports: #179 switched from Adobe Reader on
  Windows ("covers nearly everything I used Reader for"); #232 replacing macOS Preview; #273
  "open source alternative to Acrobat"; #195 would "replace Acrobat completely" once hardware-token
  signing exists.
- **What users hit** (issue titles, excluding 35 agent-filed `fix(...)` reports): installation,
  launch and GPU/window problems 54, rendering and display 46, editing text and images 41, CJK and
  other fonts and glyphs 41, signing and certificates 35, printing 23, forms 18, conversion and
  export 16, OCR 5. Roughly two thirds are bugs (≈ 213 vs ≈ 111 feature requests), concentrated in
  core paths rather than niche features.

The praise comes overwhelmingly from Reader-class work (view, annotate, fill, sign, organize), where
the mainstream number is highest; the requests and bugs cluster on editing, CJK, printing,
conversion and signing tokens, which is where the gaps are. That supports raising the full number
from 40% to 47% (the double count; restated as 49% by the weighted-sum method) and reporting the mainstream 55% beside it; it does not support
calling PdfCraft a replacement for Acrobat Pro yet.

## By dimension

Hours are Opus 5.5 agent wall-clock hours, low–high. Rows marked *within features* are part of the
features total and are shown for orientation; the others add to it.

| Dimension | Ready | Weight | Remaining (h) | Counted | Evidence | Doc |
|---|---|---|---|---|---|---|
| Features (14 areas) | ≈ 49% depth; 67% breadth | 40% | 610–1,100 | base | Area table below | this file |
| UI/UX fidelity | ≈ 55% | 10% | 30–60 | additional | Acrobat-style shell, All tools, Home, command palette; missing single-key accelerators, rulers/guides, multiple windows, popups; user reports #739, #744, #746, #789 (#759 and #844 fixed) | [ui-parity.md](ui-parity.md) |
| File formats and conversion | ≈ 40% | 12% | 120–220 | within features | PDF read/write strong, encrypted output included (#774 fixed); export Word is layout-poor (#773); no Excel/PowerPoint export, no Office/HTML/PostScript import | [file-format-parity.md](file-format-parity.md) |
| PDF specification and standards | ≈ 60% | 8% | 150–260 | within features | ISO 32000 syntax, encryption, annotations and AcroForm strong; rendering and fonts borrowed from `hayro`; PDF 2.0 extras, linearization, public-key security absent; PDF/A partial, PDF/X/UA none | [pdf-spec-parity.md](pdf-spec-parity.md) |
| Hardware | ≈ 35% | 4% | 25–50 | additional | Page raster is CPU only (Acrobat has GPU rendering); Windows CNG and macOS Keychain keys sign, no PKCS #11; no scanners; no printing on the web (Windows shipped, #756) | [hardware-parity.md](hardware-parity.md) |
| Localization | ≈ 59% over the 12 key languages | 5% | 35–60 | additional | 15 catalogs, 13 at 94–100%; Chinese UI shows tofu in releases (#826, #688); Arabic not mirrored; no Hindi, Indonesian, Korean, Vietnamese | [localization-parity.md](localization-parity.md) |
| Performance | ≈ 40% | 6% | 25–45 | additional | 500-page smooth scrolling and large-file memory work (#307) done; no performance budgets (`misc.performance-budgets`), no lazy loading of GB files; blurry text at 1080p/1440p (#730) | [gaps.md](gaps.md) |
| Stability | ≈ 50% | 8% | 45–80 | additional | Never-crash rules and nightly fuzzing; 245 open issues on 2026-10-10, many of them `fix(...)` reports of wrong results in shipped features (the #799–#821 batch is fixed) | [gaps.md](gaps.md) |
| Platforms | ≈ 70% | 5% | 15–30 | additional | macOS (signed, notarized), Windows x64/x86/ARM64 (signed), Linux (AppImage, deb, rpm, Flatpak), FreeBSD, web (WASM). Acrobat has no Linux, FreeBSD or full web editor; we lack Windows and web printing, web OCR and web recovery | [hardware-parity.md](hardware-parity.md) |
| Ecosystem and plug-ins | ≈ 30% | 1% | 10–20 | within features | No plug-in SDK or folder-level JavaScript; Action Wizard partial. Agent automation (CLI, MCP, UI control channel) has no Acrobat equivalent | [gaps.md](gaps.md) |
| AI features | ≈ 0% (in scope) | 1% | 20–40 | within features | Acrobat's AI Assistant is cloud-only (out of scope). Local, opt-in provider interface (`misc.ai-provider`) not started | [gaps.md](gaps.md) |
| **Total (weighted sum)** | **≈ 49%** | 100% | **≈ 780–1,400** | | | |

## By feature area

Breadth is measured from the checklist (partial = ½). Ready is estimated. Hours are remaining to
full parity in that area.

| Area | Features | Shipped | Partial | Breadth | Ready | Remaining (h) | What's strong / what's missing |
|---|---|---|---|---|---|---|---|
| A Core model and fidelity | 56 | 42 | 2 | 76.8% | 70% | 25–45 | Parser, repair, R2–R6 encryption, incremental and atomic saves, undo, autosave, crash recovery, revisions. Encrypted output opens in Acrobat (#774). Missing: lazy loading of GB files, linearization, PDF 2.0 extras, Arlington validation, public-key security, own image codecs |
| B View and navigation | 92 | 52 | 11 | 62.5% | 55% | 110–190 | Shell, layouts, zoom, find, panels, tiles, web build, 500-page scrolling. **Pages are drawn by the vendored `hayro`** (22 + 9 local patches): all 7 rendering P0s are partial. Missing: own renderer or a decided replacement (#841), multiple windows, split view, rulers/guides, loupe, reflow, search across files |
| C Content editing | 61 | 29 | 7 | 53.3% | 30% | 100–180 | Edit existing paragraphs (font reused or Helvetica substituted, rewrapped), added text and images stay editable, header/footer, watermarks, backgrounds, Bates, links. Missing: robust editing of real-world text (subset fonts, CJK, RTL #766, rotated), lists, vector/object editing, arrange/align, spell check, multi-select move across pages (same-page shipped, #844) |
| D Organize pages | 76 | 45 | 3 | 61.2% | 70% | 12–25 | Organize grid, insert/extract/replace/split/combine with links, fields, layers and bookmarks carried over; page labels, boxes, bookmarks from structure. Missing: transitions, attachments editing, portfolios, struct-tree merge, field-name conflicts (destination and annotation fixes #817, #818, #821 shipped) |
| E Comments and review | 65 | 46 | 9 | 77.7% | 70% | 12–25 | Every markup type with appearances, replies, status, filters, stamps (custom, dynamic), XFDF/FDF, summaries, flatten, 2D measuring. Missing: rich-text runs, popup windows, summary layouts with pages, per-type hiding (XFDF fidelity fixes #807, #809, #819 shipped) |
| F Forms and JavaScript | 79 | 58 | 8 | 78.5% | 65% | 40–75 | Fill and author every AcroForm field type, Acrobat's AF functions in Acrobat's event order, sandboxed JavaScript (boa), data exchange, Fill & Sign; XFA static/dynamic layout, FormCalc and XFA data (partial). Missing: wider JavaScript object model, document actions, submit, debugger, barcode fields, XFA flattening and full dynamic fidelity |
| G Protect, redact, sanitize | 41 | 23 | 2 | 58.5% | 55% | 15–30 | Passwords and permissions, Remove security, redaction that removes glyphs, pixels, vectors, annotations and tags, with verification; word lists, patterns, FOIA/Privacy Act codes; sanitize. Missing: certificate security, pattern locales, custom code sets, partial-word redaction, folder redaction, protected view |
| H Digital signatures | 45 | 23 | 10 | 62.2% | 45% | 40–70 | PAdES B-B signing and validation (PKCS #12, macOS Keychain, Windows store with PIN prompts), certification, encrypted documents, certificate usage checks; B-T, LTV, OCSP/CRL with caller-supplied evidence. Missing: PKCS #11 and smart cards outside Windows, timestamp-server preferences, online revocation fetching, FieldMDP and field locking, OS trust store, EU Trusted Lists, compare signed version |
| I Scan and OCR | 26 | 5 | 2 | 23.1% | 15% | 40–75 | Searchable image (ocrs, Latin script without accents) on pages, ranges and many files. Missing: every other language (#744 Dutch; accents, CJK, Cyrillic, Arabic), editable-text output, deskew, rotation, despeckle, camera images beyond straightening (found or placed corners): orientation, clean-up, MRC compression, scanners |
| J Create and export | 34 | 12 | 3 | 39.7% | 25% | 55–100 | Create from images, multipage TIFF, text, clipboard, blank, many files at once; export PNG/JPEG/TIFF, text, RTF; Word and HTML partial. Missing: Office/HTML/web/PostScript to PDF, Excel and PowerPoint export, Word layout fidelity (#773), SVG/XML/EPS/PS/JPEG 2000 export, accessible text |
| K Optimize and standards | 58 | 15 | 10 | 34.5% | 20% | 65–115 | Reduce File Size and the Optimizer (images, discards, clean-up, space audit); PDF/A-2b/3b verify and convert (partial). Missing: Preflight (profiles, fixups, reports), PDF/A-1/4 and a/u levels, PDF/X, PDF/UA, PDF/E, PDF/VT, transparency flattening, font unembedding, monochrome JBIG2/CCITT |
| L Print | 39 | 15 | 1 | 39.7% | 35% | 30–55 | Acrobat's sizing, n-up, booklet, poster, comments & forms, preview, print-ready PDF, CUPS on macOS/Linux and the Windows spooler (#756). Missing: **printing on the web**, print as image, PostScript, all print-production tools (output preview, separations, ink manager, printer marks, colour conversion) |
| M Accessibility | 61 | 38 | 1 | 63.1% | 30% | 40–70 | Accessibility Checker (all 32 rules, report, fixes), alternate text, title and language. Missing: autotag, Tags/Order/Content panels, Reading Order tool, artifact marking, table editor, Read Out Loud, full keyboard operation of the app, screen-reader audit |
| N Automation, preferences, misc | 75 | 20 | 5 | 30.0% | 35% | 25–45 | CLI, MCP, UI control channel, 141 automation tools, Action Wizard (run, create), compare (text, visual, report). Missing: most Preferences pages, side-by-side compare, Action Wizard management, custom commands, AI providers, rich media/3D, hosted web app |
| **All** | **808** | **423** | **74** | **56.9%** | **≈ 49%** | **610–1,100** | Plus 175–325 h of cross-cutting work (dimension table) |

Shipped features rest on thin evidence: 141 of 423 cite exactly one test, and only a handful cite
an external oracle (`pdftotext`, `pdfsig`, OpenSSL, `qpdf --check`, a corpus).

The checklist lags reality in two places: `misc.localization` is still `planned` although 15
catalogs ship, and `misc.installers` is `planned` although signed macOS, Windows and Linux packages
ship (`.github/workflows/release.yml`). Neither moves the numbers by more than 0.2 points; fix them
with evidence when next touched.

## Stage

**alpha.** Ready for real work, ≈ 49%, is inside the 40–75% band, and every one of Acrobat Pro's
six everyday workflows can be completed end to end on macOS. Under the gate rule shared by all the
Crafting Apps, a workflow blocks only when a typical user can't complete it at all; lossy exchange
or a missing sub-case is a beta item. **Converting and sharing** is therefore partial, not
blocking: PDFs we save open everywhere, password-protected ones included since #836 (#774), and
export to Word, RTF, HTML, text and images works, but there is no in-app
Create PDF from Office, and Word export loses layout (#773). The gate table, with evidence, is in
[roadmap.md](roadmap.md#alpha-gate). (Earlier the same day this row was judged blocking and the
stage set to pre-alpha; see the revision history.)

| Core workflow | Works end to end? |
|---|---|
| View, search and print | yes |
| Organize, combine and split pages | yes |
| Comment and review | yes |
| Fill and sign forms | yes |
| Edit text and images | partial, not blocking (Latin text with embedded or standard fonts) |
| Convert and share (Office ↔ PDF, password protection) | partial, not blocking (Office→PDF and Word layout #773 are beta items; encryption interop #774 fixed) |

**To reach beta** (≈ 75% ready, no blocking gap in PDF interchange), ≈ 26 points and
**≈ 400–700 agent-hours**:

| Beta requirement | Hours |
|---|---|
| An interop suite that opens our outputs in other readers (encrypted output already opens in Acrobat, #774, #836; hours not re-estimated) | 8–15 |
| Rendering: a fidelity harness against Acrobat captures (local, clean-room) and fixing what it finds; settle the renderer (own M2 devices, or #841's proposal); Chinese UI faces in releases | 80–140 |
| Editing existing text robust on real files: subset fonts, CJK, RTL, rotated text | 70–120 |
| Printing on Windows and the web | 15–30 |
| OCR in the major languages (accents, Cyrillic, CJK), deskew and rotation | 35–60 |
| Export: Word that keeps layout; Excel and PowerPoint | 45–80 |
| Signatures: timestamp servers, online revocation and LTV, PKCS #11, OS trust | 30–55 |
| PDF/A (all parts and levels), PDF/UA validation, a first Preflight | 45–80 |
| Accessibility tagging: autotag, Tags panel, Reading Order | 35–60 |
| Open-issue backlog, stability and performance budgets | 40–70 |
| **Total** | **≈ 400–700** |

## Effort and calibration

**Calibrated against this repository's own history.**

- The repo is 11 days old (first commit 2026-09-30 05:17), with 591 commits and 371 merged pull
  requests (all since 2026-10-04). Rust in `crates/`, `apps/` and `xtask/` grew from 37.7k lines
  (2026-10-02) to 82.6k (10-04), 99.2k (10-08) and 152.7k (10-10).
- The previous ROADMAP measured about **1.0k kept, tested lines per agent-hour** (72k lines in
  roughly 65–75 agent-hours). New features land at about that rate: medium P1 features such as
  redaction word lists (#757, 314 lines), bookmarks from structure (#754, 588 lines) and signing
  encrypted documents (#753, 308 lines) each took about 1–3 agent-hours including tests, with 2–4 h
  from PR to merge, mostly CI. Large arcs take longer: XFA dynamic layout, its JavaScript and
  FormCalc (#121, #230, #301; ≈ 13k lines) about 15–25 agent-hours; the Arabic interface
  (#692, 2.7k lines) about 3–5.
- Hardening and fidelity work is 3–10× slower per line than new features: the 2026-10-07 → 10-10
  block landed ≈ 330 commits but moved the checklist by only 12 shipped features (411 → 423), because most of
  it was never-crash work, Windows fixes, localization and XFA.

The previous estimate (2026-10-07) was **600–1,100 h** to full parity. Since then XFA, signature
timestamps/LTV and signing encrypted documents progressed (≈ −60 h), but the first public releases
surfaced work the estimate did not hold: 245 open issues, missing Windows printing, Acrobat
interoperability of encrypted output, Chinese UI glyphs and Word-export layout (≈ +200–300 h).
Hence **≈ 780–1,400 h** now. Roughly 60–70% parallelizes across crates (3–5 agents: ≈ 300–550 h
wall clock).

**Needs a human:** the renderer decision (own M2 devices vs an outside renderer, #841); Acrobat
oracle captures on the owner's Mac (synthetic fixtures only); native-speaker review of every
catalog; smart cards and PKCS #11 tokens, scanners and Windows printers to test against; any
licensed OCR or AI model.

## Revision history

| Date | Change | Summary |
|---|---|---|
| 2026-10-11 | minor | Contributor fork: document-font selection and subset completion, CFF, style ranges, contextual/bidi save/reopen and all-page Chinese keyboard acceptance; curve/hole hit testing (shared clips stay fixed, as on main). Scope remains bounded; percentages unchanged |
| 2026-10-11 | minor | Synced with closed issues: encrypted output opens in Acrobat (#774, #836), Windows prints (#756, #847), column select (#740), 1:1 touchpad scrolling (#759), same-page multi-object move (#844), #825 and the #799–#821 fix batch. Text only: scores, readiness and hours not re-judged |
| 2026-10-10 | minor | Readiness table: hours to ≈ 95% per audience (full 780–1,400, mainstream 500–900, essentials 180–330). Full number restated as the standard's additive weighted sum over dimensions with written weights: 47% → 49%. Method aligned with the standard, no new evidence |
| 2026-10-10 | minor | Added the essentials-user score (≈ 66%): weighted depth of 13 everyday features, discounted for launch, discoverability and opening others' files |
| 2026-10-10 | minor | Consistency check across apps: re-judged the convert-and-share gate row with the shared rule (blocking only when the workflow can't be completed at all; lossy exchange and missing sub-cases are beta items). Encrypted output (#774) and Office→PDF are sub-cases, Word export is lossy not absent → partial, not blocking; stage pre-alpha → **alpha**. Numbers unchanged |
| 2026-10-10 | minor | Second look requested by the owner after practitioners praised PdfCraft: user sentiment gathered (stars, downloads, 23 praising issues, switching reports, issue themes); checklist split into mainstream (497) and specialist (311) features; the 9-point cross-cutting deduction removed as a double count (Windows printing, interop and glyphs were already scored in their areas). Ready for real work 40% → 47%; mainstream practitioner ≈ 55% added. Core-workflow alpha gate applied: convert and share fails → stage alpha → **pre-alpha**, ≈ 40–70 h from alpha |
| 2026-10-10 | major | Created from ROADMAP.md §Estimate summary and §Honest assessment (2026-10-05/07). Full re-measure against Acrobat Pro 26.002.21931: checklist recomputed (56.9% unweighted, ≈ 67% tier-weighted), ready for real work ≈ 40%, stage alpha, hours re-calibrated (780–1,400 h to parity, 400–700 h to beta), dimension and area tables |
| 2026-10-07 | minor | (in ROADMAP.md) 806 tracked features, 51.0% shipped, effort-weighted ≈ 30–35%, 600–1,100 h |
| 2026-10-05 | major | (in ROADMAP.md) First honest assessment by dimension and area |


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

