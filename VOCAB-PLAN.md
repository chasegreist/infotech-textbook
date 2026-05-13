# Tier 2 Vocabulary Pop-ups — Execution Plan

Ready-to-execute spec for adding click-to-define pop-ups on Tier 2 academic vocabulary across the textbook. Mirrors the Phuket textbook implementation, adapted to the infotech palette.

## What's already staged

- `scripts/vocab.js` — new file, already written. Standalone, no external deps. Reads `data-def` from any `<span class="vocab">` and renders a popover positioned next to the word. Handles click, keyboard (Enter/Space/Esc), scroll-to-dismiss, viewport clamping.

## What still needs to land (when image task finishes)

1. CSS block appended to `styles/textbook.css` (snippet below)
2. `<script src="scripts/vocab.js"></script>` inserted before `</body>` in all 8 HTML files
3. Inline `<span class="vocab" data-def="...">word</span>` wraps for ~80 Tier 2 words (lists below)

## Selection principles

- **Tier 2 only** — academic / cross-domain words EAL learners struggle with. Not Tier 3 topic-specific terms (those are in the Key Words sidebar).
- **Skip duplication** — if a word is already in that chapter's Key Words sidebar, do not also tag it inline.
- **First occurrence per chapter** — re-tag across chapters for reinforcement, but only the first occurrence within each chapter.
- **Skip words explained inline** — many bold/italic terms in the prose already get an inline definition (e.g., "indulgences" in Ch 1 is defined in the next sentence). Do not tag those.
- **No pronunciation field** — all picks are English words; the optional `data-pron` from the Phuket version is unused.

---

## CSS to append to `styles/textbook.css`

Drop at the bottom of the file, or directly after the last existing rule block.

```css
/* ============================================================
   Vocab click-to-define
   ============================================================ */

.vocab {
  cursor: pointer;
  border-bottom: 1.5px dotted var(--accent);
  color: inherit;
  position: relative;
  transition: background .15s ease;
  padding: 0 1px;
}
.vocab:hover,
.vocab:focus {
  background: rgba(138, 42, 42, .10);
  outline: none;
}
.vocab.is-open {
  background: rgba(138, 42, 42, .15);
}

.vocab-pop {
  position: absolute;
  z-index: 1000;
  max-width: min(320px, calc(100vw - 16px));
  background: var(--bg);
  border: 1px solid rgba(42, 34, 27, .35);
  padding: .85rem 1rem;
  font-family: 'Lora', Georgia, 'Times New Roman', serif;
  font-size: 16px;
  line-height: 1.5;
  color: var(--ink);
  box-shadow: 3px 4px 0 rgba(42, 34, 27, .12);
  animation: vocab-fade-in .15s ease-out;
}
.vocab-pop::before {
  content: "";
  position: absolute;
  inset: 3px;
  border: 1px solid rgba(42, 34, 27, .12);
  pointer-events: none;
}
@keyframes vocab-fade-in {
  from { opacity: 0; transform: translateY(-2px); }
  to   { opacity: 1; transform: translateY(0); }
}
.vocab-pop-term {
  font-family: 'Inter', sans-serif;
  font-size: 11px;
  letter-spacing: .22em;
  text-transform: uppercase;
  color: var(--accent);
  font-weight: 600;
  margin-bottom: .4rem;
}
.vocab-pop-def {
  color: var(--ink);
}
```

Design choices vs Phuket: Inter (not JetBrains Mono) for the term label to match infotech's `.series`/`.label` typography. Lora for the definition body to match the textbook's reading font. Accent burgundy from infotech's palette.

---

## Script tag to add to each HTML file

Insert one line just before `</body>` in:

- `00-prologue.html`
- `01-printing-press.html`
- `02-telegraph.html`
- `03-radio.html`
- `04-television.html`
- `05-internet.html`
- `06-smartphones.html`
- `07-epilogue.html`

