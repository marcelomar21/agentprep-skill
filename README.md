# AgentPrep — Claude Code skill

Gamified exam-prep coach for [Anthropic's Claude certifications](https://agentprep.dev) (CCAR-F, CCAO-F, and more as they launch): daily quests, Socratic tutoring, timed mock exams, and a readiness forecast that tells you the day you'll be ready.

## Install

```bash
npx skills add marcelomar21/agentprep-skill
```

Then, inside Claude Code:

```
/agentprep
```

## Free vs Pro

- **Free** (no card): the daily quest on the Telegram bot [@AgentPrep_bot](https://t.me/AgentPrep_bot) — 3 questions/day, plus mastery per domain.
- **Pro** unlocks the full 5-question quest, unlimited practice, your exact ready-by date, the 60-question timed simulado, and **this Claude Code skill**.

## Requirements

- **This skill is a Pro feature** — it needs an **AgentPrep Pro license key** from [agentprep.dev/buy](https://agentprep.dev/buy) (US$ 49.90/year, geo-priced in BRL for Brazil; includes the Telegram bot and every certification in the catalog). No key yet? Start free on Telegram (above).
- The skill talks to the AgentPrep API live and never ships question content. Progress is shared with the Telegram bot through one account.

## Not affiliated with Anthropic

AgentPrep is an independent product. It is not affiliated with, endorsed by, or sponsored by Anthropic. All practice questions are original material created from publicly available information.
