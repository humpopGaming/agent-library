---
name: find-creators
description: Find YouTube creators who suit an app's ideal customer and suggest them in Notion for the owner to vet. Research only; never contacts anyone. Use when the user asks to find creators/influencers for an app.
---

# find-creators

Finds YouTube creators for one app and writes suggestions to the Notion **Creators** database. The owner vets every row. Nothing is contacted, drafted or sent (rules.md #2). The only offer ever considered is free access to the app; bigger creators are flagged as partner candidates and no terms are proposed.

## Inputs (read first, every run)
1. `config/creators.local.json` (gitignored; template `config/creators.example.json`): YouTube API key, Notion IDs, app profile path. If missing or the key is a placeholder, stop and tell the owner what to add.
2. The **app profile** at `app_profile_path`: what the app does, the ideal customer in the owner's words, platform, stage. Never copy its contents into this repo.
3. The Notion **Creator criteria** page: thresholds, tiers, rejects, learned preferences. Thresholds there override anything below.
4. The **Creators** database: every existing row, so no creator is suggested twice. Rows with `Your feedback` text are the learning signal: read them all and let them adjust angles and scoring.

## Steps
1. **Propose angles.** Produce 8 to 12 search angles in three layers, each with a one-line reason:
   - Core: creators who speak directly to the ideal customer.
   - Adjacent: the same mindset in another wrapper (e.g. life systems, home automation, parenting hacks).
   - Wildcard: angles you infer from the profile and past feedback.
   Do not restrict to one niche. Ask the owner which to run. **Wait for approval.** Do not search first.
2. **Search** each approved angle with the YouTube Data API (free quota; keep a running tally of units used and stop well under the daily 10,000):
   - `search.list` (type=channel or video, ~100 units per call) to find candidates; prefer few well-chosen queries over many.
   - `channels.list` (statistics, snippet, brandingSettings; 1 unit) for subscribers and About text.
   - `playlistItems.list` on the uploads playlist, then `videos.list` (statistics) for the last 10 videos (views, dates).
   - `commentThreads.list` on the last 3 videos for comment activity and creator replies.
3. **Apply the criteria** from the Notion page. Reject automatically per its list. Do not store rejected channels.
4. **Score Fit 1 to 5** against the ideal customer: subject matter (does the content solve the app's problem?), comment activity, creator replies, audience age (inferred from content and comments; say it is inferred). 4 or 5 are worth the owner's time; do not suggest below 3.
5. **Tier** from subscribers: 8,000 to 50,000 = `Free access`; 50,000 and over = `Partner candidate` (use the thresholds on the criteria page).
6. **Write rows** to the Creators database with Decision = `Suggested`. Fill only: Name, Channel URL, Tier, Fit, Why suggested (two sentences max, with evidence), Angle, Subscribers, Views vs subs %, Contact route (public business email or About link if shown; never scrape or guess). Leave `Your feedback` empty.
7. **Report** in the terminal: angles run, creators added, quota used, and anything uncertain.

## Rules
- Only official APIs and public pages. Do not work around any block. X/Twitter is out of scope (rules.md #8).
- Don't invent facts: if a number or reply pattern wasn't checked, say so in Why suggested.
- Never delete or overwrite owner text. Never change `Decision` or `Your feedback`.
- UK GDPR/PECR: store only public channel data and a public contact route.
- Nothing about any app's internals goes in this repo.
