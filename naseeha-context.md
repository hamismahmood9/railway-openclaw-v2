# Naseeha Foundation — Session Summary
> Date: 2026-04-06
> Last updated: 2026-04-06 19:30 PKT
> Session with: Hamis Mahmood + Mings ⚡

---

## What We Did Today

### 1. Mings Setup
- Named the assistant: **Mings ⚡** — sharp, efficient, professional, intellectual, honest
- Set up `IDENTITY.md`, `USER.md`, deleted `BOOTSTRAP.md`
- Confirmed WhatsApp self-chat mode on +923224750007

### 2. GitHub Access
- Confirmed `gh` CLI authenticated with two accounts:
  - `hamismahmood9` (active, full scopes) — primary dev account
  - `hamismahmood` (secondary)
- Listed repos under hamismahmood9:
  - `naseeha-donations-v1` (private, updated today)
  - `v0-ittekaf-review-portal` (private)
  - `naseeha-ittekaf` (private)
  - `naseeha` (public)
  - `naseehaa` (private)

### 3. Read the Roadmap
- Cloned `naseeha-donations-v1` to `/tmp/naseeha-donations-v1`
- Read `ROADMAP.md` — comprehensive platform PRD covering donations, academics, events, procurement
- Key finding: ROADMAP is a vision doc, not a build plan. Missing acceptance criteria, user stories, edge cases.

### 4. Read the PRD
- Read `Naseeha_Donation_System_PRD_v2.docx` from `/Users/hamismahmood/Downloads/`
- This is the real spec for the live system — WhatsApp → AI → Google Sheets pipeline
- Key tension identified: ROADMAP talks Supabase+Next.js but live system is Node.js+Sheets

### 5. Understood Current Live System
- Read full `CLAUDE_CONTEXT.md` from the repo
- **Phase 1.5 is live on Railway** — processing real donations
- Stack: Node.js + Whapi.Cloud + Anthropic AI + Google Sheets
- 215 donors in registry, 17 payments processed in April so far
- Connected to live Google Sheet (`1OhNt1WVnZqhAxgWPIez8SoofE48Ol7OSaWi5gKVkAew`)
- Verified system is healthy — all tabs writing correctly

### 6. Key Decisions Made

**Decision 1: Keep current stack for now**
- Whapi stays (~$30-40/month) — right tool, already working
- ChatMaxima stays ($19/month) — needed for Meta-compliant outbound templates
- Railway stays — lean, working, ~$5-10/month

**Decision 2: Historical backfill needed**
- Some donors sent payments before system went live → showing as Unpaid
- Written backfill script: `src/setup/backfillHistorical.js`
- Fetches April 1+ messages from all 203 known donor numbers via Whapi
- Deduplicates against existing Donations Log before processing
- **Not yet run** — pending

**Decision 3: Move to Supabase + Next.js (the big one)**
- Google Sheets is wrong tool for exception handling, purpose review, donor management
- Hassaan needs a real UI — not a spreadsheet
- Decision: skip "Next.js on Sheets" bridge, go straight to Supabase
- Do it once, do it right

**Decision 4: Purpose detection needs improvement**
- Current system logs "Others" for unrecognised purposes — not good enough
- Unknown purposes should be extracted, clustered by similarity, surfaced in frontend UI
- New `unknown_purposes` table added to schema for this

### 7. Supabase Setup
- Project: `naseeha-donations-v1`
- Ref: `irxmkwbwiwvsujkberum`
- Region: South Asia (Mumbai)
- Linked via CLI ✅
- **Full schema deployed** ✅ — migration `20260406000001_initial_schema.sql`

**Tables created:**
- `branches` — future multi-branch support
- `households` — family grouping
- `people` — universal person record (central entity)
- `donor_profiles` — donation-specific data, extends people
- `purposes` — GL ledger entities with keyword mapping
- `donations` — append-only payment log (immutable)
- `monthly_recon` — per-donor per-month reconciliation
- `unknown_purposes` — surfaces unrecognised purposes to frontend
- `meta_log` — pipeline execution audit trail
- `audit_log` — data change history
- `staff` — RBAC with @naseeha.live Google OAuth

**Supabase keys saved in `~/.openclaw/boot.md`**

### 8. Railway Auth — UNRESOLVED
- Railway CLI installed (v4.30.4) but auth token expired
- Need fresh `railway login --browserless` → visit URL → enter pairing code
- Projects on Railway:
  - `spirited-motivation` — existing Node.js backend
  - `keen-heart` — naseeha-finance-app (previous attempt)
  - `grand-contentment` — previous frontend attempt

---

## Current State

| Item | Status |
|------|--------|
| Live donation pipeline (Phase 1.5) | ✅ Working |
| Google Sheets | ✅ Live, writing correctly |
| Supabase schema | ✅ Deployed |
| Railway CLI auth | ❌ Token expired — fix first |
| Historical backfill script | ✅ Written, not run |
| Sheets → Supabase data migration | ⏳ Not started |
| Node.js pipeline rewire to Supabase | ⏳ Not started |
| Next.js frontend | ⏳ Not started |
| Purpose detection improvement | ⏳ Schema ready, logic not built |

---

## Immediate Next Steps (in order)

1. **Fix Railway auth** — `railway login --browserless` → visit https://railway.app/cli-login → enter pairing code
2. **Run historical backfill** — `node src/setup/backfillHistorical.js` from `/Users/hamismahmood/claude_code/naseeha-donation-automation`
3. **Run Daily Audit** after backfill to update Monthly Recon totals
4. **Build Sheets → Supabase migration script** — move 215 donors + 17 donations to Supabase
5. **Rewire Node.js pipeline** — dual-write Sheets + Supabase, validate 2 weeks, then cut over
6. **Build Next.js frontend** (via Claude Code) — flag queue, purpose management, donor profiles, monthly recon
7. **Deploy frontend to Railway**

## First Thing Next Session
> Fix Railway auth, then run historical backfill.

---

## Key Credentials & Paths

| Item | Value |
|------|-------|
| Backend repo | `/Users/hamismahmood/claude_code/naseeha-donation-automation` |
| GitHub | `hamismahmood9/naseeha-donations-v1` |
| Google Sheet ID | `1OhNt1WVnZqhAxgWPIez8SoofE48Ol7OSaWi5gKVkAew` |
| Service account JSON | `/Users/hamismahmood/.openclaw/workspace/naseeha-service-account.json` |
| Supabase ref | `irxmkwbwiwvsujkberum` |
| Railway project | `spirited-motivation` (d195a6e2-18ec-44c2-b62b-f1235e421ae4) |
| WhatsApp Business | +92 321 1115881 (Whapi) |
| Donation system Anthropic key | sk-ant-api03-vXn...SQAA (confirmed active) |

---

## Architecture Decision Log

| Decision | Rationale |
|----------|-----------|
| Anthropic models only | Ethical + operational — no OpenAI/Google/xAI |
| Whapi over Meta API | Meta API blocked by Pakistan phone verification bug |
| ChatMaxima for outbound | Only Meta-approved BSP for templates — $19/month |
| Supabase over plain Postgres | Auth, RLS, Realtime, Storage all built in |
| Railway over Vercel | Hamis has Railway already, prefers it over Vercel |
| Google OAuth (@naseeha.live) | Org-restricted, no password management overhead |
| Person-centric data model | Donor is also parent, student, volunteer — one record |
| Sadaqah only, no Zakat | Naseeha policy — important for GL separation |
