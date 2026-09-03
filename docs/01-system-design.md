# 01 — System design

## The shape of it

A **scheduled Claude session** wakes twice on a cadence, reads Outlook live, and writes
briefs Pratekk can read in under two minutes. Nothing is sent to third parties. The only
outbound email in v1 is the brief itself, to his own inbox, and even that starts as a
draft he approves.

```
                 ┌─────────────────────────────────────────────┐
   Outlook /     │            The routine (Claude)             │
   MS 365   ───▶ │  reads inbox + sent + junk + calendar live  │ ──▶  Brief to
   (live)        │  classifies → open loops, deadlines, funnel │      Pratekk's inbox
                 │  writes outputs/ + updates state            │      (+ feedback ask)
                 └─────────────────────────────────────────────┘
                                   ▲        │
                        tuning     │        │  his 1-tap answers
                                   └────────┘
                              runbook/feedback-log.md
```

## The three systems

### System 1 — Regulatory safety net  *(shippable now, no WhatsApp)*
Highest stakes, most fixable, fully buildable from Outlook alone. Catches hard-deadline
regulatory/compliance mail — in inbox **or** junk — before it is missed.
- Source of truth for counterparties, entities and the live deadline calendar:
  `docs/03-regulatory-map.md`.
- Junk is swept every run (the fear is specifically "it landed in spam and I missed it").
- Output feeds section 3 of the daily brief.

### System 2 — Deal pipeline ledger  *(partial — WhatsApp-blocked)*
A rollup across all three team members (they run the **same** funnel, not territory-split)
of calls done, deal notes sent to Pratekk, and follow-up state.
- **Email only shows the formal residue:** daily EOD reports from Neeti/Shruti/Smridh,
  meeting minutes (MoM) emails, calendar invites, cold-intro emails, decks.
- **The deciding substance — founder conversations, diligence back-and-forth — lives on
  WhatsApp.** Until that export is wired in, this ledger is a count of *observable*
  activity, and every rollup says so. Do **not** present it as the complete funnel.
- Best email-native signal today: the **EOD emails** (structured, daily, per-person) and
  **MoM** emails. These seed the weekly funnel numbers.

### System 3 — Investor update engine  *(template ready)*
Keeps existing LPs and Fund II prospects continuously warm — the cheapest way to stay
top-of-mind without asking for anything. Written in his voice.
- Template reverse-engineered from **"GCV Fund 1_Q1 FY 2027_Quaterly Investor Update"**
  (sent 3 Sep 2026): `templates/investor-update.md`.
- Structure observed: cover note → portfolio highlights → the new investment → sector
  outlook/thesis → GP's desk (Fund I + Fund II) → team additions, brand-building, LP asks.
- QA lesson banked from the real thread: an LP (Venkatesan) caught two portfolio
  companies mis-labelled as the same sector. The engine must **fact-check portfolio
  attributions** before drafting. See the template's checklist.

## The cadence (his final, specific ask)

### Daily — ~7:30am IST, half a page max
1. **Blocked on his sign-off** — what is stalled waiting on *him* (e.g. valuation
   approvals, RSU decisions).
2. **Delegated & gone quiet** — name of the person + days elapsed.
3. **Regulatory deadlines landing this week.**
+ a one-tap **feedback ask**.

### Weekly — Friday
1. **Deal funnel numbers** across all three team members (with the WhatsApp caveat).
2. A **draft investor update**, ready to send or edit.
+ a one-tap **feedback ask**.

## "Delegated & gone quiet" — how detection works (and its v1 limits)

An open loop is: *Pratekk (or the team) owes the next move, and the clock is running.*

**v1 signals (live today):**
- **Outbound delegations** in his Sent Items using his known syntax — `++ @Name`,
  `Looping in <Name>`, `request <Name> to…`, `pls engage/take forward` — with the elapsed
  clock from the send date.
- **Inbound "circling back"** — counterparties writing *"just following up / floating this
  back up / in case it slipped through."* Each is a loop where **his** side went quiet;
  the original date sets the clock. (Vendor spam of this shape is filtered out.)

**What v1 cannot yet see (be honest in every brief):**
- Whether a delegated item was *already handled* off-thread (a reply we didn't parse, or a
  WhatsApp resolution). So v1 can over-report. Each item carries a confidence marker.
- True thread state (did the other side ever respond?) — needs conversation-level tracking,
  next iteration.

**Roadmap to sharpen:** per-thread state (last inbound vs last outbound, per participant)
→ WhatsApp merge → a persistent open-loops ledger the brief reads/writes instead of
re-deriving each morning.

## Guardrails
- **No auto-send to third parties in v1.** Draft only.
- Briefs go to **his own inbox**; start as drafts until he says "just send it."
- **Feedback loop is mandatory.** Every recurring email ends with a lightweight, useful,
  yes/no-ish ask, and answers tune the next run (`runbook/feedback-log.md`).

## Build order (where we are)
1. ✅ Wire Outlook/Graph access — **live** (`get_me` → pratekk@growthcap.vc).
2. ✅ Re-run + deepen the regulatory sweep — done, `docs/03-regulatory-map.md`.
3. ✅ Daily/weekly routine off regulatory data — built; first brief generated.
4. ⏳ WhatsApp export → System 2 + enrich voice doc. **Blocked on upload.**
5. ✅ System 3 template from Q1 FY27 update — done.
6. ✅ Feedback loop baked into the daily brief from day one.
