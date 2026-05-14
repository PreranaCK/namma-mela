# 🎭 Namma-Mela — Digital Box Office

A theatrical Android app for rural drama companies (Company Nataka).
Built with Kotlin, Room DB, Navigation Component, Glide, ViewModel + LiveData.

---

## 📁 Project Structure

```
NammaMela/
├── app/
│   ├── src/main/
│   │   ├── java/com/nammamela/
│   │   │   ├── NammaMelaApp.kt              ← Application class
│   │   │   ├── model/
│   │   │   │   ├── Play.kt                  ← Tonight's play entity
│   │   │   │   ├── Seat.kt                  ← Seat entity + SeatStatus enum
│   │   │   │   ├── CastMember.kt            ← Cast member entity
│   │   │   │   └── FanComment.kt            ← Fan wall comment entity
│   │   │   ├── data/
│   │   │   │   ├── db/
│   │   │   │   │   ├── NammaMelaDatabase.kt ← Room DB + seed data
│   │   │   │   │   ├── PlayDao.kt
│   │   │   │   │   ├── SeatDao.kt
│   │   │   │   │   ├── CastDao.kt
│   │   │   │   │   ├── FanCommentDao.kt
│   │   │   │   │   └── Converters.kt
│   │   │   │   └── repository/
│   │   │   │       └── NammaMelaRepository.kt
│   │   │   ├── ui/
│   │   │   │   ├── MainActivity.kt          ← Host + Bottom Nav
│   │   │   │   ├── MainViewModel.kt         ← Shared ViewModel
│   │   │   │   ├── tonight/
│   │   │   │   │   ├── TonightFragment.kt   ← Play poster screen
│   │   │   │   │   └── ManagerUpdateActivity.kt ← Manager edit screen
│   │   │   │   ├── cast/
│   │   │   │   │   └── CastFragment.kt      ← Cast display
│   │   │   │   ├── seats/
│   │   │   │   │   └── SeatsFragment.kt     ← Grid seat map
│   │   │   │   └── fanwall/
│   │   │   │       └── FanWallFragment.kt   ← Fan comments
│   │   │   └── adapter/
│   │   │       ├── CastAdapter.kt           ← Horizontal cast cards
│   │   │       ├── SupportCastAdapter.kt    ← Vertical support list
│   │   │       ├── SeatAdapter.kt           ← Grid with headers
│   │   │       └── FanCommentAdapter.kt     ← Comment list
│   │   ├── res/
│   │   │   ├── layout/                      ← All XML layouts
│   │   │   ├── drawable/                    ← Vector icons + shape BGs
│   │   │   ├── values/
│   │   │   │   ├── colors.xml
│   │   │   │   ├── strings.xml
│   │   │   │   ├── themes.xml
│   │   │   │   └── font_certs.xml
│   │   │   ├── navigation/nav_graph.xml
│   │   │   ├── menu/bottom_nav_menu.xml
│   │   │   ├── font/playfair.xml
│   │   │   └── color/nav_selector.xml
│   │   └── AndroidManifest.xml
│   ├── build.gradle
│   └── proguard-rules.pro
├── build.gradle
├── settings.gradle
├── gradle.properties
└── local.properties
```

---

## ⚙️ Setup Instructions (Step-by-Step)

### Step 1 — Prerequisites
- Android Studio **Hedgehog (2023.1.1)** or newer
- JDK 17 (bundled with Android Studio)
- Android SDK API 34
- Emulator or physical device with Android 7.0+ (API 24+)

### Step 2 — Open in Android Studio
1. Open **Android Studio**
2. Click **"Open"** (not "New Project")
3. Navigate to the `NammaMela/` folder and click **OK**
4. Wait for **Gradle sync** to complete (~2–3 minutes first time)

### Step 3 — Fix local.properties
Open `local.properties` and set your SDK path:
- **Mac:** `sdk.dir=/Users/YOUR_NAME/Library/Android/sdk`
- **Windows:** `sdk.dir=C\:\\Users\\YOUR_NAME\\AppData\\Local\\Android\\Sdk`
- **Linux:** `sdk.dir=/home/YOUR_NAME/Android/Sdk`

### Step 4 — Add mipmap icons (launcher icons)
Android Studio needs launcher icons. Quick fix:
1. Right-click `app/src/main/res` → **New → Image Asset**
2. Set **Icon Type** to "Launcher Icons"
3. Choose any icon, click **Next → Finish**

### Step 5 — Run the App
1. Select your emulator/device in the toolbar
2. Click the **▶ Run** button (Shift+F10)
3. App will launch with pre-seeded data (play, cast, seats, comments)

---

## 🎯 Features

| Feature | Status | Details |
|---|---|---|
| Tonight's Play Poster | ✅ | Title, time, duration, acts, venue, Glide poster |
| Manager Update Screen | ✅ | Edit all play details, persisted to Room DB |
| Cast Display | ✅ | Lead/Comedian/Singer cards + supporting cast list |
| Seat Map | ✅ | Grid layout, VIP/Front/Mid/Back sections |
| Live Seat Updates | ✅ | Tap to select, confirm booking updates Room DB |
| Seat Stats | ✅ | Live count: Total / Available / Booked |
| Fan Wall | ✅ | Post comments, clap for others, timestamps |
| Room DB Persistence | ✅ | All data survives app restart |
| Glide Image Loading | ✅ | Poster + cast photos with placeholder |

---

## 🏗️ Architecture

```
UI Layer (Fragments/Activities)
        ↕  LiveData / StateFlow
ViewModel Layer (MainViewModel)
        ↕  suspend functions
Repository Layer (NammaMelaRepository)
        ↕  DAO calls
Room Database (NammaMelaDatabase)
        ↕  SQLite
Local Storage
```

**Pattern:** MVVM + Repository + Room  
**Reactive:** LiveData for all DB-backed lists  
**Concurrency:** Kotlin Coroutines (viewModelScope)

---

## 🎨 Design Language

- **Primary:** Deep crimson `#8B0000` — curtain red
- **Accent:** Gold `#C9941A` / `#F0C040` — stage spotlight
- **Background:** Near-black `#0E0500` — dark stage
- **Font:** Playfair Display (serif, theatrical) via Google Fonts

---

## 🔧 Common Issues & Fixes

**Gradle sync fails:**
→ File → Invalidate Caches → Restart

**Font not loading:**
→ Needs internet on first run (downloadable font). Falls back to sans-serif offline.

**Images not loading:**
→ Make sure `INTERNET` permission is in Manifest (already added). Check emulator network.

**Room crash on first install:**
→ Uninstall app from device, reinstall fresh. Seed data runs on first DB creation only.

---

## 📦 Dependencies Used

| Library | Purpose |
|---|---|
| Room 2.6.1 | Local SQLite database |
| ViewModel + LiveData | MVVM architecture |
| Navigation Component | Fragment routing + bottom nav |
| Glide 4.16 | Poster + cast photo loading |
| Kotlin Coroutines | Async DB operations |
| Material Components | UI components (Cards, Buttons, TextInput) |
| RecyclerView | Seat grid + cast lists |

---

## 👨‍💻 Student Success Criteria Checklist

- [x] Seat Map updates when a seat is Reserved (Room DB + LiveData)
- [x] Tonight's Play is easily updatable by the manager (ManagerUpdateActivity)
- [x] UI is theatrical and bold (crimson + gold + Playfair Display font)

---

*Namma-Mela — Bringing Digital Management to Traditional Drama 🎭*
