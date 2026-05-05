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
| barrowbound-pricing-guide.docx | Pricing decisions, competitor comparison, change checklist |
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
- 3 reading challenges
- Book Trivia (1 game only)
- Forums, group chats and friend chats
- Photos and videos in forum posts (up to 4 photos or 1 video per post, max 3 minutes)
- Reels tab (vertical video feed)
- Friend system and activity feed
- 2 book clubs
- Basic reading stats
- Badges for free features
- 3 themes (Candlelight, Midnight, Slate)

### Gold Plan — $17/month NZD (launching 2-3 months post-launch)
- Everything in Free, plus:
- 500 notes
- All 55 reading challenges
- All 7 games
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

No Bronze tier. No founding member pricing. No annual pricing yet. No Author Q&As (Phase 3). See barrowbound-pricing-guide.docx for full pricing decisions and change checklist.

---

## Themes

Free (3): Candlelight (default), Midnight, Slate
Gold (7): Forest, Ocean, Ember, Dusk, Parchment, Rose, Noir

Each theme updates ALL CSS variables throughout the app. Selected theme stored in database and persists across sessions.

---

## Games (7 total)

Full spec in barrowbound-games-challenges-badges.docx

### Free (1 game)
- Book Trivia

### Gold (all 7)
- Book Trivia
- Genre Bingo (multiplayer comparison with friends)
- Blind Roulette
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

### Challenge flow
- Join/Joined buttons on all challenge cards
- Tapping Joined shows leave confirmation: "Do you want to leave [Name]? Your progress will be lost."
- Game challenges: Play Now button opens linked game
- Tracking challenges: Open Challenge button opens purpose-built tracker
- Manage button on Your Active Challenges: opens modal showing all joined challenges with red Leave buttons

### Fandom challenges (updated May 2026)
Replaced Discworld Journey, Stephen King Survivor, Brandon Sanderson Scholar with:
- The Series Completionist (Ongoing, Moderate)
- The Award Hunter (Year-Long, Moderate)
- The Adaptation Chase (Year-Long, Casual)

### Diversity challenges (updated May 2026)
- The Marginalised Voices Challenge (replaced Read the World)
- Own Voices Challenge
- The First Voices Challenge — Indigenous/First Nations authors (replaced Amplify Diverse Voices)

### Social challenges (updated May 2026)
- Buddy Read Challenge
- Book Club Pick
- Read and Recommend (replaced Review Swap)

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

Triggers a notification for:
- Someone likes your forum post
- Someone replies to your forum post
- Friend request received and accepted
- Book club discussion post added (notifies all club members)
- Book club meeting reminder (1 hour before scheduled discussion)
- Reading streak reminder at 8pm if no reading logged today (opt-in, default on)
- Challenge milestone hit (halfway, nearly complete)
- Buddy read partner logs progress
- Weekly reading summary (opt-in, sent Sunday)

Database: notifications table with id, user_id, type, title, body, read (boolean), created_at. Bell icon shows red badge count for unread.

---

## Search

Two distinct types:

Home screen global search: searches Open Library books, users by username, book clubs by name, forum posts. Results in tabs: All, Books, People, Clubs, Forum.

Library search: searches only within user's own library by title and author.

Book search ranking: exact title match first, starts with search term second, most popular by editions count as tiebreaker. Uses Open Library API with title: prefix and sort=editions.

---

## Find Friends

- Primary: search by username (case insensitive, partial match)
- Secondary: QR code (generates unique profile QR, scannable by another user)
- Suggested: 5 users based on shared genre preferences from onboarding
- No contacts sync

---

## Onboarding (first login only)

3-step flow after email verification. Tracked with has_completed_onboarding boolean on user_profiles.

1. Genre preferences — select minimum 3 from all 22 genres (saved to user_profiles)
2. Reading goal — number input, defaults to 26, quick-select: 12, 26, 52
3. Theme — pick from 3 free themes (Candlelight pre-selected)

After completing: has_completed_onboarding = true, show welcome card, then home screen.

---

## Email Notifications (via Resend)

All from hello@barrowbound.app with Barrowbound branding.

Active: email verification, password reset, friend request notification
Opt-in: weekly reading digest (Sunday), friend request email
Built not yet sent: Gold plan launch announcement template

---

## Forum — Media Posts

- Photos: up to 4 per post (jpg, png, webp, under 1MB each)
- Videos: 1 per post, maximum 3 minutes, maximum 200MB (mp4, mov)
- No mixing photos and videos in same post
- All media stored on Cloudinary (not database or Replit filesystem)
- Single photo: full width. Multiple photos: 2-column grid. Videos: thumbnail with play button.

### Reels Tab
- Separate Community tab alongside Clubs, Groups, Friends, Forum
- Vertical scrolling feed of video posts only
- Autoplay on scroll, pause on scroll away (muted by default)
- Right side: likes, comments, share. Optional book tag links to book detail.

---

## Chats

Three types — save to database, update via polling every 3 seconds:
- Friend Chats: direct messages between two users
- Group Chats: multi-user community chats
- Book Club Discussions: threaded posts within a club

All chats: chronological order, auto-scroll to latest, timestamps, unread indicators, 📎 image attachment button.

---

## Review Flow

