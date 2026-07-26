---
name: cost
description: Show what this chat, today, and this month have cost in tokens and dollars (authoritative Bedrock-billed usage from the firm's metering proxy). Use when the user asks "/cost", "what has this chat cost", "how much am I spending", "token usage", or similar.
---

# /cost — usage & spend readout

Report the user's authoritative Bedrock spend from the firm's metering proxy.
All numbers are Bedrock-billed usage recorded by our own in-account proxy —
never estimates.

## Steps

1. **Load config** (per-machine, created during onboarding). Read the three
   `KEY=VALUE` lines (`METERING_URL`, `METERING_READ_TOKEN`, `METERING_USER`) from:
   - macOS/Linux: `~/.config/cowork-metering.env`
   - Windows: `%USERPROFILE%\.cowork-metering.env`
   If the file is missing, stop and tell the user: "Metering isn't configured on
   this machine — ask the pilot admin for your `cowork-metering.env`."
   Never print `METERING_READ_TOKEN`.

2. **This chat**: take the first user message of THIS conversation (you have it
   in context — the earliest human message, not tool output), truncate to the
   first 1000 characters, and POST it as JSON. Use `curl` (preinstalled on
   macOS and Windows 10+; use `curl.exe` in PowerShell). Write the JSON body
   yourself — do not depend on `jq` being installed:
   ```
   curl -s -X POST "$METERING_URL/usage/chat" \
     -H "X-Usage-Token: <token>" -H "Content-Type: application/json" \
     -d '{"user":"<METERING_USER>","firstMessageText":"<first-1000-chars, JSON-escaped>"}'
   ```
   (This text goes only to the firm's own metering endpoint — the same server
   that already relays every prompt to Bedrock; it is hashed in memory and
   discarded, never stored.)

3. **Today + month** (same on every OS; parse the JSON responses yourself —
   no `jq` required):
   ```
   curl -s -H "X-Usage-Token: <token>" "$METERING_URL/usage?scope=today&user=<METERING_USER>"
   curl -s -H "X-Usage-Token: <token>" "$METERING_URL/usage?scope=month&user=<METERING_USER>"
   ```

4. **Render** a compact readout (round to cents; use `totals`, `turns`,
   `lastTurn`, `cacheSavedUsd` from the responses):

   > **This chat:** $X.XX over N turns (M model calls) · last turn $Y.YY
   > **Today:** $A.AA · **This month:** $B.BB
   > **Prompt caching saved you:** $Z.ZZ
   > Top model: <family> · Tokens this chat: <in> in / <out> out / <cacheRead> cached

   Then ONE practical tip chosen from what the data shows:
   - Long chat (>15 turns or chat cost > $1): "Long threads resend the whole
     history every turn — starting a fresh chat for a new topic is the single
     biggest cost saver."
   - High cacheRead ratio: "Caching is doing its job — repeat questions about
     the same documents are cheap. No need to re-attach documents Claude has
     already read in this chat."
   - Otherwise: "Costs here are per-turn: each message resends the conversation
     so far, so shorter, focused chats cost less."

5. **Fallbacks**: if the per-chat lookup returns zero calls (brand-new chat, or
   history was compacted so the fingerprint changed), say per-chat history
   isn't available for this thread and show today/month only. If curl fails,
   say the metering service is unreachable and that chat itself is unaffected.
