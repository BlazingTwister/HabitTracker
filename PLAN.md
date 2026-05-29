# PLAN.md — StreakForge Development Roadmap

This file is the source of truth for Jules AI and all contributors.
Every task Jules is given should align with a phase below.

---

## App Goal

Build a cross-platform habit tracking app (Android + iOS) using React Native (Expo)
with a freemium monetization model. Target: consistent individuals aged 18–35
who want to build better daily routines.

---

## 🛠 Tech Decisions (non-negotiable for Jules)

- **Framework:** React Native with Expo SDK 51+
- **Language:** TypeScript (strict mode)
- **Navigation:** React Navigation v6 — Bottom Tab Navigator + Stack
- **Backend:** Supabase (auth, PostgreSQL database, real-time)
- **State management:** Zustand
- **Notifications:** expo-notifications
- **Payments:** RevenueCat SDK
- **Styling:** StyleSheet API (no styled-components or NativeWind)
- **Theme:** Dark background (#0F0F14), purple primary (#7C3AED), white text

---

## Phase 1 — Project Setup (Week 1–2)

**Goal:** Working Expo app with navigation, Supabase connected, placeholder screens.

Tasks:
- [ ] Init Expo project with TypeScript template
- [ ] Install and configure React Navigation (Bottom Tabs: Home, Stats, Settings)
- [ ] Set up Supabase client (supabase.ts) with .env config
- [ ] Create placeholder screens for all 3 tabs with correct layout shell
- [ ] Set up Zustand store structure (habitStore, userStore)
- [ ] Configure ESLint + Prettier
- [ ] Create constants file (colors, spacing, icons map)
- [ ] Add .env.example with required keys documented

**Jules prompt for this phase:**
"Set up a React Native Expo project with TypeScript. Add React Navigation with
a bottom tab navigator (Home, Stats, Settings screens). Create a Supabase client
in lib/supabase.ts reading from .env. Add Zustand for state. Use a dark theme
with #0F0F14 background and #7C3AED purple accent. Placeholder screens should
show the screen name centered."

---

## Phase 2 — Core Habit Features (Week 2–4)

**Goal:** Users can create, view, complete, and delete habits.

Tasks:
- [ ] Supabase schema: `habits` table (id, user_id, name, icon, color, frequency, created_at)
- [ ] Supabase schema: `completions` table (id, habit_id, completed_date)
- [ ] Habit creation form (name, icon picker, color picker, frequency selector)
- [ ] Home screen: list today's habits with completion checkboxes
- [ ] Swipe-to-delete on habit items
- [ ] Streak calculation logic (current streak, longest streak)
- [ ] Habit detail screen (edit, view full history)
- [ ] Calendar heatmap component (show completions over past 3 months)
- [ ] Free tier enforcement: block habit creation at 4th habit, show paywall

**Jules prompt example:**
"Build the habit creation screen. It should have a text input for habit name,
a horizontal scroll icon picker (use emoji), a color picker (6 preset colors),
and a frequency selector (Daily / Weekdays / Custom days of week). On save,
insert to Supabase habits table and navigate back to Home."

---

## Phase 3 — Notifications (Week 4)

**Goal:** Each habit can have a daily push notification reminder.

Tasks:
- [ ] Request notification permissions on first launch
- [ ] Notification time picker in habit create/edit form
- [ ] Schedule local notifications per habit using expo-notifications
- [ ] Cancel notifications when habit is deleted
- [ ] Update notification time when habit is edited

---

## Phase 4 — Stats Screen (Week 4–5)

**Goal:** Users see meaningful progress data.

Tasks:
- [ ] Weekly completion bar chart (last 7 days)
- [ ] Monthly completion line chart
- [ ] Per-habit stats: current streak, longest streak, total completions, % completion
- [ ] "Best day of week" insight card
- [ ] Stats gated by Pro for history beyond 7 days

---

## Phase 5 — Auth & Accounts (Week 5)

**Goal:** Users can sign up, log in, and have data persist across devices.

Tasks:
- [ ] Supabase Auth: email/password sign up and login screens
- [ ] Google OAuth via Supabase
- [ ] Auth flow: onboarding → signup/login → home
- [ ] Persist session with AsyncStorage
- [ ] Settings screen: account info, sign out, delete account
- [ ] Row-level security on Supabase tables (users only see their own data)

---

## Phase 6 — Monetization (Week 5–6)

**Goal:** RevenueCat integrated, paywall functional, Pro features gated.

Tasks:
- [ ] Install and configure RevenueCat SDK
- [ ] Create products in App Store Connect and Google Play Console
- [ ] Build paywall screen (show Free vs Pro, highlight benefits)
- [ ] Trigger paywall at: 4th habit creation, 7-day stats limit, theme picker
- [ ] Restore purchases button in Settings
- [ ] 7-day free trial for Pro
- [ ] Unlock Pro features on active subscription (check RevenueCat entitlements)

**Free vs Pro gates to enforce in code:**
- `habits.length >= 3` → show paywall on add
- `statsRange > 7` → blur/lock older data
- `themes.length > 1` → lock non-default themes
- `remindersPerHabit > 1` → lock in habit edit form

---

## Phase 7 — Polish & Launch Prep (Week 6–8)

Tasks:
- [ ] 3-screen onboarding flow (shown once on first launch)
- [ ] App icon (1024x1024 PNG) + adaptive icon for Android
- [ ] Splash screen
- [ ] Empty states for Home (no habits yet) and Stats (no data)
- [ ] Loading skeletons for data fetch states
- [ ] Haptic feedback on habit completion
- [ ] Error boundaries and crash-safe async handling
- [ ] App Store metadata: title, description, keywords, screenshots (6.7", 5.5", iPad)
- [ ] Google Play metadata: same + feature graphic
- [ ] Privacy Policy URL (required by both stores)
- [ ] TestFlight internal testing (iOS)
- [ ] Google Play internal testing track (Android)

---

## Monetization Strategy

**Model:** Freemium + subscription
**Pricing:** $3.99/month or $24.99/year (37% saving)
**Trial:** 7 days free on annual plan

**Target metrics:**
- 3% free-to-paid conversion rate
- < $0.50 cost per install (organic/ASO first)
- 4.5+ App Store rating (drives organic installs)

**Revenue milestones:**
- 500 downloads → ~$60 MRR
- 2,000 downloads → ~$240 MRR
- 10,000 downloads → ~$1,200 MRR

---

## Launch Checklist

- [ ] Both stores approved and live
- [ ] RevenueCat webhook → Supabase (track paid users)
- [ ] Post on r/getdisciplined, r/habit, r/startups
- [ ] Product Hunt launch scheduled
- [ ] 3 short-form videos of app in use (TikTok/Reels)
- [ ] Build-in-public thread started (X/Twitter)

---

## Jules AI Notes

- Always use TypeScript with strict types — no `any`
- All Supabase calls go through a service layer in `/lib` — never call Supabase directly from screens
- Never hardcode strings — use a constants file
- One PR per feature — keep PRs small and reviewable
- Write a brief comment above any non-obvious logic
- Follow the existing folder structure (see README.md)
