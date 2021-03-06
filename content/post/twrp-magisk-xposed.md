---
author: XhstormR
categories:
- Android
date: 2019-12-17T10:34:56+08:00
title: TWRP Magisk EdXposed
---

<!--more-->

Updated on 2019-12-17

>

## ADB
```bash
https://dl.google.com/android/repository/repository2-1.xml

curl -k https://dl.google.com/android/repository/platform-tools_r29.0.1-windows.zip | busybox unzip -
```

## Bootloader Driver
```bash
https://dl.google.com/android/repository/addon2-1.xml

curl -k https://dl.google.com/android/repository/usb_driver_r12-windows.zip | busybox unzip -
```

## TWRP
* Redmi 6: https://dl.twrp.me/cereus/
* OnePlus 5: https://dl.twrp.me/cheeseburger/

```bash
adb devices -l
adb reboot bootloader

fastboot devices -l
fastboot oem unlock
fastboot flash recovery twrp.img
fastboot reboot bootloader
```

## Magisk
* https://github.com/topjohnwu/Magisk/releases/latest

## EdXposed
* https://github.com/RikkaApps/Riru/releases/latest
* https://github.com/ElderDrivers/EdXposed/releases/latest
* https://github.com/ElderDrivers/EdXposedManager/releases/latest

```bash
adb push Magisk-v20.3.zip magisk-riru-core-v19.7.zip EdXposed-YAHFA-v0.4.6.1.4510.-release.zip /sdcard/Download/

adb install -r EdXposedManager-4.5.4-45401-org.meowcat.edxposed.manager-release.apk
```

## LSPosed
* https://github.com/RikkaApps/Riru/releases/latest
* https://github.com/LSPosed/LSPosed/releases/latest
