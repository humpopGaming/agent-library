# Studio pipeline: roles

The studio is a pipeline of agent roles that serves the owner's apps (the run prompt lists them). For every idea, the researcher decides which role(s) it fits, whether it is **generic** (reusable across any app) or **app-specific**, and what it needs from and gives to neighbouring roles.

Status: `exists` = built and working; `planned` = wanted, not built; `candidate` = idea only.

| # | Role | Purpose | Status | Notes |
|---|------|---------|--------|-------|
| 1 | **Build** (issue-driven feature and bug pipelines) | Takes GitHub issues through research, spec, test-first code, tests, review, PR to dev | exists in some apps | Defined in each app's own repo. Output is code on dev behind automated gates. Owner checks on dev. |
| 2 | **Intake / research** | Reviews saved links and ideas, proposes where they fit, drafts GitHub issues for approval | being built | `agents/idea-researcher` |
| 3 | **User feedback** | Reads reviews and comments on the owner's app and on competitor apps, validates them, proposes improvement items | planned | Must show the exact comment, never a summary. Raises improvement ideas as drafts. |
| 4 | **User support** | Drafts replies to users; possible in-app AI assistant giving users instant answers | planned | Draft only: show original message + drafted reply; owner sends. In-app assistant is a separate product decision. |
| 5 | **Design / web UI** | Look and feel, landing pages, store listing visuals (e.g. Magic UI skill) | planned | Check licence and fit with the app's design system. |
| 6 | **Content creation** | Posts, short videos, scripts; avatar-led (Higgsfield) for the owner's TikTok/YouTube | planned | AI content must be labelled. Faceless/avatar only. |
| 7 | **Promotion / channel strategy** | Decides which platform to focus on (YouTube vs TikTok etc.); finds creators who could promote the app | planned | Assume a cold start unless the app profile says otherwise. |
| 8 | **Sales / partnerships** | Finds collaborators and prospects (e.g. Harvey-style outreach) | candidate | Draft only. Check UK GDPR/PECR for outreach. |
| 9 | **Release & store** | Play Store listing, ASO, release checklist, analytics | candidate | Release checklists live in each app's repo. |

## Cross-cutting
- **Owner approval gates**: anything reaching a person; production release.
- **Generic vs app-specific**: prefer ideas reusable across future apps. Mark clearly when something is specific to one app.
- **Missing roles**: if an idea implies a role not listed here (legal/privacy, pricing, analytics...), say so and propose adding it.
