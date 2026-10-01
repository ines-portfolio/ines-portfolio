# Prospecting Clay with Clay: 3 campaigns, 1 workbook

**Goal:** get each of your 3 NY applications in front of a real human at Clay with proof of work. Track it like a pipeline.

| Campaign | Proof asset | Who to reach (3–5 people max) |
|---|---|---|
| Deal Desk | Deal approval workflow + discount calculator | Deal Desk / RevOps lead, 1 teammate, GTM or G&A recruiter |
| GTME & AI Teacher | 3-min Loom teaching one Clay workflow | Head of GTM Eng / Education lead, 1 GTM Engineer, recruiter |
| Growth Strategy Enablement | 1-page "how a new rep prospects with Clay" playbook | Enablement / Growth lead, 1 AE or Sales Manager, recruiter |

Keep it to about 12–15 people in total. At one company, 40 messages looks like spam. 12 looks like you did your homework.

---

## 0. Before you start (10 min)

- [ ] **Fix your portfolio first.** Hiring managers *will* click. Right now `index.html` says *"moving to San Francisco, CA"*, but all 3 roles are in **New York**. It also has `LinkedIn: (add)` / `Portfolio: (add)` placeholders, and the Portfolio section is empty. Add the 3 assets there.
- [ ] Have the 3 asset links + Loom links ready, or use placeholders and fill them later.
- [ ] Clay workspace: free trial credits are enough for about 15 people.

---

## 1. Workbook structure

Create a workbook called **"Clay Job Campaign: Inês"** with 2 tables:

```
Campaigns (3 rows, lookup) ──lookup by Campaign──▶ People (12–15 rows, the work happens here)
                                                       ├─ View: Deal Desk
                                                       ├─ View: GTME & AI Teacher
                                                       ├─ View: Growth Strategy Enablement
                                                       └─ View: Due today (follow-ups)
```

One People table with 3 filtered views, not 3 separate tables. You then build every enrichment and AI column once, and your tracking lives in one place.

### Table 1: Campaigns
Import `campaigns_lookup.csv`. Replace `PASTE_LINK`, `PASTE_LOOM` and the application dates. Edit the **Why Me** lines in your own voice. The AI columns pull from them.

### Table 2: People: find the humans
Use either option:

**Option A (recommended): Clay's "Find People" source**
1. New table → *Find People* → Company: `clay.com`
2. Location: `New York`. Also run once without the location filter, because some hiring managers sit elsewhere.
3. Job title keywords: copy from the `Title Keywords` column, one campaign at a time.
4. Pull about 10 per campaign. Then **delete down to 3–5** using the Persona Tiers below.
5. Add a text column `Campaign` and fill it per row.

**Option B:** Find people on LinkedIn manually and import `people_import_template.csv` with their LinkedIn URLs. Then add *Enrich Person* from the LinkedIn URL.

**Persona Tiers (keep 1 of each per campaign, 2 max for Team Member):**
| Tier | Who | Why |
|---|---|---|
| Hiring Manager | Leads the team the role reports to | Decides |
| Team Member | Would be your peer | Gives a warm internal referral, answers honestly |
| Recruiter | Recruiter/TA who covers GTM or G&A | Already has your application, can flag it |

---

## 2. Columns on the People table (in this order)

Type `/` in any Clay prompt or formula to insert a column reference. Below, `/Column Name` means that.

### Inputs
| Column | Type |
|---|---|
| Campaign | Text (Deal Desk / GTME & AI Teacher / Growth Strategy Enablement) |
| Persona Tier | Select: Hiring Manager / Team Member / Recruiter |
| First Name, Last Name, Title, LinkedIn URL | From Find People |

