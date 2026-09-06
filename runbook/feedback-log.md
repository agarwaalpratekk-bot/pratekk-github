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
