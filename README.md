# Bluebook Style — Epps Version

A [Bluebook](https://www.legalbluebook.com/) legal-citation style for [Zotero](https://www.zotero.org/), adapted by **Prof. Daniel Epps** (Washington University School of Law) from the community Bluebook CSL style.

This page is also published at **<https://danepps.github.io/bluebook/>**.

---

## What you get

Two versions of the style:

| Style | File | Install URL |
| ----- | ---- | ----------- |
| **Main** (stable) | `BluebookDSEStyle.csl` | <https://danepps.github.io/bluebook/BluebookDSEStyle.csl> |
| **Experimental** (work-in-progress fixes) | `BluebookDSEStyle-Experimental.csl` | <https://danepps.github.io/bluebook/BluebookDSEStyle-Experimental.csl> |

Both can live side-by-side in Zotero — they have distinct titles.

> **Note on signals.** Bluebook introductory signals (*See*, *See also*, *Cf.*, *But see*, etc.) are **not** produced by this style. They are inserted by a companion Zotero plug-in: **[danepps/zotero](https://github.com/danepps/zotero)** — install that alongside this style if you use signals.

---

## Install

### Zotero (desktop)

Works with Zotero 7 and Zotero 8. (On Zotero 6 the style mostly works, but the **Preprint** item type doesn't exist — see the Preprint section below for the workaround.)

1. Open **Preferences → Cite → Styles**.
2. Click the **+** button in the lower left.
3. In the file picker, paste one of the install URLs above into the filename field and press Enter.
   - *Alternative:* download the `.csl` file to your desktop first (right-click the install URL → "Save Link As") and select it in the picker.
4. The new style appears in the list. Select it whenever you create a bibliography or insert citations.

### Word / Google Docs

The Zotero plug-ins for Word, LibreOffice, and Google Docs pick up the style automatically — once installed in Zotero, choose it from the document-preferences dropdown.

---

## Updating

Zotero only auto-updates styles installed from the [official CSL repository](https://www.zotero.org/styles). This style is not there — so updates are **manual**:

1. **Preferences → Cite → Styles.**
2. Select the existing "Bluebook Style — Epps Version" (or "…Experimental") entry and click **−** to remove it.
3. Re-install from the URL above.

If you care about knowing when to update, go to the [GitHub repository](https://github.com/danepps/bluebook) and **Watch** it (top-right of that page → *Watch → Custom → Releases*). Each notable change is tagged, and you'll get an email.

---

## How the style works (things everyone should know)

A few principles that apply across every item type. Read these once — they'll explain most "why is it doing that?" questions.

- **No trailing period.** Output ends without a final period. In a footnote, type the period yourself; inline, let the surrounding sentence punctuate. This is deliberate — law-review footnotes often chain multiple citations with semicolons, and the sentence-ending period belongs to the footnote, not to any single citation.
- **Note-style, footnote-oriented.** The style is built for law-review footnote citations, not inline author-date parentheticals. Insert citations with Zotero's "Insert Footnote" (in Word) or equivalent.
- **Italics and small caps are rich-text formatting.** The style emits *italic* / SMALL CAPS as styled-text attributes. Word, LibreOffice, Google Docs, and Pages render them correctly. Plain-text contexts (Markdown, terminal, some email clients) will show unformatted text.
- **Short forms are automatic, based on citation position.** The style looks at whether a citation is first or subsequent:
  - Same source immediately prior → `*Id.*` (with pincite: `*Id.* at 495`)
  - Later reference to a non-case → `AUTHOR, *supra* note N, at X`
  - Later reference to a case → Rule 10.9 short form: `*Brown*, 347 U.S. at 495`
- **The style renders what's in the data — it doesn't look anything up.** If an output is wrong, check the Zotero fields on the item first. The style doesn't validate that `347 U.S. 483` exists or that a journal volume makes sense — it simply formats whatever you typed.
- **Journal abbreviations come from each item's `Journal Abbr` field.** The style reads the Bluebook-style abbreviation directly from the **Journal Abbr** field on the Zotero item (e.g., `Harv. L. Rev.`, `Yale L.J.`, `Stan. L. Rev.`). You must fill this in on every journal article when you create the item — there is no central list, and the style does not compute it from the full journal name. **Do not enable Zotero's MEDLINE abbreviation setting** (Preferences → Cite) — MEDLINE uses a different abbreviation scheme (biomedical, no periods) that is not Bluebook-compliant.
- **Signals are handled by a separate plug-in.** *See*, *See also*, *Cf.*, *But see*, *Contra*, etc. are inserted by **[danepps/zotero](https://github.com/danepps/zotero)** — install that alongside this style if you cite with signals. You **can** type signals manually into the footnote text (or into Zotero's **Prefix** field) instead of using the plug-in, but there's a catch: Bluebook wants `id.` lowercase when it follows a signal (`See id.` at 5, not `See Id.` at 5). The style only knows to drop the capital when the signal is supplied through the plug-in or the Prefix field — a signal you type directly into the Word document leaves the style thinking `Id.` starts a new sentence, and it will be capitalized. Using the plug-in (or, failing that, the Prefix field) is the only way to get signal-then-`id.` rendered correctly.
- **Short Title controls the short form.** For books, articles, and cases, the Zotero **Short Title** field (or the CSL `title-short` variable) determines how the shortened name appears in subsequent citations. Fill it in for cleaner *supra* and short-form cites.
- **Explanatory parentheticals go in manually, per cite.** Bluebook often wants a parenthetical after a source (e.g., `(holding that ...)`, `(noting that ...)`, `(per curiam)`). This style doesn't generate those — add them by hand using Zotero's "Suffix" field in the Add/Edit Citation dialog. In a **string cite where each source has its own parenthetical**, it's easiest to insert each source as its own separate citation rather than combining them into one multi-source cite — that way each source gets its own suffix, and semicolons and signals are easier to control.

### Changes from the base CSL Bluebook style

These aren't disagreements with the Bluebook — they're tweaks to the underlying CSL to make it render more cleanly in practice.

- **No trailing period.** The base style emits a period at the end of each citation. That interferes with chained footnote cites (where multiple sources are joined with semicolons, and the period belongs to the footnote sentence, not to any single cite). This style drops the trailing period and expects you to add it in context.
- **`et al.` at 5 authors**, not 3. A personal preference of the author — the 3-author threshold produces a lot of `X et al.` in footnotes where spelling out all three would read better.

---

## How to enter items in Zotero

Bluebook requires different output for different kinds of sources. The style renders based on the Zotero **Item Type** and a few specific fields. Below is a type-by-type guide.

> **Conventions in the tables below:**
> - *italic* = should appear italicized in output; SMALL CAPS = should appear in small caps.
> - 🔴 = **required** for a correct citation — leave it blank and the output will be broken or missing a piece.
> - ⚪ = **optional** — the field adds detail or triggers an alternate rendering, but can be left blank.

### Journal article

| | Zotero field | Example | Renders as |
| - | ------------ | ------- | ---------- |
| | Item Type | `Journal Article` | |
| 🔴 | Author | `Jane Doe` | `Jane Doe` |
| 🔴 | Title | `Why the Bluebook` | *Why the Bluebook* |
| 🔴 | Publication | `Harvard Law Review` | (full name — used as a fallback if Journal Abbr is blank) |
| 🔴 | Journal Abbr | `Harv. L. Rev.` | Harv. L. Rev. (small caps) |
| 🔴 | Volume | `137` | `137` |
| 🔴 | Pages | `101` | used as first page |
| 🔴 | Date | `2024` | `(2024)` |

**Typical output:** `Jane Doe, *Why the Bluebook*, 137 Harv. L. Rev. 101 (2024).`

### Forthcoming journal article

Use Item Type `Journal Article` exactly as above, **plus** add a `status` line to the **Extra** field:

```
status: forthcoming
```

🔴 The `status:` line is what triggers the forthcoming rendering. ⚪ Fill in **URL** with the SSRN or repository link — it will now be rendered (URLs are otherwise suppressed for normal journal articles). Volume and Pages become optional in this mode. The style will render:

`Jane Doe, *Why the Bluebook*, 137 Harv. L. Rev. (forthcoming 2027), https://papers.ssrn.com/...`

You can also write `status: accepted`, `status: in press`, etc. — whatever you type in `status` appears verbatim inside the parenthetical.

### Preprint / working paper

Use Item Type `Preprint` (which maps to CSL `article`). Preprint was introduced in **Zotero 7** and is present in Zotero 8; on Zotero 6 it doesn't exist — use `Document` or `Report` instead and expect rougher output.

| | Field | Example |
| - | ----- | ------- |
| 🔴 | Author | `Jane Doe` |
| 🔴 | Title | `Draft Paper` |
| 🔴 | **Series** | `NBER Working Paper` |
| 🔴 | **Series Number** | `12345` |
| 🔴 | Date | `2025` |
| ⚪ | URL | SSRN/NBER link |

**Output:** `Jane Doe, *Draft Paper* (NBER Working Paper No. 12345, 2025), https://...`

> *Zotero fields:* use **Series** and **Series Number** (which map to CSL `collection-title` / `collection-number`) — *not* "Repository" / "Archive ID", which map elsewhere. The style automatically inserts `No.` before the number.

> **Not sure which type to use for a draft?** If the paper has been placed with a journal (even just accepted), use **Journal Article** with `status: forthcoming` (see the *Forthcoming journal article* section above). Use **Preprint** only for pure working papers that aren't tied to an upcoming journal issue — NBER series papers, unplaced drafts, etc.

### Newspaper article

Item Type `Newspaper Article`. 🔴 Required: Author, Title, Publication, Date. The style switches form based on whether Pages and/or URL are filled:

| Has Pages? | Has URL? | Output |
| ---------- | -------- | ------ |
| Yes | No | `Author, *Title*, Paper, Date, at A1.` |
| No | Yes | `Author, *Title*, Paper (Date), https://...` |
| Yes | Yes | `Author, *Title*, Paper, Date, at A1, https://...` |
| No | No | `Author, *Title*, Paper, Date.` |

### Magazine article

Same rules as newspaper (Item Type `Magazine Article`).

### Webpage

Item Type `Web Page`.

| | Field | Notes |
| - | ----- | ----- |
| 🔴 | Website Title | renders as the italic container name, e.g., *Divided Argument* |
| 🔴 | Title | the specific page/post title (italic) |
| 🔴 | URL | the page's address |
| ⚪ | Date | publication date |
| ⚪ | Accessed | fill this to add `(last visited Mon. D, YYYY)` — **only** Webpages get "last visited" |

**Output with Accessed:** `Author, *Page Title*, *Website Title* (Jan. 27, 2025), https://... (last visited Apr. 10, 2026).`

### Blog post

Item Type `Blog Post` (CSL `post-weblog`). Like a webpage, but the style **does not** add "last visited" (blog posts carry their own publication date). 🔴 Required: Author, Title, Blog Title, URL, Date.

### Book

Item Type `Book`. Author and title render in **small caps** per Rule 15. 🔴 Required: Author, Title, Date. ⚪ Edition, Editor/Translator (added to parenthetical if present).

**Output:** `JANE DOE, THE TREATISE 101 (2024).`

### Book chapter / paper in a book

Item Type `Book Section` (Zotero) maps to CSL `chapter`. 🔴 Required: Author, Title (chapter), Book Title, Date. ⚪ Editor (adds the `ed.` parenthetical).

**Output:** `Jane Doe, *Chapter Title*, in SOME EDITED VOLUME 101 (Bob Smith ed., 2024).`

### Legal case

Item Type `Case`.

| | Field | Example |
| - | ----- | ------- |
| 🔴 | Case Name | `Brown v. Board of Education` |
| 🔴 | Reporter | `U.S.` |
| 🔴 | Reporter Volume | `347` |
| 🔴 | First Page | `483` |
| ⚪ | Court | (leave blank for U.S. Supreme Court; otherwise court name) |
| 🔴 | Date Decided | `1954` |

**First citation:** `Brown v. Board of Education, 347 U.S. 483 (1954).`

**Short-form citation** (Rule 10.9, used automatically on subsequent references): `*Brown*, 347 U.S. at 495.`

**Immediately-subsequent citation** renders as `*Id.* at 495.`

> Fill the **Short Title** field on the case (e.g., `Brown`) to control how the short name appears.

### Report (government, institutional, Rule 15)

Item Type `Report`. 🔴 Required: Institution, Title, Date. ⚪ Report Number. (The **Institution** field is Zotero's label for the publisher on this type.) Institution and title render in small caps.

`U.S. DEP'T OF JUSTICE, ANNUAL REPORT 12 (2024).`

### Statute / bill / regulation

These use Zotero's `Statute` / `Bill` / `Regulation` item types. They're currently passed through generic rendering — heavy statute users should double-check output; open an issue if a specific format is off.

---

## The Extra field: cheat sheet

Zotero's **Extra** field lets you override or add CSL variables that aren't in the normal Zotero form. Use `key: value`, one per line.

| Line in Extra | What it does |
| ------------- | ------------ |
| `status: forthcoming` | Renders `(forthcoming YYYY)` on journal articles and preprints; also enables URL rendering |
| `status: accepted` | Same mechanism, different word |
| `event-title: ...` | Override conference/event title |
| `number-of-pages: ...` | For books |

Lowercase keys are the convention; Zotero's parser is actually case-insensitive, so `Status: forthcoming` works too. Whitespace around the colon is tolerated.

---

## Subsequent-citation behavior

| Situation | Output |
| --------- | ------ |
| Immediately after the same source | `*Id.*` (or `*Id.* at 495` with a pincite) |
| Later reference to a non-case | `AUTHOR, supra note N, at X` |
| Later reference to a case | `*Brown*, 347 U.S. at 495` |
| 5 or more authors | `First Author et al.` |

---

## Known limitations

- **No auto-update.** Zotero only auto-updates styles from its official repository. Reinstall manually when new versions ship (see above).
- **No introductory signals.** *See*, *Cf.*, *But see*, etc. are produced by a separate Zotero plug-in, not this style.
- **Limited statute / regulation coverage.** The style is primarily tuned for cases, books, journal articles, working papers, and internet sources.
- **Bibliography rendering is approximate.** The style targets law-review footnotes (note-style). If you ask Zotero to build a bibliography/works-cited list, it will produce something reasonable but not a Bluebook Table of Authorities.
- **No `[hereinafter shortname]` support.** Bluebook lets authors coin a custom short form on first citation (e.g., `[hereinafter Reimagining]`) and then use that short form on every subsequent cite. CSL has no native concept of author-defined short forms, so the style can't generate the `[hereinafter …]` marker or honor it on subsequent cites.
- **Can't detect "volume number is a year."** When a journal's volume *is* a year (e.g., `2024 Wis. L. Rev. 501`), Bluebook suppresses the redundant trailing `(2024)`. This style renders both (`2024 Wis. L. Rev. 501 (2024)`), because CSL can't introspect the volume to tell whether it looks like a year.
- **Can't detect "title ends in a numeral."** When a book or report title ends in a number (e.g., *Article III* at 45), Bluebook requires the pincite be written `, at 45` to avoid running the two numbers together. This style just emits the page number, so you may get ambiguous output like `ARTICLE III 45`.

> **Coming later.** Several of these gaps (hereinafter, volume-as-year, title-ends-in-numeral) are on the roadmap for the companion Zotero plug-in — see **[danepps/zotero](https://github.com/danepps/zotero)**. The plug-in can introspect the data and post-process citation output in ways that a pure CSL file cannot.

---

## Feedback / bug reports

Open an issue: <https://github.com/danepps/bluebook/issues>

When reporting a bad render, paste the output you got, the output you expected, and (if possible) a screenshot of the Zotero item so the fields can be verified.

---

## Credits

- Original Bluebook CSL by **Bruce D'Arcus** and **Nancy Sims**, with contributions from **Patrick O'Brien**.
- Modifications for this fork by **Dan Epps** (<epps@wustl.edu>).
- Licensed under [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/).
