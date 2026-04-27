# Clinique To-Do — AI Context File
_Last synced: 2026-04-27 @ 74734ed_

## 1. What This Is (Plain English)
- **In one sentence:** A French-language website that helps Moroccan medical students and doctors take a complete patient observation (history + physical exam) without forgetting anything, and spits out a clean text report at the end.
- **Why it exists:** The author is a med student / junior doctor who got tired of forgetting items during bedside exams and re-typing the same boilerplate observation into Word every time. This is the personal "checklist + form-filler + report generator" that fixes that.
- **Who uses it:** The author and friends (medical students/interns). Public-facing on GitHub Pages but not advertised. Treat as a personal tool — UX polish matters more than enterprise rigor.
- **Vibe:** Polished personal tool. Single-file vanilla HTML/JS, no build step, no npm. Lots of medical content baked into the HTML. Written by a vibe coder using AI assistants (Claude / Gemini), so commits are large and hand-edits are rare.

## 2. How To Run It
- **Setup once:** Nothing. No `npm install`, no Python venv, no Docker. It's static HTML.
- **Run dev:** Open `index.html` in a browser. That's it. For nicer paths during dev: `python3 -m http.server` from the repo root, then visit `http://localhost:8000/`.
- **Build / deploy:** No build. Deployed via **GitHub Pages** from the `main` branch — pushing to `main` updates `https://achma-learning.github.io/clinique_to_do/` (per `README.md:1`). No `.github/workflows/` exists yet.
- **Required env vars:** None. No `.env.example`, no secrets, no backend.

## 3. Tech Stack
- **Language + runtime:** Plain HTML5 + CSS + vanilla JavaScript (ES6+, runs straight in modern browsers). No transpiler, no module bundler.
- **Framework / key libraries:** **None.** Zero `<script src>` tags across `index.html`, `simplechecklist.html`, `observation.html` (verified). All logic is inline. No `package.json`, no lockfile.
  - ⚠️ `GEMINI.md:14` claims `docx.js` is used for `.docx` export — **this is wrong**. The actual export buttons are `.txt` download (`observation.html:2358`) and "Google Docs" via `navigator.clipboard.writeText` + opening `docs.new` (`observation.html:3361`). No real `.docx` generation exists.
- **What kind of project:** Static multi-page web app, deployed on GitHub Pages. Effectively three single-file apps that link to each other.
- **External services:** None at runtime. Outbound links only — `clinxpert.glide.page` (a separate Glide app), Moroccan health sites (MSPS, AMMPS, the 6 CHUs), and `docs.new` for the Google Docs paste flow.

## 4. Code Map (The Important Files Only)
- `index.html` — The hub. Two main buttons (Checklist / Observation), specialty search with autocomplete (`index.html:518` defines the `specialties` array), chips for direct specialty links, and a collapsible panel of resources + module links + clinXpert guides. Self-contained, ~530 lines.
- `simplechecklist.html` — Mobile-first bedside checklist. Floating-island top bar, progress tracking, system-by-system checkboxes (~590 lines). Use this on a phone at the patient's bedside.
- `observation.html` — The big one (~3430 lines). Desktop form that captures the full medical observation (identité, ATCDs, histoire de la maladie, examen clinique, paraclinique with biological reference-range validation, conclusion, CAT). Generates a printable page (`generatePage`), `.txt` download (`generateTxt`), or copies to clipboard for pasting into Google Docs (`generateGoogleDocs`).
- `observation_ressources/` — Modular staging area. Each `0_..` to `6_..` HTML file is a standalone section being prototyped before being "fused" into `observation.html`. See `observation_ressources/GEMINI.md` for the fusion rules (no floating-island in modules, keep `name`/`id` identical to root, UTF-8 no BOM, French only).
- `services/<spe>/<spe>.html` — Specialty-specific templates. Currently `ccv/` (cardio-vasc), `hemato/`, `radio/`, plus a stub `CCI-A (Traumato-ped)/`. Each is a standalone copy of the observation form tailored for that service.
- `clinXpert/` — Reference library. HTML + matching `.txt` per body system (Général, cardio-vasculaire, Abdominal, neurologique, pleuro-pulmonaire, ostéoarticulaire, gynécologique, urologique). Linked from the hub's "Guides clinXpert" section. The `.txt` files are the source-of-truth medical content; the `.html` files are the styled presentation.
- `backup/` — Old versions kept around on purpose (see §6).
- `other/idea.txt`, `other/plan.txt`, `other/note to update.txt` — The author's running roadmap notes.
- `GEMINI.md` — Older AI context file. Mostly accurate on structure; **wrong about `docx.js`** (see §3).
- `README.md` — Tiny human-facing pointer to the live site.

