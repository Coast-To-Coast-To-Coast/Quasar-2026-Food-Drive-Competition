# Quasar + Pratus Holiday Food Drive 2026: Project Brief

This repo hosts the site for the company-wide holiday food drive at Quasar Consulting Group and Pratus Group. Read this whole file before making changes.

## Who this is for

- Owner: Nathaniel (Nate), Marketing Coordinator at Quasar. He's a designer and marketer, not a developer. Explain steps in plain language, one at a time, and don't assume Git or coding knowledge.
- Audience: 334 employees across six offices. Most will open the site from a button on The Pulse (Quasar's internal SharePoint hub) or a Teams post, often on a phone.

## The goal and why the site exists

Last year's drive missed its goals mainly because it was confusing:
- Scoring used meals, with contradictory conversions ($1 = 2 meals vs $2 = 1 meal) and extra goal adjustments for some offices.
- Updates went out by email and got lost. There was no single place to see standings or find donation links.
- Each office used a different local food bank, and some (North Bay) had no online tracker, so totals were hard to collect.

This year's theme is **one link, one number, one place**. Every design or content decision should make the drive simpler to understand and easier to give to.

## The format: the whole company, one goal

There is **no competition**. No teams, no winners or losers, no rankings, no "matchup" or "underdog" language. (An earlier HQ vs. challengers version was dropped.)

- Every person counts the same: the company goal is headcount × `goalPerPerson` ($20), so 334 × $20 = **$6,680**. The site calculates it from the numbers block; never hardcode it.
- Official headcounts: Woodbridge 260, Sterling Road (Toronto, Pratus) 30, Vancouver 20, Ottawa 15, North Bay 6, Timmins 3.
- Everyone donates through **one company donation link** (`donateUrl`).
- Participation (donors out of 334) is shown next to the total.

## The coast-to-coast journey (the centrepiece)

A road-trip style route, not a real map. Six evenly spaced stops run west to east, each a round "postcard stamp" badge with a landmark:

| Stop | Office label | % of goal | Reward | Landmark |
|---|---|---|---|---|
| Vancouver | Vancouver office | 0% (start) | Starting line | North Shore mountains and Lions Gate Bridge |
| Timmins | Timmins office | 20% | Raffle draw | Gold mine headframe with pines |
| North Bay | North Bay office | 40% | Ugly sweater day on a company call | Canoe on Lake Nipissing, pines on shore |
| Woodbridge | Woodbridge HQ | 60% | Raffle draw | HQ building with the Quasar chevron and an "HQ" flag |
| Toronto | Toronto (Pratus, Sterling Road) | 80% | Raffle draw | CN Tower and skyline |
| Ottawa | Ottawa office | 100% | Leadership dare (to be announced) | Peace Tower on Parliament Hill |

- Landmarks are inline SVG in index.html (the `PLACES` object): flat, 2 to 3 colours each, same style, respectful hometown pride, never caricatures. Each has alt text naming the landmark and office.
- Locked stops are greyscale with a lock. Unlocked stops are full colour with a gold ring and a check. The next stop gets a gentle blue highlight, and a "Next stop: X, $Y to go" line sits above the route.
- Stops unlock **automatically** when the company total reaches their %. Rewards are editable in the numbers block.
- A delivery truck loaded with grocery bags sits on the road at the company's % of goal with a "$X raised, Y%" tag. On load it drives from Vancouver, the road fills in gold behind it and badges pop as it passes them. Past 100% it parks at Ottawa with confetti and a "Goal reached!" banner. Reduced motion: no animation, final state only.
- Desktop: the route runs left to right. Phones (760px and narrower): top to bottom like a trip itinerary.
- Below the route: stat tiles (total raised, % of goal, participation), then an "Every office counts" section showing what each office added, in route order, with no ranking.

## Raffle

- A draw happens at each stop whose reward mentions "raffle" (currently 20%, 60% and 80%). Each draw is for a $25 digital gift card. The site works out which % values to list from the milestones.
- Two equal ways to enter: "Donated? Enter the draw" (`drawFormUrl`, a Microsoft Form) and "Share your holiday sweater" (`photoFormUrl`, a Microsoft Form; one entry, no donation needed).
- One entry per person per way to enter. The FAQ says each draw picks from everyone who has entered so far (entries carry over). Confirm with Nate if that changes.

## Sweater photo book

- Polaroid-style cards with washi tape and handwritten-style captions (first name and office) on a soft festive background. Clicking a photo opens a simple lightbox (close button, Esc or clicking outside).
- Photos live in the `photos` folder. Each photo gets a line in the second editable block, "SWEATER PHOTOS: ADD ONE LINE PER PHOTO": `{ file: "jordan-ottawa.jpg", name: "Jordan", office: "Ottawa" },`
- The last card is always "Add yours!" linking to `photoFormUrl`. With no photos, three "Your sweater here" placeholder cards show.
- Save photos at about **1000px wide, JPG, under 300 KB**, with location data removed. First names only. The site is public, so the FAQ tells people anyone with the link can see the photo book.
- To add photos, use the `/add-photos` command (see below).

## Where donations go

- A **Canada-wide food bank partner**, likely Food Banks Canada (to be confirmed). Don't name it on the site until confirmed.
- Messaging: "supporting food banks in every community where we live and work." Don't say donations go to one specific local food bank.
- Tax receipts come from the partner.

## Timeline

- Kickoff: Monday, November 23, 2026
- Friday updates: Nov 27 (Week 1), Dec 4 (Week 2), Dec 11 (Week 3), Dec 18 (Week 4, last before holiday closure)
- Donations close: Friday, January 1, 2027
- Wrap-up: first week back in January

## How the site is built

- The site is **one file: index.html** (HTML, CSS and JavaScript together), plus sweater photos in `photos/`. Keep it that way. No build tools or frameworks unless Nate asks.
- Hosted free on **GitHub Pages** from the main branch, root folder. Live at https://nathanielmarketing.github.io/Quasar-2026-Food-Drive-Competition/
- Pushing to main redeploys the site in about a minute.
- The repo is **public**. Never add passwords, logins, personal contact details, surnames, donor names, dashboard screenshots, or anything sensitive. `.gitignore` blocks image files everywhere except `photos/*.jpg` as a safety net.

### The numbers block

At the top of index.html is a block marked "FOOD DRIVE NUMBERS: EDIT THIS BLOCK EACH FRIDAY." It holds:
- `lastUpdated` (date text), `goalPerPerson`, and the links `donateUrl`, `drawFormUrl`, `photoFormUrl`. A link that doesn't start with `https://` shows as a "coming soon" pill.
- `offices`: one line per office, west to east, with `raised`, `donors` and `people`.
- `unassigned`: money and donors the dashboard doesn't link to an office (used when there's only a company total). Usually 0.
- `milestones`: one line per stop with its `at` % and `reward` text.