When a book is marked as Read:
1. Bottom sheet appears: "You finished [Book Title]! 🎉" with star rating and review text area
2. Save Review (saves to database and book detail Review tab) or Maybe Later
3. After saving: optional "Share to Forum?" prompt
4. Maybe Later: reminder banner shown on Review tab next visit

---

## Quick Note on Currently Reading

📝 button on each Currently Reading card on home screen. Opens quick note bottom sheet for that book. Saves to book's Notes tab. Updates The Annotator challenge progress.

---

## Performance and Stability

- Database indexes on: email, username, user_id, book_id, conversation_id, created_at
- Pagination on all list endpoints (default limit 20)
- Short-term caching (60 seconds) for Open Library results and user profile data
- All image uploads compressed (max 1200px, under 500KB, webp where possible)
- Error boundaries: API failures show retry button not blank screen

---

## PWA

manifest.json: name Barrowbound, display standalone, background #0e0c0a, theme #d4a843, icons 192x192 and 512x512, Apple meta tags. Installable on Android and iPhone home screen.

---

## SEO

Open Graph meta tags on app HTML: title, description, og:title, og:description, og:image (Barrowbound logo), og:url, twitter:card, canonical URL.

---

## Data Export

Settings > Import/Export:
- CSV: library with title, author, shelf, format, dates, rating, pages, review
- JSON: complete profile data
- PDF reading journal: profile header, year stats, books read, quotes, challenge progress

---

## Replit — Real App Progress

### Completed
- Custom JWT auth (Clerk fully removed), Resend email, bcrypt passwords
- PostgreSQL: users, user_profiles, books, messages, conversations, conversation_members, notifications tables
- Admin account auto-grant (is_pro + is_admin)
- Full library CRUD, reading progress, home screen stats
- Community screens, forum, chats, book clubs
- Profile screen, settings, all sub-screens
- Gold waitlist button (gold_waitlist boolean in database)
- Username duplicate checking with bookish suggestions
- Themes stored in database and persisting
- Challenge cards, game tiles, Manage modal with Leave confirmation
- Review prompt when book marked as Read
- Quick note button on Currently Reading cards
- 3-step onboarding for new users
- Notifications system with all defined triggers
- Global search and library-only search
- Find Friends (username search, QR code, suggested friends)
- PWA manifest and app icon
- Open Graph SEO meta tags
- Data export (CSV, JSON, PDF)
- Photos and videos in forum posts (Cloudinary)
- Reels tab in Community
- Chat system with polling and unread indicators
- Performance optimisation (indexes, pagination, caching, compression)
- Error boundaries

### Still to build (in order)
1. Batch 4 — Add Book cover photo upload
2. Batch 5 — BookOpoly overhaul (5 board versions)
3. Batch 6 — Reading RPG + unified XP system
4. Batch 8 — Free/Gold feature gating
5. Batch 9 — Responsive layout
6. Batch 10 — Game completion flow + multiplayer Trivia and Bingo
7. Book Trivia question database (5,000-10,000 questions, 11 categories)
8. Fantasy Book Bingo completion popup + Start New Board
9. Roulette wheel angle math fix
10. Purpose-built trackers for all tracking challenges
11. Reading Passport passport/book layout with page flipping
12. 26 in 2026 Barrowbound B stamp animation
13. BookOpoly 5 themed board versions

---

## Website Deploy Checklist

- ✅ coming-soon.html live at barrowbound.app
- ❌ pricing.html — built, not yet uploaded to GitHub
- ❌ terms.html — not yet uploaded
- ❌ privacy.html — not yet uploaded
- ❌ refund-policy.html — not yet uploaded
- ❌ community-guidelines.html — not yet uploaded

---

## Pre-Launch Checklist

### Must do before launch
- Security audit (45-point prompt written — run when app is feature-stable)
- Tester/promoter accounts (set up 1-2 weeks before launch)
- NZ lawyer review of legal documents
- All Batches 4-10 complete
- All website deploy checklist items uploaded
- Book search ranking fixed
- Barcode scanner camera working
- Profile photo upload working
- Forum filters working
- Calendar month navigation working
- Themes fully applying and persisting
- Hardware back button closing modals app-wide

### Growth before launch
- Update TikTok bio with barrowbound.app
- Post 5 social content pieces (scripts ready in barrowbound-social-content-plan.docx)
- Build waitlist to 1,000
- Find BookTok micro-influencers
- Set up Kit Gold launch broadcast template

### Post-launch (1-3 months)
- Stripe integration and Gold plan launch at $17/month NZD
- Annual pricing for Gold (on hold)
- BookOpoly multiplayer
- App Store and Google Play (Phase 3)
- Author Q&As (Phase 3)
- NZ business registration and GST (when needed)

---

## Tester/Promoter Accounts

Set up 1-2 weeks before launch. To grant Gold access:
- Add email to ADMIN_EMAILS secret in Replit before they sign up, OR
- Run: UPDATE user_profiles SET is_pro = true WHERE email = 'their@email.com';

---

## Replit Prompting Rules

Every prompt sent to Replit must:
1. Diagnose first — check files/configs before touching anything
2. Report findings at each step
3. Fix based on evidence not assumptions
4. Test end to end before finishing
5. Only touch minimum code required — do not cause regressions
6. Report all changes made at the end

---

*Last updated: May 2026*
*Real app: Replit with PostgreSQL + custom JWT auth + Resend*
*Owner: Courtney, New Zealand*

