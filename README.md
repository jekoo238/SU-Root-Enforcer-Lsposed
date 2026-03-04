# RootEnforcer

<img src="https://img.shields.io/badge/Contact-Telegram-blue?style=for-the-badge&logo=telegram" alt="Telegram">

**RootEnforcer** is a lightweight LSPosed module designed to force specific Android applications to trigger a Superuser (root) permission request upon launch.

Many system-level apps or custom utilities require root access to function correctly but lack the internal code logic to explicitly request it. This module resolves that issue by hooking into the application's lifecycle and executing a `su` command, thereby forcing the Magisk/KernelSU manager to display the permission prompt to the user.

## 🚀 Features

* **Forced Triggering:** Automatically executes the `su` command when the target application's `onCreate()` method is called.
* **Minimal Overhead:** Uses efficient LSPosed hooking, ensuring negligible impact on application performance.
* **Developer-Friendly:** Perfect for testing apps that require elevated privileges during development or debugging.
* **Seamless Integration:** Works transparently with existing root managers (Magisk, KernelSU, etc.).

## 📋 Requirements

* **Android Device** with root access.
* **LSPosed Framework** installed (with Zygisk enabled).
* **Root Manager:** Magisk or KernelSU.

## 🛠 Installation

1. **Download:** Get the latest `.apk` from the [Releases](https://github.com/jekoo238/SU-Root-Enforcer-Lsposed/releases/tag/V1.0) page.
2. **Install:** Install the APK on your Android device.
3. **Activate:**
    * Open the **LSPosed Manager** app.
    * Navigate to the **Modules** tab.
    * Select **RootEnforcer** and toggle the switch to enable it.
4. **Select Scope:**
    * Click on **RootEnforcer** to open its settings.
    * Check the boxes for the specific applications you want to force-request root.
5. **Reboot:** Reboot your device to apply the changes.

## ⚠️ Safety & Disclaimer

**Use this module with extreme caution.**

* **Security Risk:** Granting root access to applications that are not designed for it or that you do not trust can lead to system instability, data loss, or unauthorized access to sensitive device information.
* **No Warranty:** This software is provided "as-is" without any warranty. By using this module, you acknowledge that you are responsible for any issues that may arise on your device, including bootloops or system malfunctions.
* **Best Practice:** Only enable this module for applications you are developing or trusted system utilities. Never use this on third-party financial or banking apps.

## 💻 For Developers (Technical Details)

This module hooks into `android.app.Application#onCreate`. When the hooked application initializes, it executes:

```kotlin
Runtime.getRuntime().exec("su")
