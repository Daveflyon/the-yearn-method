# The Yearn Method — Status & Handover

If you're reading this because you've opened this folder fresh, this file is everything: what it is, what's open, what's next, and the full history — no other doc in this folder to check.

## What this actually is

The Yearn Method is a classroom hook technique Dave devised for Miriam Agyei to use in her HLTA (Higher Level Teaching Assistant) role at Landau, teaching post-GCSE SEN learners Functional Skills English and Maths. Named after Antoine de Saint-Exupéry's line: "If you want to build a ship, don't drum up the men to gather wood, divide the work, and give orders. Instead, teach them to yearn for the vast and endless sea."

The mechanic: Miriam reads a quote or fact aloud without naming who it's from. The class guesses. If nobody gets it, she holds the tension — "I'll tell you after class" — rather than telling them straight away. She reveals the person, tells the story of a teacher (or education-related turning point) who made a difference for them, then ties it straight into that day's lesson. Repeated across a term, it becomes Miriam's signature rather than a one-off trick.

This folder contains the actual tool: a single self-contained HTML file that runs the whole ritual for her — an informational arc explaining the method, a working story generator (pick a subject or let it choose, get the quote/reveal/teacher-story/lesson tie-in), an A-Z Who's Who reference with searchable bios and achievement highlights, and a rule-based feedback logging tool (no live AI, no API costs, works offline).

Last updated 8 Sep 2026, after the sticky top bar was split into two separate Expand all / Minimise all buttons, replacing the earlier single toggle button.

## Files in this folder

- `index.html` — the whole tool. Single file, no build step, no external dependencies.
- `CLAUDE.md` — points here; read by Claude Code automatically on opening this folder.
- `01-status-handover-yearn-method.md` — this file.
- `.gitignore` — keeps build tooling out of the repo.

## Where it lives

- **Live URL:** https://yearnmethod.pages.dev — always live, bookmarkable, works on Miriam's phone.
- **Hosting:** Cloudflare Pages (not Workers — see the historical log for why that distinction mattered during setup), auto-deploys on every push to the GitHub repo.
- **GitHub repo:** github.com/Daveflyon/the-yearn-method, `main` branch.

## How it's built

Everything — HTML, CSS, JS — lives in the one `index.html` file. Built to Dave's HTML Output Design System (navy #1F3864, Arial, collapsible `<details>` sections, callout boxes). Story data lives in a single JS array (`stories`) near the bottom of the file; each entry has an id, name, profession, subject tag, quote, teacher-story, lesson tie-in, source link, bio, bio quote with its own source, and an achievements array (3–5 bullets). All content is real, sourced and checkable — nothing invented. Currently 18 people in the story bank, spanning English, Maths and General/Education tags. Every quote also carries a short inline `quoteContext` (where/when it was said), shown directly under the quote in the generator, in addition to the full sourced link.

The Who's Who & Story Bank section (section 5) is built dynamically from that same `stories` array at page load: it populates the A-Z bio cards, a describe-your-task search box (multi-term scored search across name/profession/bio/quotes/achievements), a plain live filter, and the Story Bank summary table — so adding a new person to the array is the only edit needed; nothing else needs touching by hand.

## How to deploy a change

1. Edit `index.html` in this folder directly.
2. Test locally first (Playwright headless-browser check is the established pattern — open the file, click through the generator, run both search boxes, check mobile viewport, confirm zero console errors) before anything goes live.
3. `git add index.html && git commit -m "..." && git push origin main` from this folder.
4. Cloudflare Pages auto-rebuilds on push, usually live within 30–60 seconds.
5. Verify the live site directly (browser navigate + screenshot or page-text check) rather than assuming the push worked — this project's standing rule is "we don't guess, we check things."

## Still open, not urgent

