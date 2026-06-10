# CLAUDE.md — notes for future Claude (and future me)

Persistent project context that survives conversation resets. Keep it tight; long files dilute the useful bits.

## Keep this file up to date

Whenever a new workflow convention or CSL design choice gets settled in a session — a new intentional deviation, a new "out of scope" item delegated to the plug-in, a change to the narrow-PR / experimental-first workflow, a new author preference — **append or update the relevant section of this file before ending the turn**, and include the update in the same PR as the code/README change it documents. Don't wait to be asked.

If the relevant section is already covered but slightly out of date, edit in place rather than adding a new bullet. Preserve brevity: this file is useful only while it stays scannable.

## What this repo is

A CSL 1.0 note-style **citation style** for Zotero implementing Bluebook legal citations, with customizations by Prof. Daniel Epps (Washington University School of Law). The code artifact is the `.csl` XML file; the README is the user-facing manual.

## Files

- `BluebookDSEStyle.csl` — the **stable, user-facing style**. This is what people install.
- `BluebookDSEStyle-Experimental.csl` — the author's testing workspace. **Not documented in the README.** Not for end users.
- `README.md` — the full user-facing guide, rendered at <https://danepps.github.io/bluebook/> via GitHub Pages.
- `_config.yml` — Jekyll theme (`jekyll-theme-cayman`) for the Pages site.
- `.github/workflows/bump-updated.yml` — rewrites the CSL's `<updated>` element to the commit-time UTC timestamp on every push to `main` that touches a `.csl` file, then commits with `[skip ci]`.

## Workflow conventions

1. **Narrow PRs, one concept per PR.** Don't bundle unrelated changes. Small PRs are easier to review, easier to roll back, and easier to explain in the commit log.
2. **Test CSL changes in the experimental file first.** When a change is validated, **promote** the experimental content to the main file by copying it wholesale while preserving the main file's own `<title>`, `<id>`, and `<link rel="self">`. See PR #10 as the canonical example.
3. **Auto-delete head branches is enabled** on this repo. After a PR merges, its branch is gone — if a follow-up commit needs to land, open a new PR off main, don't try to re-push the old branch.
4. **`main` is protected** (no force-push, no deletion). Develop on feature branches named `claude/<short-slug>`.
5. **Don't skip hooks or bypass the workflow**. If the `bump-updated.yml` workflow fails, diagnose it — don't work around it.

## CSL design choices (intentional)

These have been debated and settled. Don't "fix" them without asking.

- **`et-al-min="5"`** — the author prefers listing up to four names before abbreviating, even though Bluebook Rules 15.1/16.1 specify three.
- **No trailing period** on output. Author-introduced change from the base Bluebook CSL: primarily to let users type explanatory parentheticals right after the citation without first having to delete an auto-inserted period; also keeps semicolon-chained footnote cites clean. Users add the period in context.
- **URLs only render for internet-first item types**: `webpage`, `post-weblog`, `article`, `article-newspaper`, `article-magazine`, and `article-journal` *only when `status` is set* (forthcoming articles).
- **"Last visited" parenthetical is gated to `type="webpage"`** only. Blog posts, news, etc. have their own publication dates.
- **Newspaper/magazine URL decision matrix** in `source` macro:
  - `page-first` set → print form (`Title, Paper, Date, at Page`; URL appended by `access` if also present)
  - no `page-first` but URL set → web form (`Title, Paper (Date)` + URL)
  - neither → bare (`Title, Paper, Date`)
