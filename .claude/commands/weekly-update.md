---
description: Friday update. Paste screenshots of the donation dashboard and Claude updates the site.
argument-hint: (paste dashboard screenshots)
---

# Weekly food drive update

Nate pastes screenshots of the food bank donation dashboard with this command. Follow these steps in order. Use plain language, one step at a time, and never use em dashes.

## 1. Get the latest version

- Run `git pull --ff-only` in this repo before reading or changing anything, so edits Nate made on github.com aren't overwritten. If the pull fails, stop and explain what happened.
- If the message has no screenshots, ask Nate to paste them and stop.

## 2. Read the screenshots

- Find the **company total raised** and the **number of donations** (gifts). The site tracks one company total only, not offices: employees, family and friends all count.
- **Never guess a number.** If a number is cut off, blurry, or you're not sure which number is the total, say so and ask.
- Ignore donor names, emails and messages. Never repeat them in replies, on the site, in commit messages or in the Teams message.

## 3. Check with Nate before changing anything

Show a small table: last week's `raised` and `gifts` (from the numbers block in index.html), this week's (from the screenshots), and the change.

Flag anything that looks off, for example:
- A total or gift count that went down.
- A number you couldn't read clearly.
- A jump that looks unusually big.

Ask Nate to confirm and wait for a clear yes. Don't edit anything until he confirms.

## 4. Update the numbers block

In index.html, in the block marked "FOOD DRIVE NUMBERS: EDIT THIS BLOCK EACH FRIDAY":
- Update `raised` and `gifts`. Plain numbers only: no dollar signs, no commas, rounded to the nearest dollar.
- Set `lastUpdated` to today's date in the same style, for example "Friday, December 11".
- Don't change anything else (people, goal, links, milestones) unless Nate asks.

## 5. Milestones

Using `goal` from the numbers block, work out which stops the total has passed before and after the update. Tell Nate which stops this update unlocks, if any:
- A raffle draw stop: remind him to draw a winner from the entries in the Microsoft Forms.
- Any other reward: remind him to announce it.

If nothing new unlocked, tell him how far away the next stop is in dollars.

## 6. Preview

Open the page in the preview and check that the truck, the stats and the "Next stop" line show the new numbers. Show Nate a screenshot.

## 7. Teams message

Write a short, casual update Nate can paste into Teams: 2 to 3 sentences, no em dashes, curly apostrophes. Include the new total, the meals it provides (total × `mealsPerDollar`), the % of goal, the next stop and how much is left to reach it, plus any stop that just unlocked. Never compare or single out offices. End with the site link: https://coast-to-coast-to-coast.github.io/Quasar-2026-Food-Drive-Competition/

## 8. Commit and push

- Run `git status` and make sure index.html is the only changed file. **Screenshots must never be saved in or committed to this repo:** it's public, and dashboards can show donor names and emails. If an image or any other unexpected file shows up, stop and ask.
- Commit only index.html with the message "Week N totals" (Dec 4 is Week 1, Dec 11 is Week 2, Dec 18 is Week 3; after donations close on January 1, use "Final totals").
- Push to main. If the push needs a GitHub sign-in that can't appear here, ask Nate to run `git push origin main` in a terminal opened in this folder.
- Remind Nate the site updates in about a minute, and to hard refresh with Ctrl + F5.
