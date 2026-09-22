# Runbook — how the routine runs

The "engine" is a **scheduled Claude session** with live Microsoft 365 (Outlook) access to
`pratekk@growthcap.vc`. It runs twice on a cadence and writes to this repo.

## Cadence
- **Daily, ~07:30 IST** → generate the daily brief.
- **Friday, ~16:30 IST** → generate the weekly brief.

Because the plain in-session scheduler is ephemeral, the durable version uses a **Claude
Code routine / scheduled trigger** (see "Turning it on" below). Times are IST; convert to
UTC when the scheduler is UTC-based (07:30 IST = 02:00 UTC; 16:30 IST = 11:00 UTC).

## Each daily run — steps
1. **Read live** (do not trust yesterday's cache):
   - Inbox, newest ~50; Sent Items, newest ~50; **Junk**, newest ~25; today+week calendar.
2. **System 1 — regulatory sweep:** match inbox + Junk against `docs/03-regulatory-map.md`
   (counterparties, entities, recurring rhythms). Extract hard deadlines within 7 days.
   Note if Junk is clean (reassurance line).
3. **Blocked-on-him:** find loops stalled on Pratekk's sign-off/decision (valuation
   certification, RSU/stamp-duty calls, fee-proposal go-aheads, approvals addressed to him).
4. **Delegated & gone quiet:** scan Sent Items for his delegation syntax (`++ @Name`,
   `Looping in`, `request X to`, `pls take forward`); set the clock from the send date;
   tag confidence. Add inbound "circling back" loops (filter vendor spam).
5. **Write** `outputs/daily/{date}-daily-brief.md` from `templates/daily-brief.md`. Half a
   page. Every item: owner + clock.
6. **Apply feedback:** read `runbook/feedback-log.md` and adjust length/content/emphasis per
   his latest answers before finalising.
7. **Deliver:** **send** the brief to `pratekk@growthcap.vc` via `outlook_send_mail`
   (bodyType `html`). He said "just start sending" on 2026-09-06, so v1 is now send-to-self,
   not draft. **Never send to third parties** — only to his own inbox.
8. **End with the feedback ask.** Non-negotiable.

## Each Friday run — steps
1–2. As above, plus pull the week's **EOD reports** and **MoM** emails.
3. **Funnel rollup** across Neeti/Shruti/Smridh (one shared funnel). Label counts as
   email-observable floors; state the WhatsApp caveat.
4. **Investor-update draft** via `templates/investor-update.md` — run the portfolio
   fact-check checklist first.
5. Write `outputs/weekly/{date}-weekly-brief.md`; **send** to his own inbox; end with feedback ask.

## Each EOD-check run — steps (08:00 IST cut-off, Tue–Sun)
A tiny standalone email: **who on the team missed the previous day's EOD by the 08:00
cut-off.** All three send their own daily EOD to Pratekk from their own address, in the
evening/overnight IST (sends can land past midnight).
- **Cut-off rule (Pratekk, 6 Sep):** an EOD for a day is on-time only if it arrives by
  **08:00 IST the next morning**; later = missed. **Saturday is a reporting day; Sunday is not.**
- Senders + subject patterns: **Neeti** `Neeti.B@growthcap.vc` ("EOD - {date}" / "{date} -
  EOD"); **Shruti** `Shruti.Inani@growthcap.vc` ("Eod {date}"); **Smridh** `Smridh.K@growthcap.vc`
  (replies on an "EOD Report" thread, date in the body).
- Per person, search Inbox by **sender + afterDateTime "yesterday"** (date-filtered, not a
  free-text query). Received before 08:00 IST today = on time; else missing.
- **Leave-aware (added 16 Sep):** individual leaves are announced by email — a teammate
  sends a "Leave request - {date}" / "on leave today" note (seen: Neeti → `info@tbrone.in`
  cc Pratekk). If the person being checked emailed a leave notice covering that day, they are
  **on leave, not missing** — say so explicitly, don't flag a gap. Also treat a day on the
  office holiday calendar (`office@growthcap.vc` "Holiday - X") as non-reporting once Pratekk
  confirms; until then, flag-with-context.
- Send one short email to Pratekk only: who's missing (+ who's in / on leave), or "all 3 in ✅".
- Runs **Tue–Sun** at 08:00 (covers **Mon–Sat** EODs). Monday skipped — it would cover
  Sunday, which is not a reporting day. Never nag the team; the email goes to Pratekk only.

