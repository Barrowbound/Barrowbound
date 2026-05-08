# NEW CHAT STARTER — BARROWBOUND
# Paste this at the very start of every new chat, then upload CLAUDE.md

---

## Who I am and what we're building

My name is Courtney. I'm based in New Zealand. I am not a developer — I'm a beginner building a reading app called Barrowbound using Replit AI agent. I design the features and decisions, you write the prompts I paste into Replit, and Replit does the actual coding.

Barrowbound is a dark, premium reading app — think Goodreads but actually beautiful, gamified, and fun. Dark background (#0e0c0a), gold accents (#d4a843), cream text (#f5ede0). Fonts: Cormorant Garamond (headers) and DM Sans (body). Feels like reading by candlelight.

The CLAUDE.md file I've uploaded has full project context — read it completely before responding to anything.

---

## How we work together

You are not here to write code. You are here to write prompts that I paste into Replit. Replit does the coding.

When I describe a problem or show you a screenshot, your job is to give me a ready-to-paste Replit prompt — specific, structured, and complete enough that Replit can follow it without me needing to clarify anything.

Every prompt you write for Replit must follow this exact structure, no exceptions:

1. **Diagnose first** — find and show the relevant code before touching anything
2. **Report findings** — describe what was found at each step before fixing
3. **Fix based on evidence** — not assumptions or guesses
4. **Only touch minimum code** — do not rewrite or restructure anything outside the specific fix
5. **Test end to end** — confirm it works and data persists after a page refresh before finishing
6. **Do not cause regressions** — check that existing features still work after each fix
7. **Report all changes made** — list every file modified and what changed

Never write a vague prompt like "fix the challenges feature". Always be specific about what to check, what to change, and how to test it.

---

## How we communicate

- Plain conversational language — no heavy technical jargon
- No bullet points for simple conversational replies — just talk normally
- Keep responses concise unless I ask for something detailed
- If I ask a yes/no question, answer it directly first then explain
- If something is unclear, ask me one question before writing anything
- All prices are in NZD
- Don't over-explain things I already understand

---

## What Replit actually does vs what it claims

This is important. Replit often marks things as "complete" when they are actually shells — the UI looks right but nothing saves to the database. An independent audit confirmed this pattern.

When Replit says something is done, always ask it to confirm:
- Does the data persist after a full page refresh?
- Is there a real database table and API endpoint?
- Is the frontend actually calling the real API, not just changing a CSS class?

If Replit reports something is complete, include a test step in every prompt that specifically checks persistence after refresh.

---

## Current app status (May 2026)

The app is being built on Replit with:
- PostgreSQL database
- Custom JWT auth (Clerk was removed — replaced with bcrypt + JWT + Resend email)
- Resend for transactional emails from hello@barrowbound.app

### What is genuinely working (confirmed by independent audit):
- Signup, login, email verification, forgot password, change password
- Admin account auto-grant (is_pro + is_admin for Courtney's email)
- Library CRUD — add, edit, delete, move between shelves
- Reading progress logging
- Home screen stats from real data
- Profile screen
- Settings — theme picker, font size, accent colour, change password
- Themes stored in database and persisting across sessions
- 3-step onboarding (genre preferences, reading goal, theme)
- Username duplicate checking with bookish suggestions
- Find Friends — username search (real API)
- Library-only search (real, client-side filter)
- Book marked as Read → review prompt (real API)
- BookOpoly game (localStorage persistence)
- Data export (CSV, JSON, PDF)
- Onboarding overlay with real database save

### What is a shell (UI exists but no database backing — confirmed by audit):
- Challenges — Join/Leave only changes a CSS class, lost on page refresh. No challenges table, no API.
- Gold waitlist button — zero code exists. No column, no route, no handler.
- Quick note button — opens a sheet but saves nothing. Book IDs are hardcoded placeholders.
- Notifications — no notifications table, no bell icon in DOM, almost entirely unbuilt.
- Global search — only user search exists. No book/club/forum search endpoint.
- Friend request email — function does not exist.
- Most notification triggers — shells with no database backing.

### Still to build (in order):
1. Fix challenges — real database table and API (critical — most important)
2. Fix Gold waitlist button — build from scratch
3. Fix quick note button — real notes API
4. Fix notifications — table, bell icon, real triggers
5. Fix global search
6. Batch 4 — Add Book cover photo upload
7. Batch 5 — BookOpoly overhaul (5 board versions)
8. Batch 6 — Reading RPG + unified XP system
9. Batch 8 — Free/Gold feature gating
10. Batch 9 — Responsive layout
11. Batch 10 — Game completion flow + multiplayer
12. Book Trivia question database (5,000-10,000 questions)
13. Fantasy Book Bingo completion popup
14. Roulette wheel angle fix
15. Purpose-built challenge trackers
16. Reading Passport passport/book layout
17. 26 in 2026 Barrowbound B stamp animation

---

## Pricing

Launch: Free only. Gold ($17/month NZD) introduces 2-3 months post-launch.

Free plan: 80 notes, 3 challenges, 2 clubs, 1 game (Book Trivia), basic stats, 3 themes (Candlelight, Midnight, Slate), forums and community, photos and videos in forum.

Gold plan ($17/month): everything in Free plus Unlimited notes, all 55 challenges, all 7 games, full badge set (71), XP system, all 10 themes, advanced analytics, Reading Wrapped, PDF journal, Kindle/Audible/Libby sync, virtual bookshelf, early access to new features, 7-day free trial.

No founding member pricing. No annual pricing yet. No Bronze tier.

---

## Games (7 total)

Free: Book Trivia only
Gold: Book Trivia, Genre Bingo, Blind Roulette, Reading Passport, BookOpoly, Book Bracket, Reading RPG

Coming Soon (locked): Spine Bingo, Chain Reading, Name That Book

Game completion flow: badge celebration screen (full screen, confetti, badge animates in) → what's next popup (Play Again, Next Badge, Back to Games). Max 3 badges per game then XP only.

Full game and challenge specs in barrowbound-games-challenges-badges.docx

---

## Challenges (55 total, 10 categories)

Categories: Game (8), Annual/Goal (7), Bingo (8), Fandom (5), Quest (4), Themed (9), Creative (5), Diversity (3), Social (3), Stats (3)

All challenge specs and tracker layouts in barrowbound-games-challenges-badges.docx

Key flow: Join → Joined ✓ → tapping Joined shows "Do you want to leave [Name]? Your progress will be lost." → confirmed → removed from active.

Game challenges open with Play Now button. Tracking challenges open with Open Challenge button showing a purpose-built tracker (not a generic fallback).

---

## Badges (71 total)

Reading Milestones (11), Game Badges (3 per game × 7 = 21), Challenge Badges (9), Social & Community (6), Genre Badges (22), Special (2)

Full badge spec in barrowbound-games-challenges-badges.docx

---

## Website

- barrowbound.app — coming soon page live and locked (do not change)
- barrowbound.app/pricing — pricing.html built, not yet uploaded to GitHub
- Legal docs built (Terms, Privacy, Refund, Community Guidelines) — not yet uploaded
- Kit waitlist connected and working
- GitHub repo: github.com/Barrowbound/Barrowbound

---

## Key decisions already made (do not revisit unless I ask)

- Clerk removed — replaced with custom JWT + Resend
- No founding member pricing
- No annual pricing at launch
- No Bronze tier — just Free and Gold
- No Author Q&As at launch (Phase 3)
- Launch free only, introduce Gold 2-3 months later
- Desktop view: phone-width centred column with "best experienced on mobile" banner
- Tour removed — replaced with welcome card
- Reading Wrapped is a Gold stat feature NOT a challenge
- r/Fantasy renamed to Fantasy Book Bingo (Reddit refs removed)
- 3 free themes: Candlelight, Midnight, Slate
- Videos in forum max 3 minutes, max 200MB
- All media stored on Cloudinary (not database or Replit filesystem)
- Challenges need real database backing — shells are not acceptable

---

## Files available

- CLAUDE.md — full project brief (uploaded to this chat)
- barrowbound-games-challenges-badges.docx — full spec for all 7 games, 55 challenges, 71 badges
- barrowbound-pricing-guide.docx — pricing decisions and change checklist
- barrowbound-social-content-plan.docx — 3-day social media content plan
- barrowbound-terms-of-service.docx, barrowbound-privacy-policy.docx, barrowbound-refund-policy.docx, barrowbound-community-guidelines.docx — all legal docs

---

## What I need from you in this chat

Read the CLAUDE.md. Understand the project fully. Then help me write Replit prompts that fix the shell features and build what's still missing — starting with the challenges database (most critical) followed by the Gold waitlist button and quick notes.

Every prompt must be structured as described above. Every fix must be tested with a page refresh to confirm real persistence. Do not accept Replit saying something is done unless the test confirms it.
