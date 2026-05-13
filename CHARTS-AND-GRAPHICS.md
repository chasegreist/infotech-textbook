---
document: Charts and Graphics Proposal — How Information Changed the World
audience: Chase (author)
reviewer: Claude (research pass)
date: 2026-05-13
status: ideas + datasets identified; awaiting selection before any are built
---

# Charts and Graphics Proposal

A short menu of charts and tables that could strengthen the textbook's argument and give G7 / MYP Y2 students concrete evidence they can manipulate themselves. Two kinds of suggestions are mixed here:

- **Source (S)** — an existing chart on the open web with a clear license, drop into a `<figure>` with attribution.
- **Build (B)** — open data exists and we can render it as inline SVG in the book's existing visual idiom (no JS, matches the Pattern Tracker aesthetic, prints cleanly).

The goal isn't to add many charts. It's to find the 3–5 that pay off the most for student understanding. I've flagged my top picks at the bottom.

---

## The single chart this book most needs

**B1. Time-for-each-technology-to-reach-50-million-users.** This is the canonical "compression" chart that supports the entire through-line. The book *tells* readers the arc is speeding up; this chart *shows* them.

| Technology | Years to 50M users |
|---|---|
| Telephone | 75 |
| Radio | 38 |
| Television | 13 |
| Internet | 4 |
| Facebook | 3.5 |
| YouTube | 4 |
| Instagram | 2.5 |
| TikTok | 0.75 |
| ChatGPT | 0.2 (~2 months) |

- **Data source:** Numbers vary slightly by source. Cleanest published version is Visual Capitalist's "Time taken to reach 50 million users" infographic, but the underlying numbers come from MIT Technology Review, Statista, and UN ITU. For the *book* I'd build this from scratch using ITU and Pew adoption tables rather than reproducing someone else's infographic.
- **Where it goes:** Either in the Prologue (as a teaser for the compression theme) or in the Epilogue (as the payoff). Recommendation: Epilogue, alongside the "All Six Arcs" stacked SVG.
- **Visual:** horizontal bars sorted longest-to-shortest. Bars in the book's gold-blue-red palette would be wrong (those colors mean miracle/ordinary/weaponized in the rest of the book). Use neutral parchment + ink.
- **Effort:** small. ~80 lines of SVG, all hand-coded. I can produce this from scratch.

**This is the chart most worth adding.** It's the empirical spine of the book's main claim.

---

## Other "build" candidates, in priority order

### B2. Books printed in Europe per decade, 1450–1700