| Item | Why it's open | Key notes | Next review |
|---|---|---|---|
| GitHub token embedded in plaintext in the git remote URL | Functional as-is; flagged once earlier in the project and deliberately not re-raised per Dave's standing instruction not to loop on this | Push/pull both work correctly today | If the repo is ever made public, shared with anyone else, or the token's 90-day expiry approaches |
| Story bank sourcing standard | Pop-culture relatability was deliberately prioritised over strict academic/direct-quote accuracy, per Dave's explicit instruction — not every entry has a direct "celebrity credits a teacher" quote | Not a gap — an agreed, documented standard (see "Decisions made" below) | If a new person is added and the sourcing standard needs re-checking |

## What to do next

- [ ] Confirm with Miriam that yearnmethod.pages.dev works for her on her actual phone, not just in testing
- [ ] Watch the GitHub token's 90-day expiry and regenerate before it lapses, or the auto-deploy pipeline breaks silently
- [x] Anxiety angle addressed — Lucy Bronze added (anxiety, dyslexia, ADHD, autism, all first-person and sourced). Worth keeping an eye on whether Miriam feels this covers the gap she noticed, or whether a second, more explicitly mental-health-framed entry is still wanted.
- [ ] Optional: revisit Larry Mullen Jr. (dyscalculia) and Robbie Williams (dyslexia/dyscalculia/ADHD/autism/Tourette's) for a future story-bank pass — both researched, both held back for now (see historical log, 8 Sep 2026 entry)

## Progress

- Live and verified at yearnmethod.pages.dev, on Cloudflare Pages (confirmed genuine `.pages.dev`, not `.workers.dev`).
- 18 story-bank entries (up from an original 9): Adele, Jay-Z, John Legend, Ian Wright, Stormzy, Marcus Rashford, Rihanna, Billy Joel, Lizzo, Dua Lipa, Tom Holland, Lewis Hamilton, Ed Sheeran, Richard Branson, Zayn Malik, Maya Hawke, Susan Boyle, Lucy Bronze.
- Every entry now has a `quoteContext` field, rendered as a short bracketed line directly under the main quote in the generator (e.g. "(in an England Football Mental Health Awareness Week interview)") — a quick sourcing snapshot in the flow, separate from the full "Source: [link]" citation that still sits below.
- All sections now default to collapsed on page load (previously "What This Is" and "Pick Today's Story" opened by default). The single expand/collapse toggle button went through two iterations and is now two separate, always-fixed-function buttons — "Expand all sections" and "Minimise all sections" — sitting side by side in a sticky bar pinned to the top of the viewport, always visible regardless of scroll position. No toggling or label-switching logic remains; each button always does the same thing. Added 90px of bottom padding to the page so the last section always clears the fixed top bar and the "Jump to" button bottom-right.
- Gap fixed above the "Used X of Y stories" progress line in the generator (margin-top increased on `.progress-note`).
- Duplicated Saint-Exup\u00e9ry quote removed from Section 1 body (it already appears once in the page-top quote block); replaced with a one-line reference back to it.
- Section 5 ("Who's Who & The Story Bank") merged from two former separate sections, with a describe-your-task search box, a plain filter, an A-Z index, profession tags per person, and 3–5 achievement bullets per person.
- Every section renumbered sequentially (1–6), no sub-numbering.
- Subtitle changed to "Teaching them to yearn for the vast and endless sea," with the full Saint-Exupéry quote and attribution added as its own block.
- "What This Is" section expanded with new introductory content, original content kept intact.
- "Why It Works" renamed "How It Works."

## Decisions made

- Hosted on Cloudflare Pages under the name `yearnmethod` (not `.workers.dev`), deployed via the direct Pages-specific import flow after two accidental Worker deployments during setup.
- Pop-culture relatability prioritised over strict academic/direct-quote accuracy for the story bank, given the teenage SEN audience — a "fairly generous" standard applies where a direct teacher-credit quote isn't available (self-taught journeys, mentorship, scholarships all count if genuine and sourced).
- Requested Cloudflare Pages name `yearnmethod` chosen after confirming `yearn.pages.dev` alone was already taken by an unrelated site.
- Feedback logging tool is rule-based, not live-AI, so the tool works fully offline with no ongoing API costs or key management.
- Iterative UI/CSS/JS tweaks to index.html (button behaviour, layout fixes, small logic corrections) go through Dave's local Claude Code session in VS Code directly, not this remote session's device bridge — direct filesystem access means no staging round-trip and tighter, more inspectable diffs. This remote session stays the right tool for research, sourcing, cross-file work, and anything needing its broader toolset (web search, Playwright verification, live-site checks).

## Risks or blockers

- None currently blocking. The GitHub token embedded in the git remote is a standing minor risk (see open items table) but not blocking any current work.

## Historical log

- **8 Sep 2026 (two separate expand/minimise buttons; local Claude Code adopted for precision tweaks)** — The single expand/collapse-all button (previous entry, floating bottom-left) turned out unreliable in practice: Dave found that if a section was opened or closed individually by clicking its own header, the button's label could show "Expand all" when he actually wanted to collapse everything, requiring him to read the label state rather than just act. Replaced entirely: the button is now a sticky bar pinned to the top of the viewport (not floating bottom-left) containing two separate, always-fixed-function buttons — "Expand all sections" and "Minimise all sections" — with all label-switching/state-checking logic (`syncExpandAllLabel` and its toggle listeners) removed. Each button always does the same thing regardless of current section states. This change was made directly in Dave's local Claude Code session in VS Code (commit `66e8db4`, following an interim sticky-bar-with-synced-label fix in commit `aae83ef` that solved the positioning complaint but not the label-reliability one) rather than through this remote session's device bridge. Both Dave and this session agreed going forward that precision UI/CSS/JS tweaks to index.html are better done through his local Claude Code session — same model, but direct filesystem access removes the staging round-trip this remote session's device bridge otherwise requires, giving tighter and more inspectable diffs. Verified live on yearnmethod.pages.dev after the fix.
- **8 Sep 2026 (floating controls + Lucy Bronze + inline quote sourcing)** — Moved the Expand/Collapse-all button from a static row above Section 1 to a floating fixed-position button (bottom-left, mirroring the existing "Jump to" button bottom-right) after Dave flagged that a top-of-page-only control is useless once you've scrolled down. Shortened both floating buttons' labels and padding so they sit compactly in the corners rather than spanning wide enough to obscure page content; added bottom padding to the page so the last section always has room to clear them. Researched anxiety/mental-health-in-education more thoroughly after Dave pushed back on the first pass being too quick to call it thin territory — found Lucy Bronze (England international, Euro 2022 and Euro 2025 winner, most decorated English footballer in the women's game), who has spoken first-person about anxiety and dyslexia at school (England Football, Mental Health Awareness Week 2023) and, more recently, about being diagnosed with ADHD and autism as an adult, calling it her "superpower" on the pitch (Yahoo Sports/Reuters, 2025) — added as the 18th story-bank entry, covering four SEN-relevant categories in one first-person, current, highly recognisable story. Added a `quoteContext` field to all 18 entries (not just Bronze) giving a short inline "(where/when this was said)" line directly under the main quote in the generator, per Dave's request for a quick sourcing snapshot in the flow rather than only the separate "Source: [link]" citation at the bottom of the card. Verified locally with Playwright across all 18 entries (every one confirmed to render a non-empty quote context, zero console errors) before pushing, then confirmed live on yearnmethod.pages.dev via direct browser navigation (dropdown list, story count, and Bronze's bio text all confirmed present in the live DOM).
- **8 Sep 2026 (mobile UX + SEN-condition story bank expansion)** — Fixed missing gap above the generator's "Used X of Y stories" line. Changed default state so every section loads collapsed (previously "What This Is" and "Pick Today's Story" were open on load) and added an Expand all sections / Collapse all sections toggle button so the user isn't stuck scrolling past several open sections to find the one to close. Removed the duplicated Saint-Exup\u00e9ry quote from inside Section 1 (kept the one at the top of the page) and replaced it with a one-line reference. Added 3 new first-person story-bank entries specifically chosen for direct, own-words accounts of SEN-relevant conditions, following Miriam's feedback that Marcus Rashford's entry (his own words, not a third party describing him) was the one that landed best and a request to add more like it, plus a gap she noticed searching "anxiety" with no match: Zayn Malik (ADHD, diagnosed at Tong High School, quote from his 2016 memoir), Maya Hawke (dyslexia, kicked out of school for not being able to read, quote from a TODAY interview), Susan Boyle (Asperger's, diagnosed at 51 after decades of being misunderstood at school, quote from CBS News). All three sourced to named outlets with working links, verified via Playwright locally (mobile viewport, all three generate correctly, task search correctly surfaces Zayn under "adhd" and Maya Hawke under "dyslexia", zero console errors) then confirmed live on yearnmethod.pages.dev via direct browser navigation. Deliberately did not add an anxiety/mental-health-specific entry this round \u2014 flagged to Dave as a separate, more sensitive category (health disclosure vs. learning difference) needing a considered approach, possibly with Miriam/Landau safeguarding input, before adding names under that heading. Larry Mullen Jr. (dyscalculia) and Robbie Williams (dyslexia/dyscalculia/ADHD/autism/Tourette's) were researched but held back \u2014 Mullen Jr.'s public quotes cover the adult impact on drumming but not a school-years account, and Williams's conditions were revealed piecemeal across different interviews making one clean sourced quote harder to pin down; both are candidates for a future pass if wanted.
- **8 Sep 2026** — Full section restructure: new subtitle and full Saint-Exupéry quote block, expanded "What This Is" intro, "Why It Works" renamed "How It Works", sequential section numbering throughout (no more sub-numbering), "Who's Who" and "Story Bank" merged into one section positioned directly before "How Did It Go?", a describe-your-task search box added above the A-Z index, profession tags added to every Who's Who entry, 3–5 achievement bullets added per person, and the story bank expanded from 9 to 14 people (Dua Lipa, Tom Holland, Lewis Hamilton, Ed Sheeran, Richard Branson added, each researched and sourced individually). Tested locally with Playwright first — mobile viewport, generator, both search boxes, achievement rendering all verified, zero console errors — before deployment. Committed, pushed, and verified live on yearnmethod.pages.dev via direct browser navigation and screenshot, matching the local test exactly.
- **8 Sep 2026 (earlier same day)** — Added the A-Z celebrity bio reference for the first time, with an auto-populated bio snapshot shown inside the generator's reveal card when a story is picked.
- **8 Sep 2026 (documentation)** — README.md removed from this folder; its from-zero orientation content folded into this file's opening sections instead. A CLAUDE.md was added so Claude Code auto-reads this status-handover file on opening the folder, without being told to. Going forward, this is the single doc for this folder.
- **Prior to 8 Sep 2026 (build and deploy)** — Built from scratch as a self-contained, offline-capable HTML tool: collapsible informational arc, working story generator, rule-based feedback logging (deliberately not live-AI, to avoid ongoing API costs and key management). Deployed live via GitHub (Daveflyon account) and Cloudflare Pages. Two early deployment attempts landed on a `.workers.dev` URL instead of the required `.pages.dev` Pages domain, because Cloudflare's generic "Create application" flow silently ran `npx wrangler deploy` (a Worker deploy) rather than static Pages hosting; both wrong deployments were deleted and redone using the direct Pages-specific import URL, which produced the correct result. An early commit also accidentally included the entire `.git` internal folder as public static assets, before a `.gitignore` existed; fixed with `git rm -r --cached .` and a proper `.gitignore`. Domain name settled on `yearnmethod` after confirming via the Cloudflare dashboard that `yearn.pages.dev` alone was already taken by an unrelated site.
