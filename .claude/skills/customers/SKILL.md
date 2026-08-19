# Skill: Customer Research & Context

## Quando ativar
Ativa este skill sempre que a utilizadora mencionar:
- "novo cliente", "nova empresa", "novo projecto"
- O nome de uma empresa com quem ainda não trabalhou (não existe pasta em `customers/`)
- "pesquisa [nome da empresa]", "analisa [nome da empresa]"

## Workflow obrigatório (executa sempre por esta ordem)

### Passo 1 — Verificar se já existe contexto
Verifica se `customers/<nome-empresa>/context.md` já existe.
- Se sim: lê o ficheiro e usa como base. Pergunta se quer atualizar.
- Se não: avança para o Passo 2.

### Passo 2 — Recolher informação básica
Pergunta à utilizadora (se não tiver dito):
- Nome exato da empresa
- Website (se souber)
- LinkedIn da empresa (se souber)
- Qualquer documento que queira partilhar (deck, proposta, email recebido)

### Passo 3 — Pesquisa online
Usa WebSearch e WebFetch para recolher:

**Website:**
- O que fazem (produto/serviço, proposta de valor)
- Mercados e geografias
- Dimensão estimada (nº de funcionários, clientes, faturação se pública)
- Página "About", "Team", "Clients/Cases"

**LinkedIn (usa `site:linkedin.com/company/<empresa>` se não tiveres o URL direto):**
- Tamanho da equipa
- Setor de atividade
- Posts recentes (últimos 3-6 meses) — usa `site:linkedin.com/posts` com o nome da empresa
- Tom de comunicação (formal, técnico, inspiracional, etc.)
- Temas recorrentes nos posts

**Notícias e presença pública:**
- Pesquisa `"<nome empresa>" news site:pt` ou equivalente
- Financiamentos, parcerias, expansões, prémios recentes
- Qualquer evento ou mudança relevante nos últimos 6 meses

### Passo 4 — Criar estrutura de pastas
Cria a seguinte estrutura em `customers/<nome-empresa>/`:

```
customers/<nome-empresa>/
├── context.md              ← ficheiro principal (criado agora)
├── 1. Research/
│   └── README.md           ← placeholder para análise aprofundada
├── 2. Onboarding Forms/
│   └── README.md           ← placeholder para onboarding preenchido
├── 3. Meetings/
│   └── README.md           ← placeholder para prep de reuniões
└── 4. Improvements/
    └── README.md           ← placeholder para melhorias identificadas
```

### Passo 5 — Preencher context.md
Usa o template abaixo e preenche com o que encontraste. Marca com `[A PREENCHER]` o que não conseguiste encontrar — não inventes.

```markdown
# [Nome da Empresa] — Contexto GTM

**Última atualização:** [data]
**Fonte:** pesquisa automática + [documentos fornecidos se aplicável]

---

## Visão Geral
- **O que fazem:** 
- **Proposta de valor:**
- **Setor:**
- **Dimensão:** [nº funcionários / clientes / receita se pública]
- **Sede / Geografias:**
- **Website:**
- **LinkedIn:**

## Pessoas-Chave
[Lista de founders, C-suite, decisores identificados — nome, cargo, LinkedIn se encontrares]

## Presença no LinkedIn
- **Seguidores:** [número se disponível]
- **Frequência de posts:**
- **Tom de comunicação:**
- **Temas recorrentes:**

## Posts Recentes (últimos 3-6 meses)
[Resume os 3-5 posts mais relevantes — tema, ângulo, engagement se visível]

## Notícias / Eventos Recentes
[Financiamentos, parcerias, expansões, prémios, mudanças de liderança]

## Análise GTM
- **O que funciona bem na sua comunicação:**
- **O que está em falta ou pode ser melhorado:**
- **Possíveis dores/problemas que a Inês pode resolver:**
- **Ângulo de entrada recomendado:**
- **Signals de timing:** [porquê agora é bom momento para contactar]

## Notas da Inês
[Espaço para notas manuais adicionadas depois da pesquisa automática]
```

### Passo 6 — Resumo final
No final, dá um resumo em **5-7 linhas** com:
- O que a empresa faz em linguagem simples
- Dimensão e contexto
- 1-2 insights mais úteis para preparar o primeiro contacto
- O que ficou por preencher e porquê

Não digas apenas "feito" — o resumo é parte do entregável.

---

## Notas técnicas
- LinkedIn bloqueia acesso direto na maioria dos casos. Usa os snippets dos resultados de pesquisa Google como fallback — frequentemente têm informação suficiente.
- Se o website usar JavaScript pesado e o WebFetch retornar pouco conteúdo, tenta as subpáginas (/about, /team, /clients).
- Nunca inventes informação. Marca sempre com `[A PREENCHER]` o que não encontraste.
