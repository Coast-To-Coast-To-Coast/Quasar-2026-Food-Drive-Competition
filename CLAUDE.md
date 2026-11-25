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

- **No per-office totals or per-office participation anywhere.** Not everyone belongs to one office, families donate too, and the drive must never feel like it's shaming offices. The site tracks one company total only.
- The goal is a round **$5,000** (`goal` in the numbers block), agreed with leadership in November 2026: about $15 a person for 334 people and 10,000 meals. Last year the company raised about $3,160 with 277 employees (about $11.40 a person), so $5,000 is a meaningful stretch that's still achievable, helped by family and friends giving too. Nate wants round numbers, so keep the goal a number whose 20% steps are round. Stop targets are calculated from it; never hardcode them.
- The How it works goal box mentions last year's total (`lastYearRaised` in the numbers block) to encourage beating it. Never compare offices.
- Everyone donates through **one "Donate here" link** (`donateUrl`) to a single food bank donation page, whose dashboard is where the weekly total comes from. Employees are encouraged to share it with family and friends.
- The third stat tile shows the number of gifts ("from our people, family and friends"), not a participation %.
- The raffle is for employees only (family and friends can donate but don't enter).

## The coast-to-coast journey (the centrepiece)

A road-trip style route, not a real map. Six evenly spaced stops run west to east, each a round "postcard stamp" badge with a landmark:

| Stop | Office label | % of goal | At $5,000 goal | Reward | Landmark |
|---|---|---|---|---|---|
| Vancouver | Vancouver office | 0% (start) | $0 | Starting line | North Shore mountains and Lions Gate Bridge |
| Timmins | Timmins office | 20% | $1,000 | Raffle draw: $50 | Gold mine headframe with pines |
| North Bay | North Bay office | 40% | $2,000 | Raffle draw: $100 | Canoe on Lake Nipissing, pines on shore |
| Woodbridge | Woodbridge HQ | 60% | $3,000 | Raffle draw: $150 | HQ building with the Quasar chevron and an "HQ" flag |
| Toronto | Toronto (Pratus, Sterling Road) | 80% | $4,000 | Raffle draw: $175 | CN Tower and skyline |
| Ottawa | Ottawa office | 100% | $5,000 | Grand prize raffle draw: $200 | Peace Tower on Parliament Hill |

The offices are only places on the route; they don't have their own totals.

- Landmarks are inline SVG in index.html (the `PLACES` object): flat, 2 to 3 colours each, same style, respectful hometown pride, never caricatures. Each has alt text naming the landmark and office.
- Each stop's pill shows its dollar target first, then the %: "$1,000 · 20%" (calculated from the goal).
- **No lock icons and no "Locked" labels** (Nate didn't like them). Stops ahead are softly faded but still in colour. Reached stops are full colour with a gold ring, a gold check and "Unlocked!". The next stop gets a gentle blue highlight, and a "Next stop: X, $Y to go" line sits above the route. Raffle chips say "Coming up" until reached.
- Stops unlock **automatically** when the company total reaches their %. Rewards are editable in the numbers block.
- A delivery truck loaded with grocery bags sits on the road at the company's % of goal with a "$X raised, Y%" tag. On load it drives from Vancouver, the road fills in gold behind it and badges pop as it passes them. Past 100% it parks at Ottawa with confetti and a "Goal reached!" banner. Reduced motion: no animation, final state only.
- Desktop: the route runs left to right. Phones (760px and narrower): top to bottom like a trip itinerary.
- Below the route: stat tiles (total raised, meals provided, % of goal, gifts so far). The truck tag reads "$X raised, Y meals". The "Every office counts" section was removed on purpose; don't bring back per-office numbers.

## Raffle

- A draw happens at each stop that has a `prize` in the milestones (every stop after Vancouver: 20%, 40%, 60%, 80% and 100%). Prizes grow as the drive goes: $50, $100, $150, $175, then a $200 grand prize at the goal ($675 in all if we reach the goal). The leadership dare and the ugly sweater day were dropped (the sweater photo book and sweater raffle entry stay). The site builds the draw list, the "Win up to $200" heading and the FAQ from the milestones.
- Two equal ways to enter: "Donated? Enter the draw" (`drawFormUrl`, a Microsoft Form) and "Share your holiday sweater" (`photoFormUrl`, a Microsoft Form; one entry, no donation needed).
- One entry per person per way to enter. The FAQ says each draw picks from everyone who has entered so far (entries carry over). Confirm with Nate if that changes.

## Sweater photo book

- Polaroid-style cards with washi tape and handwritten-style captions (first name and office) on a soft festive background. Clicking a photo opens a simple lightbox (close button, Esc or clicking outside).
- Photos live in the `photos` folder. Each photo gets a line in the second editable block, "SWEATER PHOTOS: ADD ONE LINE PER PHOTO": `{ file: "jordan-ottawa.jpg", name: "Jordan", office: "Ottawa" },`
- The last card is always "Add yours!" linking to `photoFormUrl`. With no photos, three "Your sweater here" placeholder cards show.
- Save photos at about **1000px wide, JPG, under 300 KB**, with location data removed. First names only. The site is public, so the FAQ tells people anyone with the link can see the photo book.
- To add photos, use the `/add-photos` command (see below).

## Where donations go: Food Banks Canada

- Our partner is **Food Banks Canada** (confirmed). Name it on the site; never use generic "our food bank partner" wording.
- Messaging: supporting food banks in every community where we live and work, from coast to coast to coast. Don't say donations go to one specific local food bank.
- Tax receipts come from Food Banks Canada.
- **Never use the Food Banks Canada logo.** We don't have permission yet. Use their name in text only.
- Meals: Food Banks Canada's meal metric is $1 = 2 meals, set as `mealsPerDollar` in the numbers block. Every meal number on the site (hero line, meals stat, truck tag, goal line, gift tiles, FAQ) is calculated from it and the totals. Never hardcode meal numbers.
- Tone: food banks are grateful for every kind of donation. Explain why money goes further, but never suggest food donations are bad or unwanted.

### Food Banks Canada sections and sources

Page order: hero, journey and stats, What your gift does, How it works, Why money goes further, raffle, sweater photo book, Why it matters, About Food Banks Canada, timeline, FAQ, closing. Section backgrounds alternate (white, sky, gold, festive, navy).

- **What your gift does:** four tiles ($5, $10, $25, $50) with meals from `mealsPerDollar`; each tile links to `donateUrl`. Source line links to https://foodbankscanada.ca/give/
- **Why money goes further:** three cards (better prices, where it's needed most, behind the scenes). Link to https://foodbankscanada.ca/give/
- **Why it matters this year** (navy band). Stats, checked against Food Banks Canada's site in November 2026:
  - 2.35M visits to food banks in March 2026, a record. HungerCount 2026 (released October 2026): https://foodbankscanada.ca/hunger-in-canada/hungercount/
  - 1 in 3 visits are by children (32.5%). HungerCount 2026, same link.
  - 21% of food banks ran out of food before demand was met. https://foodbankscanada.ca/give/
  - 1 in 4 people in Canada live in food insecure households (their site says "more than 1 in 4"). https://foodbankscanada.ca/give/
  - 2.35M and 21% count up on scroll; "1 in 3" and "1 in 4" stay static (counting them would show odd values like "1 in 0"). Report button: https://foodbankscanada.ca/hungercount-report-2026/
  - Update these when a new HungerCount comes out.
- **About Food Banks Canada:** short description (5,500+ food banks and community organizations), tied to the road trip, plus four outline link buttons: about-us, our-impact, find-a-food-bank, how-to-help/ways-to-support.

### Link rules for Food Banks Canada links

- Give them `class="ext"` and `target="_blank" rel="noopener"`. A script adds the external-link icon and "(opens in a new tab)" for screen readers to every `a.ext`.
- Links use the `--link` colour token (brand blue in light mode, light blue in dark mode, gold on the navy band) and are underlined.

## Timeline

- Kickoff: Friday, November 27, 2026 (the drive runs Nov 27 to Jan 1)
- Friday updates: Dec 4 (Week 1), Dec 11 (Week 2), Dec 18 (Week 3, last before holiday closure)
- Donations close: Friday, January 1, 2027
- Wrap-up: first week back in January

## How the site is built

- The site is **one file: index.html** (HTML, CSS and JavaScript together), plus sweater photos in `photos/`. Keep it that way. No build tools or frameworks unless Nate asks.
- Hosted free on **GitHub Pages** from the main branch, root folder. Live at https://coast-to-coast-to-coast.github.io/Quasar-2026-Food-Drive-Competition/. The repo lives in the GitHub organization `Coast-To-Coast-To-Coast` (display name Coast2Coast2Coast), owned by Nate's personal account NathanielMarketing. It was moved there before launch; older nathanielmarketing.github.io and quasar-food-drive-2026.github.io addresses no longer work.
- Pushing to main redeploys the site in about a minute.
- The repo is **public**. Never add passwords, logins, personal contact details, surnames, donor names, dashboard screenshots, or anything sensitive. `.gitignore` blocks image files everywhere except `photos/*.jpg` as a safety net.

### The numbers block

At the top of index.html is a block marked "FOOD DRIVE NUMBERS: EDIT THIS BLOCK EACH FRIDAY." It holds:
- `lastUpdated` (date text).
- `raised` (company total in dollars) and `gifts` (number of donations). These are the only two numbers that change each week.
- `goal` (5000, the company goal in dollars) and `people` (334, only used for the "about $15 a person" line).
- `lastYearRaised` (3160, last year's company total, shown in the goal box; set to 0 to hide the line).
- `mealsPerDollar` (2, Food Banks Canada's meal metric).
- The links `donateUrl`, `drawFormUrl`, `photoFormUrl`. A link that doesn't start with `https://` shows as a "coming soon" pill.
- `milestones`: one line per stop with its `at` %, `reward` text and, for raffle stops, a `prize` in dollars.

Rules:
- Everything else (goal, % of goal, meals, stop dollar targets, unlocked stops, next stop, truck position, raffle draw list) is calculated from this block. Never hardcode those numbers elsewhere.
- Nate sometimes edits this block directly on github.com with the pencil icon. Keep it simple and clearly labelled: plain numbers, no dollar signs or commas.
- Before editing, pull the latest version from GitHub so web edits aren't overwritten.
- Before kickoff, `raised` and `gifts` are 0, and the page shows "First update Friday, December 4".

## Project commands

These live in `.claude/commands/` and work when Claude Code is opened in this repo folder.

- **`/weekly-update`**: each Friday Nate pastes screenshots of the food bank donation dashboard. Claude pulls, reads the company total and number of gifts, shows a table against last week and flags anything odd, never guesses a number, waits for Nate's OK, updates the block and `lastUpdated`, reports newly unlocked stops (raffle draw or reward to announce), writes a 2 to 3 sentence Teams message, then commits "Week N totals" and pushes. Screenshots are never saved in the repo.
- **`/add-photos`**: Nate gives photo files with first names and offices. Claude resizes them (about 1000px wide, JPG, under 300 KB, rotation fixed, metadata stripped), saves them in `photos/`, adds lines to the photo block, previews, and commits and pushes after Nate confirms.

## Brand and design

The site should feel like part of **The Pulse**, Quasar's internal SharePoint hub, but brighter and more festive.

- Fonts: Segoe UI first, with system fallbacks. Photo captions use a handwritten-style system font (Segoe Print and fallbacks).
- Colours: brand blue `#1d5bd8`, deep blue `#123f9e`, navy `#10285c`, gold `#ffc21a`, light sky `#eaf2ff`.
- Section pattern from The Pulse: a gold eyebrow line above a large heading.
- The Quasar chevron shapes appear as decoration in the hero and on the Woodbridge landmark.
- The browser tab icon is the Quasar mark (blue and grey hexagon of parallelograms), traced as an inline SVG data link in the `<head>`. No separate icon file.
- Rounded cards, pill buttons, gold for anything reached or unlocked.
- Motion: the truck drives, the road fills and numbers count up when the journey scrolls into view; the Why it matters numbers count up too. Respect reduced-motion settings.
- Must work well on phones, and in both light and dark mode.

## Writing rules

- **Never use em dashes**, in page text, code comments or messages to Nate. Use commas, colons, parentheses or new sentences instead.
- Use curly apostrophes and quotes (’ “ ”) in visible text; straight quotes in code.
- Tone: friendly, casual, upbeat, clear. Short sentences. Canadian spelling (colour, centre, cheque).
- Keep explanations of the rules short. If something needs a paragraph to explain, simplify the rule.

## Still to confirm

- The real `donateUrl` (the Food Banks Canada donation page).
- The sweater photo Microsoft Form link (`photoFormUrl`). The draw form (`drawFormUrl`) is set.
- What form the raffle prizes take (gift card or otherwise); the site just says "$100 prize" for now.

## Planned additions

- Champion spotlights: headshots and trading-card style or Quick Q's style mini profiles for each office's champion.

## Working with Nate

- Show him what changed before pushing, and preview the page when possible.
- If a push needs a GitHub sign-in that can't appear in Claude's shell, ask him to run `git push origin main` in a terminal opened in this folder.
- After pushing, remind him the site takes about a minute to update and to hard refresh (Ctrl + F5).
- If something might break the weekly update process, flag it before doing it.
- When a decision changes, update this file too.
