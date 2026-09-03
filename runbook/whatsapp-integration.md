# WhatsApp integration — the named gap

Most of Pratekk's real deal work happens on **WhatsApp**. Until it's wired in, System 2
(deal pipeline) and part of the voice document are structurally incomplete. This is a known,
named gap — not forgotten, not yet solved.

## Status
- A WhatsApp chat export (`.zip`) was uploaded in the earlier **Claude chat** session but
  couldn't be read there (that environment had no file access). **That constraint was
  specific to the chat sandbox — it does not apply here.** Claude Code in this environment
  can read local files directly.
- Pratekk said he'd re-upload the export for Claude Code to use.

## What to do when the export arrives
1. **Locate it.** Check the repo root, `inbox/`, and the session scratchpad. If it's not
   obvious, **ask Pratekk where he placed the file** rather than assuming it's missing.
2. **Unzip & read.** WhatsApp exports are `_chat.txt` per conversation (+ media). Parse:
   `DD/MM/YY, HH:MM - Sender: message`.
3. **Feed System 2:** per-deal threads → real funnel state (calls, stage, last contact,
   who owes the next move). Merge with the email residue so the weekly funnel stops being a
   floor.
4. **Enrich the voice doc** (`docs/02-voice-profile.md`) → v1.0 with his most natural register.
5. **Extend open-loops detection** to WhatsApp delegations, so "gone quiet" covers where the
   work actually happens.

## Guardrails
- WhatsApp content is personal — keep parsed data inside this repo/session; don't send it
  anywhere external.
- Still **flag-only**: surface loops, don't auto-reply on WhatsApp.

## Until then
Every System-2 output must carry the caveat that it reflects **email-observable activity
only** and is a floor, not the full pipeline.
