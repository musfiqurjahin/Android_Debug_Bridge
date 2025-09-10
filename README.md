Android Debug Bridge (ADB) - Command Reference
Overview
Android Debug Bridge (ADB) is a versatile command-line tool that lets you communicate with an Android device or emulator. It facilitates various device actions like installing and debugging apps, and it provides access to a Unix shell.

Installation
Windows
Download Android SDK Platform Tools from developer.android.com

Extract the ZIP file

Add the directory to your system PATH

macOS
bash
# Using Homebrew
brew install android-platform-tools

# Or download manually from Android website
Linux (Ubuntu/Debian)
bash
sudo apt-get install android-tools-adb android-tools-fastboot
Basic Setup
Enable USB debugging on your Android device:

Go to Settings > About phone

Tap "Build number" 7 times to enable Developer options

Go to Settings > Developer options

Enable "USB debugging"

Connect your device via USB cable

Verify connection:

bash
adb devices
If your device isn't showing up, you may need to install device-specific USB drivers.

Basic Commands
Device Management
bash
# List connected devices
adb devices

# List devices with details
adb devices -l

# Connect to a device over WiFi (requires USB initially)
adb tcpip 5555
adb connect <device-ip>:5555

# Disconnect from WiFi device
adb disconnect <device-ip>:5555

# Reconnect to USB
adb usb

# Get device state
adb get-state

# Wait for device to be in a specific state
adb wait-for-device
adb wait-for-recovery
adb wait-for-bootloader
App Management
bash
# Install an app
adb install path/to/app.apk

# Install with options
adb install -r path/to/app.apk  # Replace existing app
adb install -s path/to/app.apk  # Install on SD card
adb install -d path/to/app.apk  # Allow version code downgrade

# Uninstall an app
adb uninstall com.example.package

# Uninstall with keeping data/cache
adb uninstall -k com.example.package

# List all installed packages
adb shell pm list packages

# List third-party packages only
adb shell pm list packages -3

# Clear app data
adb shell pm clear com.example.package

# Grant/revoke permissions
adb shell pm grant com.example.package android.permission.CAMERA
adb shell pm revoke com.example.package android.permission.CAMERA

# Path to APK for package
adb shell pm path com.example.package
File Operations
bash
# Push file to device
adb push localfile /sdcard/remotefile

# Pull file from device
adb pull /sdcard/remotefile localfile

# Copy directory recursively
adb push localdir/ /sdcard/remotedir/
adb pull /sdcard/remotedir/ localdir/
System Operations
bash
# Reboot device
adb reboot

# Reboot to bootloader
adb reboot bootloader

# Reboot to recovery
adb reboot recovery

# Take screenshot
adb exec-out screencap -p > screenshot.png

# Record screen
adb shell screenrecord /sdcard/demo.mp4
# Stop with Ctrl+C

# Get device log (logcat)
adb logcat

# Filter logcat by tag
adb logcat -s TAG_NAME

# Clear logcat buffer
adb logcat -c

# Get bug report
adb bugreport
Shell Commands
bash
# Start interactive shell
adb shell

# Execute single command
adb shell <command>

# Examples:
adb shell ls /sdcard
adb shell ps
adb shell dumpsys battery
adb shell am start -n com.example.package/.MainActivity
adb shell input keyevent KEYCODE_HOME
adb shell input text "Hello World"
Advanced Commands
Backup and Restore
bash
# Backup apps and data
adb backup -f backup.ab -apk -shared -all

# Restore from backup
adb restore backup.ab
Port Forwarding
bash
# Forward host port to device port
adb forward tcp:6100 tcp:7100

# Remove forwarding
adb forward --remove tcp:6100

# List all forwardings
adb forward --list
Wireless Debugging
bash
# Set up wireless debugging (device connected via USB first)
adb tcpip 5555
adb connect <device-ip>:5555

# Disconnect USB after successful wireless connection
adb usb  # To switch back to USB mode
Power Management
bash
# Put device to sleep
adb shell input keyevent KEYCODE_SLEEP

# Wake up device
adb shell input keyevent KEYCODE_WAKEUP

# Turn screen on/off
adb shell input keyevent KEYCODE_POWER
Useful Tips
Multiple Devices: When multiple devices are connected, specify which device to target with the -s flag:

bash
adb -s <device-serial-number> <command>
Run as Root: Some commands require root access:

bash
adb root
adb remount  # Remount /system as read-write
Wireless Debugging: For wireless debugging without USB:

bash
adb pair <ip-address>:<port>
Logcat Filters: Useful logcat filters:

bash
adb logcat -v time  # Show timestamps
adb logcat *:E      # Show only errors
adb logcat -b radio # Show radio logs
Activity Manager: Control activities:

bash
adb shell am start -a android.intent.action.VIEW -d "http://example.com"
adb shell am force-stop com.example.package
Troubleshooting
Device not detected:

Check USB debugging is enabled

Try different USB cable/port

Install proper USB drivers

ADB server issues:

bash
adb kill-server
adb start-server
Permission denied:

Try running commands with root access: adb root

Check if app is debuggable
