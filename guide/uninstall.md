# Uninstalling Windows

## Prerequisites
- [Android Platform Tools](https://developer.android.com/studio/releases/platform-tools)

- [Modified recovery](https://github.com/) (recovery method)

- [gpt_both0.bin](https://github.com/hi_lol_lmao/releases/download/Files/gpt_both0.bin) (fastboot method)

## Recovery method

### Switch to Android
> Or your device will not boot into Android after uninstalling Windows
- Run the **Switch to Android** or **Android** shortcut on your desktop, or flash a **boot.img** backup in fastboot/recovery.

### Entering fastboot mode
> The method to enter fastboot mode may differ depending on the device, the most common methods are;
- Run `adb reboot bootloader` while booted into Android or a potentially already installed custom recovery.
- Hold the **volume down** while your device is powered off, then plug a USB cable into it.

### Boot into the modified recovery
- > Delete second part of the first line if only 1 recovery is present (e.g vayu)
- Download the **modified recovery image**. If there are multiple files available, select the one for your Android version / ROM.
> Replace `path\to\modified-recovery.img` with the actual path to the modified recovery image.

> [!Note]
> If there are any spaces in your path, put the path between quotation marks (or change the path altogether) like so: `fastboot boot "path with spaces\to\modified-recovery.img"`
>
> Remember this advice and use it later in the guide if necessary, as it will not be repeated.
```cmd
fastboot boot path\to\modified-recovery.img
```

### Execute the restore script
```cmd
adb shell restore
```

##### Finished!


## Fastboot method 
> In case the new one didn't work

### Switch to Android
> Or your device will not boot into Android after uninstalling Windows
- Run the **Switch to Android** or **Android** shortcut on your desktop, or flash a **boot.img** backup in fastboot/recovery.

### Entering fastboot mode
> The method to enter fastboot mode may differ depending on the device, the most common methods are;
- Run `adb reboot bootloader` while booted into Android or a potentially already installed custom recovery.
- Hold the **volume down** while your device is powered off, then plug a USB cable into it.

### Restore GPT
> Replace ```path\to\gpt_both0.bin``` with the actual path to the **gpt_both0.bin** file.
```cmd
fastboot flash partition:0 path\to\gpt_both0.bin
```

### Format userdata 
```cmd
fastboot -w
```

##### Finished!
