# Today: 6–8 people, one message each, one follow-up

This replaces the 3-campaign plan in `CLAY_BUILD_GUIDE.md`. You now run one short list, on Clay's NY sales side, with one ask: **15 minutes over coffee near the office before Nov 30.**

## 1. The list (8 max)

| # | Who | How many |
|---|---|---|
| 1–5 | GTM Engineers (GTMEs), NY | 4–5 |
| 6–7 | ClayDRs, NY | 1–2 |
| 8 | Whoever manages the ClayDR team | 1 |

Import `today_shortlist.csv` or start straight from Find People (below).

## 2. Build it in Clay (about 30 min)

New workbook **"Prospecting Clay with Clay"** → new table → **Find People**:
- Company: `clay.com`
- Location: `New York`
- Job titles, one search each:
  - `GTM Engineer`, `GTM Engineering`
  - `ClayDR`, `Development Representative`, `SDR`, `BDR`
  - `ClayDR Manager`, `Development Manager`, `SDR Manager`, `Head of Development`
- Look at the results and **keep 6–8 people**. Prefer people who post on LinkedIn, because they're easier to write to and more likely to reply.

Add these columns:

| Column | Clay action | Why |
|---|---|---|
| LinkedIn Profile | Enrich Person from LinkedIn | headline, tenure, background |
| Recent Post | Claygent (prompt below) | one real thing to mention |
| Work Email | Work Email waterfall + Validate Email | send only to `valid` |
| Direct Phone | Mobile/phone waterfall | **call only if one is found** |
| Personal Line | Use AI (prompt below) | the one personal sentence |
| Email / LinkedIn Note / Follow-up | Formulas or AI, from the templates below | drafts to review |
| Sent Date | Date | |
| Follow-up Due | Formula: `Sent Date` + 3 days | |
| Status | Select: To send / Sent / Followed up / Replied / Coffee booked / Moved on | |

**Claygent: Recent Post**
```
Find one specific public thing /First Name /Last Name (/Title at Clay, New York) posted,
wrote or said in the last 6 months (LinkedIn, Clay blog, podcast, talk).
Return one sentence describing it, plus the URL. If nothing verifiable, return NONE.
Never invent or paraphrase quotes you didn't find.
```

**AI: Personal Line**
```
Write ONE sentence (max 20 words) to /First Name that references /Recent Post naturally,
without flattery. If /Recent Post is NONE, reference their role (/Title) and what
GTMEs/ClayDRs do at Clay instead. No exclamation marks, no em dashes. Output only the sentence.
```

**Follow-up Due formula**
```js
/Sent Date ? new Date(new Date(/Sent Date).getTime() + 3*864e5).toISOString().slice(0,10) : ""
```

## 3. The messages

Each one has: who you are, one real result, the Clay-on-Clay proof, and one specific ask.

### Email
**Subject:** `coffee before Nov 30? (found you with Clay)`

```
Hi {First Name},

I'm Inês. I spent six years in banking ops and compliance and now build outbound in Clay.
My last campaign went to 150 contacts and got 14 replies and 7 meetings.

I found you the same way: a Clay table of Clay's NY GTMEs and ClayDRs, enriched and
drafted from there. {Personal Line}

I've applied to Clay in New York and would love 15 minutes of your take, over coffee near
the office, any day before November 30. Happy to work around your calendar.

Inês
```
About 85 words. Keep it there.

### LinkedIn connection note (171 characters, under the 200 limit)
```
Hi {First Name}, I found you with a Clay table I built to prospect Clay. My last campaign: 150 contacts, 14 replies, 7 meetings. Coffee near the NY office before Nov 30? Inês
```

### Phone (only if Clay found a direct number), about 20 seconds
> "Hi {First Name}, it's Inês. I'll be quick. I found you through a Clay table I built to prospect Clay. My last campaign got 7 meetings from 150 contacts. I've applied to the NY team and I'd love 15 minutes over coffee near the office before the end of November. I've also sent you an email. Is there a day that works?"

If it goes to voicemail, leave the same message once. Don't call again.

### Follow-up, once, 3 days later (reply in the same email thread)
```
Hi {First Name}, following up once. Even 15 minutes before or after work near the
office would be great, any day before Nov 30. If the timing's wrong, no problem,
and thanks either way.

Inês
```
On LinkedIn, if they accepted but didn't reply, send the same 2 lines as a DM.
**Then set Status = Moved on and stop.**

## 4. Today's checklist

- [ ] Find People → keep 6–8 (4–5 GTMEs, 1–2 ClayDRs, 1 ClayDR manager)
- [ ] Enrich: LinkedIn, email (validated), phone, Recent Post
- [ ] Generate Personal Line → **read and fix every draft by hand**
- [ ] Send email + LinkedIn note to each person; call the ones with a direct number
- [ ] Fill in Sent Date. Follow-up Due fills itself in.
- [ ] In 3 days: one follow-up each → then Moved on
- [ ] Take screenshots of the table as you go. They're your "Prospecting Clay with Clay" proof for the coffee chats and a future Loom.

**Before you hit send:** your portfolio still says "moving to San Francisco" and has empty LinkedIn and portfolio links. Anyone who clicks will see that.
