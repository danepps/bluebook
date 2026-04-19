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
- **No trailing period** on output. Removed because the base CSL style's trailing period interferes with chained footnote cites joined by semicolons. Users add the period in context.
- **URLs only render for internet-first item types**: `webpage`, `post-weblog`, `article`, `article-newspaper`, `article-magazine`, and `article-journal` *only when `status` is set* (forthcoming articles).
- **"Last visited" parenthetical is gated to `type="webpage"`** only. Blog posts, news, etc. have their own publication dates.
- **Newspaper/magazine URL decision matrix** in `source` macro:
  - `page-first` set → print form (`Title, Paper, Date, at Page`; URL appended by `access` if also present)
  - no `page-first` but URL set → web form (`Title, Paper (Date)` + URL)
  - neither → bare (`Title, Paper, Date`)
- **Rule 10.9 case short form** in `subsequent` position: italic short name + volume + reporter(short) + `at` pincite. All other subsequent cites use `AUTHOR, supra note N, at X`.
- **`<bibliography>` element is approximate** — the style targets law-review footnotes, not Bluebook Tables of Authorities. Don't over-invest here.
- **Stable distribution URL** is `https://danepps.github.io/bluebook/BluebookDSEStyle.csl`. Never revert to `raw.githubusercontent.com`.

## Out of scope for this CSL (delegated to companion plug-in)

The [`danepps/zotero`](https://github.com/danepps/zotero) Zotero plug-in handles what CSL can't:

- Introductory signals (*See*, *Cf.*, *But see*, *Contra*, etc.)
- `[hereinafter shortname]` coined short forms
- Volume-number-is-a-year detection (suppressing redundant `(YYYY)`)
- Title-ends-in-a-numeral detection (forcing `, at X` pincite)
- Rule 10.9's five-footnote rule for case short forms (CSL has no footnote-distance awareness)

Don't try to implement these in pure CSL. Point users at the plug-in instead.

## Author workflow preferences

- The author typically **enters cases and case short forms manually** in the footnote text rather than through Zotero, because of the five-footnote-rule limitation. The style's case output is a safety net, not the primary path.
- **Explanatory parentheticals are entered manually per cite**, via Zotero's Suffix field. For a string cite where each source has its own parenthetical, insert each source as a separate cite rather than combining into one multi-source cite.
- **Journal abbreviations come from each item's `Journal Abbr` field** in Zotero, filled in per item. The MEDLINE abbreviation setting in Zotero is NOT Bluebook-compliant and should be off.
- **Signals via the plug-in or Zotero's Prefix field**, never typed directly into the document — that breaks automatic `id.` lowercasing.

## Bug reports

Route to **email Prof. Epps at <epps@wustl.edu>**, not GitHub issues.

## Current status (April 2026)

The style and its surrounding infrastructure are **stable and shipped**. As of the latest session:

- **CSL is production-ready.** All known code-review fixes applied (Rule 10.9 italic short-form, URL-emission gated by item type, newspaper/magazine page-vs-URL decision matrix, forthcoming-journal via `status`, webpage-only "last visited", dead `report` branch removed, `<bibliography>` element added).
- **Distribution is live.** GitHub Pages serves `https://danepps.github.io/bluebook/BluebookDSEStyle.csl` as the canonical install URL. `bump-updated.yml` auto-rewrites `<updated>` on every CSL push to `main`.
- **README is comprehensive.** Intro + Zotero onboarding, install (Zotero 7/8, Word/Docs plug-in note, "Zotero must be running"), updating (manual reinstall + early-adopter migration note for old `raw.githubusercontent.com` installs), "How the style works" principles, per-item-type data-entry guide with 🔴/⚪ required/optional convention, Extra-field cheat sheet, subsequent-citation table, known limitations, email for bug reports.
- **Out-of-scope items** (hereinafter, volume-as-year, title-ends-in-numeral, five-footnote rule, signals) are documented as delegated to `danepps/zotero`.

**Nice-to-have follow-ups** (not urgent, no one asked for them):

- Type-specific rendering for `statute` / `bill` / `regulation` — currently falls through to generic output.
- Verify webpage-author fallback (using site name when author is blank) matches Bluebook Rule 18.
- Start cutting tagged releases (`v1.0`, …) so the README's "Watch → Releases" path actually notifies subscribers.
- Bibliography/Table-of-Authorities tuning — output is "approximate" today; fine for law-review footnote workflow but not a true ToA.

Update this section when any of the above ships, or when a new batch of work materially changes what's running in production.

## Things to double-check before releasing a CSL change

- `xmllint --noout BluebookDSEStyle.csl` is clean.
- Install the modified style in Zotero and spot-check at least: one case, one book with 3+ authors, one journal article, one forthcoming article (with `status: forthcoming`), one webpage (with accessed date), one newspaper article (with both page and URL set).
- `<updated>` will be rewritten automatically by the workflow; don't bother editing it manually.
