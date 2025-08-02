---
title: 'Install Kodi to the Fire TV'
date: 2022-03-14 13:47:24
tags: []
published: true
hideInList: false
feature: 
isTop: false
categories: '教程'
id: 'install-kodi-fire-tv'
---


## Install Kodi to the Fire TV

> Note: If your APK file name contains spaces, make sure you put quotes around it in the adb commands. On OS X and Linux, you may need to prepend ./ to the adb commands.

1. On your host (PC or other Android device), download your desired Kodi APK

2. Open a Command Prompt (Windows), Terminal (OS X/Linux), or Terminal Emulator app (Android)
3. Navigate (CD) to the directory with your Kodi APK (In Terminal Emulator on Android you only need to run the adb commands)
4. Run the following commands

```shell 
adb kill-server
adb start-server
adb connect <ip-address-of-fire-tv>
```



5. ADB is connected when it reports the message "connected to <ip-address-of-fire-tv>:<port>"

6. Run one of the following commands

   ```shell 
   adb install <apk-file-name>
   ```


   (or if you are upgrading from a previous Kodi install, use this instead)

   ```shelle 
   adb install -r <apk-file-name>
   ```

7. Installation is complete when it reports the message "success"

>  (Note: For Android you need to type in the full path. e.g. >adb install /sdcard/Download/apk-file-name.apk)


<!-- more -->


https://kodi.wiki/view/HOW-TO:Install_Kodi_on_Fire_TV


