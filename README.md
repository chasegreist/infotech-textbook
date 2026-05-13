# How Information Changed the World

A short web textbook for Grade 7 Individuals & Societies (MYP Year 2) at UWC Thailand.

Six story-driven chapters tracing how each new information technology — from the printing press to the smartphone — has followed the same arc: **miracle → ordinary → weaponized**. The pattern has been running for five hundred years.

**Live:** [infotech.brightplanetlabs.com](https://infotech.brightplanetlabs.com)

## Structure

```
.
├── index.html                  ← landing page / cover + table of contents
├── 01-printing-press.html      ← Chapter 1 (complete)
├── OUTLINE.md                  ← master outline for all chapters
├── styles/textbook.css         ← shared design tokens (used by future chapters)
├── scripts/                    ← shared client-side JS (currently empty)
├── images/                     ← chapter images
└── .github/workflows/deploy.yml ← auto-deploy to Cloudflare Pages on push
```

## Local preview

```bash
python3 .claude/serve.py
# then open http://localhost:4401
```

## Deploy

Pushes to `main` auto-deploy via GitHub Actions → Cloudflare Pages (project `infotech-textbook`). The workflow file is at `.github/workflows/deploy.yml`.

## Authoring

The full editorial brief, design conventions, and chapter outline live in `OUTLINE.md`. The handover document in the source repo (`cowork-unit-planning`) is the canonical brief for new chapter drafts.

---

By Kru Chase · UWC Thailand · A [Bright Planet Labs](https://brightplanetlabs.com) publication.
