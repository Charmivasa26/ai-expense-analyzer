# 📋 JobTracker – Flutter Job Application Tracker

A fully offline, mobile-first Flutter app to track your job applications. Built with Hive for local storage, Material 3 design, and zero backend dependencies.

---

## ✨ Features

- ➕ Add applications with company, role, date, status, and notes
- 📋 View all applications in a clean list with swipe-to-edit/delete
- ✏️ Edit and delete entries (swipe left on a card)
- 🔍 Search by company name, role, or notes
- 🎯 Filter by status (Applied / Interview / Offer / Rejected)
- 📊 Dashboard showing count per status
- 📤 Export all data as CSV
- 📥 Import from CSV
- 💾 100% offline — data stored locally with Hive
- 📱 Mobile-first Material Design 3 UI

---

## 🗂️ Project Structure

```
lib/
├── main.dart                    # App entry point
├── models/
│   ├── job_application.dart     # Hive data model
│   └── job_application.g.dart   # Generated Hive adapter
├── screens/
│   ├── home_screen.dart         # Main list + dashboard
│   ├── add_edit_screen.dart     # Add / Edit form
│   ├── detail_screen.dart       # Application detail view
│   └── settings_screen.dart     # Export / Import / About
├── services/
│   └── database_service.dart    # Hive CRUD + CSV logic
├── utils/
│   └── app_theme.dart           # Colors, typography, theme
└── widgets/
    ├── application_card.dart    # Swipeable list card
    ├── dashboard_header.dart    # Stats banner
    └── status_badge.dart        # Colored status chip
```

---

## 🛠️ Prerequisites

Install these before starting:

### 1. Flutter SDK
```bash
# Download Flutter from https://docs.flutter.dev/get-started/install
# Then verify:
flutter --version   # Should show Flutter 3.x
```

### 2. Java Development Kit (JDK 17)
```bash
# macOS (with Homebrew)
brew install openjdk@17

# Windows: Download from https://adoptium.net/

# Verify
java -version
```

### 3. Android Studio (for Android SDK)
- Download from https://developer.android.com/studio
- During install, include: Android SDK, Android SDK Platform-Tools
- After install: Open Android Studio → SDK Manager → Install Android 13 (API 33) or higher

### 4. Accept Android Licenses
```bash
flutter doctor --android-licenses
# Press 'y' to accept all
```

### 5. Verify Setup
```bash
flutter doctor
# All items should show ✓ (except iOS if you're on Windows/Linux — that's fine)
```

---

## 🚀 Step-by-Step: Run the App

### Step 1 – Clone / Copy the Project
```bash
# If you have the zip, extract it. Then:
cd job_tracker
```

### Step 2 – Install Dependencies
```bash
flutter pub get
```

### Step 3 – Connect a Device or Start Emulator

**Option A – Physical Android phone:**
1. Enable Developer Options on your phone:
   - Go to Settings → About Phone → tap "Build Number" 7 times
2. Enable USB Debugging in Developer Options
3. Connect phone via USB
4. Run: `flutter devices` — your phone should appear

**Option B – Android Emulator:**
1. Open Android Studio → Device Manager → Create Virtual Device
2. Pick a Pixel device → Select Android 13+ system image → Finish
3. Click the ▶ Play button to start it

### Step 4 – Run the App
```bash
flutter run
```

The app will build and launch on your connected device/emulator.

---

## 📦 Build a Release APK

### Step 1 – Build the APK
```bash
flutter build apk --release
```

### Step 2 – Find the APK
```
build/app/outputs/flutter-apk/app-release.apk
```

### Step 3 – Install on Your Phone
```bash
# Via ADB (USB connected)
adb install build/app/outputs/flutter-apk/app-release.apk

# Or manually: Copy the APK to your phone and open it
# (You may need to allow "Install from unknown sources" in Settings)
```

### Build a Smaller APK (split by ABI)
```bash
flutter build apk --split-per-abi --release
# Creates 3 smaller APKs optimized for different chip types
# Use app-arm64-v8a-release.apk for most modern phones
```

---

## 📱 How to Use the App

### Adding an Application
1. Tap the **"+ Add Application"** button (bottom right)
2. Fill in Company Name and Role (required)
3. Pick the date you applied
4. Select the current status
5. Add optional notes
6. Tap **"Add Application"**

### Editing / Deleting
- **Swipe left** on any card to reveal Edit and Delete buttons
- Or **tap a card** to open detail view → use the edit/delete icons in the top bar

### Filtering
- Use the filter chips below the dashboard to show only one status
- Tap the 🔍 search icon in the top bar to search by text

### Export Data
1. Go to **Settings** (gear icon, top right)
2. Tap **"Export to CSV"**
3. Share or save the file using the system share sheet

### Import Data
1. Go to **Settings** → **"Import from CSV"**
2. Select a CSV file with the format:
   ```
   Company,Role,Date Applied,Status,Notes
   Google,SWE Intern,2024-03-15,Interview,Referred by John
   ```

---

## 🎨 Status Types

| Status    | Emoji | Meaning                        |
|-----------|-------|-------------------------------|
| Applied   | 📤    | Application submitted          |
| Interview | 🗣️    | Interview scheduled/completed  |
| Offer     | 🎉    | Offer received                 |
| Rejected  | ❌    | Application rejected           |

---

## 🔧 Troubleshooting

### "flutter: command not found"
Add Flutter to your PATH:
```bash
export PATH="$PATH:/path/to/flutter/bin"
# Add this line to ~/.zshrc or ~/.bashrc
```

### Build fails with Gradle error
```bash
cd android
./gradlew clean
cd ..
flutter clean
flutter pub get
flutter run
```

### "No devices found"
```bash
flutter devices        # Lists connected devices
flutter emulators      # Lists available emulators
flutter emulators --launch <emulator_id>
```

### Hive adapter error
The `job_application.g.dart` file is pre-generated and included. If you ever modify the model, regenerate it:
```bash
flutter pub run build_runner build --delete-conflicting-outputs
```

---

## 📦 Dependencies Used

| Package              | Purpose                        |
|----------------------|-------------------------------|
| `hive`               | Local NoSQL database (offline) |
| `hive_flutter`       | Flutter integration for Hive   |
| `path_provider`      | File system paths              |
| `intl`               | Date formatting                |
| `share_plus`         | Native share sheet for export  |
| `file_picker`        | Pick CSV files for import      |
| `flutter_slidable`   | Swipe-to-action cards          |
| `animations`         | Page transition effects        |

---

## 🏗️ Building for Production

### Signed APK (for Play Store or distribution)
```bash
# 1. Create a keystore
keytool -genkey -v -keystore ~/upload-keystore.jks \
  -keyalg RSA -keysize 2048 -validity 10000 \
  -alias upload

# 2. Create android/key.properties:
storePassword=<your-store-password>
keyPassword=<your-key-password>
keyAlias=upload
storeFile=<path-to-keystore>/upload-keystore.jks

# 3. Build signed APK
flutter build apk --release
```

---

## 📄 License
MIT — Free to use and modify.
