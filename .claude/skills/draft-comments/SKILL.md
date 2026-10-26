---
name: draft-comments
description: Draft specific, genuine comment options for a vetted creator's recent YouTube videos, each pinned to an exact moment (timestamp link plus the words said there) so the owner only watches that clip. Never posts. Use after the owner marks a creator Interested.
---

# draft-comments

Helps the owner build a real presence on a creator's channel before any approach. Drafts only: the owner reads, watches, rewrites if needed and posts every comment themselves (rules.md #2). The agent never posts, likes, subscribes or contacts anyone. How and when to approach the creator is out of scope here.

## Inputs
1. `config/creators.local.json` (YouTube API key, Notion Creators data source).
2. The creator's row in the Notion **Creators** database. Only run for rows with Decision = `Interested`. If the owner names a different row, say so and ask.
3. The row's page body: the **Comment log** (see below) tells you what was already posted and when.
4. The row's `Your feedback` and the Notion Creator criteria page: what the owner likes and dislikes.

## Steps
1. Resolve the channel from `Channel URL` (`channels.list` with `forHandle`).
2. Take the 3 to 5 newest videos (`playlistItems.list` on the uploads playlist, then `videos.list` for snippet and statistics), plus any older video the owner names.
3. For each video gather:
   - with the official API: title, description, chapter markers (parse timestamps in the description), and the top comments and creator replies (`commentThreads.list`, part snippet,replies);
   - the **timed transcript** from the video's public captions, using the free open-source `youtube-transcript-api` (Python, `pip install youtube-transcript-api`). One request per video, only for videos you are drafting for, never in bulk and never for creators who aren't `Interested`. If captions are unavailable or the library is blocked, do not work around it: fall back to chapters and description only, say "no transcript" on that video, and skip it if no precise moment can be found.
4. Find a **hook moment**: a specific claim, tip, story or question that a real viewer could react to, located in the transcript with its start and end time (aim for a 15 to 45 second clip). Cross-check with chapters and viewer comments that cite timestamps. If a video has no usable moment, write "No specific moment, skip" and move on. Never write a generic comment.
5. Draft 2 or 3 short options per video. Types to mix: a specific question, a genuine reaction to a stated tip, a useful addition, a respectful different view. Plain everyday language, one to three sentences. Each option is written up as:
   - **Watch:** a link that opens at the moment (`https://youtu.be/<id>?t=<start seconds>`), the time range (e.g. 4:12 to 4:40) and the chapter name if any;
   - **They say:** the exact words from the transcript for that range, quoted, trimmed to the lines that matter (auto-captions can be wrong, so say they are auto-captions);
   - **Why this comment fits:** one line linking the quote to the comment;
   - **Comment:** the text to post;
   - **Confidence:** High (clear quote, comment obviously fits), Medium (captions look garbled or the moment is implied) or Low (say what to check while watching). Do not offer Low options unless nothing better exists.
6. Write the drafts into the row's page body under a dated heading (`## Comment drafts YYYY-MM-DD`) with a checkbox per option. Leave the `## Comment log` section for the owner. Keep the owner in the loop: end the run by listing, in the terminal, each draft's comment, watch link and time range so they can review at a glance.

## Hard rules (no fake engagement, no spam)
- Every draft cites a specific moment from that video with a timestamp link and the quoted words. No "great video!", no filler.
- The quote must come from the transcript you actually fetched. Never reconstruct or paraphrase it as if it were a quote.
- No app mention, no links, no promotion, no hints about outreach.
- Nothing the owner can't truthfully say: no invented experiences, results or family details. Prefer questions, opinions and reactions to what the creator actually said.
- Vary wording across drafts and against the Comment log; never reuse phrases or the same opening.
- Pacing: suggest at most 1 comment per creator per week for the first weeks, at most 2 videos in a day, and none on a video the log shows already commented. Say the suggested schedule at the top of the drafts.
- Remind the owner to watch the linked clip (not the whole video) before posting, and to rewrite in their own voice if it doesn't sound like them.
- Don't draft replies to other viewers' comments unless the owner asks.

## Comment log (owner maintains)
Each creator row's body has a `## Comment log` section. The owner adds one line per comment actually posted: date, video, and the text as posted (it may differ from the draft). This is what the pacing and variety checks read. If the log is missing or empty, treat the creator as new and say so.

## Rules
- Official API plus public captions for transcripts (see approved-tools.md; flagged as a terms grey area under rules.md #8, so no workarounds if blocked). X/Twitter is out of scope (rules.md #8).
- Don't invent facts about a video: if you only saw the description or have no transcript, say so.
- Store transcripts nowhere in this repo or Notion beyond the short quoted lines in the drafts.
- Never edit `Decision`, `Your feedback` or the owner's Comment log.
