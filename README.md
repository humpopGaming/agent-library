# agent-library

A library of AI agent roles, rules and skills for an **agentic software studio**: a pipeline of agents that help build, support, distribute and promote apps. It is app-agnostic. Each app's own details live in that app's repo, never here.

Guiding principle: **everything here exists to reduce the time the owner personally spends**, so their thinking time goes to improving their apps.

## What's in here

| Path | Purpose |
|---|---|
| `agents/idea-researcher/AGENT.md` | Weekly research agent. Reads new ideas/links from a Notion database, researches them and proposes where they fit in the studio pipeline. |
| `pipeline/roles.md` | The studio's roles (build, feedback, support, design, content, promotion, sales, release) and what each needs. |
| `.claude/skills/find-creators/SKILL.md` | Manual skill (`/find-creators`). Proposes search angles, you approve, then it finds YouTube creators for an app and suggests them in a Notion Creators database for you to vet. Research only, never contacts anyone. Config: `config/creators.local.json` (gitignored; see `config/creators.example.json`). |
| `.claude/skills/draft-comments/SKILL.md` | Manual skill (`/draft-comments`). For creators you marked Interested, drafts specific, genuine comment options for their recent videos, each with a timestamp link and the words said at that moment so you only watch the relevant clip. You post them yourself; it never posts. |
| `rules.md` | Guardrails every agent follows (draft-only for anything reaching people, free-first budget, disclosure). |
| `approved-tools.md` | Tools already available, approved or planned. |
| `templates/report.md` | The report format written into each Notion row. |
| `config/notion.md` | Column layout of the Notion ideas database (IDs are supplied by the run prompt, not stored here). |

## How the weekly routine works

1. The owner adds rows to a Notion **Idea reports** database: an idea or link, optional notes, optional area. Sites that block automated access (e.g. X) need their text pasted into Notes.
2. A scheduled remote task runs the idea researcher every Friday morning (UK time). The run prompt supplies the Notion IDs and the list of the owner's apps and their repos.
3. For each `New` row the agent researches the idea, splits link-lists into one row per link, writes a report into the row and sets Status to `Proposed`.
4. The owner reviews in Notion and leaves **Notion comments**. The next run replies and revises (`Revised`).
5. When the owner sets `Approved`, the agent finalises a draft GitHub issue. It only opens the issue when the owner replies "open it".
6. The owner gets a push notification when the run finishes.

## Changing the agent's behaviour

Edit the files here, then:

```powershell
git add -A
git commit -m "Describe the change"
git push
```

The scheduled task reads this repo on every run, so pushed changes apply from the next run.

## Principles (full detail in rules.md)

- Anything that reaches a real person is **draft only**: the full original shown unsummarised plus the drafted reply. The owner presses send.
- Code may be built and pushed to a **dev/test environment** behind automated gates. The owner checks there; production stays manual.
- **Free or open-source first.** Always state cost.
- AI-generated content is labelled as such; content promoting the owner's own app is flagged for any promotion label platforms or UK rules require.

## Keep this repo free of secrets and app internals

This repo is public. Do not commit credentials, personal data, or details from private app repos. Agents read app context at run time from the app's own repo.
