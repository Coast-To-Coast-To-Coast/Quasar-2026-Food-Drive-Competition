---
description: Friday update. Paste screenshots of the donation dashboards and Claude updates the site.
argument-hint: (paste dashboard screenshots)
---

# Weekly food drive update

Nate pastes screenshots of the food bank donation dashboards with this command. Follow these steps in order. Use plain language, one step at a time, and never use em dashes.

## 1. Get the latest version

- Run `git pull --ff-only` in this repo before reading or changing anything, so edits Nate made on github.com aren't overwritten. If the pull fails, stop and explain what happened.
- If the message has no screenshots, ask Nate to paste them and stop.

## 2. Read the screenshots

- For each screenshot, find the amount raised and the number of donors.
- If the dashboard shows separate office team pages, read each office's numbers and match them to the six offices in the numbers block: Vancouver, Timmins, North Bay, Woodbridge, Toronto (Sterling Road, Pratus) and Ottawa.
- If a screenshot only shows a company total, use it as the company total (see step 4).
- **Never guess a number.** If a number is cut off, blurry, or you're not sure which office it belongs to, say so and ask.
- Ignore donor names, emails and messages. Never repeat them in replies, on the site, in commit messages or in the Teams message.

## 3. Check with Nate before changing anything

Show a small table with one row per office, plus Unassigned and Company total. Columns: last week's raised and donors (from the numbers block in index.html), this week's raised and donors (from the screenshots), and the change.

Flag anything that looks off, for example:
- A total or donor count that went down.
- An office missing from the screenshots.
- A number you couldn't read clearly.
- More donors than the office's headcount, or a jump that looks unusually big.
- Office totals that don't add up to the company total shown on the dashboard.

Ask Nate to confirm and wait for a clear yes. Don't edit anything until he confirms.

## 4. Update the numbers block

In index.html, in the block marked "FOOD DRIVE NUMBERS: EDIT THIS BLOCK EACH FRIDAY":
- Update `raised` and `donors` for each office. Plain numbers only: no dollar signs, no commas, rounded to the nearest dollar.
- If there's only a company total, or the office pages don't add up to it, put the difference in `unassigned`: company total minus the sum of the office totals, and the same for donors. If that would go below 0, stop and ask Nate.
- Set `lastUpdated` to today's date in the same style, for example "Friday, December 4".
- Don't change anything else (headcounts, goal, links, milestones) unless Nate asks.

## 5. Milestones

Work out the company's % of goal before and after the update: company total divided by (total headcount × goalPerPerson). Tell Nate which stops this update unlocks, if any:
- A raffle draw stop: remind him to draw a winner from the entries in the Microsoft Forms.
- Any other reward: remind him to announce it.

If nothing new unlocked, tell him how far away the next stop is.

## 6. Preview

Open the page in the preview and check that the truck, the stats and the "Next stop" line show the new numbers. Show Nate a screenshot.

## 7. Teams message

Write a short, casual update Nate can paste into Teams: 2 to 3 sentences, no em dashes, curly apostrophes. Include the new total, the % of goal, the next stop and how much is left to reach it, plus any stop that just unlocked. End with the site link: https://nathanielmarketing.github.io/Quasar-2026-Food-Drive-Competition/

## 8. Commit and push

- Run `git status` and make sure index.html is the only changed file. **Screenshots must never be saved in or committed to this repo:** it's public, and dashboards can show donor names and emails. If an image or any other unexpected file shows up, stop and ask.
- Commit only index.html with the message "Week N totals" (Nov 27 is Week 1, Dec 4 is Week 2, Dec 11 is Week 3, Dec 18 is Week 4; after donations close, use "Final totals").
- Push to main. If the push needs a GitHub sign-in that can't appear here, ask Nate to run `git push origin main` in a terminal opened in this folder.
- Remind Nate the site updates in about a minute, and to hard refresh with Ctrl + F5.
