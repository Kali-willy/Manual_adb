# Manual_adb
WARNINGS: - BACKUP your data before making system changes. - Some commands may not apply on all devices or OEM skins; incorrect use can cause UI instability. - Rooted commands MUST NOT be used on non-rooted devices. - Use at your own risk. Reboot required for many changes to take effect.

🛠️ 144Hz REFRESH RATE UNLOCK — ADB COMMAND PACK
Author: WillyGailo (template)
Purpose: Force device refresh rate settings to 144Hz via ADB (non-root & rooted options included).
WARNINGS:
- BACKUP your data before making system changes.
- Some commands may not apply on all devices or OEM skins; incorrect use can cause UI instability.
- Rooted commands MUST NOT be used on non-rooted devices.
- Use at your own risk. Reboot required for many changes to take effect.

──────────────────────────────────────────────────────────
SECTION 1 — Quick description (what these groups do)
──────────────────────────────────────────────────────────
1) Global / System / Secure settings
   - These 'settings put' entries write refresh-rate related keys to Android settings databases (global, system, secure).
   - They attempt to force min/max/peak/target refresh rates and toggle refresh-rate-related flags (showing refresh rate, switching mode, content detection, etc.)

2) Game-specific overrides
   - game_refresh_rate_force, game_overlay_refresh_rate and pkg lists attempt to force specific apps (e.g., PUBG, Mobile Legends, CoD) to use the requested refresh rate.

3) Root-only setprop
   - setprop persist.sys.refresh_rate and similar alter persistent system properties at low level — requires root (su).
   - Use these only if your device is rooted and you understand risks.

4) Reboots
   - ADB reboot is needed after changing many values for them to apply properly.

──────────────────────────────────────────────────────────
SECTION 2 — COPY-READY COMMAND BLOCKS
(Non-root usage — suitable for most devices)
──────────────────────────────────────────────────────────
adb shell settings put global user_refresh_rate 144
adb shell settings put global preferred_refresh_rate 144
adb shell settings put global refresh.active 1
adb shell settings put global refresh_rate_mode 3
adb shell settings put global refresh_rate_force_high 1
adb shell settings put global peak_refresh_rate 144
adb shell settings put global min_refresh_rate 144
adb shell settings put global max_refresh_rate 144
adb shell settings put global target_refresh_rate 144
adb shell settings put global sys.display.refresh_rate 144
adb shell settings put global refresh_rate_switching_type 1
adb shell settings put global settings_enable_monitor_physical_refresh_rate 1
adb shell settings put global show_refresh_rate 1
adb shell settings put global show_refresh_rate_switch 1
adb shell settings put global surface_flinger.use_content_detection_for_refresh_rate false

adb shell settings put global game_refresh_rate_force 1
adb shell settings put global game_overlay_refresh_rate 144
adb shell settings put global game_refresh_rate_pkgs "com.mobile.legends,com.tencent.ig,com.activision.callofduty.shooter"
adb shell settings put global game_refresh_rate_values "144,144,144"

adb shell settings put system display_refresh_rate 144
adb shell settings put system display_min_refresh_rate 144
adb shell settings put system hwui_refresh_rate 144
adb shell settings put system sf.refresh_rate 144
adb shell settings put system min_refresh_rate 144
adb shell settings put system min_refresh_rate_for_fps_boost 144
adb shell settings put system peak_refresh_rate 144
adb shell settings put system peak_refresh_rate_float 144
adb shell settings put system peak_refresh_rate_override 144
adb shell settings put system peak_refresh_rate_forced 144
adb shell settings put system thermal_limit_refresh_rate 144
adb shell settings put system max_refresh_rate 144
adb shell settings put system max_refresh_rate_for_fps_boost 144
adb shell settings put system max_refresh_rate_for_gaming 144
adb shell settings put system max_refresh_rate_for_ui 144
adb shell settings put system tran_refresh_mode 144
adb shell settings put system tran_need_recovery_refresh_mode 144
adb shell settings put system vendor.display.refresh_rate 144
adb shell settings put system vendor.display.enable_optimize_refresh 1
adb shell settings put system last_tran_refresh_mode_in_refresh_setting 144
adb shell settings put system display_min_refresh_rate 144

adb shell settings put secure refresh_rate 144
adb shell settings put secure refresh_rate_mode 144
adb shell settings put secure user_refresh_rate 144
adb shell settings put secure miui_refresh_rate 144
adb shell settings put secure oplus_customize_screen_refresh_rate 144
adb shell settings put secure peak_refresh_rate_forced 144

