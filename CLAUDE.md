# Textbook Context

> Read this first. This is the publishing repo for *How Information Changed the World*, a web textbook for Grade 7 / MYP Year 2 Individuals & Societies at UWC Thailand. The book is live at **https://infotech.brightplanetlabs.com**.

## What This Is

- **Project:** A short web textbook — Prologue + six chapters + Epilogue — tracing how every new information technology follows the same arc: **miracle → ordinary → weaponized**. From the printing press (1450s) to smartphones (now).
- **Audience:** Grade 7 / MYP Year 2 students at UWC Thailand (ages 12–13). All classes include EAL learners — scaffold language without reducing cognitive demand.
- **Author:** Chase Greist, UWC Thailand. Coding beginner — keep technical explanations plain.
- **Status (2026-05-13):** First edition shipped, all nine pages live. Images are still dashed-border placeholders pending sourcing. Editorial review pending.

## Where the Authoring Brief Lives

The editorial brief, the master outline, the unit planner, and the class-side context live in a **separate** repo:

`~/Documents/Cowork Unit Planning/IS-G7/Unit4/1-ClassroomMaterials/Textbook/`

When drafting a new chapter or doing substantial revision, read `_HANDOVER-TO-CLAUDE-CODE.md` in that folder first. `OUTLINE.md` in this repo is a copy of the master outline that lives there.

The split is intentional: planning materials, student data, and lesson plans stay in the private cowork repo; only polished published artifacts live here.

## File Layout

```
.
├── index.html                ← landing page (cover + TOC)
├── 00-prologue.html
├── 01-printing-press.html
├── 02-telegraph.html
├── 03-radio.html
├── 04-television.html
├── 05-internet.html
├── 06-smartphones.html
├── 07-epilogue.html
├── OUTLINE.md                ← copy of the master outline from the authoring repo
├── README.md
├── styles/textbook.css       ← shared design tokens; every chapter <link>s to it
├── scripts/                  ← currently empty
├── images/                   ← chapter images (placeholders until sourced)
└── .github/workflows/deploy.yml
```

`index.html` has its own embedded CSS — it's the only page with a cover layout. Every chapter links to `styles/textbook.css` and has no inline `<style>` block.

## Deploy Pipeline

- **Live URL:** https://infotech.brightplanetlabs.com (also https://infotech-textbook.pages.dev)
- **Hosting:** Cloudflare Pages, project `infotech-textbook`, account `74febbe8ea5813e45be9b0ea4859942d`
- **Trigger:** push to `main` → GitHub Actions runs `.github/workflows/deploy.yml` → `wrangler pages deploy .` → live in ~30s
- **Secrets on the repo:** `CLOUDFLARE_API_TOKEN`, `CLOUDFLARE_ACCOUNT_ID`

You don't need to do anything to deploy — commit and push. Cloudflare strips `.html` extensions automatically (so `/01-printing-press.html` 308-redirects to `/01-printing-press`). Internal `<a href>`s can use either form; the redirect is harmless.

## Local Preview

```bash
python3 .claude/serve.py
# open http://localhost:4401
```

In Claude Code, `preview_start` with name `infotech-textbook` also works (launch config lives at `~/Documents/Projects/.claude/launch.json`). Note: `preview_start`'s bundled server has been unreliable on this machine for `curl`/`fetch` testing — for those, prefer the bash-launched server above.

## Chapter Structure

Every chapter follows Ch 1's 12-part shape, in this order:

1. **Header** — series eyebrow, chapter number ("Chapter Two"), title, subtitle (technology + era)
2. **The Moment** — dramatic opening scene in a `.moment` callout. Drop cap on the first paragraph. Italic burgundy "beat line" (`<p class="nailed">`) somewhere mid-section. 200–300 words.
3. **Before** — what the world looked like before this technology. 150–250 words.
4. **The Tech** — what the invention actually was, in plain language. 150–250 words.
5. **The Ripples** — what changed, including winners, losers, and the seeds of weaponization. 300–400 words.
6. **Voices from the Time** — one primary-source quote in a `.voices` blockquote box.
7. **The Pattern** — explicitly names where the chapter sits on the miracle/ordinary/weaponized arc and connects back to the prior chapter. 150–200 words.
8. **Pattern Tracker SVG** — horizontal timeline with three colored bands plus a faded summary strip of all prior chapters' arcs below. Accumulates across the book.
9. **Now** — **deliberately brief in Ch 1–5** (1–3 sentences, ~25–60 words; no naming of modern technologies). Only Chapter 6 goes fully explicit (~100–150 words).
10. **Key Words** sidebar — 6–8 Tier 2 academic words with EAL-friendly definitions.
11. **Reflect** — exactly 2 questions: one factual, one conceptual/debatable.
12. **Chapter nav** — anchor links to previous and next.

