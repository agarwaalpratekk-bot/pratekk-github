# GrowthCap Ventures — AI Ops Layer

An operating system for **Pratekk Agarwaal** (Founder & GP, GrowthCap Ventures) that
closes open loops, protects his time, and keeps the Fund II raise warm — delivered as a
short email he can *just read*, on a running cadence, with a feedback loop baked in.

> **The problem, in his words (locked — do not re-litigate):** he cannot track what he
> has delegated. Things handed to the team / founder's office fall into a black hole
> until his memory randomly surfaces them. This is an **open-loops problem, not an inbox
> problem.** He wants everything tech-driven and tracked, and wants ~30% of his time back
> from operational noise so he can focus on closing the ₹1,000 Cr Fund II. The system's
> job is to be a **shield**, not just a report. (Full statement: `docs/00-diagnosis.md`.)

---

## What this repo is

This is the design, the running artifacts, and the runbook for a recurring assistant. It
is **not** a codebase that calls APIs on a server — the "engine" is a scheduled Claude
session that, each morning and each Friday, reads Pratekk's Outlook (Microsoft 365),
regenerates the briefs in `outputs/`, and (once approved) delivers them to his inbox.

```
docs/         The thinking: diagnosis, system design, regulatory map, voice document
templates/    Reusable prompts/skeletons the routine fills each run
outputs/      The actual generated briefs (real data), dated
runbook/      How the recurring routine runs, and how feedback tunes it
```

## Status — verified live on 2026-09-03

The mailbox is **connected live** to `pratekk@growthcap.vc` via Microsoft 365. Everything
below was checked against the real inbox today, not assumed from the handoff doc.

| System | What it does | Status | WhatsApp-blocked? |
|---|---|---|---|
| **1 — Regulatory safety net** | Catches hard-deadline regulatory/compliance mail before it's missed | **Shippable now.** First sweep re-run & extended live. | No |
| **Daily + weekly routine** | 7:30am daily brief + Friday weekly, each ending in a feedback ask | **Built.** First daily brief generated from live data → `outputs/daily/2026-09-03-daily-brief.md` | No (daily); partial (weekly funnel) |
| **2 — Deal pipeline ledger** | Rollup of calls / deal notes / follow-up state across Neeti, Shruti, Smridh | **Partial.** Email shows the formal residue (EOD reports, MoMs, intros). Substance lives on WhatsApp. | **Yes — structurally incomplete until WhatsApp lands** |
| **3 — Investor update engine** | LP/prospect updates in his voice for the Fund II raise | **Template reverse-engineered** from the Q1 FY27 quarterly update. Draft engine in `templates/investor-update.md`. | Partly (portfolio substance) |

### Two verified facts worth telling Pratekk directly
1. **Spam is still clean of regulatory risk.** Re-scanned Junk (414 items) today — cold
   outreach, event invites, newsletters, vendor pitches. Nothing from Stockholding,
   Kaytes, Orbis, Purva, SEBI, or the auditors was sitting in spam. The spam-loss fear
   remains **unconfirmed = good news.**
2. **The valuation/audit chain is his recurring bottleneck, live right now.** The FY26
   audited-financials signing loop (Kaytes → Orbis/TBR/Nangia → sign-offs) ran Sep 1–2,
   and a hard **TDS deadline lands Mon 7 Sep**. This is the open-loops problem showing up
   in the highest-stakes place — surfaced in today's brief, not buried in a list.

## Known gaps (named, not hidden)
- **WhatsApp is not wired in yet.** System 2 and part of the voice document depend on it.
  Every artifact that would be incomplete without it says so, inline, rather than
  presenting partial data as complete. See `runbook/whatsapp-integration.md`.
- **"Gone quiet" detection is v1.** It currently reads a recent sent-items window plus
  inbound "just circling back" signals. Full thread-state tracking (did the other side
  ever reply?) sharpens once wired — see `docs/01-system-design.md`.

## Guardrails (v1)
- **Flag only. No auto-send to third parties.** The routine drafts; Pratekk sends.
- Briefs are delivered to **his own inbox** for him to read — the only "send" in v1.
- Every recurring email ends with a **one-tap feedback ask**, and the routine is tuned
  from the answers (`runbook/feedback-log.md`). This is a hard requirement, not optional.

## Start here
1. `docs/00-diagnosis.md` — the locked problem statement
2. `docs/01-system-design.md` — how the whole thing works
3. `outputs/daily/2026-09-03-daily-brief.md` — the first real brief
4. `runbook/agent-instructions.md` — how the routine runs each day
