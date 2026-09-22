# Feedback log — how the routine learns

Every brief ends with a one-tap ask. His answers are recorded here, and each run reads this
file and adjusts **before** writing. This is the mechanism that makes the system a routine
he tunes, not a static tracker — he asked for it twice; it is a hard requirement.

## How to use
1. After each brief, capture his reply (even one word) as a dated row below.
2. Translate it into a concrete adjustment (length, sections, emphasis, tone).
3. The next run applies the **current** adjustments (latest wins on conflicts) and notes
   which it applied.

## Adjustment levers the routine can pull
- **Length:** tighter / looser (default: half a page daily).
- **Sections:** drop or add (e.g. mute "circling back", add "calendar for tomorrow").
- **Confidence threshold:** hide low-confidence "quiet" items if he finds them noisy.
- **Emphasis:** more regulatory vs more delegation vs more funnel.
- **Tone of the investor draft:** warmer / crisper / more numbers.
- **Delivery:** draft vs send; time of day.

## Current active adjustments
- **Delivery flipped to send-to-self** (was draft) on his instruction 2026-09-06 — the
  briefs now land directly in his inbox, no draft step.
- **Cadence live:** daily Mon–Sat ~07:30 IST, weekly Fri ~16:30 IST. Sunday muted.
- Nothing tuned on content yet — awaiting his first answer.

## Log
| Date | His answer | Adjustment applied next run |
|---|---|---|
| 2026-09-22 | (format feedback) "All tasks in pending seem to be mapped to one in regulatory." Confirmed: **both** — (a) distinct tasks were collapsed into single bullets (Delegated = one bullet with 4 items; Regulatory = Crisil+ODI+audit jammed together), and (b) Regulatory was acting as a catch-all for non-deadline compliance/ops items. | **Two rules added to `templates/daily-brief.md`:** (1) **one task = one line** — never merge items into a bullet; trim by dropping whole lines, never concatenating; (2) **section = category, strictly** — 📅 Regulatory is statutory/regulator items ONLY (no deal/LP/delegation/ops), and this-week hard deadlines are flagged vs. "no hard date" watch items. **Resent** Tue 22 Sep brief in the corrected structure. Applies to all future daily briefs. |
| 2026-09-21 | (correction) "How come the email from Prateek Garg is missed in the missed emails to respond?" — the **Agrify / Prateek Garg** pitch (recd 16 Sep, founder chased 21 Sep) was absent from the 20 Sep open-loops audit. | **Root cause:** the audit keyed "pending" on *unread + no reply*, so **read-but-unanswered** threads dropped out. **Fixed:** open-loop rule is now *no reply in thread, independent of read state* (read only downgrades urgency) — added to `agent-instructions.md` (new "Open-loops audit" section) and applies to daily briefs too. **Resent** corrected audit v2 (led with the fix + Agrify recovered, days re-clocked to 21 Sep). Offered to draft the Agrify pass. |
| 2026-09-20 | (engagement signal + reply) Acted on the Sat brief: replied "CKYC is being done by Kaytes team" (i.e. treat as handled) and "FTD termsheet has a lot of comments — this version cannot be signed," then pushed Neeti "shared with lawyers?" → Neeti: "not engaged with lawyers yet." Separately, the **IDFC WC/OD draft** the routine created was sent by Pratekk and already drew an RM reply (Shikha Pandey) + a bank case number. | No format change. Confirms briefs are used as an action trigger. Keep **FTD term sheet** as a tracked "blocked-on-you" item until counsel is engaged; mark **CKYC closed** (Kaytes owns). System note: draft-to-Outlook + open-loops audit both landed and produced real movement. |
| 2026-09-16 | (discovery, follow-up to the 14 Sep leave question) During the Tue-15 EOD check, found the **individual-leave source**: teammates email a "Leave request - {date}" / "on leave today" note (Neeti → `info@tbrone.in` cc Pratekk). | EOD check is now **leave-aware** — a person who emailed a leave notice for the checked day is reported "on leave," not "missing" (applied same run: Neeti on leave Tue 15, Smridh flagged missing, Shruti in). This closes the open leave-visibility gap for individuals; holidays still pending Pratekk's reporting-day ruling. |
| 2026-09-14 | (in-chat request) "Check the leave calendar and tell me if the team has leaves today?" | No dedicated leave register wired in (checked calendar/SharePoint/mail + no delegate access to team calendars). **Located the office holiday calendar** instead — `office@growthcap.vc` organises all-day "Holiday - X" events + "Working Saturday (WFH)" for the team. Daily brief now carries a light holiday/working-Sat note in the footer; individual team leaves still need a source (shared leave calendar / tracker / email). Open with Pratekk. |
| 2026-09-10 | (behavioural signal, not a reply) Pratekk forwarded the daily brief to the **whole team** (Neeti/Shruti/Smridh); earlier forwarded Tue's to Neeti. | No change needed — briefs are being used as a team action-list, confirming the format lands. Keep delivery/length as-is; keep every item owner-tagged so it forwards cleanly. |
| 2026-09-06 | (EOD tracker reply) "Check for Saturday as well and make the report cut-off by next day 8am." | EOD check retuned: **Saturday now a reporting day**; **08:00-next-day cut-off** enforced; time 08:30→**08:00**; cadence Tue–Sat→**Tue–Sun** (`30 2 * * 0,2-6`). Corrected 1–5 Sep report re-sent. |
| 2026-09-06 | "send me a list at 8:30am of who hasn't sent their EOD report" + "everybody sends from their own email ID." | Added EOD-check routine keyed on each person's own sender address. |
| 2026-09-06 | "set up the routines… just start sending emails to him tomorrow onwards" — kickoff daily brief sent live to his inbox; durable daily + weekly routines enabled. | Draft → **send-to-self**; schedule turned on (first scheduled daily Mon 7 Sep). |
| 2026-09-03 | _(superseded by first live send)_ | — |

## Health metric (tie back to his goal)
Track, monthly, a rough proxy for "**~30% less time on operational noise**":
- # open loops surfaced vs # closed within the week after surfacing.
- # regulatory deadlines caught with >48h to spare.
- His answers trending toward "keep it" / away from "wrong stuff".
Report this in the last Friday brief of each month.