## Pitch tracker — keep it live (every daily run)
`runbook/pitch-tracker.md` holds pitches allocated to Neeti & Smridh (22 Sep), each to be
driven to **response closure**. Two allocation emails (subject "Pitches to own & close-loop")
cc Pratekk, so analyst status replies land in his inbox on one thread per analyst.
- Each daily run: read those two threads (search `conversationId` / subject). For each row,
  if the analyst replied since allocation, update **Status** + **Last update** in the tracker.
- Any row still `allocated` (no analyst reply) past the asked-for date → surface it in the
  daily brief under **⏳ Delegated & gone quiet** with a days-pending clock.
- When all rows for an analyst are closed (in diligence / passed), note it and stop chasing.

## Open-loops audit — steps (on-demand sweep)
A periodic "what's slipping" sweep of Inbox + Junk + Sent over the last ~2–3 weeks, grouped
into: (1) startup pitches received, not responded to; (2) other personal emails awaiting his
reply; (3) delegations he made that aren't close-looped; (4) team to-dos with no action.
- **Open-loop rule (corrected 21 Sep):** an item is an open loop when **there is no sent
  reply in the thread** — *independent of read state*. **Read ≠ responded.** The read flag
  only downgrades *urgency* (he's at least seen it); it never closes the loop. The earlier
  audit (20 Sep) keyed "pending" on *unread + no reply* and so dropped read-but-unanswered
  threads (e.g. the **Agrify / Prateek Garg** pitch — read 16 Sep, founder chased 21 Sep, no
  reply). Never gate the audit on unread again.
- **Reply detection:** confirm "no reply" by checking Sent for a message in the same
  conversation / to the sender (recipient filter runs without `folderName`), not by read
  status. A pitch a *teammate* is actively handling (e.g. Neeti/Smridh coordinating a slot)
  is *their* loop, not his — say so rather than listing it as his miss.
- Tag every row with days-pending (to today) and a confidence note; keep the WhatsApp/call
  caveat (email-observable only).

## Standing constraints
- **No auto-send to third parties.** Briefs and the investor draft go to Pratekk's own
  inbox only; he decides what leaves for LPs/counterparties.
- **Confirm before big mailbox pulls** (e.g. the 12-month voice read) — don't silently max.
- **Flag WhatsApp-dependent gaps inline** rather than presenting partial data as complete.
- **Feedback loop is mandatory** every run.

## Turning it on (durable schedule) — LIVE as of 2026-09-06
Enabled on Pratekk's OK ("set up the routines... just start sending emails to him tomorrow
onwards"). Two durable Claude Code routines (scheduled triggers), **bound to the build
session** (`session_01Keys2UxBH3k46qWmWkXHtN`) so his feedback replies land in the same
chat and tune the next run:

| Routine | Trigger ID | Cron (UTC) | Local (IST) | First run |
|---|---|---|---|---|
| Daily brief | `trig_015yCqQbMhHCzcXiesqAtTV9` | `0 2 * * 1-6` | ~07:30 Mon–Sat | Mon 7 Sep |
| EOD check | `trig_015WyFVk2SQishViCNQNeaMw` | `30 2 * * 0,2-6` | ~08:00 Tue–Sun | Tue 8 Sep |
| Weekly brief | `trig_01MnpyZUJ2PMLocevfCfew7f` | `0 11 * * 5` | ~16:30 Fri | Fri 11 Sep |

- **Delivery: send-to-self** (not draft). Sunday is intentionally muted; adjust via feedback.
- **Watch on first live fire (Mon 7 Sep):** the triggers stored no MCP connectors. Because
  they resume *this* session in the same environment that already has Outlook connected,
  the Microsoft 365 tools should reconnect on resume (as they did during the build). If a
  fired run reports no `mcp__Microsoft_365__*` tools, recreate the routines from the
  claude.ai Routines UI (which can attach the connector), keeping the same prompts.
- Managed with `mcp__Claude_Code_Remote__list_triggers` / `update_trigger` / `delete_trigger`.
