# bluebook

A CSL 1.0 note-style citation format implementing Bluebook legal citations, with
customizations by Prof. Daniel Epps (Washington University School of Law).

File: [`BluebookDSEStyle.csl`](BluebookDSEStyle.csl)

## Install

Install the style in Zotero (also works in any CSL-compatible processor such as
Pandoc or Mendeley):

1. In Zotero, open **Settings** (or **Preferences** on macOS) → **Cite** →
   **Styles**.
2. Click the **+** button.
3. Select the `BluebookDSEStyle.csl` file, or point Zotero at the stable URL:

   ```
   https://danepps.github.io/bluebook/BluebookDSEStyle.csl
   ```

## Updating

Zotero only auto-updates styles that ship with its official style repository.
Because this is a self-hosted custom style, **updates require a manual
reinstall**:

1. In Zotero, go to **Settings → Cite → Styles**.
2. Select **Bluebook Style — Epps Version** and click **−** to remove it.
3. Reinstall from the URL above (or the file in this repo).

The `<updated>` timestamp inside the CSL is rewritten automatically on every
push to `main` (see `.github/workflows/bump-updated.yml`), so the freshly
installed copy will always reflect the latest commit.

## Signals

Bluebook introductory signals (*See*, *See also*, *Cf.*, *But see*, etc.) are
handled by a separate plug-in and are not emitted by this style.
