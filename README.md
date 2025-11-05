# Birthday Android App

**Birthday-AndroidApp**

A simple Android application to store and remind birthdays. This repository contains the Android Studio project source code for the app.

---

## Table of Contents

* [Features](#features)
* [Prerequisites](#prerequisites)
* [Getting the code (clone)](#getting-the-code-clone)
* [Open and run (Android Studio)](#open-and-run-android-studio)
* [Run on emulator or device](#run-on-emulator-or-device)
* [Build APK (debug & release)](#build-apk-debug--release)
* [Generate signed APK / Release](#generate-signed-apk--release)
* [Troubleshooting](#troubleshooting)
* [Contributing](#contributing)
* [License](#license)
* [Contact](#contact)

---

## Features

* Add, edit, and delete birthday entries
* Store name, date, and optional notes
* View upcoming birthdays
* (Optional) Local notifications/reminders if implemented in the codebase

> Adjust this features list to match what your project actually implements.

## Prerequisites

* Android Studio (latest stable recommended)
* Java JDK (11 or 17 recommended depending on project configuration)
* Android SDK (installed via Android Studio)
* Gradle (bundled with project; no global install required)
* USB debugging enabled on a physical device if you plan to run on hardware

## Getting the code (clone)

```bash
# Clone the repo
git clone https://github.com/Thejas79/Birthday-AndroidApp.git
cd Birthday-AndroidApp
```

## Open and run (Android Studio)

1. Open Android Studio.
2. Choose **File → Open** and select the project's root folder (`Birthday-AndroidApp`).
3. Let Android Studio sync Gradle and download dependencies. (This may take a few minutes the first time.)
4. Once the project sync finishes, select a run target (emulator or connected device) from the toolbar.
5. Click the green **Run** ▶ button or use **Shift + F10** to install and run the app.

## Run on emulator or device

### Emulator

1. Open **AVD Manager** in Android Studio.
2. Create a virtual device with a recommended Android API level (match the project's `minSdkVersion` / `targetSdkVersion`).
3. Start the emulator and then run the app from Android Studio.

### Physical device

1. On your Android device, enable **Developer options** and **USB debugging**.
2. Connect the device via USB (or use ADB over Wi‑Fi if configured).
3. Choose the device as run target and click **Run**.

## Build APK (debug & release)

### Build debug APK (quick)

From Android Studio:

* **Build → Build Bundle(s) / APK(s) → Build APK(s)**.
* After build completes, click **Locate** in the notification to open the folder containing the debug APK. Usually: `app/build/outputs/apk/debug/app-debug.apk`.

Or from the command line (project root):

```bash
# Linux / macOS
./gradlew assembleDebug

# Windows (PowerShell / cmd)
gradlew assembleDebug
```

Debug APK path: `app/build/outputs/apk/debug/app-debug.apk`.

### Build release APK (unsigned)

```bash
./gradlew assembleRelease
```

Release APK path: `app/build/outputs/apk/release/app-release-unsigned.apk`.

> An unsigned release APK cannot be installed on devices. Sign it (see next section) before distributing.

## Generate signed APK / Release

To publish or share a release APK, generate a signed APK (or App Bundle):

### Using Android Studio (recommended)

1. **Build → Generate Signed Bundle / APK...**
2. Choose **APK** (or **Android App Bundle** if you plan to publish to Play Store).
3. Create or choose an existing **key store** and provide key alias, password, and key password.
4. Select build variant (`release`) and finish.
5. Android Studio will produce a signed APK/App Bundle and show the output location.

### Using the command line (with `keystore`)

```bash
# Example: sign the unsigned release APK with apksigner (Android SDK build-tools must be installed)
# 1. Build unsigned release
./gradlew assembleRelease

# 2. Sign using apksigner
$ANDROID_SDK_ROOT/build-tools/<version>/apksigner sign --ks my-release-key.jks --out app-release-signed.apk app/build/outputs/apk/release/app-release-unsigned.apk

# 3. Verify the signature
$ANDROID_SDK_ROOT/build-tools/<version>/apksigner verify app-release-signed.apk
```

Replace `<version>` with your installed build-tools version and `my-release-key.jks` with your keystore path.

**Important:** Keep your keystore and passwords safe. Losing the release keystore will prevent you from updating the app on Google Play.

## Troubleshooting

* **Gradle sync fails**: try `File → Sync Project with Gradle Files` or delete `.gradle` and `build` directories and rebuild.
* **SDK / Build tools missing**: open SDK Manager in Android Studio and install the required SDK platforms and build-tools.
* **Device not detected**: ensure USB debugging is enabled and proper USB drivers are installed (Windows). Run `adb devices` to confirm.
* **APK not installing**: on Android 8+ devices, enable **Install unknown apps** for the app installing source (e.g., file manager) or use `adb install -r path/to/app.apk`.

## Contributing

Contributions are welcome. Suggested workflow:

1. Fork the repository.
2. Create a feature branch: `git checkout -b feature/my-change`.
3. Make changes and test on emulator/device.
4. Commit and push: `git push origin feature/my-change`.
5. Open a Pull Request with a clear description of changes.

## License

Include a license file if you want to open-source this project (for example, MIT). If you don’t have one yet, you can add `LICENSE` at the repo root.

## Contact

If you need help or want to report bugs, open an issue in the repository.

---

*Notes*

* Tailor any paths, build commands, SDK versions, or feature descriptions to match your project configuration.
* If the app uses Room/SQLite, permissions, or broadcast receivers for alarms/reminders, list required permissions and brief setup steps here.
