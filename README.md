# Bluebook Style — Epps Version

A [Bluebook](https://www.legalbluebook.com/) legal-citation style for [Zotero](https://www.zotero.org/), adapted by **Prof. Daniel Epps** (Washington University School of Law) from the community Bluebook CSL style. (The file is a standard CSL 1.0 style, so it also works in other CSL-compatible processors like Pandoc or Mendeley — but Zotero is the intended and primary target, and the rest of this guide assumes Zotero.)

> **Style last updated: May 31, 2026.** If you installed this style previously, see [Updating](#updating) below to get the latest version.

---

## What you get

One CSL style file, installable in Zotero:

| Style | File | Install URL |
| ----- | ---- | ----------- |
| **Bluebook Style — Epps Version** | `BluebookDSEStyle.csl` | <https://danepps.github.io/bluebook/BluebookDSEStyle.csl> |

> **Note on signals.** Bluebook introductory signals (*See*, *See also*, *Cf.*, *But see*, etc.) are **not** produced by this style. They are inserted by a companion Zotero plug-in: **[danepps/zotero](https://github.com/danepps/zotero)** — install that alongside this style if you use signals.

---

## Install

### New to Zotero?

[Zotero](https://www.zotero.org/) is a free, open-source reference manager: it stores your sources (cases, articles, books, websites) in a personal library and lets you insert properly-formatted citations and bibliographies into Word, LibreOffice, or Google Docs at the click of a button. Most academic writers in law and the humanities use Zotero (or one of its commercial cousins like EndNote), and the Bluebook citation style this repo distributes plugs into Zotero to produce footnote-ready Bluebook cites.

If you don't have Zotero yet:

1. **Download Zotero** from <https://www.zotero.org/download/>. The desktop app is the main piece — install it for your operating system.
2. **Install the browser connector** (also linked from that page) — a small browser extension that grabs source metadata from Westlaw, Lexis, SSRN, journal sites, etc., and saves it into your Zotero library with one click.
3. **The Word / LibreOffice plug-in is bundled** with the Zotero installer and gets set up automatically the first time you launch Zotero. (For Google Docs, the browser connector handles citation insertion.)
4. Spend a few minutes with [Zotero's Quick Start Guide](https://www.zotero.org/support/quick_start_guide) — it covers adding sources, organizing them in collections, and inserting cites. Then come back here to install this Bluebook style.

### Zotero (desktop)

Works with Zotero 7 through 10. (On Zotero 6 the style mostly works, but the **Preprint** item type doesn't exist — see the Preprint section below for the workaround.)

1. Open **Preferences → Cite → Styles**.
2. Click the **+** button in the lower left.
3. In the file picker, paste one of the install URLs above into the filename field and press Enter.
   - *Alternative:* download the `.csl` file to your desktop first (right-click the install URL → "Save Link As") and select it in the picker.
4. The new style appears in the list. Select it whenever you create a bibliography or insert citations.

### Word / Google Docs

The Zotero plug-ins for Word, LibreOffice, and Google Docs pick up the style automatically — once installed in Zotero, choose it from the document-preferences dropdown. **Zotero must be running** in the background while you're inserting or editing citations from Word/Docs/LibreOffice; if Zotero is closed, the plug-in buttons do nothing.

> **Long articles: turn off automatic updating.** In the same **Document Preferences** dialog where you pick this style, un-check **"Automatically update citations"** when you're working on a large document. A full law-review article with hundreds of footnotes gets sluggish if Zotero re-renders every cite on each edit. With it off, citations that need updating are flagged, and you update them all at once with Zotero's **Refresh** button. **Refresh before you finalize** — this style's Rule 10.9 five-footnote short-/full-form logic settles only on a refresh, so a manual refresh at the end makes sure case cites resolve correctly.

---

## Updating

Zotero only auto-updates styles installed from the [official CSL repository](https://www.zotero.org/styles). This style isn't there, so you update it yourself — but **you don't need to remove the old copy first.** Just install the new version on top of it: Zotero recognizes that it's the same style and replaces your existing copy.

To update:

1. **Download** the latest `.csl` file (right-click the install URL above → "Save Link As").
2. Install it, either way works:
   - **Double-click** the downloaded file — Zotero opens and offers to install it; or
   - In Zotero, open **Preferences → Cite → Styles**, click **+**, and select the downloaded file.
3. Zotero detects the existing style and asks to **replace** it. Confirm, and you're on the latest version.

If you care about knowing when to update, go to the [GitHub repository](https://github.com/danepps/bluebook) and **Watch** it (top-right of that page → *Watch → Custom → Releases*). Each notable change is tagged, and you'll get an email.

See what changed between versions in the [commit history](https://github.com/danepps/bluebook/commits/main) or on the [Releases page](https://github.com/danepps/bluebook/releases).

> **Early adopter migration note.** If you installed an old version of this style from the `raw.githubusercontent.com` URL (before the move to the GitHub Pages URL), your installed copy has a different internal `<id>` than the current file. Zotero won't recognize the new file as the same style, so installing on top produces a generic "unexpected error." This is the **one case where you do need to remove first**: in **Preferences → Cite → Styles**, select the existing "Bluebook Style — Epps Version" entry, click **−** to delete it, then install the new file. One-time only — after that, the normal replace-in-place update above works for every future version.

---

## How the style works (things everyone should know)

A few principles that apply across every item type. Read these once — they'll explain most "why is it doing that?" questions.

- **No trailing period.** Output ends without a final period. In a footnote, type the period yourself; inline, let the surrounding sentence punctuate. This is a deliberate change Prof. Epps made to the base Bluebook CSL style — chiefly to make it easy to type an explanatory parenthetical right after the citation (`Brown v. Bd. of Educ., 347 U.S. 483 (1954) (holding that ...)`) without having to delete an auto-inserted period first. It also keeps things clean when law-review footnotes chain multiple citations with semicolons — the sentence-ending period belongs to the footnote, not to any single citation.
- **Note-style, footnote-oriented.** The style is built for law-review footnote citations, not inline author-date parentheticals. Insert citations with Zotero's "Insert Footnote" (in Word) or equivalent.
- **Italics and small caps are rich-text formatting.** The style emits *italic* / SMALL CAPS as styled-text attributes. Word, LibreOffice, Google Docs, and Pages render them correctly. Plain-text contexts (Markdown, terminal, some email clients) will show unformatted text.
- **Short forms are automatic, based on citation position.** The style looks at whether a citation is first or subsequent:
  - Same source immediately prior → `*Id.*` (with pincite: `*Id.* at 495`)
  - Later reference to a non-case → `AUTHOR, *supra* note N, at X`
  - Later reference to a case, **within five footnotes** (Rule 10.9) → short form: `*Brown*, 347 U.S. at 495`
  - Later reference to a case **more than five footnotes back** → reverts to the full cite: `Brown v. Board of Education, 347 U.S. 483, 495 (1954)`
- **The style renders what's in the data — it doesn't look anything up.** If an output is wrong, check the Zotero fields on the item first. The style doesn't validate that `347 U.S. 483` exists or that a journal volume makes sense — it simply formats whatever you typed.
- **Journal abbreviations come from each item's `Journal Abbr` field.** The style reads the Bluebook-style abbreviation directly from the **Journal Abbr** field on the Zotero item (e.g., `Harv. L. Rev.`, `Yale L.J.`, `Stan. L. Rev.`). You must fill this in on every journal article when you create the item — there is no central list, and the style does not compute it from the full journal name. **Do not enable Zotero's MEDLINE abbreviation setting** (Preferences → Cite) — MEDLINE uses a different abbreviation scheme (biomedical, no periods) that is not Bluebook-compliant.
- **Signals are handled by a separate plug-in.** *See*, *See also*, *Cf.*, *But see*, *Contra*, etc. are inserted by **[danepps/zotero](https://github.com/danepps/zotero)** — install that alongside this style if you cite with signals. You **can** type signals manually into the footnote text (or into Zotero's **Prefix** field) instead of using the plug-in, but there's a catch: Bluebook wants `id.` lowercase when it follows a signal (`See id.` at 5, not `See Id.` at 5). The style only knows to drop the capital when the signal is supplied through the plug-in or the Prefix field — a signal you type directly into the Word document leaves the style thinking `Id.` starts a new sentence, and it will be capitalized. Using the plug-in (or, failing that, the Prefix field) is the only way to get signal-then-`id.` rendered correctly.
- **Short Title controls the short form.** For books, articles, and cases, the Zotero **Short Title** field (or the CSL `title-short` variable) determines how the shortened name appears in subsequent citations. Fill it in for cleaner *supra* and short-form cites.
- **Explanatory parentheticals go in manually, per cite.** Bluebook often wants a parenthetical after a source (e.g., `(holding that ...)`, `(noting that ...)`, `(per curiam)`). This style doesn't generate those — type them by hand directly into the footnote text, after the citation, rather than trying to stuff them into Zotero's Suffix field. In a **string cite where each source has its own parenthetical**, it's easiest to insert each source as its own separate citation rather than combining them into one multi-source cite — that way you can type each parenthetical between the inserted cites, and semicolons and signals stay easy to control.

### Changes from the base CSL Bluebook style

These aren't disagreements with the Bluebook — they're tweaks to the underlying CSL to make it render more cleanly in practice.

- **No trailing period.** The base style emits a period at the end of each citation; this style drops it. Rationale and downstream effects are covered in [How the style works](#how-the-style-works-things-everyone-should-know) above — short version: it lets you type explanatory parentheticals immediately after the cite without first having to delete an auto-period, and it keeps semicolon-chained footnote cites clean.
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

**Pincites on forthcoming articles render as `(manuscript at N)`.** Because the journal's printed pagination doesn't exist yet, the pincite refers to the page of the draft manuscript instead of the (nonexistent) journal page. The style emits this automatically — you just enter the pincite as the citation locator the same way you would for any other source. Example with a pincite:

`Jane Doe, *Why the Bluebook*, 137 Harv. L. Rev. (forthcoming 2027) (manuscript at 12), https://papers.ssrn.com/...`

Subsequent (`supra`) cites of a forthcoming article use the same form: `Doe, *supra* note 3 (manuscript at 12)` rather than `Doe, *supra* note 3, at 12`. As soon as the article is no longer forthcoming, remove the `status:` line from Extra and pincites revert to ordinary `at N` rendering.

### Student note, comment, or other designated article type

Some journal articles carry a designation — *Note*, *Comment*, *Recent Development*, *Essay*, etc. — that Bluebook requires between the author and the title. Add it via the **Extra** field:

```
genre: Note
```

The style inserts it automatically and title-cases it regardless of how you type it (`note`, `NOTE`, and `Note` all render as `Note`).

**Typical output:** `Jane Doe, Note, *The Fourth Amendment's Third Way*, 120 Harv. L. Rev. 1627 (2007).`

For **anonymous** student notes (no author listed), leave the Author field blank and set `genre: Note`. The short-cite form will use the italicized short title as the supra anchor — fill in Zotero's **Short Title** field if you want a trimmed version:

- First cite: `Note, *The Fourth Amendment's Third Way*, 120 Harv. L. Rev. 1627 (2007).`
- Short cite: *The Fourth Amendment's Third Way*, supra note 3, at 1630.

### Working paper (Bluebook Rule 17.4)

For a paper formally part of a numbered working-paper series — NBER, Columbia Public Law, university working-paper series, etc. Use Item Type `Preprint` (CSL `article`). Preprint was introduced in **Zotero 7** and is present in Zotero 8; on Zotero 6 it doesn't exist — use the workflow-by-overrides note at the bottom of this section.

**Recommended fields:**

| | Field | Example |
| - | ----- | ------- |
| 🔴 | Author | `Alan J. Auerbach` |
| 🔴 | Title | `National Savings, Economic Welfare…` |
| 🔴 | **Repository** | `Nat'l Bureau of Econ. Rsch.` (the sponsoring institution) |
| 🔴 | **Genre** | `Working Paper` (or `Discussion Paper`, `NBER Working Paper`, etc.) |
| 🔴 | **Series Number** | `729` |
| 🔴 | Date | `1981` |
| ⚪ | URL | SSRN/NBER link |

**Output:** `Alan J. Auerbach, *National Savings…* (Nat'l Bureau of Econ. Rsch., Working Paper No. 729, 1981), https://...`

**Trigger:** Series Number is the signal that says "this is a numbered working paper, render it under Rule 17.4." Without a Series Number, the style falls back to the unpublished-manuscript form (Rule 17.2.1) — at which point you should usually switch to the **Manuscript** item type instead (see *Unpublished manuscript* below).

**Field fallbacks** (for when your Zotero version, translator, or muscle memory landed the data in a different field, the style reads each slot through a priority chain):

| Slot | Priority chain |
| ---- | -------------- |
| Sponsoring org | `publisher` (via Extra: `publisher: NBER`) → **Repository** → **Series** *(only when Genre is also set, so Series isn't doing double duty)* |
| Descriptor (e.g., "Working Paper") | **Genre** → **Series** *(when Genre is empty)* |
| Paper number | `number` (via Extra: `number: 729`) → **Series Number** |

So if you populate Genre + Series + Series Number (Repository empty), the style still produces `(Series, Genre No. Number, Year)` — Series fills the sponsor slot because Genre is occupying the descriptor. Only when both Genre and Repository are empty does Series collapse back to descriptor duty.

> **Zotero 6 workaround.** If you're on a version without the Preprint type, use Item Type `Document` and put `publisher: <sponsor>`, `genre: Working Paper`, and `number: <N>` in the Extra field. Output is the same.

> **Not sure which type to use for a draft?**
> - Paper *placed with a journal* (even just accepted)? → **Journal Article** with `status: forthcoming` (see *Forthcoming journal article* above).
> - Paper *part of a numbered working-paper series* (NBER WP No. 729, etc.)? → **Preprint**, this section.
> - Bare unpublished draft, on SSRN or in a drawer, no series, no journal? → **Manuscript**, see next section.

### Unpublished manuscript (Bluebook Rule 17.2.1)

For unpublished work that isn't part of a numbered series and isn't placed with a journal — bare SSRN drafts, in-progress papers, student notes/comments not selected for publication, conference drafts on file with the author. Item Type `Manuscript`. Renders in **roman type** (no italics, no small-caps) per Rule 17.2.

| | Field | Example |
| - | ----- | ------- |
| 🔴 | Item Type | `Manuscript` |
| 🔴 | Author | `Anatoliy Bizhko` |
| 🔴 | Title | `Capitalism and Democracy` |
| 🔴 | Date | `2000-02-29` (most precise writing date available) |
| ⚪ | **Manuscript Type** | `comment`, `note`, `dissertation`, etc. — defaults to `manuscript` |
| ⚪ | **Archive** | location string — `author`, `the University of Pennsylvania Journal of Labor and Employment Law`, etc. (just the location, the style adds `on file with`) |
| ⚪ | URL | SSRN/repository link |

**Output:** `Anatoliy Bizhko, Capitalism and Democracy 25 (Feb. 29, 2000) (unpublished manuscript) (on file with author).`

**With a Manuscript Type set:** `Victoria E. Anderson, Company Outing… 12 (Mar. 15, 2004) (unpublished comment) (on file with the University of Pennsylvania Journal of Labor and Employment Law).`

**With a URL (SSRN draft):** `Jane Doe, Some Paper Title 12 (Mar. 15, 2024) (unpublished manuscript), https://ssrn.com/abstract=12345.`

> **Genre / Manuscript Type renders lowercased** to match Bluebook examples — `(unpublished comment)`, not `(unpublished Comment)`. So `comment`, `Comment`, and `COMMENT` all produce the same output.

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

### Podcast (Bluebook Rule 18.8.1(c))

Item Type `Podcast`. The podcast/show name renders in small caps, followed by a colon and the italic episode title, with the streaming service and date in a trailing parenthetical.

| | Field | Example | Renders as |
| - | ----- | ------- | ---------- |
| | Item Type | `Podcast` | |
| 🔴 | **Podcaster** | `Digging a Hole: The Legal Theory Podcast` (enter as a *single-field* name — click the icon to switch from two-field, or the show name will be split into first/last) | DIGGING A HOLE: THE LEGAL THEORY PODCAST (small caps) |
| 🔴 | Title | `John Goldberg and Benjamin Zipursky` | *John Goldberg and Benjamin Zipursky* |
| 🔴 | **Publisher** | `Apple Podcasts` | `(Apple Podcasts, …)` — the streaming service |
| 🔴 | Date | `11/24/2026` | `Nov. 24, 2026` |
| ⚪ | URL | `https://...` | appended after the parenthetical |
| ⚪ | Accessed | only fill if Date is unknown | renders in place of Date — Rule 18.8.1(c) allows "last streamed" when release date is unavailable |

**Output:** `DIGGING A HOLE: THE LEGAL THEORY PODCAST: *John Goldberg and Benjamin Zipursky* (Apple Podcasts, Nov. 24, 2026), https://www.diggingaholepodcast.com/episodes/episode-09-goldberg-zipursky`

**Time-marker pincites** (`, at 12:34`) come from Zotero's citation **Locator** at insert time — leave the Locator label set to its default and type the time in the locator field. The style emits `, at <locator>` between the episode title and the parenthetical.

> **Series Title also works** as a fallback if you prefer to keep the show name out of the Podcaster (creator) field — the style falls back from Podcaster (CSL `host`) to Series Title (CSL `collection-title`) when Podcaster is blank.

### Book

Item Type `Book`. Author and title render in **small caps** per Rule 15. 🔴 Required: Author, Title, Date. ⚪ Edition, Editor/Translator (added to parenthetical if present).

**Output:** `JANE DOE, THE TREATISE 101 (2024).`

> **Edition field — type just the ordinal, not the word `ed.`** The style supplies `ed.` automatically, so put **`3d`**, **`4th`**, **`2d`**, etc. in Zotero's Edition field — not `3d ed.` (which would render `3d ed. ed.`). For a revised edition, type just **`rev.`** (renders `(rev. ed. 2024)`). Examples:
>
> | Edition field value | Output |
> | --- | --- |
> | `3d` | `JANE DOE, THE TREATISE 101 (3d ed. 2024).` |
> | `4th` | `JANE DOE, THE TREATISE 101 (4th ed. 2024).` |
> | `rev.` | `JANE DOE, THE TREATISE 101 (rev. ed. 2024).` |

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

> **Rule 10.9's five-footnote rule now works.** Bluebook's Rule 10.9 — use a short form only if the full cite appears in the same footnote or one of the preceding five footnotes, otherwise re-cite in full — is applied automatically. The style short-forms a subsequent case cite only when the prior cite is within five footnotes; beyond that window it reverts to the full cite (`Brown v. Board of Education, 347 U.S. 483 (1954)`). This relies on Zotero's footnote-distance tracking, so it's accurate within a live document but won't survive being copied into a context where the processor can't see the surrounding notes. Personally, this author still typically **enters cases and case short forms manually** in the footnote text rather than through Zotero, and that remains a reasonable workflow if precise case-citation behavior matters to you.

### Institutional report (Bluebook Rule 15.7)

For commission reports, GAO/CRS reports, agency reports, and other institutional reports treated as books in Bluebook. Item Type `Report`. Author and title render in small caps.

| | Field | Example |
| - | ----- | ------- |
| 🔴 | Item Type | `Report` |
| 🔴 | Author | `U.S. Dep't of Justice` (or a personal author, see below) |
| 🔴 | Title | `Annual Report` |
| 🔴 | Date | `2024` |
| ⚪ | Institution | optional second institutional name (see below) |

**Pure institutional report (no personal author):** put the institution in the Author field as a single-name author. Output: `U.S. DEP'T OF JUSTICE, ANNUAL REPORT 12 (2024).`

**Report with both a personal author and an institutional sponsor:** put the personal author in **Author** and the institutional name in **Institution**. Both render small-caps before the title:

`JOHN DOE, U.S. GEN. ACCT. OFF., REPORT TITLE 12 (1986).`

> **Don't use Report for working papers.** Despite both being "reports" in plain English, Bluebook 15.7 (book-style institutional reports) and Bluebook 17.4 (working papers) render very differently. Use Item Type **Preprint** for numbered working papers — see the *Working paper* section above.

### Statute / bill / regulation

These use Zotero's `Statute` / `Bill` / `Regulation` item types. They're currently passed through generic rendering — heavy statute users should double-check output; open an issue if a specific format is off.

---

## The Extra field: cheat sheet

Zotero's **Extra** field lets you override or add CSL variables that aren't in the normal Zotero form. Use `key: value`, one per line.

| Line in Extra | What it does |
| ------------- | ------------ |
| `status: forthcoming` | Renders `(forthcoming YYYY)` on journal articles and preprints; also enables URL rendering |
| `status: accepted` | Same mechanism, different word |
| `genre: Note` | Inserts article-type designation between author and title on journal articles (`Note`, `Comment`, `Recent Development`, etc.) |
| `event-title: ...` | Override conference/event title |
| `number-of-pages: ...` | For books |

Lowercase keys are the convention; Zotero's parser is actually case-insensitive, so `Status: forthcoming` works too. Whitespace around the colon is tolerated.

---

## Subsequent-citation behavior

| Situation | Output |
| --------- | ------ |
| Immediately after the same source | `*Id.*` (or `*Id.* at 495` with a pincite) |
| Later reference to a non-case | `AUTHOR, supra note N, at X` |
| Later reference to a case, within 5 footnotes (Rule 10.9) | `*Brown*, 347 U.S. at 495` |
| Later reference to a case, more than 5 footnotes back | full cite again — `Brown v. Board of Education, 347 U.S. 483 (1954)` |
| 5 or more authors | `First Author et al.` |

---

## Known limitations

- **No auto-update.** Zotero only auto-updates styles from its official repository. Install the new file yourself when versions ship — it replaces your existing copy in place (see [Updating](#updating)).
- **No introductory signals.** *See*, *Cf.*, *But see*, etc. are produced by a separate Zotero plug-in, not this style.
- **Limited statute / regulation coverage.** The style is primarily tuned for cases, books, journal articles, working papers, and internet sources.
- **Bibliography rendering is approximate.** The style targets law-review footnotes (note-style). If you ask Zotero to build a bibliography/works-cited list, it will produce something reasonable but not a Bluebook Table of Authorities.
- **No `[hereinafter shortname]` support.** Bluebook lets authors coin a custom short form on first citation (e.g., `[hereinafter Reimagining]`) and then use that short form on every subsequent cite. CSL has no native concept of author-defined short forms, so the style can't generate the `[hereinafter …]` marker or honor it on subsequent cites.
- **Can't detect "volume number is a year."** When a journal's volume *is* a year (e.g., `2024 Wis. L. Rev. 501`), Bluebook suppresses the redundant trailing `(2024)`. This style renders both (`2024 Wis. L. Rev. 501 (2024)`), because CSL can't introspect the volume to tell whether it looks like a year.
- **Can't detect "title ends in a numeral."** When a book or report title ends in a number (e.g., *Article III* at 45), Bluebook requires the pincite be written `, at 45` to avoid running the two numbers together. This style just emits the page number, so you may get ambiguous output like `ARTICLE III 45`.
- **Cases: five-footnote rule has limits.** Bluebook Rule 10.9 says a short-form case cite (`*Brown*, 347 U.S. at 495`) may be used only if the full cite appears in the same footnote or one of the preceding five footnotes — otherwise, cite in full again. The style now applies this automatically via Zotero's footnote-distance tracking: cases revert to a full cite once the prior cite falls outside the five-footnote window. The catch is that this depends on the processor seeing the surrounding notes — it's reliable in a live document but not when citation text is copied out of context, and it counts footnote distance rather than the exact "same-or-preceding-five" set Bluebook describes. For full control, many authors (including this one) still enter cases and case short forms manually in the footnote text rather than via Zotero.

> **Companion plug-in.** Several of these gaps (hereinafter, volume-as-year, title-ends-in-numeral) are handled by the **[Bluebook Citations Fixer](https://github.com/danepps/zotero/tree/main/bluebook-citations-fixer)** plug-in (part of **[danepps/zotero](https://github.com/danepps/zotero)**) — starting with Rule 4.2(b) `[hereinafter]` short forms. A plug-in can introspect the data and post-process Zotero's citation output in ways that a pure CSL file cannot.

---

## Changelog

### May 2026 — Rule 10.9 five-footnote rule

- **Case short forms now respect Bluebook Rule 10.9's five-footnote rule.** A subsequent case cite uses the short form (`*Brown*, 347 U.S. at 495`) only when the prior cite is within five footnotes; beyond that window it reverts to a full cite. Implemented via citeproc's footnote-distance tracking (`near-note-distance="5"`). Full case cites also now emit an explicit italics-off so a short-form-then-full re-render doesn't leave a stale italic run in Word.

### May 2026 — podcasts

- **Podcasts (Bluebook Rule 18.8.1(c))** now have first-class support via Item Type `Podcast`. Output: `SHOW NAME: *Episode Title* (Streaming Service, Date), URL`, with the show name in small caps and the episode title italicized. Streaming service comes from the native **Publisher** field. Time-marker pincites (`, at 12:34`) work via the citation locator. If the release date is unknown, fill the Accessed field instead — the style renders that in its place per the rule's "last streamed" provision. See *Podcast* above.

### May 2026 — working papers, unpublished manuscripts, institutional reports

- **Working papers (Bluebook Rule 17.4)** now have first-class support via Item Type `Preprint` (CSL `article`). Output: `Author, *Title* pincite (Sponsor, Working Paper No. N, YYYY)` plus URL. Reads sponsor / descriptor / number through a fallback chain (Repository / Genre / Series Number preferred; Series fills the sponsor slot when Genre is set; Extra-field overrides supported). See *Working paper* above.
- **Unpublished manuscripts (Rule 17.2.1)** now render properly via Item Type `Manuscript`. Output: `Author, Title pincite (Mon. DD, YYYY) (unpublished {type|"manuscript"}) (on file with X)` — all roman per Rule 17.2. Includes URL. See *Unpublished manuscript* above.
- **Institutional reports (Rule 15.7)** with both a personal author and an institutional sponsor now render both in small-caps before the title (`JOHN DOE, U.S. GEN. ACCT. OFF., REPORT TITLE 12 (1986)`). Item Type `Report` is reserved exclusively for true Rule 15.7 reports — working papers moved off it.
- The earlier hybrid `report` rendering that conflated working papers and institutional reports is removed.

### April 2026 — forthcoming articles

- **Forthcoming journal articles** now use `(manuscript at N)` for the pincite on both first-cite and `supra` short-cite, when `status: forthcoming` (or any non-empty `status`) is set in Extra. So `Jane Doe, *Title*, 137 Harv. L. Rev. (forthcoming 2027) (manuscript at 12)` and the corresponding `Doe, *supra* note 3 (manuscript at 12)`.
- URL emission enabled for forthcoming journal articles.


---

## Feedback / bug reports

Two ways to report:

- **Email** Prof. Epps at <epps@wustl.edu>.
- **Open a GitHub issue** at <https://github.com/danepps/bluebook/issues> — click *New issue*, give it a short title, and paste the details below. (A free GitHub account is required to file one.)

When reporting a bad render, paste the output you got, the output you expected, and (if possible) a screenshot of the Zotero item so the fields can be verified.

---

## Credits

- Original Bluebook CSL by **Bruce D'Arcus** and **Nancy Sims**, with contributions from **Patrick O'Brien**.
- Modifications for this fork by **Dan Epps** (<epps@wustl.edu>).
- Licensed under [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/).
