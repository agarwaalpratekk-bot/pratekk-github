# 03 — Regulatory map (System 1)

The reference the regulatory safety net matches against. Compiled from the sent-items read
plus two live sweeps (the original handoff sweep + a re-run on 2026-09-03).

> **Status of the spam-loss fear: still UNCONFIRMED = good news.** Junk (414 items) was
> re-scanned on 2026-09-03. Contents: cold outreach, event invites, newsletters, vendor
> pitches. **Nothing** from any regulatory counterparty below was found in spam. Keep
> sweeping Junk every run anyway — that is the whole point of System 1.

## GCV entities (for correct matching/filtering)
- GROWTHCAP FOUNDATION
- GROWTHCAP VENTURES PVT LTD
- GCV Fund 1 / GVFIF (GrowthCap Ventures Fund I)
- GrowthCap Ventures AIF Trust — Scheme II
- AIF ISIN-style codes seen: **INF0U6B22012 / INF0U6B22046**

## Known regulatory / compliance counterparties

| Counterparty | Addresses | Domain |
|---|---|---|
| Stockholding (custodian/RTA ops) | cit@, shilpa.tayade@, hemangi@, instreports@ **stockholding.com** | Fund transfers, client reports, custody |
| Orbis Trusteeship | via investor@growthcap.vc chains; prateek.patel@orbisfinancial.in | AIF Trustee |
| Kaytes Consulting | bk@, dr@, dk@, gc@, growthcap@ **kaytesconsulting.com** | Audit, valuation, scheme docs |
| Kaytestech | gdeshamane@, bkotak@, directors@ **kaytestech.com** | TDS, tax working, Fund II setup |
| Nangia Global / Nangia & Co | mayank.garg@nangiaglobal.com, apoorva.choudhary@nangia.com | Statutory audit, DD/forensics |
| Purva Share Registry | corporateaction@purvashare.com | RTA — AIF unit allotment notices |
| Crisil | aif.benchmarking@crisil.com | **SEBI-mandated AIF performance benchmarking** |
| Anuj Desai & Associates | compliance@anujdesaiassociates.com | AIF Trust monthly compliance calendar |
| IDFC First Bank | corporateservices@, ishan.pandita1@, mugdha.supal@ | Banking / balance sheets |
| Kotak, Yes Bank | (various) | Banking, liquid-fund parking |
| ANP Partners | asingh@, zmody@, ssingh@ anppartners.in | RSU / stamp duty |
| CA Pratik Shah | shahpratikpca@gmail.com | Chartered accountant |
| TBR One | info@tbrone.in | Payroll, financials signing |
| GCV internal | compliance@, investor@, office@ growthcap.vc | Internal compliance/IR |

**Not yet confirmed with Pratekk (open questions):**
- Does **SEBI** correspond with him directly, or only via Stockholding / Trustee / Kaytes?
- Is the counterparty list above complete?
- Lookback window for the sweep (default used: **6 months**, unconfirmed).
- Sweep depth per run (default: **flag-only, no auto-drafted replies** — confirmed intent).

## Live deadline calendar (as of 2026-09-03)

| Due | Item | Source | Owner / state |
|---|---|---|---|
| **Mon 7 Sep 2026** | **TDS payment, Aug 2026** for GCV Fund I | gdeshamane@kaytestech.com (3 Sep) | Neeti: "will process tomorrow" (4 Sep). Watch it clears before 7th. |
| This week | **Crisil AIF benchmarking — data collection** (SEBI circular-mandated) | aif.benchmarking@crisil.com (3 Sep, unread, has attachment) | Needs GCV data submission. **Unread — surface.** |
| September (month) | **AIF Trust monthly compliance items** — "the one email to act on before September" | compliance@anujdesaiassociates.com (4 Aug) | Confirm September filings are scheduled. |
| Open | **AIF unit allotment** — CA files INF0U6B22012 / INF0U6B22046 | corporateaction@purvashare.com (17 Aug, one copy still **unread**, "Kind Attn: Mr. Karan D.") | Confirm processed by RTA/custodian. |
| Open (legal) | **Defaulting Investor** — designation & invocation of remedies, Fund I | investor@growthcap.vc (6 Aug) | Legal/regulatory; confirm counsel path. |
| In-flight | **FY26 statutory audit / signed financials** (GCV Fund I) | Kaytes/Orbis/TBR/Nangia (1–2 Sep) | Signing chain active; near-complete. |
| In-flight | **RSU agreement / stamp duty** | ANP Partners (2 Sep) | **Blocked on Pratekk** — he asked for the details list to organise receipts. |

## Recurring regulatory rhythms to encode (so the routine anticipates, not just reacts)
- **Monthly TDS** payment (Kaytestech sends working ~3rd, due ~7th).
- **Monthly AIF Trust compliance** calendar (Anuj Desai & Associates).
- **Periodic AIF benchmarking** (Crisil, per SEBI circulars).
- **AIF unit allotment** cycles (Purva, tied to drawdowns/transfers).
- **Annual statutory audit** (Kaytes + Nangia), FY close 31 March.
- **Quarterly investor update** (feeds System 3).
