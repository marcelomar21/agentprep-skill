# AgentPrep — Claude Code Skill

Instala a skill `agentprep` no Claude Code do comprador. É ela que conduz a tutoria
socrática (o motor de LLM é a própria assinatura Claude Code do cliente — o backend do
AgentPrep nunca chama um LLM). A skill não contém nenhuma questão: tudo vem, em tempo
real, da API do AgentPrep.

> **Esta skill é um recurso Pro.** O tier **grátis** do AgentPrep vive no bot do Telegram
> ([@AgentPrep_bot](https://telegram.me/AgentPrep_bot?start=s_skill) — quest diária de 3 questões,
> sem cartão). A skill
> (tutoria socrática + simulado de 60 questões) exige uma license key Pro.

## Pré-requisitos

- Claude Code instalado.
- Uma **license key Pro** do AgentPrep (recebida por e-mail após a compra em
  `https://agentprep.dev/buy` — US$ 49,90/ano de tabela (o preço corrente, com promoção
  vigente se houver, é o que essa página mostra), ou US$ 4,99/semana em
  `https://agentprep.dev/buy?plan=weekly` se você preferir entrar pela porta menor; os dois com preço
  geo em BRL no Brasil; se sua instância for self-hosted sob outro domínio, troque o domínio e
  mantenha o path `/buy`) — ou uma dev key
  (`DEV_LICENSE_KEYS`) se estiver testando contra uma API self-hosted.

## Instalar

Escolha uma das opções abaixo. Todas terminam com o mesmo resultado: a pasta
`agentprep/` (contendo `SKILL.md`) dentro de `~/.claude/skills/`.

### Opção A — `npx skills add` (recomendado)

```bash
npx skills add marcelomar21/agentprep-skill
```

> A skill é distribuída pelo repositório público
> [`marcelomar21/agentprep-skill`](https://github.com/marcelomar21/agentprep-skill)
> (validado de ponta a ponta em 13/jul/2026). Publicação: ao alterar
> `skill/agentprep/SKILL.md` aqui (fonte da verdade), copiar pro repo público e push.

### Opção B — `git clone`

```bash
git clone https://github.com/marcelomar21/agentprep-skill.git /tmp/agentprep-install
mkdir -p ~/.claude/skills
cp -r /tmp/agentprep-install/agentprep ~/.claude/skills/agentprep
rm -rf /tmp/agentprep-install
```

### Opção C — cópia manual

Se você recebeu apenas o conteúdo de `skill/agentprep/SKILL.md` (por exemplo, colado em
um e-mail ou baixado de um link), crie o arquivo manualmente:

```bash
mkdir -p ~/.claude/skills/agentprep
$EDITOR ~/.claude/skills/agentprep/SKILL.md   # cole o conteúdo recebido
```

## Ativar

Não existe um passo de "instalação" separado de configuração — na primeira vez que você
pedir algo relacionado (`/agentprep quest`, "bora estudar pro CCA-F", etc.), o Claude
Code segue o fluxo de **Setup** descrito no próprio `SKILL.md`: ele pergunta sua license
key, confirma o idioma (en / pt-BR / es) e ativa a chave contra a API
(`POST /v1/licenses/activate`). O resultado fica salvo em `~/.agentprep/config.json` —
você não precisa editar esse arquivo manualmente, exceto para trocar de idioma ou apontar
para outra API (`api_url`) durante testes.

## Uso do dia a dia

Dentro de qualquer sessão do Claude Code:

```
/agentprep quest       # quest diária — 5 questões com tutoria socrática
/agentprep simulado    # simulado completo — 60 questões / 120 min, modo prova
/agentprep stats       # XP, nível, rank, streak, accuracy por domínio
```

Também funciona por linguagem natural ("bora fazer a quest de hoje", "quero um simulado
do CCA-F") — a descrição da skill (`SKILL.md`) já lista os gatilhos que o Claude Code
reconhece.

## Testando localmente contra uma API self-hosted

```bash
export AGENTPREP_API_URL=http://localhost:8080
```

Com essa variável setada, a skill usa esse endpoint em vez do `api_url` salvo no config.
Use junto com uma `DEV_LICENSE_KEYS` da API local (ver `.env.example` na raiz do repo).

## Desinstalar

```bash
rm -rf ~/.claude/skills/agentprep
rm -rf ~/.agentprep   # remove license key salva e preferências locais
```