## 5. Rules For Editing This Code
- **Zero dependencies, on purpose.** Do **not** add `npm`, a bundler, a framework, or any `<script src="https://cdn...">` tag. If you need a library, paste it inline or argue for it first.
- **Static-site only.** No backend. No build step. Anything you ship must work by double-clicking the HTML file or serving it from GitHub Pages.
- **French is the product language.** All labels, placeholders, toasts, comments-visible-to-user must stay in French. Code identifiers can be French or English (existing code mixes both).
- **UTF-8 without BOM.** Preserve French accents as literal characters (`é`, `è`, `à`, `ç`). Do not convert to HTML entities (`&eacute;`). Per `observation_ressources/GEMINI.md:22`.
- **Modular files in `observation_ressources/` follow extra rules** (per `observation_ressources/GEMINI.md`):
  - No `.floating-island` header — they're meant to be viewed as partials.
  - Use `padding-top: 20px` on `body` (not `80px` like the root).
  - Keep `id`/`name` attributes identical to `observation.html` so the fusion merge keeps export logic working.
- **Mobile matters.** `simplechecklist.html` is used on phones at the bedside. Don't break the responsive layout or the floating-island header.
- **Don't rename anchors / IDs in `observation.html` casually.** The export functions (`buildObservationText`, `generateTxt`, `generateGoogleDocs`) walk the form by `name=` — renaming silently breaks the report output.

## 6. Fragile Bits & Landmines
- **Filenames with spaces, accents, parentheses are intentional and load-bearing.** Examples: `clinXpert/Général.html`, `clinXpert/ostéoarticulaire.html`, `clinXpert/+++ these interne - observation médicale.docx`, `services/CCI-A (Traumato-ped)/`, `observation_ressources/0. information clinicien/`, `observation - before edit.html`. The `index.html` and `observation.html` link to these exact strings — renaming any of them breaks links silently. Check `index.html:402-425` before "tidying" the `clinXpert/` folder.
- **`backup/` is not auto-deletable.** It contains `index latest.html`, `index old.html`, `v1.html`, `v1.2.html`, `v2.html`, `checklist for mobile.html`, plus `simplechecklist_backup/` and `observation_backup/`. These are the author's manual restore points after a vibe-coding session goes sideways. Do not delete on a "cleanup" pass.
- **`observation - before edit.html` (~178 KB) and `observation_old_but_working caractere.txt` (~158 KB) at the repo root** look like junk but are kept as reference snapshots when accents broke. Leave them.
- **`.gitignore` only excludes two specific PDFs** (in `observation_ressources/1. Sémiologie/` and `organise this/1. Sémiologie/`) — likely copyrighted textbooks the author doesn't want on GitHub. Don't `git add -f` them.
- **`generateGoogleDocs` (`observation.html:3361`) auto-opens `docs.new` in a new tab** ~800ms after the clipboard write. Browsers may block this as a popup if the user didn't trigger via a real click — keep the call inside the click handler chain.
- **`navigator.clipboard.writeText` falls back to a hidden `<textarea>` + `document.execCommand('copy')`** (`observation.html:3367-3372`). The `execCommand` path is deprecated but still works in current browsers; don't rip it out without testing on Safari iOS where the Clipboard API is finicky.
- **The "search bar" in `index.html` uses an inline-defined `autocomplete()` function** (`index.html:444`) and a hardcoded `specialties` array (`index.html:518`). If you add a new service folder, you must also add it to that array, or it won't show up in the search.
- **`services/hemato/ccv.htmlZone.Identifier`** is a Windows ADS leftover from a download — harmless but ugly. Safe to delete; not load-bearing.
- **The `clinXpert` ↔ `clinxpert` casing mismatch** is real. The folder is `clinXpert/` (capital X). Linux deployments (GitHub Pages) are case-sensitive, so any link must match exactly.

## 7. Current State
- **Last shipped:** `idea.txt` added under `services/CCI-A (Traumato-ped)/` (commit `74734ed`); `index.html` rewritten with the new hub layout (chips + collapsible Resources & Modules panel + ClinXpert guides) and Papyrus-styled clinXpert section (commits `97150ce`, `898e7f3`).
- **Working on now:** Adding/refreshing AI context documentation on branch `claude/add-context-documentation-aBKjZ` (this file).
- **Next up** (from `other/idea.txt`, `other/plan.txt`, `other/note to update.txt`):
  1. Build out more service templates under `services/` (start with what `observation.html` already covers, scrub patient names from any sample `ressources/`).
  2. When an ATCD checkbox like HTA / Diabète is ticked, reveal sub-fields for treatment, posologie, nb de prises (per `other/note to update.txt`).
  3. Make `.docx` export actually work — current "Word" path is just clipboard-to-Google-Docs.

## 8. Update Protocol (Verbatim)
> **For the AI Assistant:** When asked to "Update CONTEXT.md":
> 1. Re-run Phase 0 — check for new `GEMINI.md` / `CLAUDE.md` / `.github/` files.
> 2. Re-scan the tree, manifests, and `.github/workflows/` for drift.
> 3. Read our recent conversation for new decisions, fragile bits discovered, or shifted goals.
> 4. Refresh the `_Last synced_` line with today's date and current commit SHA.
> 5. Rewrite — do not append. One clean source of truth. Preserve still-true content, revise the rest.
> 6. Keep §1 and §2 in plain English. Keep the file under ~350 lines.
