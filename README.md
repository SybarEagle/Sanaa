# Muslim Lite — Islamic Lifestyle App

A full-featured Islamic companion app built with React and Capacitor, available on iOS and Android. Sanaah provides GPS-based prayer times, a full Quran reader, Qibla compass, automatic Azaan playback, and a suite of daily Islamic tools — all in one place.

---

## Features

### Prayer Times
- Automatic GPS-based prayer time calculation
- Supports multiple calculation methods (ISNA, Karachi, MWL, Umm Al-Qura, Egyptian, Diyanet, Russia)
- Live countdown to the next prayer
- Displays city, region, and country flag via reverse geocoding
- Caches today's times locally so the app works offline

### Azaan Player
- Toggle automatic Azaan for each prayer individually
- Full-length bundled Adhan audio (standard + Fajr variant) plays at prayer time — even when the screen is locked
- iOS: uses `AVAudioSession` (`.playback` category) and a silent heartbeat to keep the app alive in the background, firing a native Swift timer at the exact prayer time
- Local notifications delivered with a short notification sound; the full Adhan plays natively via `AppDelegate`
- Preview any Azaan from within the app

### Quran Reader
- Full 30-Juz / 114-Surah Quran
- Browse by Juz or by Surah
- Arabic text with English transliteration and translation
- Per-verse audio playback via streaming
- Remembers your last position

### Qibla Compass
- Real-time compass bearing to Mecca using `DeviceOrientation` API
- Visual alignment indicator with haptic feedback when aligned
- Falls back gracefully if sensor permission is unavailable

### Tasbih
- Digital dhikr counter with haptic feedback
- Preset Tasbih targets (33 / 99 / custom)
- Session history

### Prayer Tracker
- Log each of the five daily prayers
- Weekly and monthly completion statistics
- Persistent local storage

### Islamic Calendar
- Full Hijri calendar with Gregorian conversion
- Highlights major Islamic events (Ramadan, Eid, Ashura, Mawlid, etc.)
- Browse by month with event badges

### 99 Names of Allah (Asmaul Husna)
- All 99 names with Arabic script, transliteration, and meaning
- Searchable by transliteration or meaning
- Colour-coded by group of 20

### Daily Dua Banner
- A different Dua shown on every app open with Arabic, translation, and Quranic reference

### Date Converter
- Tap-to-step Gregorian ↔ Hijri date converter

---

## Tech Stack

| Layer | Technology |
|---|---|
| UI | React 18, Tailwind CSS 3 |
| Build | Vite 6 |
| Mobile | Capacitor 8 |
| iOS native | Swift, AVFoundation, UNUserNotificationCenter |
| Prayer times API | [Aladhan API](https://aladhan.com/prayer-times-api) |
| Reverse geocoding | [Nominatim / OpenStreetMap](https://nominatim.openstreetmap.org) |
| Quran data | [AlQuran Cloud API](https://alquran.cloud/api) |

---

## Getting Started

### Prerequisites
- Node.js 18+
- Xcode 15+ (for iOS)
- Android Studio (for Android)
- Capacitor CLI (`npm install` installs it locally)

### Install & Run Web

```bash
npm install
npm run dev
```

### Build & Sync to Native

```bash
npm run build
npx cap sync
```

### Run on iOS

```bash
npx cap open ios
# Then build and run from Xcode
```

### Run on Android

```bash
npx cap open android
# Then build and run from Android Studio
```

---

## iOS Background Azaan

The full Azaan plays at prayer time even when the screen is locked. This works through a three-part mechanism in `AppDelegate.swift`:

1. **`AVAudioSession` (`.playback`)** — declared in `UIBackgroundModes: audio`, this keeps the audio session active when the silent switch is on
2. **Silent heartbeat** — a 0-volume looping `.caf` file keeps the app process alive up to 12 hours before the next prayer
3. **Native Swift timers** — scheduled from pending `UNCalendarNotificationTrigger` requests; fire at the exact prayer time and play the full bundled `adhan.caf` or `adhan_fajr.caf`

---

## App Store

- **Bundle ID:** `com.sanaah.app`
- **Platform:** iOS 15+, Android
- **Developer:** Sybar Systems LLC
- **Category:** Reference / Lifestyle

---

## License

Private — © Sybar Systems LLC. All rights reserved.
