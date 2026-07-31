# AgentPrep — Claude Code Skill

Installs the `agentprep` skill into the buyer's Claude Code. The skill is what runs the
Socratic tutoring — the LLM engine is the customer's own Claude Code subscription, so the
AgentPrep backend never calls an LLM. The skill ships no question content: everything comes
from the AgentPrep API, live.

**New here?** Start at the product page: [agentprep.dev](https://agentprep.dev/?utm_source=skill)
— which certifications it covers, how the free tier works, and what a Pro subscription includes.

> **This skill is a Pro feature.** AgentPrep's **free** tier lives in the Telegram bot
> ([@AgentPrep_bot](https://telegram.me/AgentPrep_bot?start=s_skill) — a daily 3-question quest,
> no card). The skill (Socratic tutoring + the 60-question mock exam) requires a Pro license key.

> The skill itself speaks **en / pt-BR / es** — it asks for your language during setup and
> serves questions and tutoring in it. This README is in English because it is the page
> strangers land on; it says nothing the skill won't repeat in your own language.

## Requirements

- Claude Code installed.
- An AgentPrep **Pro license key** (emailed to you after purchase at
  `https://agentprep.dev/buy` — US$ 49.90/year **list** price; that page always shows the
  current price, which is often BELOW this value when a promotion is live — the page, never
  this file, is the source of truth for today's price. Or US$ 4.99/week at `https://agentprep.dev/buy?plan=weekly` if you
  would rather come in through the smaller door; both are geo-priced in BRL inside Brazil. If
  your instance is self-hosted under another domain, swap the domain and keep the `/buy` path)
  — or a dev key (`DEV_LICENSE_KEYS`) if you are testing against a self-hosted API.

## Install

Pick any option below. All three end at the same place: an `agentprep/` folder (containing
`SKILL.md`) inside `~/.claude/skills/`.

### Option A — `npx skills add` (recommended)

```bash
npx skills add marcelomar21/agentprep-skill
```

> The skill is distributed through the public repository
> [`marcelomar21/agentprep-skill`](https://github.com/marcelomar21/agentprep-skill)
> (validated end to end on 2026-07-13). That repository is a **mirror**: the source of truth is
> `skill/` in the AgentPrep repo, and CI republishes it automatically whenever the source
> changes, so what you install here matches what production serves.

### Option B — `git clone`

```bash
git clone https://github.com/marcelomar21/agentprep-skill.git /tmp/agentprep-install
mkdir -p ~/.claude/skills
cp -r /tmp/agentprep-install/agentprep ~/.claude/skills/agentprep
rm -rf /tmp/agentprep-install
```

### Option C — copy by hand

If all you received was the contents of `agentprep/SKILL.md` (pasted into an email, say, or
downloaded from a link), create the file yourself:

```bash
mkdir -p ~/.claude/skills/agentprep
$EDITOR ~/.claude/skills/agentprep/SKILL.md   # paste the contents you received
```

## Activate

There is no "install" step separate from configuration. The first time you ask for something
related (`/agentprep quest`, "let's study for the CCA-F", etc.), Claude Code follows the
**Setup** flow described inside `SKILL.md` itself: it asks for your license key, confirms your
language (en / pt-BR / es) and activates the key against the API
(`POST /v1/licenses/activate`). The result is saved to `~/.agentprep/config.json` — you never
need to edit that file by hand, except to change language or point at another API (`api_url`)
while testing.

## Day-to-day use

Inside any Claude Code session:

```
/agentprep quest       # daily quest — 5 questions with Socratic tutoring
/agentprep simulado    # full mock exam — 60 questions / 120 min, exam mode
/agentprep stats       # XP, level, rank, streak, accuracy by domain
```

Natural language works too ("let's do today's quest", "I want a CCA-F mock exam", "bora fazer a
quest de hoje", "quiero un simulado del CCA-F") — the skill's description (`SKILL.md`) already
lists the triggers Claude Code recognizes.

## Testing against a self-hosted API

```bash
export AGENTPREP_API_URL=http://localhost:8080
```

With that variable set, the skill uses this endpoint instead of the `api_url` saved in the
config. Use it together with a `DEV_LICENSE_KEYS` value on your local API.

## Uninstall

```bash
rm -rf ~/.claude/skills/agentprep
rm -rf ~/.agentprep   # removes the saved license key and local preferences
```