### Enrichment
| # | Column | Clay action |
|---|---|---|
| 1 | **Campaign Info** | *Lookup Single Row in Other Table* → table `Campaigns`, match `Campaign` = `/Campaign`. Then extract `Role Applied`, `Asset Link`, `Loom Link`, `Angle`, `Why Me` as their own columns. |
| 2 | **LinkedIn Profile** | *Enrich Person from LinkedIn Profile* (headline, summary, tenure, past companies) |
| 3 | **Recent Posts** | *Get LinkedIn posts* for the person (or the Claygent below) |
| 4 | **Work Email** | *Work Email* waterfall (Findymail → Prospeo → Hunter, etc.) + *Validate Email*. Only keep emails marked `valid`. |
| 5 | **Public Signal** (Claygent) | Prompt below |

**Claygent: Public Signal**
```
Find one specific, recent (last 6 months) public thing that /First Name /Last Name
(/Title at Clay) has said, written, posted, or presented. Look at LinkedIn posts,
podcasts, YouTube, Clay's blog/community, conference talks.

Return JSON:
{"signal": "<one sentence, concrete, what they said or made>",
 "source_url": "<url>",
 "relevance": "<how it connects to: /Role Applied>"}

If you cannot find anything specific and verifiable, return {"signal": "NONE"}.
Never invent quotes.
```

### Personalized link (so you know who viewed)
Formula column **Tracked Asset Link**:
```js
/Asset Link + (/Asset Link.includes("?") ? "&" : "?") + "ref=" + encodeURIComponent((/First Name + "-" + /Last Name).toLowerCase())
```
If the asset is on your own site or a tool with view analytics (Loom, Notion, a short-link tool like Dub/Bitly), each `ref=` tells you *who* opened it.

Formula column **QR Code URL** (for the handwritten card):
```js
"https://api.qrserver.com/v1/create-qr-code/?size=400x400&data=" + encodeURIComponent(/Tracked Asset Link)
```

### AI writing columns (Use AI → Claude or GPT; temperature low)

Paste this **shared context** at the top of each prompt:
```
You are writing as Inês Rodrigues Gouveia. Background: 6 years in operational support and
compliance at Caixa Geral de Depósitos (bank, Portugal): approvals, controls, complaint
resolution, Salesforce. Now moving into AI-driven GTM work. She applied to /Role Applied at
Clay in New York and built a proof asset for it: /Angle
Why her: /Why Me
Recipient: /First Name, /Title, persona tier /Persona Tier.
Their public signal (use only if not "NONE"): /Public Signal
Tone: warm, direct, specific, zero fluff, no "I hope this finds you well", no flattery
adjectives, no exclamation marks, no em dashes. Sound like a sharp human, not a template.
```

**AI column 1: LinkedIn Note** (send Day 0)
```
Write a LinkedIn connection note. HARD LIMIT 200 characters including spaces.
Structure: name + I applied for [role] + I built [asset, 3-6 words] for it + soft offer to share.
If Persona Tier is Recruiter: mention it's to help them review the application.
If Team Member: ask nothing heavy, just say you'd value their take.
Output only the note.
```
> Example, Deal Desk / Hiring Manager:
> *"Hi Sam, I applied for Deal Desk in NY and built a discount calculator + approval flow for it. Happy to share the link if useful. Inês"*

**AI column 2: Email Subject**
```
Write a 3-6 word email subject, lowercase except names, that names the asset.
No clickbait. Output only the subject.
```
> e.g. `deal desk: built you a discount calculator`

**AI column 3: Email Body** (send Day 3)
```
Write a cold email, max 90 words, 4 short paragraphs:
1. One line hook. If Public Signal exists, connect it to the role in one sentence. Otherwise open with the asset.
2. "I applied for /Role Applied. Instead of telling you I'd be good at it, I built [asset]:" + /Tracked Asset Link
   + one line on what it does.
3. One line from Why Me.
4. CTA by tier. Hiring Manager: "Worth 15 minutes?". Team Member: "Would love your honest take on it."
   Recruiter: "Could you flag it to the hiring team?"
Sign off: Inês. Add the Loom link as a P.S. only if /Loom Link is not empty.
Output only the body.
```

