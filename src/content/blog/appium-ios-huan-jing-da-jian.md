---
title: 'appium ios 环境搭建'
date: 2022-05-11 15:45:40
tags: []
published: true
hideInList: false
feature: 
isTop: false
categories: '自动化测试'
id: 'appium-ios-environment-setup'
---
## 安装xcode
可使用第三方下载工具安装`https://github.com/vineetchoudhary/Downloader-for-Apple-Developers`
```shell
curl -s https://xcdownloader.com/install.sh | bash
```
## 安装xcode command line tools
同上

## 安装brew
```shell
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

## 安装nvm
brew install nvm

## 安装node
nvm list-remove #查看版本
nvm install 

## 安装appium-doctor
npm install -g appium-doctor

## 检测依赖
appium-doctor --ios

```shell
appium-doctor --ios                                                                              22-05-11 - 9:37:48
info AppiumDoctor Appium Doctor v.1.16.0
info AppiumDoctor ### Diagnostic for necessary dependencies starting ###
info AppiumDoctor  ✔ The Node.js binary was found at: /Users/apple/.nvm/versions/node/v16.15.0/bin/node
info AppiumDoctor  ✔ Node version is 16.15.0
WARN AppiumDoctor  ✖ Error running xcrun simctl
info AppiumDoctor  ✔ Xcode Command Line Tools are installed in: /Applications/Xcode.app/Contents/Developer
info AppiumDoctor  ✔ DevToolsSecurity is enabled.
info AppiumDoctor  ✔ The Authorization DB is set up properly.
WARN AppiumDoctor  ✖ Carthage was NOT found!
info AppiumDoctor  ✔ HOME is set to: /Users/apple
info AppiumDoctor ### Diagnostic for necessary dependencies completed, 2 fixes needed. ###
```
## 根据检测结果安装相关依赖
brew install Carthage
npm i -g mjpeg-consumer
brew install lyft/formulae/set-simulator-location


## 安装Appium-Server-GUI
下载dmg
`https://github.com/appium/appium-desktop/releases/tag/v1.22.3`
运行报java错误解决
```shell
xattr -cr "/Applications/Appium Server GUI.app"

codesign --deep --sign - /Applications/Appium\ Server\ GUI.app
```
## appium中文文档
`http://appium.io/docs/cn/about-appium/intro/`

# 安卓环境

## 配置JAVA_HOME环境变量

```shell
export JAVA_HOME=$(/usr/libexec/java_home)
export PATH=$JAVA_HOME/bin:$PATH
export CLASS_PATH=$JAVA_HOME/lib
```

## 配置ANDROID_HOME环境变量

下载sdk http://tools.android-studio.org/index.php/sdk解压

```shell
# android_home
export ANDROID_HOME=/Volumes/D/android-sdk-macosx
export PATH=${PATH}:${ANDROID_HOME}/tools
# adb
export PATH="/Volumes/D/android-sdk-macosx/platform-tools:$PATH"

```

## 检测
```shell
appium-doctor --android
info AppiumDoctor Appium Doctor v.1.16.0
info AppiumDoctor ### Diagnostic for necessary dependencies starting ###
info AppiumDoctor  ✔ The Node.js binary was found at: /Users/apple/.nvm/versions/node/v16.15.0/bin/node
info AppiumDoctor  ✔ Node version is 16.15.0
info AppiumDoctor  ✔ ANDROID_HOME is set to: /Volumes/D/android-sdk-macosx
info AppiumDoctor  ✔ JAVA_HOME is set to: /Library/Java/JavaVirtualMachines/jdk-11.0.1.jdk/Contents/Home
info AppiumDoctor    Checking adb, android, emulator
info AppiumDoctor      'adb' is in /Volumes/D/android-sdk-macosx/platform-tools/adb
info AppiumDoctor      'android' is in /Volumes/D/android-sdk-macosx/tools/android
info AppiumDoctor      'emulator' is in /Volumes/D/android-sdk-macosx/tools/emulator
info AppiumDoctor  ✔ adb, android, emulator exist: /Volumes/D/android-sdk-macosx
info AppiumDoctor  ✔ 'bin' subfolder exists under '/Library/Java/JavaVirtualMachines/jdk-11.0.1.jdk/Contents/Home'
info AppiumDoctor ### Diagnostic for necessary dependencies completed, no fix needed. ###
```