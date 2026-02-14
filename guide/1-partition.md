# Partitioning your device

## Prerequisites
- Unlocked bootloader

- Latest stock ROM (recommended)

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
> Download the **modified recovery image**. If there are multiple files available, select the one for your Android version / ROM.
>
> Replace `path\to\modified-recovery.img` with the actual path to the modified recovery image.
```cmd
fastboot boot path\to\modified-recovery.img
```

> [!Note]
> If fastboot commands are not working (e.g **< waiting for device >** is displayed on the screen), you may need to install / update your USB drivers using [these instructions](troubleshooting.md#device-is-not-recognized-in-fastboot-or-recovery).
>
> Use the same steps again if **adb** commands in recovery fail.

### Backing up your boot image
> This will back up your boot image into the currently selected **platform-tools** directory.
```cmd
adb pull /dev/block/by-name/boot boot.img
```

### Backing up other important partitions
> This will back up **fsc**, **fsg**, **modemst1** and **modemst2** into the currently selected **platform-tools** directory.
> 
> Keep these backups in a safe place. If your device's software ever gets destroyed, you might need these backups or your phone could lose cellular capabilities.
>
> If you've got anything else you want to back up, do this now. Your Android data will be erased in the next steps.
```cmd
cmd /c "for %i in (fsg,fsc,modemst1,modemst2) do (adb shell dd if=/dev/block/by-name/%i of=/tmp/%i.bin & adb pull /tmp/%i.bin)"
```

### Notes
> [!Warning]
> In the next few steps your data will be formatted. If you have any important data, back it up now.
>
> DO NOT REBOOT YOUR PHONE if you think you made a mistake. Instead, ask for help in the [Telegram chat](https://t.me/project_aloha_issues).
> 
> Do not run all commands at once, execute them in order and wait for any lengthy operations to finish before continuing.

### Resizing the partition table
> By default, the partition limit for Android is too low. This command will increase it to 64 partitions.
>
> You will likely be told that you may need to reboot your device, ignore this advice and continue.
```cmd
adb shell sgdisk --resize-table 64 /dev/block/sda
```

### Opening a shell
```cmd
adb shell
```

### Opening parted
```cmd
parted /dev/block/sda
```

### Printing the current partition table
> This will display a list of partitions on your device. 
```cmd
print
``` 

> [!Note]
> Note to M2K, this whole list is unfinished (I know it looks bad)

> This list may be complicated to understand, so here is a short example showcasing the **userdata** partition.

Number  Start   End     Size    File system  Name

31      8811MB  512GB   503GB   ext4         userdata

> The first number, in this case **31** is the partition number.
>
> The second number, in this case **8811MB**, is the start value of this partition.
>
> The third number, in this case **512GB**, is the end value of the partition. It is worth nothing that the end value of a partition should always be identical to the start value of the **next** partition, as to not create unnecessary gaps.
> 
> The fourth number, in this case **503GB**, is the size of the partition. This value can also be obtained by subtracting the **start value** from the **end value**.
>
> The fifth field displays the file system of this partition. It is often left blank, usually due to parted not being able to recognize it.
>
> The sixth field displays the name of the partition, which should be self explanatory.

### Removing userdata
> Replace **$** with the number of the **userdata** partition, which should be the last partition in the list.
> 
- > Delete below line if not LG
> 
> If there is a partition named **grow** after **userdata**, remove it as well.
```cmd
rm $
```
> If there is an error (like pictured below) asking you if you want to continue, type `yes`.
![Are you sure you want to continue?](https://raw.githubusercontent.com/n00b69/woa-template/refs/heads/main/guide/images/parted-usedpartition.png)

> If there are any `udevadm` errors (like pictured below), ignore them.
> 
![udevadm](https://raw.githubusercontent.com/n00b69/woa-template/refs/heads/main/guide/images/parted-udevadm.png)

### Recreating userdata
- > IF VAYU:, 11.7GB / 70GB / =58.3GB

- > IF NABU: 10.9GB / 70GB / =59.1GB

- > IF CEPHEUS & RAPHAEL; 2080MB / 60GB / =58GB

- > IF HOTDOG & GUACAMOLE; 7971MB / 64GB / =56GB

- > IF SDM845 XIAOMI; 1611MB / 50GB / =48.4GB

- > IF G8/G8S/G8X/V50; 19.3GB / 70GB / =50.7GB

- > IF V50S; 19.3GB / 128GB / =108.7GB

> Replace **19.3GB** with the former start value of **userdata** which we just deleted. This value differs per device model, so make sure you grab the actual value from the partition list.

> Replace **70GB** with the end value you want **userdata** to have. In this example your available usable space in Android will be 70GB-19.3GB = **50.7GB**.
```cmd
mkpart userdata ext4 19.3GB 70GB
```
> If there is an error (like pictured below) complaining about the partition not being properly aligned, type `ignore` to continue.
![Not properly aligned.](https://raw.githubusercontent.com/n00b69/woa-template/refs/heads/main/guide/images/parted-aligned.png)

### Creating the ESP partition
> Replace **70GB** with the actual end value of **userdata**.
>
> Replace **70.3GB** with the same value, adding **0.3GB** to it.
```cmd
mkpart esp fat32 70GB 70.3GB
``` 

### Creating the Windows partition
> Replace **70.3GB** with the end value of **esp**
>
> The **-0MB** value will result in the Windows partition automatically filling up the rest of your storage. There is no need to change this value.
```cmd
mkpart win ntfs 70.3GB -0MB
``` 

### Making ESP bootable
> Use `print` to see all partitions again. Replace **$** with the actual number of the **ESP partition**.
```cmd
set $ esp on
``` 

### Exit parted
```cmd
quit
``` 

### Formatting data
- Format all data in recovery, or Android will likely not boot.
- ( Go to Wipe > Format data > type yes ) 
- If this does not work, boot into fastboot using `adb reboot bootloader` and format your data using the `fastboot -w` command.

### Check if Android starts
- Restart the phone, and see if Android still works.

### Formatting Windows and ESP partitions
> Boot back into the modified recovery, then run the below command.
```cmd
adb shell format
```

### Fixing the GPT
> If you do not do this, Windows may break your device.
```cmd
adb shell fixgpt
```

> [!Note]
>
> If your device is not yet rooted, it is advised to do so now (and to create a new **boot.img backup** afterwards).

## [Next step: Installing Windows](/guide/2-install.md)















