# RTS Business Manager

> A simple, offline Android app to track **inventory**, **customer payments**, and **supplier advances** in one place, with every amount in Indian Rupees (₹).

![Platform](https://img.shields.io/badge/platform-Android-3DDC84?logo=android&logoColor=white)
![Built with](https://img.shields.io/badge/built%20with-Capacitor-119EFF?logo=capacitor&logoColor=white)
![Offline](https://img.shields.io/badge/works-offline-success)
![Currency](https://img.shields.io/badge/currency-INR%20(%E2%82%B9)-orange)
![License](https://img.shields.io/badge/license-All%20Rights%20Reserved-red)

---

## Table of Contents

- [About](#about)
- [Features](#features)
- [Screens](#screens)
- [How It Works](#how-it-works)
- [Data, Privacy and Backup](#data-privacy-and-backup)
- [Install the APK](#install-the-apk)
- [Build From Source](#build-from-source)
- [Project Structure](#project-structure)
- [Tech Stack](#tech-stack)
- [Roadmap](#roadmap)
- [FAQ](#faq)
- [License](#license)
- [Author](#author)

---

## About

**RTS Business Manager** is built for small traders and shop owners who deal in physical materials and want to replace the paper register with something quick and phone-friendly.

It answers three everyday questions:

1. **What stock do I have, and what is it worth?** (Inventory)
2. **Who still owes me money?** (Payments)
3. **How much have I paid suppliers in advance, and what is still pending to arrive?** (Advance)

There is no sign-up, no server, and no internet requirement. Open the app, enter your name once, and start recording.

---

## Features

### Inventory
- Add materials with **name, size, units, price per unit and date**
- Choose from common preset sizes (for example 40×45, 50×60, 72×80) or type a **custom size**
- Live **total inventory value** at the top of the screen
- Edit or remove items, with a confirmation prompt before deleting
- Stock changes are logged automatically (stock in, stock out, edits, removals)

### Payments (money to receive from buyers)
- Record **buyer name, units bought, size, rate per unit and date**
- Total is calculated automatically (units × rate)
- Record **partial payments** as they arrive; the balance updates instantly
- **PENDING / COMPLETED** status on every entry
- Optionally link a sale to an inventory item so **stock reduces automatically**, with a check that blocks selling more than you have
- Header shows the total **pending amount** across all open payments

### Advance (money paid to suppliers)
- Record **supplier, size, quantity ordered, advance paid and date**
- Mark material as received in parts, with status **WAITING → PARTIAL → FULLY RECEIVED**
- When material arrives, choose to **add it to inventory automatically**
- Header shows the value of advance still tied up in pending material

### Across the whole app
- **Search** by name or material on any tab
- **History** view for each tab: a timestamped log of every change, plus completed entries
- **Light, dark and auto theme**
- **Adjustable text size** with the − and + buttons
- Modern frosted-glass interface designed for small phone screens
- Indian number formatting (for example ₹1,25,000)
- Input validation: no negative numbers, no overpaying a balance, no receiving more than ordered

---

## Screens

The app has three tabs along the top:

| Tab | What it tracks | Header summary |
|---|---|---|
| **INVENTORY** | Materials in stock | Total inventory value |
| **PAYMENTS** | Money buyers owe you | Total pending amount |
| **ADVANCE** | Advances paid to suppliers | Advance tied up in pending material |

Buttons on every screen:

- **+** (green, bottom right): add a new entry for the current tab
- **Clock icon** (bottom left): open the history log
- **Backup** (top): copy or restore all your data
- **Theme**: switch between auto, light and dark
- **Your business name** (top left): tap to change it

> Add screenshots here: create a `docs/screenshots/` folder and reference them, e.g. `![Inventory](docs/screenshots/inventory.png)`

---

## How It Works

A typical flow:

1. **Order material.** In *Advance*, log the supplier, quantity and advance you paid.
2. **Material arrives.** Tap *Material Received*, enter the quantity and choose *Add to inventory: Yes*. Stock is created or topped up for you.
3. **Make a sale.** In *Payments*, add the buyer, units and rate. Pick the inventory item in *Reduce stock of* so stock goes down automatically.
4. **Collect money.** Tap *Add Payment* each time the buyer pays. When the balance reaches zero the entry moves to **COMPLETED** and into History.

---

## Data, Privacy and Backup

- All data is stored **locally on your phone**. Nothing is uploaded and no account is needed.
- The app does not ask for contacts, location, camera or any other sensitive permission for its core features.
- Because data lives on the device, **uninstalling the app or clearing its storage deletes your records**.

### Backup and restore

1. Tap **Backup** at the top of the app.
2. Tap **Copy** and paste the text somewhere safe (WhatsApp "Message yourself", Notes, email).
3. To restore, open **Backup**, paste your saved text and tap **Restore**.

Make a backup regularly, and always before updating or reinstalling.

---

## Install the APK

> Requires **Android 6.0 or later** (this may vary with your build configuration).

1. Download `app-debug.apk` from the [Releases](../../releases) page.
2. Open the file on your phone.
3. If prompted, allow **Install unknown apps** for your browser or file manager.
4. Tap **Install**, then open the app and enter your name.

> **Note:** the file named `app-debug.apk` is a **debug build**, intended for testing and personal use. A signed **release build** (or an AAB) is needed for the Google Play Store.

---

## Build From Source

The app is a single-page web app wrapped as a native Android app with [Capacitor](https://capacitorjs.com/).

### Prerequisites

- [Node.js](https://nodejs.org/) 18 or newer
- [Android Studio](https://developer.android.com/studio) (includes the Android SDK and Gradle)
- JDK 17

### Steps

```bash
# 1. Clone the repository
git clone https://github.com/<your-username>/rts-business-manager.git
cd rts-business-manager

# 2. Install dependencies
npm install

# 3. Copy the web app into the Android project
npx cap sync android

# 4. Open in Android Studio and run on a device or emulator
npx cap open android
```

### Command-line debug build

```bash
cd android
./gradlew assembleDebug
# Output: android/app/build/outputs/apk/debug/app-debug.apk
```

### Release build (for distribution)

```bash
cd android
./gradlew bundleRelease     # AAB for Google Play
./gradlew assembleRelease   # signed APK for direct distribution
```

You must sign release builds with your own keystore. **Never commit your keystore or its passwords to GitHub.**

### Running in a browser (quick preview)

Because the UI is plain HTML, you can preview it without Android:

```bash
npx serve www
```

---

## Project Structure

```
rts-business-manager/
├── www/
│   └── index.html            # The whole app: UI, styles and logic
├── android/                  # Native Android project generated by Capacitor
├── capacitor.config.json     # App ID, app name and web directory
├── package.json
├── README.md
└── LICENSE
```

Key configuration (`capacitor.config.json`):

| Setting | Value |
|---|---|
| App name | `RTS` |
| App ID | `com.myfather.business` |
| Web directory | `www` |

---

## Tech Stack

- **HTML, CSS and vanilla JavaScript**, with no frameworks and no external libraries
- **Capacitor** to package the web app as an Android APK
- **localStorage** for on-device persistence
- CSS custom properties for light and dark theming

---

## Roadmap

Ideas for future versions:

- [ ] Export to Excel / PDF reports
- [ ] File-based backup (not just copy-paste text)
- [ ] Optional cloud sync across devices
- [ ] Multiple currencies and languages
- [ ] Low-stock alerts
- [ ] Printable invoices and payment receipts
- [ ] Charts for sales and pending amounts
- [ ] PIN or fingerprint lock

---

## FAQ

**Does it need internet?**
No. It works fully offline.

**Where is my data stored?**
Only on your phone. That is why regular backups matter.

**Can I use it on two phones at once?**
Not yet. Use Backup and Restore to move data between devices.

**Is there an iPhone version?**
Not currently. The code is Capacitor-based, so an iOS build is possible in the future.

**The app says "Invalid backup text". What now?**
Make sure you pasted the complete backup text with nothing added or cut off.

---

## License

**Copyright © 2026 Kartk. All rights reserved.**

This is proprietary software. You may not copy, modify, redistribute, or resell this code or the app without written permission from the author.

---

## Author

Made and developed by **Kartk**.

For purchase, support, or feature requests, please [open an issue](../../issues) or contact the author directly.
