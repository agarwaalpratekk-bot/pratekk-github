# Routines — the GrowthCap agents (paste-ready)

Five scheduled agents. Each one runs on its own at a fixed time, reads Outlook, and emails
**only pratekk@growthcap.vc**. Nobody re-types instructions. The only direct-to-team emails
allowed are the EOD reminders and the pitch nudges described below.

## How to create each one (claude.ai → Routines → New routine)
For every routine below:
1. **Name / schedule:** as listed (time zone **Asia/Kolkata**).
2. **Repository:** `agarwaalpratekk-bot/pratekk-github`, branch `claude/growthcap-ai-ops-layer-ic5hnu`.
3. **Connectors:** tick **Microsoft 365**. This is what was missing on 5–6 Oct, when the runs
   fired but couldn't read or send mail.
4. **Each run:** start a **new session** each time.
5. **Prompt:** paste the block.

Then **turn off the three old routines** (Daily Brief `trig_015yCq…`, EOD check `trig_015Wy…`,
Weekly `trig_01Mnpy…`) so nothing runs twice. They have no Microsoft 365 connection and
fail anyway.

Every prompt ends with a guard: if Microsoft 365 tools don't load, stop and say so, and
never claim a send that didn't happen.

| # | Agent | Schedule (IST) |
|---|---|---|
| 1 | Morning Research Brief | 07:20 Mon–Sat |
| 2 | Daily Ops Brief (+ unanswered emails) | 07:30 Mon–Sat |
| 3 | EOD Check | 08:05 Tue–Sun (must run *after* the 08:00 cut-off) |
| 4 | LinkedIn | 09:00 Mon / Wed / Fri |
| 5 | Weekly Brief | 16:30 Fri |

---

## 1. Morning Research Brief — 07:20 Mon–Sat
```
[GrowthCap MORNING RESEARCH BRIEF] Research and SEND today's GrowthCap Morning Brief to Pratekk Agarwaal (GP, GrowthCap Ventures, Mumbai; SEBI Cat II AIF; pre-seed/seed FinTech, DeepTech, AI in India). Public data only. Send ONLY to pratekk@growthcap.vc.

Setup: check out branch claude/growthcap-ai-ops-layer-ic5hnu. Read runbook/feedback-log.md and apply the latest adjustments. Load the Microsoft 365 tools (ToolSearch "select:mcp__Microsoft_365__outlook_send_mail,mcp__Microsoft_365__outlook_email_search,mcp__Microsoft_365__read_resource") plus WebSearch/WebFetch. Open the last "GrowthCap Morning Brief" in Sent Items: use it as the format reference and don't repeat stale news. If Pratekk replied to it, apply the reply and log it in runbook/feedback-log.md.

Portfolio: Spense, Integra Robotics, Mylapay, Navanc, TrusTerra, TransBnk (now TBX), Advance Mobility, Replifine, RePut.ai, LogiXair, Easework AI, FTD Innovations, plus any company whose investor update reached the inbox. Peer India funds: Finvolve / India Accelerator, Arkam, 8i Ventures, Speciale Invest, 100X.VC, All In Capital, Inflexor, Unicorn India Ventures, Navam Capital, and any new India early-stage fund launch.

Sections, in this order (HTML):
1. Top 3 things to know, each with one line on why it matters to GrowthCap.
2. Your portfolio: company | latest dated news (2–3 lines) | why it matters. Include public LinkedIn posts by founders where findable. Write "no new public news since {date}" instead of repeating old items.
3. Peer India VC funds: fund | what's new (closes, deals, hires, LinkedIn announcements) | why it matters.
4. Weekly funding: list EVERY deal behind the latest Inc42/Entrackr weekly headline (startup | amount | stage | sector | lead investors). Flag fintech / deeptech / defence deals and any peer-fund or co-investor participation. If you can't verify every deal, say how many of N you verified.
5. Market and regulation pulse: funding trend; SEBI AIF / RBI / NPCI changes.
6. Caveats and Sources.

Send with outlook_send_mail (bodyType html), To pratekk@growthcap.vc only. Subject: "GrowthCap Morning Brief – {Wkdy D Mon YYYY}: {headline}". Save a copy to outputs/morning/{YYYY-MM-DD}-morning-brief.md, then commit and push. If the Microsoft 365 tools are unavailable, stop and report it plainly. Never email anyone else.
```

