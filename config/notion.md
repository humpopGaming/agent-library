# Notion ideas database: layout

The Notion page ID, database URL and data source ID are given in the scheduled task's run prompt, not stored in this public repo.

## Columns
| Column | Type | Who fills it |
|---|---|---|
| Idea / link | title | owner |
| Notes | text | owner (paste X post text here) |
| Area | select: Content creation, App improvement, Promotion, Web UI, Finding sales / collaborators, Other | owner (optional) or agent |
| Status | status: New, Needs input, Proposed, Revised, Approved, Issue opened, Split, Rejected | agent (owner sets `Approved`) |
| Summary | text | agent |
| Where it fits | multi-select of studio roles | agent |
| Reuse | select: Generic / App-specific | agent |
| Fit score | number 1-5 | agent |
| Effort | select: Low / Medium / High | agent |
| Cost | select: Free / Needs approval / Unknown | agent |
| Source | text | agent (for split rows: the post/row it came from) |
| GitHub issue | url | agent, after approval |
| Added | created time | automatic |

The report is the page content of the row. Owner feedback = Notion comments on that page.
