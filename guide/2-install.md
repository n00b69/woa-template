# Installing Windows

## Prerequisites
- [Modified recovery](https://github.com/)

- [Windows on ARM image](https://arkt-7.github.io/woawin/)

- [Drivers & UEFI](https://github.com/)

### Entering fastboot mode
> The method to enter fastboot mode may differ depending on the device, the most common methods are;
- Run `adb reboot bootloader` while booted into Android or a potentially already installed custom recovery.
- Hold the **volume down** while your device is powered off, then plug a USB cable into it.

### Boot into the modified recovery
> Replace `path\to\modified-recovery.img` with the actual path to the modified recovery image you have already used previously.
```cmd
fastboot boot path\to\modified-recovery.img
```

### Enabling mass storage mode
> If it asks you to run it once again, do so.
```cmd
adb shell msc
```

### Diskpart
> [!WARNING]
> Do NOT run any commands in diskpart other than the ones provided in this guide.
>
> Any modifications done to partitions while in diskpart can cause the entire UFS to be wiped.
>
> The only way of recovering from this state is to bring the device to a service center, or by flashing it in EDL (which may cost money).
```cmd
diskpart
```

### Listing all connected volumes
> This will list all connected drives/volumes. The Windows and ESP volumes of the phone should be listed at the bottom.
![diskpart lis vol](https://raw.githubusercontent.com/n00b69/woa-template/refs/heads/main/guide/images/diskpart-lisvol.png)

> If they aren't, please follow [these instructions](troubleshooting.md#mass-storage-mode-does-not-work)for an alternative way of entering mass storage mode.
```cmd
list volume
```

### Selecting the Windows volume of the phone
> Replace `$` with the actual number of **Windows**
```diskpart
select volume $
```

### Assign the letter X
```diskpart
assign letter x
```

### Selecting the ESP volume of the phone
> Replace `$` with the actual number of **ESP**
```diskpart
select volume $
```

### Assign the letter Y
```diskpart
assign letter y
```

### Exit diskpart
```diskpart
exit
```

### Installing Windows
> Replace `path\to\install.esd` with the actual path of install.esd (it may also be named install.wim or 26200.XXXX.XXXXXXX.esd)

```cmd
dism /apply-image /ImageFile:path\to\install.esd /index:6 /ApplyDir:X:\
```

> If you get `Error 87`, check the index of your image with `dism /get-imageinfo /ImageFile:path\to\install.esd`, then replace `index:6` with the actual index number of **Windows 11 Pro** in your image.
![dism getimageinfo](https://raw.githubusercontent.com/n00b69/woa-template/refs/heads/main/guide/images/dism-getimageinfo.png)

> If you get `Error 433`, `Error 21`, or `Error 5`, it likely means the device got disconnected or the partition is not properly formatted. Format your device's **Windows** volume in Windows explorer by right clicking it, then reapply the Windows image and make sure to not touch the cable or device until the installation finishes.
>
> If the issue persists, try using another USB port and / or cable.
![dism error](https://raw.githubusercontent.com/n00b69/woa-template/refs/heads/main/guide/images/dism-error.png)

### Installing drivers
> Before installing the drivers, ensure that Dism has completed the installation first.
- Unpack the driver archive, then open the `OfflineUpdater.cmd` file.

> If it asks you to enter a letter, enter the drive letter of **Windows** (which should be **X**), then press enter.
![offlineupdater](https://raw.githubusercontent.com/n00b69/woa-template/refs/heads/main/guide/images/offlineupdater.png)

### Create Windows bootloader files
> If any error shows up, such as "Failure when attempting to copy boot files", open `diskpart` again and assign any new letter to **ESP**, then replace the letter `Y` in the next command with the letter that you just added.
```cmd
bcdboot X:\Windows /s Y: /f UEFI
```

> Delete if secureboot device
### Enabling test signing
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" testsigning on
```

> Delete if secureboot device
### Disabling recovery
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" recoveryenabled no
```

> Delete if secureboot device
### Disabling integrity checks
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" nointegritychecks on
```

### Remove the drive letter of ESP
> If this does not work, ignore it and skip to the next command. This phantom drive will disappear the next time you reboot your PC.
```cmd
mountvol y: /d
```

### Reboot into fastboot mode
```cmd
adb reboot bootloader
```

### Boot into the UEFI
> Replace `path\to\uefi.img` with the actual path of the UEFI image
```cmd
fastboot boot path\to\uefi.img
```

### Reboot to Android
Your device should reboot by itself after +- 10 minutes of waiting, after which you will be booted into Android, for the last step.

> Delete below line if DBKP is not available
## [Last step: Setting up dualboot](dualboot-selection.md)

> Delete below line if it is a DBKP device
## [Last step: Setting up dualboot](3-dualboot.md)




