- **Rule 10.9 case short form** in `subsequent` position: italic short name + volume + reporter(short) + `at` pincite. All other subsequent cites use `AUTHOR, supra note N, at X`. **The five-footnote rule is now enforced in the stable file** via `near-note-distance="5"` on `<citation>`: a subsequent case cite renders the short form only when `position="near-note"` (within five footnotes); the `<else>` branch reverts to a full cite (calls `source` + `access`). Because a full cite can now re-render *after* a short form, the `source` legal_case branch wraps its output in `<group font-style="italic"><group font-style="normal">` so citeproc emits an explicit italics-off (RTF `\i0`) — otherwise Word keeps the stale italic run from the prior short form and a Refresh won't clear it. **Caveat:** depends on the processor seeing the surrounding notes (reliable in a live document, not in copied-out text) and counts footnote *distance* rather than the exact same-or-preceding-five set.
- **Journal year ranges are SHELVED** (June 2026) — the author decided not to pursue this for now; the experimental file was re-baselined from stable and the year-range change removed. Recover from git history (experimental file as of commit `97eea49`) if revived. Key knowledge if it comes back: citeproc has **no real `season` date-part** (a `<date-part name="season">` crashes the processor); a HeinOnline two-year volume (`"2021-2022"`) imports as `issued: {date-parts:[[2021]], season:"2022"}`, so a plain `year` render shows only `(2021)`. Emitting `<date-part name="month" form="numeric" prefix="–"/>` surfaces the season-parked second year as `(2021–2022)`, but a genuine season/month leaks as `(2020–Summer)`. Commit `0cab37b` (`date-parts="year" form="text"`) was a no-op for this.
- **Locator labels (Rules 3.3–3.4) (experimental file only, under test)** — `at` introduces only *page* pincites (`Id. at 5`); any other locator label renders via its symbol term with no `at` (`Id. § 4`, `Id. ¶¶ 12–13` — citeproc pluralizes the symbol for ranges; labels without a symbol form fall back to short form, e.g. `ch.`). All bare pincite points in `source` (journal, case, article, report, thesis, chapter, book, generic) route through a shared `pincite` macro with the same page-vs-symbol logic, so non-page locators gain their symbol there too (`TITLE § 5 (2010)`); page locators are unchanged everywhere. Podcast timestamps keep `at TT:TT` via the default *page* label. The two `(manuscript at X)` locators are intentionally left raw.
- **Authorless supra short forms (Rule 4.2) (experimental file only, under test)** — when an item has no author, the subsequent-cite chooser now falls back to a short title before *supra* instead of emitting a bare `supra note N`. Font tracks the full-cite rendering of each type: small caps for `book`/`graphic`/`motion_picture`/`report`, plain roman for the unpublished types (`article`/`manuscript`/`thesis`/`document`), italic for everything else (newspaper, magazine, webpage, blog, chapter, generic). The existing `article-journal` short-title and podcast host/show fallbacks are unchanged and take precedence.
- **Edition field `ed.` guard (Rule 15.4) (experimental file only, under test)** — the issuance macro appends the `ed.` label only when the Edition field is numeric per CSL's `is-numeric` test (`3`, `3d`, `11th`); any other value renders **verbatim** (`rev. ed.`, `2d rev. ed.`). CSL cannot string-match field content, so non-numeric values must contain the complete Bluebook text. **Promotion-time tasks:** flip the README's Edition note (it currently tells stable users to type bare `rev.`, which under the guard renders `(rev. 2024)` — the instruction becomes "type `rev. ed.` in full"), and include a migration warning for existing items entered as bare `rev.`.
- **Podcasts (Bluebook Rule 18.8.1(c))** render as `SHOW NAME: *Episode Title*, at TT:TT (Streaming Service, Date), URL` via a dedicated `else-if type="song broadcast"` branch in `source`. Zotero's Podcast item type exports as CSL `broadcast`; Podcaster creator → `host`; Series Title → `collection-title`. Show name resolves through `author` → `host` → `container-title` → `collection-title`, all rendered small-caps. Streaming service comes from native Publisher (`publisher`). Date falls back to `accessed` when `issued` is empty (rule allows "last streamed" date when no release date). The citation and bibliography layouts skip the standard author macro call for `song broadcast` (the source branch embeds it inline with a `:` separator); `broadcast` was added to the small-caps lists in `author` / `author-short` so the embedded macro call produces the right font. `host` is also rendered small-caps via a `<group font-variant="small-caps">` wrapper because the author macro only checks `author`. **Don't put `font-variant` directly on `<names>`** — the official CSL 1.0.2 schema allows it, but Zotero's installer flags such files as "not a valid CSL 1.0.2 style file." Wrap the `<names>` in a formatted `<group>` instead.
- **`<bibliography>` element is approximate** — the style targets law-review footnotes, not Bluebook Tables of Authorities. Don't over-invest here.
- **Stable distribution URL** is `https://danepps.github.io/bluebook/BluebookDSEStyle.csl`. Never revert to `raw.githubusercontent.com`.

## Out of scope for this CSL (delegated to companion plug-in)

