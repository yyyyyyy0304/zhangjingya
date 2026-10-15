# AGENTS.md

## What this is

Static HTML/CSS coursework site (《高级网页设计》课堂实践). **No build, no package manager, no tests, no linter** — there is no `package.json`, no CI, no dev server. Verify by opening files directly in a browser, or serve the root with any static server (`npx serve .`, `python -m http.server`).

## Project rules (user-mandated — follow exactly)

- **`zhang_` prefix**: every CSS class name, id, and JS variable must start with `zhang_` (e.g. `class="zhang_card"`, `id="zhang_box"`, `let zhang_index = 0`). Applies to all code you write or edit. The pre-existing exercise pages don't follow this rule — never mass-rename their classes/ids unless explicitly asked.
- **Prompt log**: before carrying out any user prompt, append one entry to `zhang_prompt.md` at the repo root. **Append only — never overwrite, truncate, or recreate the file.** Each entry records:
  - time: `yyyy-mm-dd-hh:mm` (e.g. `2026-10-12-16:03`)
  - model used (e.g. `opencode/mimo-v2.6-flash-free`)
  - the full prompt text
  - Append as UTF-8 **without BOM**: `[IO.File]::AppendAllText('zhang_prompt.md', $text, (New-Object System.Text.UTF8Encoding($false)))`. Avoid `Add-Content -Encoding UTF8` / `Set-Content` — PowerShell 5.1 gives a new file a BOM.
- **New pages link home**: every newly created HTML file must contain a hyperlink to the homepage, e.g. `<a class="zhang_home-link" href="../index.html">← 返回首页</a>` right before the `<h1>`. Lesson folders sit one level deep, so the relative path from any exercise page is `../index.html` (from the root it is `./index.html`). The link's class follows the `zhang_` prefix rule.

## Structure

- `index.html` (root) — the gallery/hub page. All navigation lives here.
- `1/` … `11/` — one folder per lesson; each contains standalone HTML exercises plus an `img/` subfolder where needed.
- `5/CSS.css` is the only external stylesheet; every other page uses inline `<style>`.

## Conventions (enforced by the assignment prompt, quoted in `index.html`)

- **No CDN, no external libraries** — vanilla HTML/CSS/JS only. Do not add CDNs, fonts, or framework links.
- Every page: `<meta charset="UTF-8">` + viewport meta, Chinese text, UTF-8 **without BOM**, **CRLF** line endings. `lang` is `zh-CN` on `index.html` and newer pages, but several older exercises say `lang="en"` — don't "fix" them unless asked.
- Filenames contain spaces and Chinese characters (`4/4-1 css2.html`). Links in `index.html` percent-encode spaces (`%20`) but leave Chinese characters raw — match that existing style when adding links.

## Editing `index.html`

- Work-card links are `./N/file.html` (e.g. `./4/4-1%20css2.html`). Add one `<a class="work-card">` per new page, continuing the sequential `01`, `02`, … numbering.
- The heading "共 N 个网页练习" is a manual count of cards (currently 17) — update it whenever cards are added or removed.
- Known gap: folder `10/` (8 animation pages) exists but is **not linked** from `index.html`. Don't assume every file on disk is reachable from the hub.
- Older exercise pages contain no back-link to `index.html` (hub-only navigation); only pages created after the "new pages link home" rule carry one.

## Environment gotchas

- Windows + PowerShell: the console renders Chinese filenames/content as mojibake (GBK codepage). Use the Read tool or `Get-Content -Encoding UTF8` — it's an display artifact, not file corruption. Don't "fix" encoding.
- Git repo has **zero commits**; everything is untracked. `core.quotepath` is unset, so `git status`/`git diff` will escape non-ASCII paths (`\344\275...`) — that is normal, not broken paths.
