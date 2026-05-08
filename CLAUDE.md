# CLAUDE.md — Barrowbound Project Brief

This file gives Claude full context on the Barrowbound project so any new conversation picks up exactly where the last one left off. Read this entire file before responding.

---

## Project Overview

Barrowbound is a reading app combining beautiful book tracking, gamified reading challenges, interactive reading games, social community features, and AI-powered book discovery — all in one dark, premium-feeling web app (native app later). The closest comparison is: Goodreads (community) + Bookmory (beautiful tracking) + TikTok (discovery energy) + Facebook Groups (book clubs) — but better than all of them combined.

Owner is Courtney, based in New Zealand, building this using Replit AI agent.

---

## Brand Identity

| Detail | Value |
|---|---|
| App name | Barrowbound |
| Primary domain | barrowbound.app |
| Secondary domain | barrowbound.co |
| Tagline | Your entire reading life, in one place |
| Gold (primary) | #d4a843 |
| Gold light | #e8c070 |
| Gold dim | #8a6e2a |
| Background | #0e0c0a (near black) |
| Surface | #1a1612 |
| Surface 2 | #221e19 |
| Border | #38302a |
| Cream (text) | #f5ede0 |
| Cream dim | #b8a898 |
| Text | #c8bfb0 |
| Text dim | #7a6e62 |
| Display font | Cormorant Garamond (serif, headers) |
| Body font | DM Sans (clean, modern) |
| Visual identity | Dark backgrounds, warm amber/gold accents, cream text. Feels like reading by candlelight. |

---

## Domains and Email

- barrowbound.app — primary domain, registered at Porkbun, live on GitHub Pages
- barrowbound.co — secondary, redirects to barrowbound.app
- Email forwarding: hello@barrowbound.app and hello@barrowbound.co both forward to owner personal email
- SSL certificate active on barrowbound.app
- GitHub repo: github.com/Barrowbound/Barrowbound

---

## Email / Kit Setup

- Kit account: hello@barrowbound.app
- Barrowbound Waitlist form connected and working
- Kit custom domain: barrowbound.kit.com
- DNS records for verified sending domain added to Porkbun
- Branded confirmation email set up with dark button and gold text
- Double opt-in ON
- Launch broadcast will be sent manually via Kit Broadcasts

---

## Social Media — All Done

| Platform | Handle |
|---|---|
| TikTok | @barrowbound |
| Instagram | @barrowboundapp |
| Threads | @barrowboundapp |
| YouTube | @barrowboundapp |
| Reddit | Barrowboundapp |
| Facebook | Barrowbound Page |

---

## Logo and Images

- coming_soon_logo.png — bookshelf arch image, transparent background, baked as base64 into prototype and pricing page
- Profile_Image.png — circular logo used across all social platforms
- barrowbound_bookshelf_logo.svg — SVG organised chaos bookshelf logo
- barrowbound_cover_clean.png — Facebook cover photo 820x312px

---

## Files

| File | Description |
|---|---|
| barrowbound-index.html | MAIN PROTOTYPE — all screens, games, modals. Latest version from Replit. |
| coming-soon.html | Coming soon page — LOCKED, live at barrowbound.app |
| pricing.html | Standalone pricing page — deploy to barrowbound.app/pricing |
| coming_soon_logo.png | Transparent arch bookshelf logo |
| CLAUDE.md | This file |
| barrowbound-terms-of-service.docx | Terms of Service |
| barrowbound-privacy-policy.docx | Privacy Policy — NZ, GDPR, CCPA, AU compliant |
| barrowbound-refund-policy.docx | Refund Policy |
| barrowbound-community-guidelines.docx | Community Guidelines |
| barrowbound-games-challenges-badges.docx | Full spec for all 7 games, 55 challenges, 71 badges |
| barrowbound-pricing-guide.docx | Pricing decisions, competitor comparison, change checklist (updated to USD May 2026) |
| barrowbound-social-content-plan.docx | 3-day social media content plan |

