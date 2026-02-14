# Reinstalling Windows

## Prerequisites
- [Android Platform Tools](https://developer.android.com/studio/releases/platform-tools)

- [Modified recovery](https://github.com/)

### Opening CMD as an administrator
> Download **platform-tools** and extract the folder somewhere, then open CMD (command prompt, not PowerShell) as an **administrator**.
>
> Keep this window open and use it throughout the entire guide, do not close it.
> 
> Replace `path\to\platform-tools` with the actual path to the platform-tools folder, for example **C:\platform-tools**.
```cmd
cd path\to\platform-tools
```

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

### Formatting the Windows and ESP partitions
```cmd
adb shell format
```

## [Next step: Reinstalling Windows](/guide/2-install.md)