adb reboot

──────────────────────────────────────────────────────────
SECTION 3 — ROOTED ONLY (use only if device is rooted)
──────────────────────────────────────────────────────────
WARNING: Root required. Do NOT run on non-rooted device.

adb shell su -c "setprop persist.sys.refresh_rate 144"
adb shell su -c "setprop persist.sys.min_refresh_rate 144"
adb shell su -c "setprop persist.sys.max_refresh_rate 144"
adb shell su -c "setprop ro.surface_flinger.refresh_rate 144"
adb shell su -c "setprop vendor.display.refresh_rate 144"
adb shell su -c "setprop debug.hwui.refresh_rate 144"

adb reboot

──────────────────────────────────────────────────────────
SECTION 4 — HOW TO USE FROM A PC / LAPTOP (Windows, macOS, Linux)
──────────────────────────────────────────────────────────
A. PREP — on the PHONE
1. Enable Developer options: Settings → About phone → tap Build number 7 times (or OEM-specific).
2. In Developer options: enable "USB debugging" (ADB).
3. Optional but recommended: enable "Stay awake" only if you want phone to remain on while connected.

B. PREP — on the PC (choose your OS)

Windows:
1. Install ADB: download platform-tools from Google (or use a package manager like winget/choco). Extract folder.
2. Open Command Prompt in platform-tools folder: Shift + Right-click → "Open PowerShell window here" or navigate in cmd.
3. Connect phone via USB. If prompted on phone, accept "Allow USB debugging from this computer".

macOS / Linux:
1. Install ADB: mac: `brew install android-platform-tools` (if Homebrew). Linux: `sudo apt install android-tools-adb` or use platform-tools.
2. Open Terminal.
3. Connect phone via USB and accept debugging prompt on phone.

C. VERIFY CONNECTION
Run:
adb devices
- First run may show "unauthorized" → accept prompt on phone.
- When authorized, you’ll see a device id and "device".
If multiple devices show, specify: `adb -s <device-id> shell ...`

D. RUN THE COMMANDS
Option 1 — Manual paste (simplest)
- Paste each block (Global / System / Secure) into your terminal in sequence.
Option 2 — Single script (recommended)
- Create a script file on your PC:

Linux / macOS: save as `set_144hz.sh`:
#!/bin/sh
# Make sure phone is connected and authorized
adb wait-for-device
# paste all 'adb shell settings put ...' lines here (the non-root block)
adb reboot

Then: `chmod +x set_144hz.sh` and run `./set_144hz.sh`

Windows: save as `set_144hz.bat`:
@echo off
adb wait-for-device
REM paste all 'adb shell settings put ...' lines here
adb reboot
pause

- Run the script from the platform-tools folder or ensure adb is in PATH.

E. ROOTED SCRIPT (if rooted)
- Use the root-only setprop lines in the script but be VERY CAREFUL; require `adb shell su -c "..."` for each line.

F. TROUBLESHOOTING / NOTES
- If changes don't show: reboot the device (adb reboot). Some OEMs ignore certain keys — results vary by device & vendor ROM.
- If UI becomes unstable: reboot into safe mode / remove the values (use `settings delete <namespace> <key>`) or factory reset if necessary (extreme).
- To revert, you can set keys back to default or delete them:
  e.g., `adb shell settings delete global user_refresh_rate`
- If `adb devices` shows multiple entries (e.g., emulator + phone), use `adb -s <id>` to target.

──────────────────────────────────────────────────────────
SECTION 5 — SAFETY REMINDERS & BEST PRACTICES
──────────────────────────────────────────────────────────
- Always test one group of settings first (e.g., global display_* keys) before applying everything.
- Keep a record of original values (run `adb shell settings get <ns> <key>` before changing).
- Some keys are vendor/OEM controlled (Xiaomi, OnePlus, OPPO, Samsung) and may be ignored or overwritten by vendor services.
- Do not run root setprop commands on non-rooted devices.

──────────────────────────────────────────────────────────
SECTION 6 — SHORT EXAMPLE: RECORD ORIGINAL VALUES (recommended)
──────────────────────────────────────────────────────────
# Example: record existing value before overwrite
adb shell settings get global user_refresh_rate > orig_user_refresh_rate.txt
adb shell settings get system display_refresh_rate > orig_display_refresh_rate.txt

──────────────────────────────────────────────────────────
END OF TEXT GUIDE
──────────────────────────────────────────────────────────
