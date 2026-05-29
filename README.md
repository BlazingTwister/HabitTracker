# StreakForge — Habit Tracker

A cross-platform habit tracking app for Android and iOS built with React Native (Expo).
Track daily habits, build streaks, and stay consistent with smart reminders.

---

## Features

- **Habit Management** — Create habits with custom icons, colors, and frequencies
- **Streak Tracking** — Daily/weekly streaks with longest-streak history
- **Smart Reminders** — Push notifications per habit at custom times
- **Visual Progress** — Calendar heatmap, completion rings, weekly charts
- **Stats Dashboard** — Monthly history, trends, and insights
- **Cloud Sync** — Cross-device sync (Pro feature)
- **Freemium Model** — Free tier (3 habits) + Pro subscription via RevenueCat

---

## Tech Stack

| Layer | Technology |
|---|---|
| Framework | React Native + Expo (SDK 51+) |
| Language | TypeScript |
| Navigation | React Navigation v6 (Bottom Tabs + Stack) |
| Backend/Auth | Supabase |
| Notifications | Expo Notifications |
| Payments | RevenueCat |
| State | Zustand |
| Storage | AsyncStorage + Supabase |

---

## Project Structure

```
streakforge/
├── app/                  # Expo Router screens
│   ├── (tabs)/           # Bottom tab screens
│   │   ├── index.tsx     # Home — today's habits
│   │   ├── stats.tsx     # Stats & history
│   │   └── settings.tsx  # Account & preferences
│   ├── habit/
│   │   ├── create.tsx    # New habit form
│   │   └── [id].tsx      # Habit detail & edit
│   └── paywall.tsx       # Pro upgrade screen
├── components/           # Reusable UI components
├── lib/
│   ├── supabase.ts       # Supabase client
│   └── revenuecat.ts     # RevenueCat client
├── stores/               # Zustand state stores
├── hooks/                # Custom React hooks
├── constants/            # Colors, icons, config
└── assets/               # Fonts, images, icons
```

---

## Getting Started

### Prerequisites
- Node.js 18+
- Expo CLI (`npm install -g expo-cli`)
- iOS Simulator (Mac only) or Android Studio

### Installation

```bash
git clone https://github.com/YOUR_USERNAME/streakforge.git
cd streakforge
npm install
cp .env.example .env
# Add your Supabase and RevenueCat keys to .env
npx expo start
```

---

## Monetization

**Freemium model with in-app subscription:**

| Feature | Free | Pro ($3.99/mo · $24.99/yr) |
|---|---|---|
| Habits | Up to 3 | Unlimited |
| Stats history | 7 days | Full history |
| Themes | 1 | 10+ |
| Home screen widget | ❌ | ✅ |
| Multiple reminders | ❌ | ✅ |
| Cloud backup & sync | ❌ | ✅ |

Payments handled by RevenueCat (App Store + Google Play).

---

## Roadmap

See [PLAN.md](./PLAN.md) for the full development roadmap.

---

## License

MIT © 2026 Ese George
