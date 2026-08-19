---
name: customers
description: Use this skill whenever the user is about to start working with a new company, client, or customer — before a project, meeting, pitch, or outreach. Triggers include "novo cliente", "nova empresa", "cliente novo", "pesquisar empresa", "pesquisar empresa no linkedin", "contexto sobre a empresa", "new client", "new company", "working with a new company", "customer research", "company context", "research this company", or simply naming a company the user hasn't worked with before ("temos uma reunião com a Empresa X amanhã", "vou começar a trabalhar com a Empresa Y"). Compiles a structured research dossier — official info, industry/positioning, and LinkedIn presence including recent posts — and saves it to customers/<company>/context.md for reuse. Use this proactively even if the user doesn't explicitly ask for "research".
---

# Customers — Company Context Research

## Why this exists

Before starting work with a new client, arriving prepared with real context — what the company does, how they present themselves publicly, what they've posted about recently — makes conversations sharper and proposals more relevant. This skill turns "let me quickly check them out" into a repeatable, saved dossier instead of one-off scattered searches.

## When to run this

Run it any time the user is about to engage with a company they haven't worked with before: a new client, a lead, a company they're meeting, pitching, or just researching. If it's unclear whether context already exists for this company, check `customers/` first (see below) before researching from scratch.

## Step 1 — Identify the company

Confirm the company name (and, if given, a website or LinkedIn URL) before researching. If the user only gives a vague reference ("aquela empresa de tecnologia que me contactou"), ask a clarifying question rather than guessing.

## Step 2 — Check for existing context

Look for `customers/<slug>/context.md` (slug = lowercase, hyphenated company name, e.g. `customers/acme-corp/context.md`) in this repo. If a file already exists, read it, tell the user what's already known, and only refresh the parts that are stale (e.g., re-check recent posts) instead of redoing everything from scratch.

## Step 3 — Research the company

Use WebSearch and WebFetch — there's no LinkedIn API available, and LinkedIn itself often blocks direct scraping of company pages. Work around this with a layered approach:

1. **Official site** — WebFetch the company's own website (About, Team, Product/Services, Blog/News pages) for the ground-truth description of what they do.
2. **LinkedIn company page** — WebSearch for `site:linkedin.com/company/<name>` (or the plain company name + "linkedin") to find the URL, then WebFetch it. If LinkedIn returns a login wall or blocked content, fall back to what the WebSearch result snippets already show (about text, employee count, industry, HQ), and note in the file that the page itself couldn't be fetched directly.
3. **Recent LinkedIn posts** — WebSearch for `site:linkedin.com/posts <company name>` and `"<company name>" linkedin posts`, and also check Google News and the company's own newsroom/blog for recent announcements. Capture the last ~3–6 months of activity: product launches, funding, hires, partnerships, events — and get a read on tone/voice (formal/corporate vs casual, thought-leadership vs product-focused, etc.).
4. **Wider context** — general news coverage, funding/size signals if surfaced by search, competitors, and industry positioning.

Don't over-fetch: a handful of well-chosen searches and page fetches beat a long scattershot list. Stop once you have enough to write a genuinely useful dossier, not just enough to fill every section — skip a section entirely rather than padding it with guesses.

## Step 4 — Write the context file

Save the result to `customers/<slug>/context.md` (create the directory if it doesn't exist). Use this structure:

```markdown
# <Company Name>

*Researched: <date>*

## Overview
- Website:
- Industry:
- Size (employees):
- HQ / locations:
- Founded:
- What they do (1-2 paragraphs, in your own words):

## LinkedIn
- Company page: <url>
- Followers (if visible):
- About text (as written on their page, if fetchable):

## Recent posts & activity (last ~3-6 months)
- <date> — <summary of post/announcement, with link>
- <date> — <summary of post/announcement, with link>

## Tone & voice
Brief read on how they communicate publicly (formal/casual, thought-leadership, product-led, etc.) — useful for matching tone in outreach or deliverables.

## Notes / talking points
Anything relevant to working with them: recent wins worth mentioning, pain points implied by their posts, competitors, potential angles for a pitch.

## Sources
- <links used>
```

## Step 5 — Summarize for the user

After saving the file, give the user a short spoken summary (a few sentences, not the whole file) of the most useful or notable findings, and point them to the saved file path. Don't just say "done" — surface the one or two things most worth knowing before they walk into a meeting or send a pitch.
