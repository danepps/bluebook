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

> **Note on signals.** Bluebook introductory signals (*See*, *See also*, *Cf.*, *But see*, etc.) are **not** produced by this style. They are inserted by a separate Zotero plug-in; keep that plug-in installed if you use signals.

---

## Install

### Zotero 6 / 7 (desktop)

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

If you care about knowing when to update, **Watch** this GitHub repo (top-right → *Watch → Custom → Releases*) — each notable change is tagged, and you'll get an email.

---

## How to enter items in Zotero

Bluebook requires different output for different kinds of sources. The style renders based on the Zotero **Item Type** and a few specific fields. Below is a type-by-type guide.

> **Convention:** *italic* = should appear italicized in output; SMALL CAPS = should appear in small caps.

### Journal article

| Zotero field | Example | Renders as |
| ------------ | ------- | ---------- |
| Item Type | `Journal Article` | |
| Author | `Jane Doe` | `Jane Doe` |
| Title | `Why the Bluebook` | *Why the Bluebook* |
| Publication | `Harvard Law Review` | Harv. L. Rev. (small caps, via Zotero's journal-abbreviation logic) |
| Volume | `137` | `137` |
| Pages | `101` | used as first page |
| Date | `2024` | `(2024)` |

**Typical output:** `Jane Doe, *Why the Bluebook*, 137 Harv. L. Rev. 101 (2024).`

### Forthcoming journal article

Use Item Type `Journal Article` exactly as above, **plus** add a `status` line to the **Extra** field:

```
status: forthcoming
```

Optionally fill in **URL** with the SSRN or repository link. The style will render:

`Jane Doe, *Why the Bluebook*, 137 Harv. L. Rev. (forthcoming 2027), https://papers.ssrn.com/...`

You can also write `status: accepted`, `status: in press`, etc. — whatever you type in `status` appears verbatim inside the parenthetical.

### Preprint / working paper

Use Item Type `Preprint` (which maps to CSL `article`):

| Field | Example |
| ----- | ------- |
| Author | `Jane Doe` |
| Title | `Draft Paper` |
| Repository (or Series) | `NBER Working Paper` |
| Archive ID (or Series Number) | `12345` |
| Date | `2025` |
| URL | SSRN/NBER link |

**Output:** `Jane Doe, *Draft Paper* (NBER Working Paper No. 12345, 2025), https://...`

> *Zotero fields:* "Repository" and "Archive ID" on a Preprint map to CSL `collection-title` and `collection-number`. The style automatically adds `No.` before the number.

### Preprint that has been accepted for publication

Preprint Item Type, plus `status: forthcoming` in Extra (and add the forthcoming journal in **Publication**):

`Jane Doe, *Draft Paper*, 138 Yale L.J. (forthcoming 2027), https://ssrn...`

### Newspaper article

Item Type `Newspaper Article`. The style switches form based on which fields you fill:

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

| Field | Notes |
| ----- | ----- |
| Website Title | *required* — renders as the italic/small-caps container name, e.g., *Divided Argument* |
| Title | the specific page/post title (italic) |
| URL | *required* |
| Date | publication date (optional) |
| Accessed | fill this to add `(last visited Mon. D, YYYY)` — **only** Webpages get "last visited" |

**Output with Accessed:** `Author, *Page Title*, *Website Title* (Jan. 27, 2025), https://... (last visited Apr. 10, 2026).`

### Blog post

Item Type `Blog Post` (CSL `post-weblog`). Like a webpage, but the style **does not** add "last visited" (blog posts carry their own publication date).

### Book

Item Type `Book`. Author and title render in **small caps** per Rule 15.

**Output:** `JANE DOE, THE TREATISE 101 (2024).`

### Book chapter / paper in a book

Item Type `Book Section` (Zotero) maps to CSL `chapter`.

**Output:** `Jane Doe, *Chapter Title*, in SOME EDITED VOLUME 101 (Bob Smith ed., 2024).`

### Legal case

Item Type `Case`.

| Field | Example |
| ----- | ------- |
| Case Name | `Brown v. Board of Education` |
| Reporter | `U.S.` |
| Reporter Volume | `347` |
| First Page | `483` |
| Court | (leave blank for U.S. Supreme Court; otherwise court name) |
| Date Decided | `1954` |

**First citation:** `Brown v. Board of Education, 347 U.S. 483 (1954).`

**Short-form citation** (Rule 10.9, used automatically on subsequent references): `*Brown*, 347 U.S. at 495.`

**Immediately-subsequent citation** renders as `*Id.* at 495.`

> Fill the **Short Title** field on the case (e.g., `Brown`) to control how the short name appears.

### Report (government, institutional, Rule 15)

Item Type `Report`. Publisher and title render in small caps.

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

The `key:` must be lowercase; the value can be anything.

---

## Subsequent-citation behavior

| Situation | Output |
| --------- | ------ |
| Immediately after the same source | `*Id.*` (or `*Id.* at 495` with a pincite) |
| Later reference to a non-case | `AUTHOR, supra note N, at X` |
| Later reference to a case | `*Brown*, 347 U.S. at 495` |
| 5 or more authors | `First Author et al.` |

The 5-author threshold is an intentional deviation from Bluebook Rule 15.1/16.1 (which uses 3). This is a personal preference of the author.

---

## Known limitations

- **No auto-update.** Zotero only auto-updates styles from its official repository. Reinstall manually when new versions ship (see above).
- **No introductory signals.** *See*, *Cf.*, *But see*, etc. are produced by a separate Zotero plug-in, not this style.
- **Limited statute / regulation coverage.** The style is primarily tuned for cases, books, journal articles, working papers, and internet sources.
- **Bibliography rendering is approximate.** The style targets law-review footnotes (note-style). If you ask Zotero to build a bibliography/works-cited list, it will produce something reasonable but not a Bluebook Table of Authorities.

---

## Feedback / bug reports

Open an issue: <https://github.com/danepps/bluebook/issues>

When reporting a bad render, paste the output you got, the output you expected, and (if possible) a screenshot of the Zotero item so the fields can be verified.

---

## Credits

- Original Bluebook CSL by **Bruce D'Arcus** and **Nancy Sims**, with contributions from **Patrick O'Brien**.
- Modifications for this fork by **Dan Epps** (<epps@wustl.edu>).
- Licensed under [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/).