- **Why it pays off:** Currently the chapter cites "8 to 20 million books by 1500." A small SVG bar chart would let students *see* the explosion — and see that it kept compounding past 1500.
- **Data source:** Eltjo Buringh and Jan Luiten van Zanden, "Charting the 'Rise of the West': Manuscripts and Printed Books in Europe, A Long-Term Perspective from the Sixth through Eighteenth Centuries" (*Journal of Economic History*, 2009). Their dataset is public; Our World in Data has rendered a version (https://ourworldindata.org/books) under CC-BY.
- **Where it goes:** Ch 1, *The Tech* section.
- **Effort:** small. ~60 lines SVG.

### B3. US radio sets per 100 households, 1922–1945

- **Why it pays off:** The chapter says "by 1930, more than half of American homes had a radio." A small chart shows the *speed* of that uptake — important for the "miracle to ordinary" compression argument.
- **Data source:** US Census historical tables; reproduced in many history-of-media texts. Cleanest: Sterling & Kittross, *Stay Tuned: A History of American Broadcasting*. Open CSV via Census Bureau historical statistics.
- **Where it goes:** Ch 3, *Ripples* section, after the FDR paragraph.
- **Effort:** small.

### B4. US TV households 1948–1980 + cable channels available 1980–2000

- **Why it pays off:** Two stacked mini-charts that compress Ch 4's whole timeline into one frame. The TV-households curve goes up sharply 1948–1960 (miracle/ordinary); the cable-channels-available curve goes up sharply 1980–2000 (the fragmentation that produces the weaponized phase).
- **Data source:** Nielsen historical reports (publicly available summaries); FCC archives; A.C. Nielsen "TV Universe Estimates" series. Sterling & Kittross again.
- **Where it goes:** Ch 4, *Ripples* section.
- **Effort:** medium (two charts paired).

### B5. Global internet users, 1990–2025

- **Why it pays off:** Currently nothing in Ch 5 shows the absolute scale. A simple curve from 1990 (a few million users worldwide) to 2025 (~5.5 billion) drives the "miracle to ordinary" compression home.
- **Data source:** UN International Telecommunication Union (ITU), `https://www.itu.int/en/ITU-D/Statistics/Pages/stat/default.aspx` — open CSV. Mirror at Our World in Data (CC-BY).
- **Where it goes:** Ch 5, *Ripples* section.
- **Effort:** small.

### B6. Smartphone adoption by world region, 2007–2024

- **Why it pays off:** Directly fixes the F6.1 factual error in REVIEW.md (the "by 2012, most adults on Earth carried a smartphone" line). A regional adoption chart makes the actual story clear: US and Europe ~2012, China ~2015–17, South Asia and Sub-Saharan Africa ~2018–22.
- **Data source:** GSMA Mobile Economy reports (open); Pew Research Center Global Attitudes Survey; ITU. Our World in Data has a clean version.
- **Where it goes:** Ch 6, *The Tech* section, replacing the bad sentence with a "look at the curve" reference.
- **Effort:** medium (multi-line chart).

### B7. Local US newspaper deaths, 2004–2024

- **Why it pays off:** Ch 6 says "local newspapers, gutted as their advertising revenue moved to the platforms." A small map or bar chart of newspaper closures would make this concrete.
- **Data source:** UNC Hussman School / Penny Abernathy, "The State of Local News" (annual report, open PDF + CSV).
- **Where it goes:** Ch 6, *Ripples* section.
- **Effort:** medium.

### B8. Adolescent mental-health indicators vs. smartphone adoption, 2007–2024

- **Why it pays off:** Ch 6 currently asserts "Mental-health rates for adolescents, especially girls, worsening in step with the rise of the apps." A chart would substantiate this — but this is also the most empirically and pedagogically delicate item on the list. Causation is contested; the correlation is real. **If we build it, we hedge the claim explicitly.**
- **Data source:** CDC Youth Risk Behavior Survey (open); Jean Twenge's published datasets; Jonathan Haidt's *The Anxious Generation* data appendix (open).
- **Where it goes:** Ch 6, *Ripples* section, with a hedged caption.
- **Effort:** medium.
- **Flag for Chase:** I'd suggest this is the one to think hardest about including. A 12-year-old reading this in 2026 is *inside* this data point. It's powerful, and dangerous; it can be empowering or distressing. Worth a conversation.

---

## "Source" candidates (existing charts on the web)

These are charts that already exist and are good. We could link or embed (with attribution).

### S1. Our World in Data — *Books published per year before the printing press*

- **URL:** https://ourworldindata.org/books
- **License:** CC-BY 4.0
- **Use:** Ch 1. Strongest alternative to B2 above if I don't build one from scratch.

### S2. Our World in Data — *Number of internet users since 1990*

- **URL:** https://ourworldindata.org/internet
- **License:** CC-BY 4.0
- **Use:** Ch 5 or Ch 6. Direct replacement for B5.

### S3. SubmarineCableMap.com — global submarine cable map (live)

- **URL:** https://www.submarinecablemap.com
- **License:** Terms permit non-commercial educational use; attribution required. Not strictly CC, but routinely used in textbooks and academic publishing.
- **Use:** Ch 2 or Ch 5. Paired with the 1858 cable map (IMAGES-PROPOSAL.md Ch 2 Image 2), this is a stunning visual: the 1858 cable's descendants now wrap the planet. Two images, side by side, 160 years apart.
- **Recommendation:** A static screenshot of the 2024 map paired with the 1858 map in the Epilogue, captioned "The descendants of the cable that worked for three weeks." Worth pursuing.

### S4. Pew Research — Smartphone Ownership by Country, 2024 update

- **URL:** https://www.pewresearch.org/internet/fact-sheet/mobile/
- **License:** Pew permits non-commercial educational use with attribution.
- **Use:** Ch 6. Could replace B6 above.

---

## Tables that could replace placeholders or improve continuity

These aren't charts, but they're "graphics" in the broader sense — and tables print very well in the book's existing style.

### T1. "What did each new technology kill?" — comparative table

A simple 2-column table running across all six chapters: technology → "who lost." Already implicit in the chapters; making it explicit in the Epilogue (alongside the existing "Six Stories, Side by Side" recap) sharpens the I&S "winners and losers" framing.

| Technology | Who lost |
|---|---|
| Printing press | Scribes, the Catholic Church's monopoly on knowledge |
| Telegraph | Town criers, slow weekly papers, message-runners |
| Radio | The idea that politics is mostly written words |
| Television | The radio prime-time audience; written political argument |
| Internet | Encyclopedias, travel agents, video stores, classified ads |
| Smartphones | Local newspapers, teenage attention spans, possibly democracy |

- **Effort:** trivial; just inline HTML.
- **Where:** Epilogue, after the existing recap table.

### T2. Speed of news, 1517 → 2011 — concrete examples table

| Year | Story | How fast it spread |
|---|---|---|
| 1517 | Luther's 95 Theses, Wittenberg → Rome | 4 weeks |
| 1865 | Lincoln assassinated, Washington → London | 12 days (no cable yet) |
| 1866 | Lincoln assassinated, if cable had worked | minutes (after 1866) |
| 1912 | Titanic SOS | seconds (radio); hours (newspapers) |
| 1969 | First Moon step | live (TV) |
| 2011 | Mubarak's resignation | seconds (Twitter) |

- **Effort:** trivial.
- **Where:** Prologue or Epilogue. Pairs well with B1.

---

## My top recommendations

If I were building only three of these, I'd build:

1. **B1 (50-million-user chart)** — biggest argumentative payoff. The book's central claim made visual.
2. **B6 (smartphone adoption by region)** — fixes the one outright factual error in the book and replaces it with something better.
3. **T2 (speed-of-news table)** — trivial to build, enormous concrete-comparison value. Pairs with B1 in either Prologue or Epilogue.

If a fourth gets added, **S3 (submarine cable map past-and-present)** would be the dramatic visual closer of the Epilogue.

**The one to think hardest about: B8 (teen mental health).** It's the most pedagogically powerful chart in this list, and the most ethically loaded. I'd want to talk through how it's framed before building it.

---

## What I'd like you to react to

1. **Which of these (if any) get built?** A simple "yes B1, yes B6, yes T2, skip the rest for now" is plenty.
2. **B8 specifically — yes, no, defer?**
3. **Where do you want B1 to live — Prologue or Epilogue?** I lean Epilogue (payoff), but Prologue has its own logic (set up the compression claim early).
4. **Implementation style.** All charts I build will be inline SVG in the book's existing visual idiom (parchment background, Cormorant + Lora + Inter fonts, no JS), matching the Pattern Tracker pages so they print cleanly and don't slow down page loads. If you prefer a different approach (an embedded Datawrapper / Flourish iframe, for instance), say so before I start.
