# HomeHub Apple TV (tvOS) Web Wrapper

A native Apple TV (tvOS) application built using React Native and Expo that embeds a remote web dashboard via `react-native-webview`.

## Features
- **Native tvOS Target**: Configured with `isTV: true` in `app.json` and `@react-native-tvos/config-tv` plugin.
- **Cloudflare Zero Trust & OAuth Compatibility**:
  - `domStorageEnabled={true}`
  - `javaScriptEnabled={true}`
  - `sharedCookiesEnabled={true}`
  - `thirdPartyCookiesEnabled={true}`
  - `userAgent` set to Mac desktop Safari (`Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/17.5 Safari/605.1.15`) to ensure standard desktop web layouts and seamless auth flow.
- **Apple TV Remote Integration**:
  - Hardware back / Menu button support via `BackHandler` (allows in-webview back navigation before app exit).
  - TV-preferred focus states on retry button for seamless Siri Remote navigation.
- **Loading & Error Recovery**: Dark-themed loading overlay and network error recovery screen.

---

## Setup & Running

### 1. Install Dependencies
```bash
npm install
```

### 2. Generate Native tvOS Xcode Project (Prebuild)
On macOS with Xcode installed:
```bash
npx expo prebuild --platform ios --clean
```

### 3. Run on Apple TV Simulator
```bash
npx expo run:ios --device "Apple TV"
```
*Or open `ios/HomeHubTV.xcworkspace` in Xcode, choose an Apple TV simulator or connected Apple TV device as the build destination, and press Run (`Cmd + R`).*

---

## Building with Expo (EAS Build)

The project is configured for EAS Build targeting tvOS using `@react-native-tvos/config-tv` with `EXPO_TV=1`.

### 1. Apple TV Simulator Build (No Apple Developer credentials required)
```bash
npx eas-cli build --platform ios --profile preview-simulator
```
Or via script:
```bash
npm run build:tvos:sim
```
This produces a `.tar.gz` with the `.app` bundle ready to run in the Apple TV Simulator.

### 2. Device / Ad-Hoc Build (For physical Apple TV)
```bash
npx eas-cli build --platform ios --profile preview
```
Or via script:
```bash
npm run build:tvos
```
*Note: For physical Apple TV builds via EAS, tvOS requires a tvOS provisioning profile created on developer.apple.com with bundle ID `com.homehub.tvos` and uploaded to your EAS credentials.*

### 3. Production / App Store Build
```bash
npx eas-cli build --platform ios --profile production
```

---

## Configuration Reference
- **Target URL**: `https://nginx.ntfsdata.com/index.html` (configured in `App.js`)
- **Bundle Identifier**: `com.homehub.tvos` (configured in `app.json`)
- **EAS Project ID**: `3e2bfa0c-6e74-4717-be3f-d9a06322204c`