**AI column 4: Follow-up** (send Day 8, same thread)
```
Write a 2-3 sentence follow-up reply to the email above. Add ONE new piece of value:
a specific idea for how this asset/workflow could be used at Clay for /Title's team.
No guilt ("just bumping"). Output only the text.
```

> **Always read each draft before sending.** Fix anything wrong or generic. With only ~15 messages, every one should be perfect.

### Tracking columns
| Column | Type |
|---|---|
| Status | Select: `To contact` → `LI sent` → `LI accepted` → `Email sent` → `Viewed` → `Replied` → `Call booked` / `Referred` / `No response` |
| LI Sent Date | Date |
| Email Sent Date | Date |
| Card Sent Date | Date |
| Viewed Asset? | Checkbox (from Loom/link analytics) |
| Reply | Long text (paste it) |
| Next Step | Text |
| **Follow-up Due** | Formula ↓ |

```js
!/Email Sent Date ? "" :
  ["Replied","Call booked","Referred"].includes(/Status) ? "" :
  new Date(new Date(/Email Sent Date).getTime() + 5*864e5).toISOString().slice(0,10)
```
**View "Due today":** filter `Follow-up Due` ≤ today, `Status` not in Replied / Call booked / Referred.

---

## 3. Cadence (per person)

| Day | Channel | Action |
|---|---|---|
| 0 | LinkedIn | Connection request + **LinkedIn Note**. Set Status = `LI sent`. |
| 1–2 | LinkedIn | If accepted: like or comment *thoughtfully* on one recent post. No pitch. |
| 3 | Email | **Email Subject + Body** with the tracked link. Status = `Email sent`. |
| 4 | Mail (optional) | Handwritten card to Clay's NY office: 3 lines + QR code (print from `QR Code URL`). Only for the **Hiring Manager** tier. Verify the office address on clay.com / LinkedIn first. |
| 8 | Email | **Follow-up** in the same thread. |
| 14 | LinkedIn | If no reply: one-line DM with the Loom. Then stop. Status = `No response`. |

**Stagger the campaigns** by 2–3 days so Clay doesn't get all 15 messages at once. Start with the one you're strongest for. Based on your background, that's **Deal Desk**.

---

## 4. Weekly scoreboard

Add a small summary on top of the People table (or just count from the views):

| Metric | Deal Desk | GTME | Enablement |
|---|---|---|---|
| Contacted | | | |
| LI accepted % | | | |
| Viewed asset | | | |
| Replied | | | |
| Conversations | | | |

---

## 5. Bonus Loom: "How I prospected Clay with Clay" (about 3 min)

This workbook *is* the GTM Engineer proof. Record it after the first campaign is live:

1. **0:00–0:20.** "I applied for 3 roles at Clay. Instead of waiting, I ran it as a GTM campaign, in Clay."
2. **0:20–1:00.** The Campaigns lookup table → the People table → Find People filters → why only 3–5 people per role.
3. **1:00–1:50.** The enrichment chain: LinkedIn → Claygent public signal (show the "never invent quotes" guardrail) → email waterfall + validation.
4. **1:50–2:30.** The AI columns: one shared context + tier-based CTAs, tracked links and QR codes, the Follow-up Due formula.
5. **2:30–3:00.** The scoreboard + what you'd improve (e.g. auto-push replies to Slack, or score personas by signal strength). End with: "I'd love to build this for Clay's customers."

Send this Loom as the Day-14 touch to the hiring managers, and put it on your portfolio.

---

## Checklist

- [ ] Fix portfolio (NY, LinkedIn link, 3 assets)
- [ ] Build / finish the 3 assets
- [ ] Import `campaigns_lookup.csv`, fill links, edit "Why Me"
- [ ] Find People → trim to 3–5 per campaign
- [ ] Add enrichment → AI → tracking columns
- [ ] Review every draft by hand
- [ ] Launch Deal Desk → GTME (+2 days) → Enablement (+4 days)
- [ ] Record the bonus Loom