The [`danepps/zotero`](https://github.com/danepps/zotero) Zotero plug-in handles what CSL can't:

- Introductory signals (*See*, *Cf.*, *But see*, *Contra*, etc.)
- `[hereinafter shortname]` coined short forms
- Volume-number-is-a-year detection (suppressing redundant `(YYYY)`)
- Title-ends-in-a-numeral detection (forcing `, at X` pincite)

(Rule 10.9's five-footnote rule for case short forms used to live here — it's now handled in pure CSL via `near-note-distance="5"`; see the CSL design choices section.)

Don't try to implement these in pure CSL. Point users at the plug-in instead.

## Author workflow preferences

- The author typically **enters cases and case short forms manually** in the footnote text rather than through Zotero. Even though the style now enforces Rule 10.9's five-footnote rule, its footnote-distance tracking is reliable only in a live document, so manual entry remains the primary path; the style's case output is a safety net.
- **Explanatory parentheticals are entered manually per cite**, typed directly into the footnote text after the citation — not into Zotero's Suffix field. For a string cite where each source has its own parenthetical, insert each source as a separate cite rather than combining into one multi-source cite, so each parenthetical can be typed between the inserted cites.
- **Journal abbreviations come from each item's `Journal Abbr` field** in Zotero, filled in per item. The MEDLINE abbreviation setting in Zotero is NOT Bluebook-compliant and should be off.
- **Signals via the plug-in or Zotero's Prefix field**, never typed directly into the document — that breaks automatic `id.` lowercasing.

## Bug reports

Two accepted routes: **email Prof. Epps at <epps@wustl.edu>** or **open a GitHub issue** at <https://github.com/danepps/bluebook/issues>. README documents both.

## Current status (June 2026)

The style and its surrounding infrastructure are **stable and shipped**. As of the latest session:

- **CSL is production-ready.** All known code-review fixes applied (Rule 10.9 italic short-form, Rule 10.9 five-footnote rule via `near-note-distance="5"`, URL-emission gated by item type, newspaper/magazine page-vs-URL decision matrix, forthcoming-journal via `status`, webpage-only "last visited", dead `report` branch removed, `<bibliography>` element added).
- **Distribution is live.** GitHub Pages serves `https://danepps.github.io/bluebook/BluebookDSEStyle.csl` as the canonical install URL. `bump-updated.yml` auto-rewrites `<updated>` on every CSL push to `main`.
- **README is comprehensive.** Intro + Zotero onboarding, install (Zotero 7/8, Word/Docs plug-in note, "Zotero must be running"), updating (manual reinstall + early-adopter migration note for old `raw.githubusercontent.com` installs), "How the style works" principles, per-item-type data-entry guide with 🔴/⚪ required/optional convention, Extra-field cheat sheet, subsequent-citation table, known limitations, email for bug reports.
- **Five-footnote rule (Rule 10.9)** is now enforced in the stable file via `near-note-distance="5"`; the year-range experiment is shelved (see design choices).
- **Experimental file was re-baselined from stable** (June 2026) and is accumulating the compliance-queue fixes, to be **promoted to stable as one batch** when the author calls it done (author's decision, June 2026). Currently carries: locator-label handling (Rules 3.3–3.4; Zotero-validated), authorless supra short-title fallback (Rule 4.2; awaiting spot-check), and the Edition-field `ed.` guard (Rule 15.4; awaiting spot-check — has a promotion-time README task). See design choices for all three.
- **Out-of-scope items** (hereinafter, volume-as-year, title-ends-in-numeral, signals) are documented as delegated to `danepps/zotero`.

**Bluebook compliance queue** (from the June 2026 review of the stable style, ranked; one PR each, experimental-first):

1. ~~Locator labels (Rules 3.3–3.4): non-page pincites rendered `at N` instead of `§ N` / `¶ N`~~ — in experimental, under test.
2. ~~Authorless newspaper/magazine/webpage subsequent cites render a bare `supra note N` — need a short-title fallback before *supra* (Rule 4.2)~~ — in experimental, under test.
3. Statutes (Rule 12): `legislation` branch emits no date parenthetical (still required for state/unofficial codes) and no `Stat.` page for session laws; `§` is hardcoded singular (no `§§`).
4. Dedicated branches for bills (Rule 13.2) and regulations (Rule 14.2) — currently fall through to the generic branch with italic title + small-caps container, clearly wrong.
5. Unreported/pending cases (Rule 10.8.1): no docket number, year-only date (full date required), and WL star pincites lose their `at`.
6. Minor: "last visited" doubles up when a webpage has both issued and accessed dates (Rule 18.2.2(c) wants it only for undated material); case short form with no pincite dangles (`Roe, 410 U.S.`); `interview`/`speech`/`patent` fall to generic output.

**Nice-to-have follow-ups** (not urgent, no one asked for them):

- Verify webpage-author fallback (using site name when author is blank) matches Bluebook Rule 18.
- Start cutting tagged releases (`v1.0`, …) so the README's "Watch → Releases" path actually notifies subscribers.
- Bibliography/Table-of-Authorities tuning — output is "approximate" today; fine for law-review footnote workflow but not a true ToA.

Update this section when any of the above ships, or when a new batch of work materially changes what's running in production.

## Things to double-check before releasing a CSL change

- `xmllint --noout BluebookDSEStyle.csl` is clean.
- Install the modified style in Zotero and spot-check at least: one case, one book with 3+ authors, one journal article, one forthcoming article (with `status: forthcoming`), one webpage (with accessed date), one newspaper article (with both page and URL set), one podcast (Item Type Podcast, with Podcaster, Title, Publisher, Date, URL set).
- `<updated>` will be rewritten automatically by the workflow; don't bother editing it manually.
- Validate against the official CSL schema, not just XML well-formedness: `java -jar jing.jar -c csl.rnc BluebookDSEStyle.csl`. **Schema-clean doesn't guarantee Zotero-clean** — Zotero's installer is stricter than the spec for some attribute placements (e.g., `font-variant` directly on `<names>`).
