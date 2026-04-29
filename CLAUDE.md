# AM Command Hub — Claude Instructions

This is Daemon's central AM dashboard. Rules below apply for any work in this folder, including freeform conversations about accounts.

---

## Critical File Rules

**Canonical file:** `hub.html`
**Backup (V4 baseline):** `index-v4-backup.html`
**State file:** `hub-state.json`

- Always make **targeted edits only** — never replace the entire `hub.html`
- If `hub.html` is ever corrupted or accidentally overwritten, restore from `index-v4-backup.html` before editing
- Do NOT update `HUB_ACCOUNTS_DEFAULT` during daily refreshes — it's for notes autocomplete only

## V4 Layout — What's In and What's Out

The V4 template includes: 2-column home grid (upside top-left, onboarding top-right, feedback bottom-left, schedule bottom-right), dark mode toggle, per-account inline notes, onboarding kanban with Closed Won/Lost sections, dual progress bar, file-based state persistence, and archive quarter chips.

**Removed in V4 — do NOT re-add:** IYC card, Key Wins card, All Accounts table.

---

## Data Sources (Priority Order)

1. **Google Sheets** — live revenue, account, and pacing data (source of truth for numbers)
2. **Granola AI (MCP)** — meeting notes, transcripts, action items
3. **hub-state.json** — persisted local state (stages, notes, archive dates)
4. **Gmail / Slack** — async conversation context
5. **User input** — manual notes and context the user provides

---

## Granola Integration

Always pull Granola context when:
- User asks about a specific account or Pro
- Reviewing upside or at-risk accounts
- Running `/prep`, `/score`, or `/ketchup`

### How to pull context

1. **Search by name** — `get_meetings` with Pro name, company, or contact. Try variations if empty.
2. **Summarize history** — `query_granola_meetings`: "What were the key points, action items, and next steps from my meetings with [name]?"
3. **Raw detail** — `get_meeting_transcript` for exact quotes or when notes are thin.
4. **Browse by folder** — `list_meeting_folders` if the account has a dedicated folder.

If Granola returns nothing: say so directly. Do not fabricate meeting context.