---

## Coming Soon Page — LOCKED

Live at barrowbound.app. Do not change without uploading a new file to GitHub. Kit form connected, SSL active, GitHub Pages deployed. Body text and title fixed May 2026. Logo baked in as base64.

---

## Auth System — Custom JWT (Clerk removed)

Clerk was removed entirely in May 2026. Replaced with custom JWT auth + Resend email.

- Signup: bcrypt (12 rounds) password hash, verification email via Resend from hello@barrowbound.app
- Email verification: link-based for better deliverability to Hotmail
- JWT stored as bb_jwt in localStorage, 30-day expiry, signed with JWT_SECRET
- Forgot password: POST /api/auth/forgot-password → reset token in DB → branded email via Resend → /reset-password?token=TOKEN
- Change password: POST /api/auth/change-password — available in Settings
- Login returns inline errors (no toasts)
- Admin account: Courtney's personal email auto-grants is_pro=true + is_admin=true on first sign-in

**Bootstrap security note:** All per-user state is keyed to the actual JWT value via a single bootstrap IIFE. Clears on logout, re-bootstraps on account switch, discards stale in-flight responses, listens to cross-tab storage events. Prevents cross-account data leaks — HIGH security issue caught and fixed May 2026.

Replit Secrets required: JWT_SECRET, RESEND_API_KEY, DATABASE_URL

---

## Monetisation — Current Plan

### Launch: Free only
No paid plans at launch. Gold introduced 2-3 months post-launch. No pressure, no countdown timers, no founding member offers.

### Free Plan (at launch)
- Book library across 6 shelves
- Reading progress logging
- Barcode and ISBN scanner
- Reading calendar
- 80 notes
- 10 reading challenges (user picks any 10 from all 55)
- 3 games: Book Trivia, Blind Roulette, Genre Bingo
- Forums, group chats and friend chats
- Photos and videos in forum posts (up to 4 photos or 1 video per post, max 3 minutes)
- Reels tab (vertical video feed)
- Friend system and activity feed
- 2 book clubs
- Basic reading stats
- Badges for free features
- 3 themes (Candlelight, Midnight, Slate)

### Gold Plan — $9.99 USD/month (launching 2-3 months post-launch)
- Everything in Free, plus:
- Unlimited notes
- All 55 reading challenges (44 more than Free)
- All 7 games (4 more than Free)
- Full badge set (71 badges)
- XP levels and cosmetic unlocks
- All book clubs
- Friend XP leaderboards
- Advanced analytics
- Reading Wrapped
- PDF reading journal
- Kindle, Audible and Libby sync
- All 10 premium themes
- Full appearance customisation
- Virtual interactive bookshelf
- Early access to new features
- 7-day free trial
- Cancel anytime

No Bronze tier. No founding member pricing. No annual pricing yet (likely $79–89 USD/year when added). No Author Q&As (Phase 3). Pricing is in USD globally — Stripe handles currency conversion for non-USD payment methods. See barrowbound-pricing-guide.docx for full pricing decisions and change checklist.

---

## Themes

Free (3): Candlelight (default), Midnight, Slate
Gold (7): Forest, Ocean, Ember, Dusk, Parchment, Rose, Noir

Each theme updates ALL CSS variables throughout the app. Selected theme stored in database and persists across sessions.

---

## Games (7 total)

Full spec in barrowbound-games-challenges-badges.docx

### Free (3 games)
- Book Trivia
- Blind Roulette
- Genre Bingo