## 2. Daily Ops Brief (+ unanswered emails) — 07:30 Mon–Sat
```
[GrowthCap DAILY OPS BRIEF] Generate and SEND today's daily brief to Pratekk now.

Setup: check out branch claude/growthcap-ai-ops-layer-ic5hnu and load the Microsoft 365 tools (outlook_email_search, read_resource, outlook_calendar_search, outlook_send_mail). If they don't load, stop and report it.

1. Feedback: find Pratekk's replies to the last few "Daily Brief" emails in the Inbox (and any feedback in-thread). Log each one as a dated row in runbook/feedback-log.md and apply the adjustment before writing.
2. Read Outlook live: Inbox newest ~50, Sent Items newest ~50, Junk newest ~25, today's and this week's calendar. Don't reuse yesterday's state.
3. Follow runbook/agent-instructions.md and templates/daily-brief.md exactly. Sections, in this fixed order: 🛑 Blocked on you → ⏳ Delegated & gone quiet → 📬 Circling back to you → ✉️ Unanswered emails → 📅 Regulatory deadlines this week → 📅 On the calendar. Every item names an owner and a clock. Match counterparties against docs/03-regulatory-map.md. Always sweep Junk, and add the reassurance line if it's clean. Flag calendar clashes. Flag security alerts (password/recovery changes, credentials sent in clear).
4. ✉️ Unanswered emails: threads from real people (not newsletters, vendor spam or automated mail) with NO reply from Pratekk in the thread, regardless of read state. Read does not mean replied, so confirm against Sent. Each line: sender | subject | received date | days pending | suggested owner (Pratekk / Neeti / Smridh / Shruti). Cap at 8, oldest-highest-stakes first. You may save a short draft reply in Outlook Drafts for the top 3. NEVER send replies to third parties.
5. Pitch tracking (runbook/pitch-tracker.md): open BOTH "Pitches to own & close-loop" threads and read the analyst replies in full. Verify closure against the calendar (call set or held) and the founder-facing thread where Pratekk is cc'd. A deal is open only if there's no analyst reply AND no founder revert AND no meeting. Nudge only that case: 1–3 lines To the analyst, cc pratekk@growthcap.vc, hyphens not em dashes, max once a day, never to anyone on leave or holiday.
6. Write outputs/daily/{YYYY-MM-DD}-daily-brief.md, then commit and push.
7. SEND with outlook_send_mail (bodyType html) to pratekk@growthcap.vc only. Subject: "Daily Brief — {Wkdy D Mon} · {top item}". End with the one-tap feedback ask.
```

## 3. EOD Check — 08:05 Tue–Sun
```
[GrowthCap EOD CHECK, 08:00 IST cut-off] Tell Pratekk which team members did NOT send the previous day's EOD by 08:00 IST today, and send each missing person a direct reminder.

Load the Microsoft 365 tools (outlook_email_search, outlook_send_mail). If they don't load, stop and report it.
Rules: an EOD is on time only if it arrives by 08:00 IST the next morning. Saturday IS a reporting day; Sunday is not. Skip national holidays (the office@growthcap.vc "Holiday - X" calendar) and anyone who emailed a leave notice for that day.
Team (each sends from their own address to pratekk@growthcap.vc):
- Neeti - Neeti.B@growthcap.vc - "EOD - {date}"
- Shruti - Shruti.Inani@growthcap.vc - "Eod {date}" / "Discoverability + EOD for {date}"
- Smridh - Smridh.K@growthcap.vc - "EOD | {dd.mm.yyyy}" or a reply on the "EOD Report" thread
Steps: for each person, search the Inbox by sender with afterDateTime = yesterday. Received before 08:00 IST today = on time.
Send Pratekk ONE short email (bodyType html):
- If anyone is missing: subject "EOD check — {names} missing for {date}", one line on who's missing and one on who's in.
- If everyone is in: subject "EOD check — all 3 in ✅ ({date})".
For each genuinely missing person only, send a separate warm reminder To that person only (no cc): "Hi {first name}, quick note - I didn't receive your end-of-day report for {date}. Could you send it across when you get a moment? Thanks, Pratekk". Use hyphens, not em dashes. If the checked day was a Sunday, email the team nothing.
```

