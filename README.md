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

## Free study guides (no key, no signup)

Fourteen guides — eleven on the Claude certifications (what each exam covers, who can sit it,
how the format and scoring work, and how to prepare) and three on the craft itself, which
mention no exam at all. They are free to read, need no license key and no account, and each one
is also published in **pt-BR** and **es** (the language links sit at the top of every guide).

On the craft:

- [What is MCP (Model Context Protocol)?](https://agentprep.dev/guide/what-is-mcp/?utm_source=skill)
- [What is a context window?](https://agentprep.dev/guide/what-is-a-context-window/?utm_source=skill)
- [What are Claude Code hooks?](https://agentprep.dev/guide/what-are-claude-code-hooks/?utm_source=skill)

On the certifications:

- [Is the Claude certification worth it?](https://agentprep.dev/guide/is-the-claude-certification-worth-it/?utm_source=skill)
- [Which Claude certification should you take?](https://agentprep.dev/guide/which-claude-certification-should-you-take/?utm_source=skill)
- [Who can take the Claude certification?](https://agentprep.dev/guide/who-can-take-the-claude-certification/?utm_source=skill)
- [What the Claude certification exam actually looks like](https://agentprep.dev/guide/claude-certification-exam-format/?utm_source=skill)
- [How to prepare for the Claude certification — and how long it takes](https://agentprep.dev/guide/how-to-prepare-for-the-claude-certification/?utm_source=skill)
- [Claude certification practice questions — where to find real ones](https://agentprep.dev/guide/claude-certification-practice-questions/?utm_source=skill)
- [Claude certification exam day — what actually happens](https://agentprep.dev/guide/claude-certification-exam-day/?utm_source=skill)
- [Claude Certified Associate — Foundations (CCAO-F)](https://agentprep.dev/guide/claude-certified-associate-foundations/?utm_source=skill)
- [Claude Certified Developer — Foundations (CCDV-F)](https://agentprep.dev/guide/claude-certified-developer-foundations/?utm_source=skill)
- [Claude Certified Architect — Foundations (CCAR-F)](https://agentprep.dev/guide/claude-certified-architect-foundations/?utm_source=skill)
- [Claude Certified Architect — Professional (CCAR-P)](https://agentprep.dev/guide/claude-certified-architect-professional/?utm_source=skill)

All of them, in the three languages: [English](https://agentprep.dev/guide/?utm_source=skill) · [Português](https://agentprep.dev/pt/guia/?utm_source=skill) · [Español](https://agentprep.dev/es/guia/?utm_source=skill)

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

> **What this skill can touch.** Public skill indexes run automated security scanners over
> everything they list, and their verdicts are worth checking before you install anything —
> including this. So that you can check ours quickly, here is the whole surface, and every
> line of it is verifiable in the repository you are about to clone:
>
> - **It is two Markdown files.** `README.md` and `agentprep/SKILL.md` — nothing else. There is
>   no `package.json`, no lockfile, no dependency of any kind, and no install or postinstall
>   step — so beyond fetching those two files themselves, the install pulls in nothing.
> - **The only command it runs that touches the network is `curl`**, against the AgentPrep API
>   (`api.agentprep.dev`) — or `localhost`, if you point it at your own instance. Every endpoint
>   it calls lives under `/v1/` and is documented publicly at
>   [agentprep.dev/docs/api](https://agentprep.dev/docs/api?utm_source=skill). The only other
>   commands it asks for are `mkdir -p ~/.agentprep` (once, to create the config directory) and
>   `date` (to time the mock exam) — both local, neither reaching the network.
> - **Once installed, it writes exactly one path on your machine:** `~/.agentprep/config.json`,
>   holding your license key and language. Installing it also places the skill file itself at
>   `~/.claude/skills/agentprep/` — that is what any Claude Code skill install does, by any of
>   the three options above. `Uninstall` below removes both.
>
> A skill is instructions, not a program: what actually executes is your own Claude Code,
> following the steps in `SKILL.md`. Read it before you install — it is short, and it is the
> entire product.

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