### Gold (all 7)
- Book Trivia
- Blind Roulette
- Genre Bingo
- Reading Passport (passport/book layout with page flipping, 50 countries)
- BookOpoly (5 themed boards: Fantasy, Romance, Thriller and Crime, Classic Literature, BookTok)
- Book Bracket (pulls from user's actual Read shelf — all logged finished books)
- Reading RPG (feeds into unified XP system)

### Coming Soon (greyed out, not clickable)
Spine Bingo, Chain Reading, Name That Book

### Game completion flow
1. Badge celebration screen — full screen, gold confetti, badge animates in, XP shown, tap to continue
2. What's next popup — Play Again, Next Badge info, Back to Games
After 3 badges earned: XP reward shown instead with "keep playing for XP" message

### BookOpoly
- 30 spaces, 5 themed board versions selectable before starting
- Token moves space-by-space with animation
- Library square: pick from 3 TBR suggestions
- Bookstore square: spend coins on power-ups (double roll, skip 3, re-roll)
- Jail/DNF Pile: skip one turn
- Free Parking/Reading Nook: collect accumulated coin pot
- Completing a lap = badge awarded
- Solo only for now

---

## Challenges (55 total, 10 categories)

Full spec with all descriptions and layouts in barrowbound-games-challenges-badges.docx

Categories: Game (8), Annual/Goal (7), Bingo (8), Fandom (5), Quest (4), Themed (9), Creative (5), Diversity (3), Social (3), Stats (3)

Free users: any 10 challenges from all 55
Gold users: all 55 challenges

### Challenge flow
- Join/Joined buttons call real API (POST /api/challenges/join, DELETE /api/challenges/leave/:challengeId)
- Cards carry data-challenge-id; join/leave awaits the API before mutating UI
- Page load fetches GET /api/challenges/active and restores joined state from database
- Tapping Joined shows leave confirmation: "Do you want to leave [Name]? Your progress will be lost."
- Game challenges: Play Now button opens linked game
- Tracking challenges: Open Challenge button opens purpose-built tracker
- Manage button on Your Active Challenges: opens modal showing all joined challenges with red Leave buttons

### Fandom challenges (updated May 2026)
- The Series Completionist (Ongoing, Moderate)
- The Award Hunter (Year-Long, Moderate)
- The Adaptation Chase (Year-Long, Casual)

### Diversity challenges (updated May 2026)
- The Marginalised Voices Challenge
- Own Voices Challenge
- The First Voices Challenge — Indigenous/First Nations authors

### Social challenges (updated May 2026)
- Buddy Read Challenge
- Book Club Pick
- Read and Recommend

### Parked future challenges
- The Midnight Stack, The One-Sitting Club, The First Chapter Test, The Borrowed Worlds Challenge

---

## Badge System (71 total)

Full spec in barrowbound-games-challenges-badges.docx

| Category | Count |
|---|---|
| Reading Milestones | 11 |
| Game Badges (7 games x 3) | 21 |
| Challenge Badges | 9 |
| Social and Community | 6 |
| Genre Badges | 22 |
| Special | 2 |
| Total | 71 |

Max 3 badges per game then XP only. Genre badges at 3 books, double XP at 6 books. Special: Beta Tester (comped accounts), Early Adopter (first month after launch).

**Badge name corrections (reconciled with spec doc May 2026 — need DB update):**
- "First Book" in DB → correct name is **First Chapter**
- "On A Roll" in DB → correct name is **Devoted Reader** (finish 10 books)
- "First Post" in DB → correct name is **Forum Voice**

---

## XP System (Gold)

- Single unified XP pool per user
- XP sources: finish book (+50), log pages (+1/10pp), complete challenge (+100), win game (+25), streak milestones (+50/200/500)
- Level curve: L1=0, L2=100, L3=250, L4=500, L5=1000, then +500/level
- Level up triggers cosmetic unlock modal
- XP leaderboard among friends (weekly + all-time)
- Reading RPG feeds into main pool — not separate economy

---

## Notifications System

**Infrastructure (real):** notifications table exists. Bell icon with unread badge in top bar. lib/notifications.ts helper callable from any route.

**Live triggers:** friend request received, friend request accepted

**Pending triggers (build after underlying features confirmed real):**
- Forum post liked, forum post replied to (forum now real — wire next)
- Book club discussion post added (club discussions now real — wire next)
- Book club meeting reminder (meetings not built)
- Reading streak reminder — partial, not streak-aware
- Challenge milestone hit (challenges real, milestone tracking not wired)
- Buddy read partner logs progress (buddy reads not built)
- Weekly reading summary (no weekly job)

---

## Notes System

Real database table. POST /api/notes, GET /api/notes/:bookId. Book ownership enforced. Quick note on Currently Reading uses real book_id. Persists in book detail Notes tab.

---

## Gold Waitlist

gold_waitlist boolean on user_profiles. POST /api/waitlist/gold. Shows "✓ You're on the list" persistently after tap.

---

## Search

Home screen global search: tabs All, Books, People, Clubs, Forum. Only user search (People tab) is a real endpoint. Others are shells still to build.

Library search: real — client-side filter over loaded data.

---

## Find Friends

- Username search — real API
- QR code — shell
- Suggested friends — shell
- No contacts sync

---

## Onboarding (first login only)

3-step flow: genre preferences → reading goal → theme. Tracked with has_completed_onboarding boolean. All real and verified.

---

## Email Notifications (via Resend)

Active: email verification, password reset. Friend request email not yet built. Weekly digest job not built.

---

## Forum

**Text posting, likes, replies:** all real. forum_posts (with title, category, spoiler, rating columns), forum_post_likes (derived counts), forum_post_replies tables. Pagination, cascade deletes, XSS protection all verified.

**Media:** photos (up to 4, max 1MB each) and videos (1 per post, max 3 min, max 200MB) wired via Replit App Storage presigned URLs. Auth gate on upload endpoint. HEAD check enforces size limits server-side.

**Share to Forum from Reviews:** real — calls POST /api/forum/posts with category=review and star rating stored in rating column.

**Reels tab:** not yet built.

---

## Chats

**Friend DMs:** real, verified, unique-index constraint on direct_conversations table.
**Group chats:** real, verified, creator-only member management.
**Club discussions:** real, verified, 32/32 e2e tests. clubs.conversation_id FK, atomic creation.

All chats: polling every 3s, chronological, auto-scroll, timestamps. Unread badges deferred.

---

## Activity Feed

Real. activity_events table with index on (user_id, created_at DESC). GET /api/activity/feed returns friends' events plus caller's own. 5 trigger points wired: finished_book, started_book, progress_update, joined_challenge, earned_badge. Paginated, relative timestamps.

---

## Review Flow

Book marked as Read → bottom sheet with star rating and review → Save (real API) or Maybe Later → optional Share to Forum (real API). Real end to end.

---

## Quick Note on Currently Reading

Real. Uses real book_id from /api/books. Saves to notes table. Updates book detail Notes tab.

---

## Reading Calendar

Real. GET /api/sessions?year=&month= wired to calendar frontend. Month navigation refetches. tapDay shows real book titles and pages logged. IDOR fix and stale-response guard in place.

---

## Performance and Stability

Database indexes, pagination (limit 20), 60s caching, image compression, error boundaries — all real and verified.

---

## PWA / SEO

PWA manifest real. Open Graph meta tags real.

---

## Data Export

CSV, JSON, PDF — all real and verified.

---

## Replit — Real App Progress

> IMPORTANT: One fix per Replit run. No bundling. Every prompt needs a scope lock and regression check. Treat completed items as claimed-completed until verified with a diagnose-only prompt.

### Completed and verified
- Full auth system (JWT, bcrypt, Resend, admin auto-grant, bootstrap security fix)
- PostgreSQL: 20+ tables including all chat, forum, activity, badge, challenge, notes tables
- Library CRUD, reading progress, home screen stats
- Reading calendar (real API, month navigation, tapDay)
- Profile, settings (mostly real — some sub-screens unverified)
- Themes persisting in DB
- 3-step onboarding
- Username duplicate checking
- Challenges — real table, API, join/leave persists
- Gold waitlist button — real
- Quick notes — real
- Notifications — table, bell icon, friend request triggers live
- Review prompt — real API
- BookOpoly game (localStorage)
- Data export (CSV, JSON, PDF)
- Find Friends — username search real
- Library-only search real
- Friend DMs, Group chats, Club discussions — all real, all tested
- Forum — posting, likes, replies, media uploads, share-to-forum — all real
- Activity feed — real, 5 triggers wired
- Badge system — 7 badges wired (64 seed rows pending)
- The Decade Hopper challenge — 11 slots, real tracker, badge at 11/11
- PWA, SEO, performance, error boundaries

### Still to build (in priority order)
1. Badge name corrections in DB (First Chapter, Devoted Reader, Forum Voice)
2. Book save flow fix — author/cover not persisting from Open Library (fixes Unknown Author, No cover, form not clearing, book not in Currently Reading)
3. My Library — tapping book doesn't open detail view
4. My Library All Books tab — show shelf status per book
5. Challenge cards — 3 per row, challenge count discrepancy (54 vs 55)
6. Reading Calendar — year jump navigation
7. Notification triggers — wire forum likes, replies, club posts (underlying features now real)
8. Reels tab
9. Unread badges across chats
10. Global search — book, club, forum tabs
11. Friend request email via Resend
12. QR code and suggested friends
13. Barcode scanner (real camera)
14. Free/Gold feature gating (10 challenges, 3 games, 80 notes, 2 clubs for Free)
15. My Library layout toggle (polish)
16. Batch 5 — BookOpoly 5 board versions
17. Batch 6 — Reading RPG + XP system
18. Batch 9 — Responsive layout
19. Batch 10 — Game completion flow + multiplayer
20. Book Trivia question database
21. Fantasy Book Bingo completion popup
22. Roulette wheel angle fix
23. Purpose-built challenge trackers
24. Reading Passport layout
25. 26 in 2026 B stamp animation
26. 64 remaining badge seed rows
27. Typecheck cleanup

---

## Website Deploy Checklist

- ✅ coming-soon.html live at barrowbound.app
- ❌ pricing.html — built, not yet uploaded
- ❌ terms.html — not yet uploaded
- ❌ privacy.html — not yet uploaded
- ❌ refund-policy.html — not yet uploaded
- ❌ community-guidelines.html — not yet uploaded

---

## Pre-Launch Checklist

### Must do before launch
- Security audit (45-point prompt written — run when feature-stable)
- Tester/promoter accounts (1-2 weeks before launch)
- NZ lawyer review of legal documents
- All Still to Build items complete
- All website pages uploaded
- Hardware back button closing modals app-wide

### Growth before launch
- Update TikTok bio with barrowbound.app
- Post 5 social content pieces
- Build waitlist to 1,000
- Find BookTok micro-influencers
- Set up Kit Gold launch broadcast template

### Post-launch (1-3 months)
- Stripe + Gold launch at $9.99 USD/month
- Annual pricing (on hold — likely $79–89 USD/year)
- BookOpoly multiplayer
- App Store and Google Play (Phase 3)
- Author Q&As (Phase 3)
- NZ GST registration (only when revenue passes NZ$60,000)

---

## Tester/Promoter Accounts

Add email to ADMIN_EMAILS secret before signup, OR run:
`UPDATE user_profiles SET is_pro = true WHERE email = 'their@email.com';`

---

## Replit Prompting Rules

1. Diagnose first
2. Report findings at each step
3. Fix based on evidence not assumptions
4. Test end to end — data must persist after page refresh
5. Only touch minimum code — no regressions
6. Report all changes at the end
7. Include explicit scope lock (list files not to touch)
8. Include regression check (5 key endpoints) before finishing
9. One fix per prompt — no bundling

---

*Last updated: May 2026 — free plan updated (10 challenges, 3 games: Trivia/Roulette/Bingo, 80 notes), gold plan updated (all 55 challenges, unlimited notes), badge names reconciled with spec, all forum/chat/activity/calendar features verified real*
*Real app: Replit with PostgreSQL + custom JWT auth + Resend + Replit App Storage*
*Owner: Courtney, New Zealand*