(`index.html` doesn't need it — no body prose.)

```html
<script src="scripts/vocab.js"></script>
```

---

## Word lists per chapter

Each row: word — definition — locator phrase (substring of the chapter that uniquely contains the word to be wrapped). When executing, `Edit` will find the locator phrase and wrap just the bolded word with `<span class="vocab" data-def="...">word</span>`.

### `00-prologue.html` (5 words)

| Word | Definition | Locator phrase |
|---|---|---|
| **specific** | one particular kind, not all kinds | "But for one **specific** kind: the kind that gives humans" |
| **predictions** | guesses about what will happen in the future | "full of grand **predictions** about how the new technology" |
| **frighten** | make someone afraid | "To **frighten** them. To unite them" |
| **unite** | bring people together so they act as one | "To **unite** them against an enemy" |
| **convince** | get someone to believe or agree | "or to **convince** them their neighbours are dangerous" |

### `01-printing-press.html` (12 words)

Already in this chapter's Key Words sidebar (do NOT tag inline): indulgences, vernacular, monopoly, pamphlet, Reformation, propaganda, obsolete, distribution.

| Word | Definition | Locator phrase |
|---|---|---|
| **bewildered** | confused; unable to make sense of what is happening | "Luther himself is **bewildered**. He later wrote" |
| **circulating** | being passed from one person to another | "copies of his 95 Theses are **circulating** in cities across Germany" |
| **scholars** | people who study a subject very deeply | "university **scholars** post arguments there all the time" |
| **institution** | a large, long-established organization, like a church, school, or government | "Most knowledge — and most power — lived inside one **institution**" |
| **assemble** | put something together piece by piece | "what if you could *assemble* a page" — note: word is already italicized in the prose; wrap span around the `<em>` |
| **viral** | spreading very fast from person to person, like a virus | "He became, in modern terms, the first **viral** author." |
| **scribes** | people whose job was to copy books and documents by hand | "A medieval **scribe** could produce maybe four" — first occurrence is "scribe" (singular), in The Tech section |
| **crumble** | slowly fall apart | "watching its monopoly on knowledge **crumble**, fought back" |
| **forbidden** | not allowed | "*Index of Forbidden Books* — a long, growing list of titles Catholics were **forbidden** to read" |
| **fueled** | gave energy or strength to | "Religious wars rolled across Europe for over a century, **fueled** in part by cheap printed propaganda" |
| **massacre** | the killing of a large number of people at one time | "The 1572 St. Bartholomew's Day **Massacre** in France" |
| **breathtaking** | so amazing or beautiful it makes you stop and stare | "A new and **breathtaking** thing" |

Note on **assemble**: the word appears as `<em>assemble</em>`. To wrap with vocab: `<span class="vocab" data-def="..."><em>assemble</em></span>`.

Note on **scribe** vs **scribes**: first occurrence is "A medieval scribe could produce maybe four." Tag that single instance.

### `02-telegraph.html` (12 words)

Already in this chapter's Key Words sidebar (do NOT tag inline): telegraph, transmit, transatlantic, simultaneous, scarcity, infrastructure, journalism, propaganda.

| Word | Definition | Locator phrase |
|---|---|---|
| **obsessed** | thinking about something all the time, unable to let it go | "fifteen years **obsessed** with a single question" |
| **identical** | exactly the same | "his assistant Alfred Vail is waiting with an **identical** machine" |
| **advantage** | something that helps you do better than others | "a real **advantage** over everyone else" |
| **arrangement** | the way things are set up or organized | "That whole **arrangement** was about to end." |
| **crisscrossed** | went across in many directions, forming a pattern of crossing lines | "Within a decade, they **crisscrossed** Europe." |
| **fragile** | easily broken or damaged | "slow, **fragile**, but real" |
| **transformed** | completely changed | "**Stock markets** transformed almost overnight" — first transform is here (inside `<strong>` block) — easier: pick first solo "transformed" → "transformed almost overnight" |
| **absurd** | so unreasonable it seems silly | "The telegraph made this **absurd**: a train schedule could not work" |
| **lurid** | shockingly violent or sensational, often made worse than reality | "Reporters in Havana telegraphed back **lurid**, sometimes invented atrocity stories" |
| **sensational** | designed to shock or excite people, often by exaggerating | "**sensational**, wire-fed, often false stories" |
| **manipulate** | unfairly control or influence someone | "to **manipulate** public opinion at home" |
| **forged** | fake; made to look real but isn't | "**forged** 'intercepted' telegrams" |

Note on **transformed**: the chapter has four bolded headings using "transformed" — easiest to wrap "transformed" inside the first "**Stock markets** transformed almost overnight" sentence. Wrap only the word, leaving the `<strong>` tag for "Stock markets" alone.

### `03-radio.html` (12 words)

Already in Key Words: wireless, broadcast, mass medium, audience, simultaneous, regulation, propaganda, genocide.

| Word | Definition | Locator phrase |
|---|---|---|
| **distress** | great trouble or danger | "the captain bursts in and orders them to begin sending **distress** calls" |
| **monitor** | watch or check something carefully and continuously | "a radio that nobody **monitored** was a radio that did nothing" — first form is "monitored"; tag that |
| **tragedy** | a terrible event, especially one causing many deaths | "the international maritime safety treaties still in force today trace their roots to a **tragedy**" |
| **vibrations** | quick small movements back and forth | "invisible **vibrations** of the electromagnetic field" |
| **detect** | notice or discover something that's hard to see | "could **detect** those waves and convert them back" |
| **faint** | weak; hard to hear or see | "Marconi received a single **faint** signal" |
| **exaggerated** | made to sound bigger or more dramatic than it really was | "much of that 'panic' story was **exaggerated**" |
| **reckless** | careless about danger; not thinking about consequences | "happy to make it look **reckless**" |
| **rallies** | large public meetings, usually political | "His **rallies** — chanting crowds, marching music" |
| **slogans** | short catchy phrases used to push an idea | "screamed **slogans** — were piped directly into millions of living rooms" |
| **casual** | relaxed; treated as if it were no big deal | "described it all in cheerful, **casual** tones" |
| **compress** | squeeze something into a smaller space or shorter time | "Each new information technology seems to *compress* the timeline" |

Note on **compress**: word is already italicized. Wrap as `<span class="vocab" data-def="..."><em>compress</em></span>`.

### `04-television.html` (12 words)

Already in Key Words: medium, broadcast, footage, perception, unify, fragment, partisan, charisma.

| Word | Definition | Locator phrase |
|---|---|---|
| **candidates** | people who are running for an elected job | "the presidential **candidates** of both major parties" |
| **policy** | the plans and decisions of a government or organization | "the two men argue **policy**: the economy" |
| **verdict** | a final decision or judgement about something | "Same words. Different medium. Different **verdict**." |
| **legend** | a famous old story, often partly true and partly exaggerated | "The story may be part **legend** — the radio survey was small" |
| **grainy** | (of a picture) rough-looking, with visible dots; not sharp | "watched a **grainy** black-and-white image" |
| **collapsed** | suddenly fell apart or failed | "Public support for the fighting **collapsed**." |
| **manifestos** | public written statements of what a person or group believes | "arguments, plans, written **manifestos**" |
| **vicious** | extremely cruel or violent | "A famous 1988 ad called 'Willie Horton' was so **vicious**" |
| **anchor** | the main person who presents a TV news programme | "the CBS **anchor** Walter Cronkite" |
| **civic** | to do with the public life of a town, city, or country | "a shared, mostly neutral **civic** space" |
| **neutral** | not on either side; balanced and fair | "openly aimed at a politically partisan audience" — wait, "neutral" appears as "mostly neutral civic space" — tag in the same sentence as civic |
| **leaned** | tilted toward one side (here: politically) | "Some **leaned** right. Some leaned left." |

Note: pick "neutral" from "mostly neutral civic space" — separate vocab span from "civic" in the same paragraph.

### `05-internet.html` (12 words)

Already in Key Words: network, ARPANET, packet, protocol, hyperlink, browser, infrastructure, public domain.

| Word | Definition | Locator phrase |
|---|---|---|
| **acknowledges** | shows that it has noticed or received something | "The Stanford machine **acknowledges** it." |
| **dedicated** | set aside for one specific purpose only | "opening a single **dedicated** wire path between caller and listener" |
| **destination** | the place something is being sent or going to | "Each packet was labelled with its **destination** and a number." |
| **reassembled** | put back together after being taken apart | "the packets were **reassembled** into the original message" |
| **proposal** | a written plan suggesting an idea | "wrote a 20-page **proposal** called *Information Management: A Proposal*" |
| **vague** | not clear or exact | "His boss famously scribbled on the cover: '**Vague** but exciting.'" |
| **archive** | a place where old documents or recordings are kept safely | "It survives today in a UCLA **archive**." |
| **startup** | a small new company, usually in technology | "a small American **startup** called Google" |
| **investors** | people who put money into a company hoping to earn more back | "**investors** poured enormous sums of money" |
| **vanished** | disappeared, often suddenly | "trillions of dollars **vanished** within a few months" |
| **patented** | got the legal right to be the only one allowed to make or sell an invention | "He could have **patented** his idea" |
| **licensed** | gave (or received) official permission to use something | "**licensed** it to companies" |

### `06-smartphones.html` (11 words)

Already in Key Words: platform, algorithm, viral, misinformation, surveillance, attention economy, addiction, democracy.

| Word | Definition | Locator phrase |
|---|---|---|
| **corrupt** | using power dishonestly for personal gain | "His government is famously **corrupt**, famously brutal." |
| **brutal** | extremely cruel and violent | "famously corrupt, famously **brutal**" |
| **uprising** | when a large group rises up against a government | "When a smaller **uprising** in next-door Tunisia" |
| **toppled** | knocked over; forced out of power | "toppled its own dictator in early January 2011" |
| **dictator** | a ruler who has total power, usually achieved by force | "toppled its own **dictator** in early January 2011" |
| **unveiling** | showing or revealing something for the first time | "he was **unveiling** three new products" |
| **fundamentally** | in a deep, important, basic way | "a **fundamentally** new kind of information technology" |
| **inflammatory** | designed to make people angry | "and **inflammatory** posts during the U.S. presidential election" |
| **conspiracy** | a secret plan, often to do something harmful or illegal | "**conspiracy** movements began to organize" |
| **compulsive** | done over and over, hard to stop, even when you want to | "as **compulsive** as the law allowed" |
| **deceive** | make someone believe something that isn't true | "AI-generated fakes designed to **deceive** everyone" |

Note: **toppled** and **dictator** are in the same sentence. Two separate vocab spans, one for each word.

### `07-epilogue.html` (4 words)

Already in Key Words (final consolidation): miracle stage, ordinary stage, weaponized stage, pattern, information technology.

| Word | Definition | Locator phrase |
|---|---|---|
| **summative** | a task at the end that sums up everything you've learned | "For your **summative** task, pick a technology" |
| **adoption** | when people start using something widely | "rates that line up suspiciously well with its **adoption** curve" |
| **suspiciously** | in a way that makes you wonder if something is wrong | "rates that line up **suspiciously** well" |
| **predict** | say what you think will happen | "and **predict**, with evidence from this book, how its 'weaponized' stage might look" |

Note: **adoption** and **suspiciously** are in the same sentence — two separate spans.

---

## Total

| File | Words tagged |
|---|---|
| 00-prologue | 5 |
| 01-printing-press | 12 |
| 02-telegraph | 12 |
| 03-radio | 12 |
| 04-television | 12 |
| 05-internet | 12 |
| 06-smartphones | 11 |
| 07-epilogue | 4 |
| **Total** | **80** |

---

## Execution checklist (when image task is finished)

1. `git pull` (or confirm working tree is up to date with whatever the image task committed).
2. Append the CSS block to `styles/textbook.css`.
3. For each of the 8 HTML files, add the `<script src="scripts/vocab.js"></script>` line before `</body>`.
4. For each HTML file, perform `Edit` operations to wrap the words from the lists above with `<span class="vocab" data-def="...">word</span>`.
5. Local preview check: open Ch 1 in the browser, click a few dotted words, verify popover styling, positioning, dismissal behaviors.
6. Commit and push — Cloudflare auto-deploys.

---

## Conflict surface with the image task

| File | Image task likely touches? | This task touches? | Conflict risk |
|---|---|---|---|
| `scripts/vocab.js` | No | Already created | None |
| `styles/textbook.css` | Yes (adds figure/img styles) | Yes (appends vocab styles) | Low — both append; resolve any merge by keeping both blocks |
| `*.html` (×8) | Yes (replaces `<div class="image-placeholder">` with `<figure class="image">`) | Yes (wraps inline words, adds script tag) | Low — different regions of each file. Run this task AFTER image task commits, then `git pull` first |
| `images/` | Yes | No | None |

Bottom line: as long as this task runs after the image task commits and pulls first, conflicts are unlikely. The two tasks edit disjoint regions of the shared files.
