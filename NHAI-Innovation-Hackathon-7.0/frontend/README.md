# NHAI SecureID — Mobile App

React Native application for offline facial authentication with BlazeFace detection, MobileFaceNet recognition, MiniFASNet anti-spoofing, and liveness detection.

## Prerequisites

- Node.js >= 18
- npm
- Expo CLI
- Android Studio (Android) or Xcode (iOS)

## Setup

```bash
cd frontend
npm install
```

## Run Development Server

```bash
npx expo start --lan
```

Scan QR code with **Expo Go** on your phone (same Wi-Fi).

## Build for Device

```bash
npx expo run:android   # Android
npx expo run:ios       # iOS
```

## Project Structure

| Directory | Purpose |
|---|---|
| `src/app/` | Screens (file-based Expo Router) |
| `src/components/` | Camera, liveness flow, UI primitives |
| `src/lib/` | Database, face API client, sync, settings |
| `src/constants/` | Theme colors, design tokens |
| `src/hooks/` | Theme and color scheme hooks |

## Architecture

```
User → React Native UI → expo-camera → Backend API
                                            ↓
                                   BlazeFace Detection
                                   MobileFaceNet Embedding
                                   MiniFASNet Anti-Spoof
                                            ↓
                                   Decision Engine (Cosine Similarity)
                                            ↓
                                   SQLite (Encrypted) → AWS Sync
```

## Key Screens

- **Splash** → Animated entry with gradient
- **Login** → Supervisor ID + PIN
- **Home** → Dashboard with stats and quick actions
- **Enroll** → 4-step capture (blink, head turns) + employee form
- **Authenticate** → Select worker → liveness challenge → verify
- **Records** → Attendance log with sync status
- **Settings** → Backend URL config, auto-discovery

## Dependencies

- expo, expo-router, expo-camera, expo-sqlite
- nativewind (Tailwind CSS)
- react-native-reanimated, react-native-gesture-handler