Rules:
- Everything else (company total, goal, % of goal, participation, unlocked stops, next stop, truck position, office breakdown, raffle draw list) is calculated from this block. Never hardcode those numbers elsewhere.
- Nate sometimes edits this block directly on github.com with the pencil icon. Keep it simple and clearly labelled: plain numbers, no dollar signs or commas.
- Before editing, pull the latest version from GitHub so web edits aren't overwritten.
- Before kickoff, every office's `raised` and `donors` is 0, and the page shows "First update Friday, November 27".

## Project commands

These live in `.claude/commands/` and work when Claude Code is opened in this repo folder.

- **`/weekly-update`**: each Friday Nate pastes screenshots of the donation dashboards. Claude pulls, reads the totals (per office if there are office team pages, otherwise the company total via `unassigned`), shows a table against last week and flags anything odd, never guesses a number, waits for Nate's OK, updates the block and `lastUpdated`, reports newly unlocked stops (raffle draw or reward to announce), writes a 2 to 3 sentence Teams message, then commits "Week N totals" and pushes. Screenshots are never saved in the repo.
- **`/add-photos`**: Nate gives photo files with first names and offices. Claude resizes them (about 1000px wide, JPG, under 300 KB, rotation fixed, metadata stripped), saves them in `photos/`, adds lines to the photo block, previews, and commits and pushes after Nate confirms.

## Brand and design

The site should feel like part of **The Pulse**, Quasar's internal SharePoint hub, but brighter and more festive.

- Fonts: Segoe UI first, with system fallbacks. Photo captions use a handwritten-style system font (Segoe Print and fallbacks).
- Colours: brand blue `#1d5bd8`, deep blue `#123f9e`, navy `#10285c`, gold `#ffc21a`, light sky `#eaf2ff`.
- Section pattern from The Pulse: a gold eyebrow line above a large heading.
- The Quasar chevron shapes appear as decoration in the hero and on the Woodbridge landmark.
- Rounded cards, pill buttons, gold for anything reached or unlocked.
- One moment of motion: the truck drives, the road fills and numbers count up when the journey scrolls into view. Respect reduced-motion settings.
- Must work well on phones, and in both light and dark mode.

## Writing rules

- **Never use em dashes**, in page text, code comments or messages to Nate. Use commas, colons, parentheses or new sentences instead.
- Use curly apostrophes and quotes (’ “ ”) in visible text; straight quotes in code.
- Tone: friendly, casual, upbeat, clear. Short sentences. Canadian spelling (colour, centre, cheque).
- Keep explanations of the rules short. If something needs a paragraph to explain, simplify the rule.

## Still to confirm

- Food bank partner name and the real `donateUrl`.
- The two Microsoft Form links (`drawFormUrl`, `photoFormUrl`).
- The leadership dare at 100%.

## Planned additions

- Champion spotlights: headshots and trading-card style or Quick Q's style mini profiles for each office's champion.

## Working with Nate

- Show him what changed before pushing, and preview the page when possible.
- If a push needs a GitHub sign-in that can't appear in Claude's shell, ask him to run `git push origin main` in a terminal opened in this folder.
- After pushing, remind him the site takes about a minute to update and to hard refresh (Ctrl + F5).
- If something might break the weekly update process, flag it before doing it.
- When a decision changes, update this file too.
