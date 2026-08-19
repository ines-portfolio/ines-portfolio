# Newronium GTM — Contexto do Projeto

## Quem sou eu
**Inês Gouveia** — GTM Engineer freelance, contratada pelo grupo Newronium.
- Email: ines.gouveia@newronium.ai
- Fundo: 8 anos na CGD, departamento de operações (backoffice, KPIs, reporting, ambiente regulado)
- Função atual: montar o processo de outbound e demand generation para as brands do grupo

---

## O Cliente

**Newronium Group** — holding portuguesa com várias marcas. Não faz campanhas próprias — é só o veículo de contrato e faturação.

### Interlocutores
- **José Velez** — quem me colocou no projeto. Visão estratégica, perfil COO. Aprova decisões.
- **João Sanches** — operacional técnico. Estava a gerir Apollo e setup antes de mim. Está a passar o testemunho e sai em breve.

---

## As Brands (por ordem de prioridade de campanha)

### 1. Valuedate ✅ PRONTA PARA ARRANCAR
- **O que é:** empresa de Data & AI — ajuda empresas a tirar valor dos dados
- **Domínio:** valuedate.net (alojado no GoDaddy, email no Microsoft 365)
- **Email de campanha:** ines.gouveia@valuedate.net (configurado no Apollo)
- **Autenticação DNS:** SPF ✅ DKIM ✅ DMARC ✅
- **Warmup:** em curso no Apollo (Progressive, min 10 / max 40 / reply rate 30% / continuous warmup ON)
- **ICP grande empresa:** Head of Data · Data Engineering Manager · Director of Analytics (Nível 1 cold email) + CDO · CTO · VP Data (Nível 2 estratégico)
- **ICP PME (<200):** CTO · VP Engineering · CEO técnico
- **Geografia:** Portugal (primeiro) → França → Suíça
- **Signals de targeting:** Snowflake, Databricks, BigQuery, dbt nas ofertas de emprego ou stack

### 2. Optimisers ⏳ A AGUARDAR DOMÍNIO/EMAIL
- **O que é:** staffing/nearshoring de engenheiros de software
- **Nome correto:** Optimisers (não "Optiwisers" nem "Optiwizers")
- **ICP grande empresa:** Head of Engineering · Engineering Manager · Tech Lead · Delivery Manager (Nível 1) + VP Engineering · CTO (Nível 2)
- **ICP PME (<200):** CTO · Head of Engineering · Founder técnico
- **Signal principal:** ofertas de emprego abertas para engenheiros

### 3. New Normal ⏳ A AGUARDAR DOMÍNIO/EMAIL
- **O que é:** consultoria de transformação organizacional, cultura e comunicação
- **ICP grande empresa:** Head of People · Director of Transformation · Director de Comunicação · Head of Culture (Nível 1) + CHRO · CMO · CEO (Nível 2)
- **ICP PME (<200):** CEO · Founder · Managing Partner
- **Segmentos principais (do grid interno):**
  - Corporate: Utilities (EDP, Galp, REN), Banking (CGD, BCP), Retail (Continente), Saúde (CUF), Telecom (NOS, MEO)
  - Growth Business: Tech B2B, Indústria exportadora, Saúde privada, Marcas D2C

### 4. Fullscreen — FORA DAS CAMPANHAS POR AGORA
- Aguardar materiais de pitch e posicionamento

### 5. Newronium — SEM ATIVIDADE COMERCIAL PRÓPRIA
- Não entra em nenhuma campanha

---

## Problema de Entregabilidade (crítico)

**Situação:** contas Microsoft 365 + domínios GoDaddy → inbox placement a 0% no Microsoft 365 (que é o que importa para B2B).

**Causa:** pool de warmup do Apollo é maioritariamente Gmail → constrói reputação nos servidores Google, não nos Microsoft. O Exchange Online Protection da Microsoft é muito agressivo com domínios novos.

**Opções apresentadas ao José Velez:**
- **Opção A (recomendada):** Google Workspace em subdomínios (ex: outreach.valuedate.net) para cold email. ~€6/conta/mês. Google → Microsoft tem entregabilidade muito superior.
- **Opção B1:** Manter Microsoft 365 + trocar ferramenta de warmup para Instantly ou Smartlead (pool com mais contas Microsoft). ~€30-50/mês.
- **Opção B2:** Manter tudo no Apollo mas warmup mais lento (8 semanas) + boas práticas de conteúdo.

**Decisão pendente** — aguardar resposta do José.

---

## Tool Stack

| Ferramenta | Função | Estado |
|---|---|---|
| Apollo.io | Prospeção + listas + sequências de email | Ativo (login: ines.gouveia@newronium.ai) |
| Claude (API) | Personalização de emails com signals | A implementar |
| Dripify | Automação LinkedIn (~€40/mês) | A implementar |
| Make.com | Automação de workflows (~€20/mês) | A implementar |
| HubSpot Free | CRM para gerir replies e calls | A implementar |
| Instantly/Smartlead | Warmup alternativo (se Opção B1) | Pendente decisão |
| Clay | Enriquecimento avançado (~€150/mês) | NÃO agora — volume não justifica |

---

## Workflow de Personalização (sem Clay)

1. Apollo → exportar lista com nome + empresa + cargo + LinkedIn URL
2. Pesquisar manualmente 1 signal por lead (post recente LinkedIn, notícia, oferta de emprego)
3. Claude → gerar primeira linha personalizada em batch de 20-30
4. Colar nas sequências Apollo antes de ativar

---

## Estrutura de Sequência (cold email)
- **Dia 1:** Email personalizado (plain text, sem imagens, sem links ou máx 1)
- **Dia 4:** Follow-up + valor / caso de uso
- **Dia 8:** Touch LinkedIn (via Dripify)
- **Dia 14/16:** Break-up email

---

## Estrutura de Pastas deste Projeto

```
GTM-Projects/
└── newronium-gtm/
      ├── CONTEXT.md                    ← este ficheiro
      ├── 00-Client-Context/            ← relação com o grupo (José, João)
      ├── Valuedate/
      │   ├── 1. Research/
      │   ├── 2. Onboarding Forms/
      │   ├── 3. Meetings/
      │   └── 4. Improvements/
      ├── Optimisers/
      │   ├── 1. Research/
      │   ├── 2. Onboarding Forms/
      │   ├── 3. Meetings/
      │   └── 4. Improvements/
      └── New Normal/
            ├── 1. Research/
            ├── 2. Onboarding Forms/
            ├── 3. Meetings/
            └── 4. Improvements/
```

---

## Estado Atual (Agosto 2026)

- [x] Valuedate configurada no Apollo (email + DNS + warmup)
- [x] Problema de entregabilidade identificado e documentado
- [x] Email enviado ao José com opções de resolução
- [x] ICP definido por brand com lógica de dois níveis (operacional + estratégico)
- [ ] Decisão do José sobre infraestrutura de envio
- [ ] Domínios e emails da New Normal e Optimisers
- [ ] Primeiras listas Apollo para Valuedate Wave 1
- [ ] Sequências de email escritas por brand
