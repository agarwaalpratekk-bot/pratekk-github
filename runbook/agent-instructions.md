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
7. **Deliver:** create the brief as a **draft** to `pratekk@growthcap.vc` (v1). Once he says
   "just send it", switch to send. Never send to third parties.
8. **End with the feedback ask.** Non-negotiable.

## Each Friday run — steps
1–2. As above, plus pull the week's **EOD reports** and **MoM** emails.
3. **Funnel rollup** across Neeti/Shruti/Smridh (one shared funnel). Label counts as
   email-observable floors; state the WhatsApp caveat.
4. **Investor-update draft** via `templates/investor-update.md` — run the portfolio
   fact-check checklist first.
5. Write `outputs/weekly/{date}-weekly-brief.md`; deliver as draft; end with feedback ask.

## Standing constraints
- **No auto-send to third parties.** Draft only; briefs go to Pratekk's own inbox.
- **Confirm before big mailbox pulls** (e.g. the 12-month voice read) — don't silently max.
- **Flag WhatsApp-dependent gaps inline** rather than presenting partial data as complete.
- **Feedback loop is mandatory** every run.

## Turning it on (durable schedule) — pending Pratekk's OK
Do **not** enable auto-generation silently. Once he approves:
- Create two durable scheduled triggers (Claude Code routine) that each fire a fresh
  session with the prompt: *"Run the GrowthCap daily/weekly brief per
  `runbook/agent-instructions.md`; read Outlook live; write the dated output; create the
  brief as a draft to pratekk@growthcap.vc; end with the feedback ask."*
- Daily `0 2 * * *` UTC (07:30 IST) and Friday `0 11 * * 5` UTC (16:30 IST).
- First 1–2 weeks: **draft-only**, so he audits before we flip to auto-send-to-self.
