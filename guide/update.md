# Updating drivers

### Method 1: OnlineUpdater
> [!Important]
> Unless specified in the driver release that a Windows reinstall is needed or that OfflineUpdater should be used to update the drivers, it is recommended to use **Method 1: OnlineUpdater**.

## Prerequisites 
- [Drivers & UEFI](https://github.com/)

### Boot into Windows
- Use the UEFI image that is already on your device to boot into Windows, trying to boot into Windows with the new UEFI image whilst older drivers are installed will not work.

### Updating the drivers
- Download and unpack the driver archive on your device while in Windows, then open the `OnlineUpdater.cmd` file.

- If there are any popups asking you for confirmation to install a driver, click on "Yes" or "Install anyway".

- If you see an error after installing **App Packages**, ignore it.

- Reboot your device manually after it says **Done!**.

### Updating the UEFI
- Download the latest UEFI image and replace the old UEFI image in your internal storage.

- If you are using Dualboot Kernel Patcher instead of WOA Helper's "Quickboot" option, you will have to re-patch your boot.img.

## Finished!


### Method 2: OfflineUpdater

## Prerequisites
- [Modified recovery](https://github.com/)

- [Drivers & UEFI](https://github.com/)

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

### Enabling mass storage mode
> If it asks you to run it once again, do so.
```cmd
adb shell msc
```

### Diskpart
```cmd
diskpart
```

### Listing all connected volumes
> This will list all connected drives/volumes. The Windows and ESP volumes of the phone should be listed at the bottom.
![diskpart lis vol](https://raw.githubusercontent.com/n00b69/woa-template/refs/heads/main/guide/images/diskpart-lisvol.png)
> If they aren't, please follow [these instructions](troubleshooting#device-does-not-show-up-in-diskpart)for an alternative way of entering mass storage mode.
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

### Exit diskpart
```diskpart
exit
```

### Reinstalling drivers
> [!Important]
> This process will take several hours. Ensure a stable connection between your device and your computer and make sure your computer does not go to sleep during the process.

- Unpack the driver archive, then open the `OfflineUpdater.cmd` file.

> If it asks you to enter a letter, enter the drive letter of **Windows** (which should be **X**), then press enter.
![offlineupdater](https://raw.githubusercontent.com/n00b69/woa-template/refs/heads/main/guide/images/offlineupdater.png)

### Reboot your device
```cmd
adb reboot
```

### Updating the UEFI
- Download the latest UEFI image and replace the old UEFI image in your internal storage.

- If you are using Dualboot Kernel Patcher instead of WOA Helper's "Quickboot" option, you will have to re-patch your boot.img.

## Finished!



