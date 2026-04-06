# MEMORY.md — Mings Long-Term Memory
> Last updated: 2026-04-06

---

## Who I Am
- **Name:** Mings ⚡
- **Vibe:** Sharp, efficient, problem-solver, professional, intellectual, honest

---

## My Human
- **Name:** Hamis Mahmood
- **WhatsApp:** +923224750007
- **Timezone:** Asia/Karachi (GMT+5)
- **Style:** Direct, no fluff. Strong PM instincts. Hates manual config. Prefers CLI/automation.
- **GitHub:** hamismahmood9 (primary)

---

## Key Project: Naseeha Foundation Donation System

Full context in `~/.openclaw/boot.md` — read that for deep detail.

**Summary:**
- Islamic nonprofit in Lahore. ~215 donors. Hamis is tech lead.
- Live system: Node.js + Whapi + Google Sheets on Railway (`spirited-motivation`)
- Repo: `/Users/hamismahmood/claude_code/naseeha-donation-automation` (GitHub: hamismahmood9/naseeha-donations-v1)
- Google Sheet ID: `1OhNt1WVnZqhAxgWPIez8SoofE48Ol7OSaWi5gKVkAew`
- Service account JSON: `/Users/hamismahmood/.openclaw/workspace/naseeha-service-account.json`

**Migration decided 2026-04-06:**
- Moving to Supabase + Next.js frontend
- Supabase project: `naseeha-donations-v1` (ref: `irxmkwbwiwvsujkberum`, Mumbai)
- Schema deployed ✅
- Railway CLI auth needs fixing before next session
- Use Claude Code for heavy coding

**Pending:**
- Railway login (token expired)
- Historical backfill (script written at `src/setup/backfillHistorical.js`)
- Sheets → Supabase data migration
- Next.js frontend build

---

## Session Notes — 2026-04-06
- First session ever. Set up identity (Mings ⚡), USER.md, deleted BOOTSTRAP.md
- Spent most of session on Naseeha architecture decisions
- Key decision: skip Sheets→Next.js bridge, go straight to Supabase
- Hamis frustrated with Google Sheets as UI — wants real frontend
- Purpose detection needs improvement — unknown purposes should surface in UI

## Working Style — 2026-04-06
- **DO NOT automatically jump into recent context**
- Wait for explicit instruction to pull up or work on something
- Stay calm until told to act
- This applies across all projects and tasks

## Communication Preferences — 2026-04-07
- **Always lead with shortcuts/fastest methods first**
- Manifest/copy-paste methods BEFORE step-by-step
- No fluff, straight to the point
- See `HAMIS_PREFERENCES.md` for complete list
