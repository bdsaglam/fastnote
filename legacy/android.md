# Android

## Uninstall APK
adb shell pm uninstall  com.mediate.supersense

## Clear all
adb shell pm clear com.mediate.supersense

## Revoke a permission
adb shell pm revoke com.mediate.supersense android.permission.RECORD_AUDIO

## Reset all permission
adb shell pm reset-permissions 

## Install release APK
find . -type f -name 'app-release.apk' -print0 | xargs -0 -I{} adb install -r {}
adb install ./app/release/app-release.apk

## Restart ADB
adb kill-server
adb start-server

## Change device locale
adb root
adb shell
setprop persist.sys.locale en-US;stop;sleep 5;start

