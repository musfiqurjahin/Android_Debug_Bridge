# 📱 ADB & Fastboot Launcher Commands Cheat Sheet

This project is a simple **HTML reference file** containing useful ADB and Fastboot commands to manage Android launchers, remove bloatware, and debug performance.

---

## 🔧 Features
- 📋 Copy-to-clipboard button for every command
- 🚀 Launcher management commands (install, uninstall, set default)
- 🎮 Performance & FPS monitoring commands
- 📱 System info & debugging commands
- ⚡ Fastboot flashing basics
- 🛠 Quick restoration checklist if home screen goes blank

---

## 📂 File Included
- `adb_launcher_commands.html` → Open in any browser to use the cheat sheet with **copy buttons**.

---

## 🖥️ How to Use
1. Enable **Developer Options** on your phone.
2. Turn on **USB Debugging**.
3. Download [Android SDK Platform-Tools](https://developer.android.com/studio/releases/platform-tools).
4. Open a terminal/command prompt inside the platform-tools folder.
5. Connect your phone via USB and allow debugging.
6. Run commands from the cheat sheet.

---

## ⚠️ Warnings
- Do **not** uninstall your only launcher — always have at least one installed.
- Uninstalling system apps only removes them for your user (they can be restored).
- Fastboot/ROM flashing can brick your device if done incorrectly.

---

## 📝 Example Commands
```bash
adb devices   # check connection
adb shell pm list packages   # list installed packages
adb shell pm uninstall --user 0 com.package.name   # uninstall an app for current user
adb shell cmd package install-existing com.package.name   # restore removed system app
adb shell cmd package set-home-activity com.microsoft.launcher/.MainActivity   # set default launcher
```

---

## ✅ Quick Restore if No Launcher
If your home screen goes blank:
```bash
adb shell cmd package install-existing <launcher_package>
```
Or sideload a launcher APK:
```bash
adb install path/to/launcher.apk
```

---