2–3 `<div class="image-placeholder">` blocks are interspersed between the content sections (not all at the top), with precise descriptions and sourcing notes.

Prologue and Epilogue do not follow the 12-part shape; they are shorter framing pages.

## Visual Design — Don't Drift

These are fixed. Don't change without asking.

- **Palette:** parchment `#f6efe1`, dark ink `#2a221b`, accent burgundy `#8a2a2a`. The three Pattern stages have fixed colors: **gold `#e9b94a` = miracle**, **blue-gray `#9aa6b3` = ordinary**, **deep red `#a83c3c` = weaponized**.
- **Fonts:** Cormorant Garamond (display), Lora (body), Inter (labels). Loaded from Google Fonts at the top of every HTML file.
- **Layout:** max content width 760px. Body 19px desktop / 17px mobile. Responsive breakpoint at 640px.

## Editorial Conventions

- **Tone:** narrative, vivid, slightly journalistic. Open with a person, a place, a moment. Then zoom out.
- **Plain-language rule:** whenever a specialized term (Reformation, propaganda, ARPANET, algorithm) appears for the first time, explain it in the body — not just in the Key Words sidebar. The sidebar is reinforcement, not the primary teaching.
- **EAL-friendly without dumbing down:** define hard words inline; use vivid concrete examples; trust students with hard ideas.
- **Diverse historical examples** where natural (Ch 3 includes Rwandan radio; Ch 5 is built around CERN/Berners-Lee in Switzerland; Ch 6 opens with Tahrir Square).
- **Honest about consequences:** the weaponized phase of each chapter is real and shouldn't be softened.

## Image Workflow

Each chapter currently has 2–3 `<div class="image-placeholder">` blocks. To replace one with a real image:

- Use **public-domain or clearly CC-licensed** sources: Wikimedia Commons, Library of Congress, NASA, CERN, FDR Presidential Library, Smithsonian Open Access.
- **No AI-generated images.** These are historical photographs and illustrations.
- Save to `images/` as `chN-NN-shortslug.jpg` (e.g. `ch1-01-luther-95-theses.jpg`).
- Optimize: ≤ 200 KB JPEG, ≤ 1200 px wide.
- Replace the placeholder `<div>` with a `<figure class="image">` containing `<img>` (descriptive `alt`), `<figcaption>` with source and license. Add matching styles to `styles/textbook.css` (mirror the placeholder's spacing but use a soft border + clean caption appropriate for real photography).

## File Naming

- Chapter files: `NN-shortname.html` (`02-telegraph.html`). The long form `IS-G7-Unit4-Chapter2-Telegraph.html` is only used in the authoring repo.
- Image files: `chN-NN-shortslug.{jpg|png|svg}`.
- Never overwrite an existing chapter without explicit OK. Use `_v2` suffix if a major revision needs to coexist with the current version.

## What NOT to Do

- Don't change the visual design or color palette without authorization.
- Don't refactor the deploy pipeline or repo layout.
- **Don't name modern technologies** (TikTok, iPhone, Instagram, the internet by name) in Chapters 1–5. Those are reserved for Chapter 6's explicit reveal.
- Don't soften the "weaponized" phase of any chapter.
- Don't rewrite Chase's prose without flagging the issue first and getting approval.
- Don't commit AI-generated images or images with unclear licensing.
- Don't push uncommitted work in progress; finish the section first.

## Git

- `gh` is authenticated as `chasegreist`. Repo: [chasegreist/infotech-textbook](https://github.com/chasegreist/infotech-textbook) (public).
- Branch: `main`. Push triggers deploy.
- No force pushes. No `--no-verify`. Commit messages should describe the editorial or structural change in one short line.

## Before Starting Any Task

Confirm: (1) which chapter(s) or section, (2) what kind of change (editorial, structural, image, design), (3) whether it should ship live immediately or stage for review. If unclear, ask Chase.