## 4. LinkedIn — 09:00 Mon / Wed / Fri
```
[GrowthCap LINKEDIN] Prepare Pratekk's LinkedIn pack and email it to pratekk@growthcap.vc only. There is no LinkedIn connection, so NEVER post or message anyone. Draft only.

Setup: check out branch claude/growthcap-ai-ops-layer-ic5hnu. Read docs/02-voice-profile.md (his voice) and runbook/feedback-log.md. Load the Microsoft 365 tools (outlook_email_search, read_resource, outlook_send_mail) and WebSearch. If Microsoft 365 doesn't load, stop and report it.

1. LinkedIn inbox digest: search the Inbox for mail from linkedin.com since the last LinkedIn pack (or the last 3 days). Group it into: messages/InMails that need a reply (who, what they want, suggested 1-line reply); mentions/comments on his posts; connection requests worth accepting (founders, LPs, fund peers); ignore the rest. Max 10 lines.
2. Portfolio and peer LinkedIn watch: via web search, find public LinkedIn posts or announcements from the last few days by portfolio founders (Spense, Integra Robotics, Mylapay, Navanc, TrusTerra, TBX/TransBnk, Advance Mobility, LogiXair, Easework AI, FTD Innovations, Replifine, RePut.ai) and peer funds (Finvolve, Arkam, 8i, Speciale, 100X.VC, All In Capital). For each: what they posted and whether Pratekk should like, comment or reshare, with a suggested one-line comment.
3. Post drafts: 2–3 ready-to-post drafts in his voice, drawn from this week's real material (portfolio milestones, a deal-funnel or market insight from the Morning Brief, the GrowthCap Signals newsletter, IVCA/SEBI events). 80–200 words each, with a hook in line one, no hashtag spam (max 3), and no confidential deal or LP info. Write "[needs your OK]" against any claim about a portfolio company that isn't already public.

Send with outlook_send_mail (bodyType html), subject "LinkedIn pack — {Wkdy D Mon}: {n} to reply, {n} drafts". Save a copy to outputs/linkedin/{YYYY-MM-DD}-linkedin.md, then commit and push.
```

## 5. Weekly Brief — 16:30 Fri
```
[GrowthCap WEEKLY BRIEF] Generate and SEND this week's Friday brief to Pratekk now.

Setup: check out branch claude/growthcap-ai-ops-layer-ic5hnu and load the Microsoft 365 tools. If they don't load, stop and report it.
1. Log any of Pratekk's replies to this week's briefs in runbook/feedback-log.md and apply them.
2. Read Outlook live: Inbox and Sent (newest ~50 each), Junk (~25), this week's EODs (Neeti, Shruti, Smridh), Minutes-of-Meeting emails, and this week's calendar.
3. Follow runbook/agent-instructions.md and templates/weekly-brief.md: (a) open loops and regulatory items; (b) the deal funnel across Neeti, Shruti and Smridh as one shared funnel, with counts labelled as EMAIL-OBSERVABLE FLOORS and the WhatsApp caveat stated; (c) an investor-update draft via templates/investor-update.md in his voice (docs/02-voice-profile.md), after running the portfolio fact-check checklist. On the last Friday of the month, add the health-metric readout.
4. Write outputs/weekly/{YYYY-MM-DD}-weekly-brief.md, then commit and push.
5. SEND with outlook_send_mail (bodyType html) to pratekk@growthcap.vc only. Subject: "Weekly Brief — wk of {D Mon} · funnel + investor draft". End with the feedback ask. Never send anything to LPs or third parties.
```
