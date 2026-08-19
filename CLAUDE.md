# GTM Projects — Instruções para Claude Code

## Quem sou eu
**Inês Gouveia** — GTM Engineer freelance.
Fundo: 8 anos na CGD (operações, backoffice, KPIs, ambiente regulado).
Função: montar processos de outbound e demand generation para os clientes que trabalho.

## Como está organizado este workspace

```
GTM-Projects/
├── CLAUDE.md                    ← este ficheiro (lê sempre)
├── .claude/skills/customers/    ← skill de pesquisa automática de clientes
├── _Templates/                  ← templates reutilizáveis
├── customers/                   ← um subdiretório por cliente novo
│   └── <NomeEmpresa>/
│       ├── context.md
│       ├── 1. Research/
│       ├── 2. Onboarding Forms/
│       ├── 3. Meetings/
│       └── 4. Improvements/
└── newronium-gtm/               ← projeto ativo atual (Newronium Group)
    ├── CONTEXT.md               ← contexto completo do projeto Newronium
    └── ...
```

## Regras de trabalho

### Novo cliente
Quando a Inês mencionar uma empresa nova ou pedir pesquisa sobre um cliente:
→ Ativa automaticamente o skill em `.claude/skills/customers/SKILL.md`
→ Não perguntes se deves fazê-lo — faz e dá o resumo

### Projeto ativo (Newronium)
O contexto completo está em `newronium-gtm/CONTEXT.md`. Lê-o sempre que trabalhares em algo relacionado com Newronium, Valuedate, Optimisers ou New Normal.

### Criação de ficheiros
- Documentos de leitura humana (emails, playbooks, cheat sheets) → HTML com design limpo
- Análises e contexto → Markdown (.md)
- Logs e registos → Markdown (.md)
- Nunca cries ficheiros desnecessários — menos é mais

### Idioma
- Trabalha em português europeu por defeito
- Muda para inglês só se a Inês pedir ou se o destinatário for estrangeiro

### Tom
- Direto, profissional, sem floreados
- Quando deres uma recomendação, diz porquê em 1 linha
- Quando algo estiver em falta ou incerto, diz claramente — não inventes

## Skills disponíveis

| Skill | Trigger | O que faz |
|---|---|---|
| Customer Research | Empresa nova mencionada | Pesquisa online, cria context.md, dá resumo |

## Stack GTM (referência rápida)
- **Apollo.io** — prospeção + listas + sequências email
- **Dripify** — automação LinkedIn
- **Make.com** — automação de workflows
- **HubSpot Free** — CRM para replies e calls
- **Claude API** — personalização de emails com signals
