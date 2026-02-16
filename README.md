# Installing Kali NetHunter on OnePlus Nord (avicii)

This guide provides a comprehensive walkthrough for installing Kali NetHunter on a OnePlus Nord (codename: avicii), starting from a stock or bricked state. It covers restoring OxygenOS 10, upgrading to OxygenOS 11, unlocking the bootloader, flashing TWRP, installing a custom NetHunter kernel, rooting with Magisk, and finally installing the NetHunter image.

**Important:** This guide is specifically for the OnePlus Nord (avicii). Using files or following steps for other devices may brick your phone.

## Prerequisites

Before you begin, ensure you have the following:

*   **Windows Machine:** Required for the Qualcomm MSM Download Tool (MSM tool).
*   **ADB and Fastboot:** Installed on your computer.
    *   **Linux (Debian/Ubuntu):** `sudo apt install android-tools-adb android-tools-fastboot`
    *   **Linux (Arch):** `sudo pacman -S android-tools`
    *   **macOS (with Homebrew):** `brew install android-platform-tools`
    *   **Windows:** Download Android SDK Platform Tools from Google and extract.
*   **OnePlus Nord (avicii):** With Developer Options and USB Debugging enabled, and OEM Unlocking enabled.
*   **Downloaded Files:**
    *   **TWRP Image:** `twrp-3.7.1_12-0-avicii.img`
    *   **TWRP Installer Zip:** `twrp-installer-3.7.1_12-0-avicii.zip`
    *   **NetHunter Kernel Zip:** `kernel-nethunter-20260214_224826-oneplus-nord-oos-eleven.zip`
    *   **Magisk v27.0 APK:** From the official release page.
    *   **NetHunter Image Zip:** `nethunter-2024.2-oneplus_nord-eleven-kalifs-full.zip`
        *   **WARNING:** Do NOT use version 16 (2024.1/16.x) NetHunter image. It will brick your phone.

## Building the Kernel

This guide utilizes a pre-built custom NetHunter kernel specifically designed for the OnePlus Nord (avicii) running OxygenOS 11. The kernel file is provided as a flashable zip: `kernel-nethunter-20260214_224826-oneplus-nord-oos-eleven.zip`. There is no kernel compilation step required.

## Flashing

Follow these steps carefully to install Kali NetHunter:

### 1. Restore to OxygenOS 10 with MSM Tool

Use the Qualcomm MSM Download Tool on a Windows machine to restore your device to a clean OxygenOS 10 installation. Refer to "TheCustomDroid OnePlus Nord Unbrick Guide" for detailed instructions. After flashing, complete the initial Android setup without extensive configuration.

### 2. Update to OxygenOS 11

Navigate to `Settings > System > System Updates` on your phone and update to OxygenOS 11. This is crucial as the NetHunter kernel and image are built for OOS 11. Complete the setup after the update.

### 3. Enable Developer Options and USB Debugging

Go to `Settings > About Phone` and tap "Build Number" seven times. Then, in `Settings > System > Developer Options`, enable "USB Debugging" and "OEM Unlocking". Connect your phone to your computer and allow USB debugging.

### 4. Unlock the Bootloader

Execute the following commands in your terminal:

```bash
adb devices
adb reboot fastboot
fastboot oem unlock
```

On your phone, confirm the bootloader unlock using the volume keys and power button. This will wipe your device. Complete the Android setup again.

### 5. Boot into TWRP

From the directory containing your downloaded TWRP image, run:

```bash
adb reboot fastboot
fastboot boot twrp-3.7.1_12-0-avicii.img
```

Your phone should temporarily boot into TWRP recovery.

### 6. Permanently Install TWRP

Copy `twrp-installer-3.7.1_12-0-avicii.zip` to your device. In TWRP, tap `Install`, select the zip, and swipe to flash. Wipe Dalvik cache when prompted.

### 7. Flash the NetHunter Kernel

You have two options:

*   **Option A (Via TWRP):** Copy `kernel-nethunter-20260214_224826-oneplus-nord-oos-eleven.zip` to your device, then use TWRP's `Install` option to flash it.
*   **Option B (ADB Sideload):** In TWRP, go to `Advanced > ADB Sideload`. From your computer, run:
    ```bash
    adb sideload kernel-nethunter-20260214_224826-oneplus-nord-oos-eleven.zip
    ```

### 8. Install Magisk 27

Download the Magisk v27.0 APK. Rename the `.apk` file to `.zip` (e.g., `Magisk-v27.0.zip`). Sideload it through TWRP:

```bash
adb sideload Magisk-v27.0.zip
```

After installation, boot into OxygenOS. If the Magisk app isn't visible, install it manually: `adb install Magisk-v27.0.apk`. Verify Magisk shows "Installed: 27.0" and "Ramdisk: Yes".

### 9. Install NetHunter via Magisk

Copy the `nethunter-2024.2-oneplus_nord-eleven-kalifs-full.zip` to your device. Open the Magisk app, go to the `Modules` tab, tap "Install from storage", and select the NetHunter zip. Allow the installation to complete without interruption.

### Conclusion

After rebooting, you should have Kali NetHunter installed alongside OxygenOS. Open the NetHunter app and update it from the NetHunter Store. You now have a mobile penetration testing platform.

---
*Source: [roan.lol](https://roan.lol/content/2026/02-oneplus-nord-nethunter/oneplus-nord-nethunter)*
