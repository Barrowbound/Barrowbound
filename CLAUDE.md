# CLAUDE.md — Barrowbound Project Brief

This file gives Claude full context on the Barrowbound project so any new conversation picks up exactly where the last one left off.

---

## Project Overview

**Barrowbound** is a reading app concept combining beautiful book tracking, gamified reading challenges, interactive reading games, social community features, and AI-powered book discovery — all in one dark, premium-feeling mobile app.

The closest comparison is: Goodreads (community) + Bookmory (beautiful tracking) + TikTok (discovery energy) + Facebook Groups (book clubs) — but better than all of them combined.

---

## Brand Identity

| Detail | Value |
|---|---|
| **App name** | Barrowbound |
| **Primary domain** | barrowbound.app |
| **Secondary domain** | barrowbound.co |
| **Tagline** | Your entire reading life, in one place |
| **Primary colour** | #d4a843 (warm gold) |
| **Background** | #0e0c0a (near black) |
| **Surface** | #1a1612 |
| **Text** | #f5ede0 (cream) |
| **Display font** | Cormorant Garamond (serif, headers) |
| **Body font** | DM Sans (clean, modern) |
| **Visual identity** | Dark backgrounds, warm amber/gold accents, cream text. Feels like reading by candlelight — intimate, eerie, premium. Inspired by ancient libraries and dark folklore. |

Both domains registered at Porkbun. Email forwarding active on both — hello@barrowbound.app and hello@barrowbound.co forward to owner's personal email.

---

## Logo & Profile Image

Professional logo already designed — circular dark bookshelf under an arch, lit candle centred, crossed quills below, BARROWBOUND gold wordmark, YOUR READING WORLD subtitle, black circle background. Used as profile image across all platforms. Saved as Profile_Image.png.

SVG version (barrowbound_bookshelf_logo.svg) also exists — organised chaos bookshelf with 3 shelves, leaning books, candle, skull, hourglass, plant, folded paper, crossed quills, stacked books, gold wordmark.

Facebook cover photo (barrowbound_cover_textonly.png) created — 820x312px, dark background, gold accent bars, centred wordmark.

---

## Social Media — All Platforms Done

| Platform | Handle | Status |
|---|---|---|
| TikTok | @barrowbound | Done |
| Instagram | @barrowboundapp | Done |
| Threads | @barrowboundapp | Done |
| YouTube | @barrowboundapp | Done |
| Reddit | Barrowboundapp | Done |
| Facebook | Barrowbound Page | Done |

---

## Files

| File | Description |
|---|---|
| barrowbound-testrun.html | MAIN FILE — full 6-screen interactive prototype, all games, all modals |
| challenges-showcase.html | Standalone challenges and games showcase |
| coming-soon.html | Coming soon landing page for barrowbound.app |
| barrowbound_bookshelf_logo.svg | SVG bookshelf logo |
| barrowbound_stacks.svg | Modified bookshelf logo with stacked books |
| barrowbound_cover_textonly.png | Facebook cover photo 820x312px |
| Profile_Image.png | Profile photo used across all social platforms |
| CLAUDE.md | This file |

---

## App Structure — 6 Screens

### Home
- Dynamic greeting (time-based)
- Reading streak + annual goal progress, gold B watermark on hero banner
- Currently Reading cards with progress bars and format badges
- Mood-to-Book matching card
- Friend Activity feed — View All opens full modal
- Recommended for You — See All opens recommendations modal

### Library
- 6 shelf tabs: All Books, Reading, Read, Want to Read, DNF, Paused
- Tabs actually filter books by data-shelf attribute on each card
- Search icon opens live search modal
- Barcode scanner modal
- Manual add modal — new books appear immediately with correct shelf
- Book Detail modal

### Challenges and Games
- Featured Challenges — 2-column grid, Browse tile first (opens All 55 overlay)
- See All 55 — full overlay with 2-row category filter, filterable 2-column grid
- Reading Games — 7 fully playable + 3 coming soon greyed out
- Active Challenges with progress bars — Manage opens All 55
- Live Community Event banner

### Reading Calendar
- Month grid with colour-coded strips, format key, monthly stats, share button

### Community
- 4 tabs (flex-wrap): Book Clubs, Group Chats, Friend Chats, Forum
- Forum shows full post text, heart expands likes, speech bubble expands replies with inline reply box, Follow button on every post

### Profile
- Reader personality badge, badges (See All 18 opens modal with 18 earned + 8 locked)
- Reading stats by format, top genres chart
- Full settings hub

---

## Settings Hub — All Working

All sub-modals use back arrow (not X) so they return to Settings rather than closing everything.

- Edit Profile — fields modal, back to settings
- Privacy Centre — 7 toggles, back to settings
- Notifications — master toggle plus granular controls
- Appearance — theme grid, accent colours, text size
- Import / Export — Goodreads/StoryGraph/Bookmory import, 6 export formats
- Help and FAQ — 8 expandable questions with numbered step-by-step answers
- Rate Barrowbound — 5-star tap selector
- Contact Support — category dropdown plus message form
- Log Out — confirmation dialog, logs out to logged-out screen with Log Back In button

---

## 7 Interactive Games (all fully playable in testrun)

| Game | How It Works |
|---|---|
| Genre Bingo | 5x5 stamp board, row completion detection, share card |
| Blind Roulette | SVG spinning wheel, picks random TBR book |
| Book Trivia | 5 questions, 20-second timer, all answers verified correct |
| Book Bracket | 8 books, quarterfinals to semis to final to champion |
| Reading RPG | Character card, class/level/XP, quests, inventory |
| Reading Passport | Country stamp grid, suggested destinations |
| BookOpoly | 30-space board, 6-column grid, animated dice, token movement |

