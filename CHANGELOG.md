# Changelog

Working journal of notable changes. Format adapted from [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

**How to read this:**
- Dates are commit dates (not write dates).
- `(a3f291)` is a short SHA — `git show a3f291` to see the diff.
- Entries explain symptom + cause, not just "fixed."
- No version tags exist (static site, no manifest); milestones are date-stamped instead.

---

## [Unreleased]
_Changes on `claude/add-context-documentation-aBKjZ`, not yet merged to `main`._

### Added
- `CONTEXT.md` at repo root — single source-of-truth onboarding file for AI assistants and the author after long gaps. `(2921fec)`

### Architectural
- Documented in `CONTEXT.md` that `GEMINI.md`'s `docx.js` claim is wrong — verified zero `<script src>` tags; export is `.txt` + clipboard-to-Google-Docs only. `(2921fec)`

---

## 2026-06-03 — autosave everywhere + desktop layout + mobile persistence
_Branch `claude/sweet-bardeen-11lFI`._

### Added
- **`observation.html` local autosave/restore.** The whole observation (all 450+ fields, tri-state exams, biology values, dynamically-added treatment rows, custom pathologies, extra diagnostic rows, medication table, and which sections were open) is now kept in `localStorage` (`observation_state_v1`) and restored on load — nothing is lost on refresh, accidental navigation, tab close or crash. Saves are debounced on edit and flushed on `visibilitychange`/`pagehide`/`beforeunload`. A "💾 Enregistré · HH:MM" indicator shows in the header; empty drafts are never persisted; `Réinit.` clears the draft.
- **`observation.html` desktop layout.** A sticky left section-navigator (jump-to-section + per-section progress + active-section highlight via `IntersectionObserver`), a wider centred grid (≥1000px), and 2-column compaction of the long checkbox/tri-state lists to use the screen width. Mobile is unchanged (single column, navigator hidden).
- **`simplechecklist.html` resilient persistence.** State is now flushed the moment the page is hidden (phone locked / app switched) via `visibilitychange`/`pagehide`/`beforeunload`, so data survives the OS killing the tab. Open/closed sections are remembered, a save indicator + "Données restaurées" toast were added, plus an expand/collapse-all button. PWA/app meta tags (`theme-color`, `apple-mobile-web-app-*`) and iOS safe-area (notch) handling added.

### Fixed
- **Biology table wiped its own data.** Switching SI↔Usuelles units *or* changing the patient's sex called `renderBiologicalTables()`, which rebuilt the table with empty inputs — silently erasing every lab value the clinician had typed. `renderBiologicalTables()` now snapshots and re-applies existing values/checks (and re-colours) across a rebuild.
- Removed `maximum-scale=1.0` from both files' viewport (was blocking pinch-zoom — an accessibility anti-pattern).

---

## 2026-04-15 — hub rewrite v2 + Traumato-ped stub

### Added
- `services/CCI-A (Traumato-ped)/` folder with placeholder `index.html` + `idea.txt` — opening slot for the next specialty template. `(97150ce, 74734ed)`

### Changed
- `index.html` rewritten as a structured hub: two main buttons, autocomplete search, specialty chips, and a collapsible "Ressources & Modules" panel listing the eight numbered observation modules and the eight clinXpert guides. `(97150ce)`
- `README.md` link formatting cleaned up — bare URL replaced with proper markdown link to the GitHub Pages site. `(a29c688, c887afb)`

---

## 2026-04-13 — clinXpert guide pages

### Added
- Eight HTML guide pages under `clinXpert/` (Général, cardio-vasculaire, neurologique, Abdominal, pleuro-pulmonaire, ostéoarticulaire, gynécologique, urologique) with embedded YouTube videos and Papyrus-font styling for the section titles. `(e114704)`
- `clinXpert-youtube-url.txt` — source list of the YouTube embeds used by the guide pages. `(46d576f)`

---

## 2026-03-15 — observation.html issue-fix sprint + tri-state UX

### Added
- Tri-state checkbox system (Normal / Anormal / Absent) for `examen clinique` Section 5, with confirmation dialog when switching N↔A and a dedicated reset button. Exports updated to reflect tri-state values. `(3519a7d, f309c6f, 4ec2353)`
- TDM and IRM detail panels in the paraclinique section with fields for étage, fenêtre, injection, coupe, pondération. `(ac9c497)`
- Comprehensive clinical guidance text added to both `observation.html` and `simplechecklist.html` (mnemonics, semiology hints inline). `(a2ad60c)`
- `index.html` hub gained full repo-content integration — links to all observation modules, clinXpert guides, and external resources surfaced in one place. `(ff78921)`

### Changed
- Word export replaced with a "Build Page" button — generated a printable HTML page instead, since the prior Word path produced unusable `.docx`. `(d11127c)`

### Fixed
- CHU links pointed at wrong/dead hosts — corrected Fès and Oujda URLs and removed the non-existent Settat entry. `(53c03a4)`
- ClinXpert PDF link in the floating-island menu was 404ing — repointed to the raw GitHub URL. `(f06f2e4)`
- Batch fix for open issues #1, #4, #6, #7, #8, #9, #10 on `observation.html` (form validation, label corrections, missing fields). `(f04bd4b)`

---

## 2026-03-02 → 2026-03-08 — observation.html restructure + dropdown menu

### Changed
- `observation.html` heavily restructured across many small "update" commits — large symmetric insert/delete diffs (~1190 lines, ~611 lines, ~1338 lines moved) indicate section reordering and a rename of `observation_text_prises.html` → `observation_1.html`. `(da4bbff, 9864e3b, f39ad06, c4222db, 6996c47, d0441ae)`
- Added dropdown menu in `observation.html` for navigating between observation sections. `(da4bbff)`

### Added
- Module file `observation_ressources/0_informations_clinicien.html` extracted from the monolith for modular prototyping. `(0def7b7)`
- `observation_ressources/2. atcds/diabete.txt` — reference text for the diabetes ATCD sub-fields. `(c9ee204)`
- Lab-reference PDFs and biological-values catalogues under `observation_ressources/7. paraclinique/bilan biologique/`. `(4e2d641, 4fc2ded)`
- Backup snapshots `backup/observation_backup/observation - Copy.html` and `observation - before edit.html` at the root — manual restore points before risky edits. `(8e37a78, 98887fc)`

### Architectural
- `observation_ressources/GEMINI.md` introduced and refined — defined the "modular prototyping then fuse into root" workflow, no `.floating-island` in modules, UTF-8 no BOM, French only. `(b3323ad, a6f9016)`

---

## 2026-02-17 → 2026-02-22 — initial bring-up + hub mode

### Added
- `simplechecklist.html` — mobile-first bedside checklist with floating-island top bar, system-by-system checkboxes, progress indicator. `(247ae7c, plus earlier vague commits)`
- Service folders `services/ccv/`, `services/hemato/`, `services/radio/` with placeholder HTML files. `(d81d99d)`
- `clinXpert/` reference library populated with `+++ AIO`, observation source PDFs, and `Examen clinique normal.pdf`. `(0ad775c, 1af00fd, 668aec9)`
- `other checklist/` reference: `Obs_Check_PC_STI.doc`, `Observation-packet`, `acute-transfer-checklist.pdf` and other external observation templates for inspiration. `(6c4338c, e5b4e07)`

### Architectural
- "Hub mode" — `secret.html` renamed to `observation.html`, new `index.html` introduced as the navigation hub. Old hub preserved under `backup/index latest.html`. `(520d848, d64b686, 70c4c04)`
- Repository converted from "single big HTML file (`secret.html`)" to multi-page hub-and-spoke layout. `(520d848, 3c514e6, 2304b5c)`
- `.gitignore` added to exclude two large copyrighted Sémiologie PDFs from `observation_ressources/`. `(e1cae60, 0ad775c)`

### Broken
- A long string of single-character "u" / "re" / "updaet" commits in this window — diffs are mostly Windows `Zone.Identifier` ADS files and binary PDF additions. Real intent for any single one is unrecoverable from the message; rely on diffs. `(18d9a68, ef0cb48, e5b4e07, d7ea9dc, 4778fe9, 330cc11, 8e37a78, etc.)`

---

<details>
<summary>Archive — entries older than 12 months</summary>

_(Empty. The repo's first commit is 2026-02-17, well within the 12-month window from today, 2026-04-27.)_

</details>

---

## Update Protocol (Verbatim)
> **For the AI Assistant:** When asked to "Update CHANGELOG.md":
> 1. Find the most recent SHA cited in the existing file.
> 2. Run `git log` and `git diff --stat` for everything since that SHA.
> 3. Apply the WIP Decoder — derive intent from diffs when commit messages are vague (this repo has many one-letter "u" / "re" / "update" commits — always inspect the stat).
> 4. Group consecutive same-intent commits into single entries; split when intent changes.
> 5. Skip noise (lockfiles, formatter passes, typos, no-op commits, `Zone.Identifier` ADS files).
> 6. No `package.json` exists — use natural date-stamped milestones instead of version tags.
> 7. Append new entries above existing ones. **Never rewrite past entries** except to fix factual errors (and note the correction inline).
> 8. Roll entries older than 12 months from today's date into the `<details>` archive.
> 9. Keep the file under 600 lines and every entry under 2 lines.
