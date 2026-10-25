# SpeedGuard KE 🇰🇪 🚗

**SpeedGuard KE** is a Flutter app that helps drivers on Kenyan roads keep an
eye on their speed, the applicable speed limit, and the instant-fine schedule.

> SpeedGuard KE is a driver-awareness aid, **not** a legal or navigation
> authority. Always follow posted road signs, NTSA directions, and the Traffic
> Act (Cap 403).

---

## Features

- 📍 **Live GPS speedometer** with colour-coded safe / warning / danger states.
- 🛣️ **Offline speed-limit reference** for major Kenyan roads and towns:
  - Urban roads: 50 km/h (40 km/h for heavy vehicles)
  - Rural highways: 80 km/h (70 km/h heavy)
  - Highways: 100 km/h (80 km/h heavy)
  - Nairobi Expressway: 110 km/h (90 km/h heavy)
  - School and residential zones: 30 km/h
  - Unmapped roads: conservative 50 km/h fallback (40 km/h heavy)
- 🚚 **Private and commercial vehicle profiles** with automatic limit changes.
- ⚠️ **Overspeed alerts**: audible warning plus a red on-screen banner, both
  toggleable in Settings.
- 💰 **Instant fine estimate** shown while speeding, based on the NTSA fine
  schedule bundled in the app.
- 📊 **Trip history** persisted on the device: distance, max/average speed,
  overspeed events, and duration.
- 🗺️ **OpenStreetMap view** with the driver marker, seeded road-limit markers,
  live speed, and a recenter button.
- 📖 **Traffic fines reference** covering speeding, licensing, safety equipment,
  and lane discipline.
- 🔎 **Sample fine lookup** for trying the UI. It is **not** connected to NTSA or
  eCitizen and never presents itself as an official result.

## What is not implemented

- No cloud account, sync, or Supabase backend.
- No offline map tile cache.
- No speed-camera database or camera alerts.
- No background/always-on tracking. Tracking runs while the app is open.
- The speed-limit dataset is small and point-based (500 m match radius), not a
  full road network. It is a reference, not a substitute for signage.

---

## Getting Started

### Prerequisites

- Flutter **3.44 or newer** (Dart 3.12+)
- Android SDK 33+ or Xcode 14+ for iOS
- A browser with HTTPS (or `localhost`) for the web build

### Install and run

```bash
flutter pub get
flutter run
```

Grant location permission when prompted and tap **START TRIP TRACKING**.

### Tests and checks

```bash
flutter analyze
flutter test
```

### Build releases

```bash
# Android APK
flutter build apk --release

# Android App Bundle (Play Store)
flutter build appbundle --release

# Web
flutter build web --release

# iOS (requires macOS + Xcode)
flutter build ios --release
```

For Play Store signing, copy `android/key.properties.example` to
`android/key.properties` and fill in your keystore details. Without it, release
builds fall back to debug signing for local testing.

### Platform notes

- **Android / iOS / web:** GPS tracking is supported.
- **Linux:** the app runs, but the `geolocator` plugin has no Linux
  implementation; the Speed screen explains that tracking is unavailable.

---

## Project Architecture

Built with Provider state management and a small layered structure:

- `lib/core/`: constants (speed limits, fine schedule), theme, utilities.
- `lib/data/`: models, repositories (local GPS, speed limits, trips, demo
  fines), and change-notifier providers.
- `lib/services/`: map configuration and the audio alert service.
- `lib/presentation/`: screens, dialogs, and reusable widgets.

### Tracking flow

1. `LocationProvider` requests permission and subscribes to the GPS stream.
2. `SpeedGuardApp` forwards each fix to `SpeedProvider` (speed + limit) and
   `TripProvider` (distance and metrics).
3. `NotificationService` plays the warning once per overspeed episode.
4. `TripProvider` saves finished trips to `shared_preferences`; `SettingsProvider`
   persists the alert preferences.

---

## Data Disclaimer

The bundled speed limits, seeded road points, and fine schedule are reference
data. They may be incomplete or outdated. The fine lookup is sample data only.
Drivers remain fully responsible for complying with posted limits and NTSA
directives.

---

## License

GPLv3 - see [LICENSE](LICENSE).
# speedlimiter
# speedlimiter
# speedlimiter
# speedlimiter