3 Coming Soon (greyed out): Spine Bingo, Chain Reading, Name That Book

---

## 55 Challenges — 10 Categories

Game (8), Annual/Goal (7), Bingo (8), Fandom (5), Quest (4), Themed (9), Creative (5), Diversity (3), Social (3), Stats (3) = 55 total

All 55 in the allChallenges JS array in testrun with name, description, category, player count, joined status.

---

## Monetisation

Free: core tracking, 3 challenges, 2 clubs, 50 notes, 2 themes, basic stats, weekly backup, 5 AI/month

Pro $10/month or $80/year: unlimited everything, 8+ premium themes, Kindle/Audible/Libby sync, advanced analytics, PDF journal, custom challenges, leaderboards, author QAs, daily backup, Reading Wrapped

---

## Coming Soon Landing Page

coming-soon.html ready to deploy at barrowbound.app. Includes animated candle glow, bookshelf SVG icon, gold wordmark, email signup form (needs Mailchimp/ConvertKit for real capture), feature pills, social links, corner marks, noise texture.

Deployment status: GitHub repo created (Barrowbound/Barrowbound). DNS TXT verification for GitHub Pages pending in Porkbun — TXT record added, awaiting propagation.

---

## Key Technical Notes

- All modals use modal-overlay class + open class (NOT modal class)
- openOverlay() / closeOverlay() handle game overlay screens
- switchScreen() closes all open overlays and modals before switching tabs
- answerTrivia(chosen, el) is current version — old modal version is answerTriviaModal(el, correct)
- Library shelf tabs use data-shelf attribute on each book card for filtering
- All JS verified clean with node --check, zero syntax errors
- Trivia timer: 0.6% decrement every 120ms = 20 seconds per question
- BookOpoly: 30 spaces, 6-column grid, min-height 46px
- FAQ accordion uses toggleFaq(id, header)

---

## Tech Recommendations

- Platform: React Native (iOS + Android)
- Initial build: Expo
- Back end: Node.js + PostgreSQL + Redis
- Hosting: AWS or Railway
- Push notifications: OneSignal
- Book database: Open Library API + Google Books API fallback
- Barcode scanning: ISBNdb
- Roulette wheel: SVG textPath only — never absolute-positioned divs

---

## Target Audience

1. BookTok Generation (18-32) — TikTok/Instagram users, love aesthetics and gamification
2. Dedicated Readers (28-45) — 20-50+ books/year, book club members, frustrated with Goodreads
3. Goal-Oriented Readers — streak trackers, challenge participants
4. Diversity-Conscious Readers — tracking global authors intentionally

Owner based in New Zealand.

---

## Outstanding To-Do

- Complete GitHub Pages DNS verification (TXT record in Porkbun, awaiting propagation)
- Get coming-soon.html live at barrowbound.app
- Connect email signup to Mailchimp or ConvertKit for real waitlist
- Same DNS setup for barrowbound.co
- Build email waitlist — target 1,000 signups before launch
- Find developer / development agency
- Partner with BookTok micro-influencers for early access content

---

*Last updated: April 2026*
*Prototype version: 2.0 — barrowbound-testrun.html*

---

## Full Checklist — Last Updated April 2026

### ✅ DONE

**Brand & Identity**
- App name, tagline, colours, fonts locked in
- Professional logo designed (circular arch bookshelf PNG)
- SVG bookshelf logo created
- Facebook cover photo created (820x312px)

**Domains**
- barrowbound.app registered at Porkbun
- barrowbound.co registered at Porkbun
- Email forwarding on both to personal email
- barrowbound.co redirects to barrowbound.app
- SSL certificate active on barrowbound.app

**Social Media**
- TikTok @barrowbound
- Instagram @barrowboundapp
- Threads @barrowboundapp
- YouTube @barrowboundapp
- Reddit Barrowboundapp
- Facebook Barrowbound Page
- All bios written and ready to paste

**Website**
- Coming soon page live at barrowbound.app
- GitHub repo set up (Barrowbound/Barrowbound)
- Kit account set up with hello@barrowbound.app
- Email signup form connected to Kit
- SSL certificate active

**Prototype — barrowbound-testrun.html**
- Login / Signup screen with Google, Apple, Facebook
- Onboarding tour (5 steps with spotlight)
- All 6 screens working
- All 7 games playable
- 55 challenges with 10-category filter
- All settings working with back arrows
- All modals working
- Friends, Badges, Leaderboard, Readathon, Share Calendar modals

---

### 🔲 STILL TO DO

**Immediate**
- Upload latest coming-soon.html to GitHub (logo + colour fixes)
- Update all social bios with barrowbound.app
- Test email signup — confirm emails land in Kit
- Create and post content on TikTok and Instagram (5 posts already written)

**Website — Build It Yourself**
- Get prototype running on Replit as a live shareable URL
- Learn basic React
- Set up Supabase for login and database (free tier)
- Build real book search using Open Library API
- Build real user profiles and library
- Build real challenges and progress tracking
- Add payments via Stripe + RevenueCat
- Terms of Service and Privacy Policy pages

**Prototype — Known Issues**
- Confirm block on home screen is fully gone
- Login screen arch SVG illustration needs fixing
- Two-Factor Auth — no modal attached
- Mood-to-Book — needs real mood selector
- AI Companion — no response modal
- Calendar month navigation not working
- Book Detail — ratings/notes not saveable
- Notifications time picker not working

**Growth**
- Build email waitlist to 1,000 before launch
- Find BookTok micro-influencers for early access
- Set up Kit broadcast for launch announcement
- Press kit for media outreach
- App Store screenshots and descriptions

**Business**
- Register as a business (when ready)
- NZ GST setup
- App Store and Google Play submission (Phase 3)
