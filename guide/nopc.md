# Installing Windows without a PC

## Prerequisites
- Unlocked bootloader & root access

- Device must be running Android 12 or newer

- [Termux](https://play.google.com/store/apps/details?id=com.termux)

- [WOA Helper app](https://github.com/n00b69/woa-helper/releases/tag/APK)

- [Modified pe.img](https://github.com/)

- [Windows on ARM image](https://arkt-7.github.io/woawin/)

- [Drivers & UEFI](https://github.com/)

> [!Caution]
> This method is only recommended as a last resort option if you do not have access to a PC, or if your device is having issues in the regular method, such as being unable to boot into the modified recovery or mass storage mode not working.
> 
> It is very important that you read the steps very carefully. If you make any mistakes you can brick your device, which can possibly only be solved using a PC.

### Backing up important partitions
- Download and install the **WOA Helper** app, then open it and grant it root access.
- Click on **BACK UP BOOT.IMG** and select **ANDROID**.
- Navigate to the `WOAHelper/backups` folder in your internal storage and copy its contents to a USB stick or an SD card (or upload it somewhere online).

### Setting up Termux
- Download Termux if you haven't already.
- In Termux, run the following commands:
> If there are any Y/N prompts, type Y
```cmd
pkg upgrade
```
```cmd
pkg install root-repo
```
```cmd
pkg install parted
```
```cmd
pkg install gptfdisk
```
> After running the below command, accept the root access popup if you haven't already done so earlier.
```cmd
su
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
/data/data/com.termux/files/usr/bin/sgdisk --resize-table 64 /dev/block/sda
```

### Preparing for partitioning
> [!Note]
> If at any moment in parted you see an error prompting you to type "Yes/No" or "Ignore/Cancel", type `Yes` or `Ignore` depending on the situation to ignore the errors and continue.
>
> If you see any **udevadm** errors, you can ignore these as well.
```cmd
/data/data/com.termux/files/usr/bin/parted /dev/block/sda
```

#### Printing the current partition table
> Parted will print the list of partitions, userdata should be the last partition in the list
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
![Are you sure you want to continue?](https://raw.githubusercontent.com/n00b69/woa-template/refs/heads/main/guide/images/termux-usedpartition.png)

> If there are any `udevadm` errors (like pictured below), ignore them.
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

> To ensure Android is stable, it is recommended to allocate at least **8GB** to userdata.
```cmd
mkpart userdata ext4 19.3GB 70GB
```
> If there is an error (like pictured below) complaining about the partition not being properly aligned, type `ignore` to continue.
![Not properly aligned.](https://raw.githubusercontent.com/n00b69/woa-template/refs/heads/main/guide/images/termux-aligned.png)

### Creating the ESP partition
> Replace **70GB** with the actual end value of **userdata**.
>
> Replace **70.35GB** with the same value, adding **0.35GB** to it.
```cmd
mkpart esp fat32 70GB 70.35GB
``` 

### Creating the Windows partition
> Replace **70.35GB** with the end value of **esp**
>
> The **-0MB** value will result in the Windows partition automatically filling up the rest of your storage. There is no need to change this value.
```cmd
mkpart win ntfs 70.35GB -0MB
``` 

### Making ESP bootable
> Use `print` to see all partitions again. Replace **$** with the actual number of the **ESP partition**.
```cmd
set $ esp on
``` 

### Verifying the partitions
> Use `print` to see all partitions again.
- Verify that the **userdata** partition is at least **8GB**.
- Verify that the **esp** partition is at least **349MB** and has the **boot & esp** flags.
- Verify that the **win** partition is at least **25GB**.

> [!Important]
> If there are any issues, remove the partitions again and try again.

> In the below example, all three partitions are correct.
![correct partitions](https://raw.githubusercontent.com/n00b69/woa-template/refs/heads/main/guide/images/termux-correctpartitions.png)

> If you continue without ensuring that the partitions are correct, you may likely brick your device!

### Exit parted
```cmd
quit
```

### Fixing the GPT
> If you do not do this, Windows may break your device
- Run the below command to open gdisk in **sda** (later this command will be reused to open **sdb**, **sdc** etc.).
```cmd
/data/data/com.termux/files/usr/bin/gdisk /dev/block/sda
```
- Run the below commands (each letter is an individual command).
```cmd
x
```
```cmd
j
```
```cmd
enter (do not actually write enter)
```
```cmd
k
```
```cmd
enter (do not actually write enter)
```
```cmd
w
```
```cmd
y
```
- Repeat this process for sdb, sdc, sdd, sde, sdf, sdg etc. until it throws an error that the disk does not exist.

### Perform a factory data reset
> [!Note]
> I need to verify if this works
- Go into your Android settings and perform a factory data reset. The location of this setting varies per device and ROM, but the option should generally appear if you search for **factory** in the settings app.

### Set up your device
- Reboot your device and set it up again.
- If it faces a bootloop, boot into (stock) recovery to perform a factory data reset again.

### Setting up Termux (again)
- Download Termux if you haven't already.
- In Termux, run the following commands:
> If there are any Y/N prompts, type Y
```cmd
pkg upgrade
```
```cmd
pkg install root-repo
```
```cmd
pkg install ntfs-3g
```
```cmd
pkg install dosfstools
```
```cmd
pkg install wimlib-imagex
```
> After running the below command, accept the root access popup if you haven't already done so earlier.
```cmd
su
```

### Formatting the Windows and ESP partitions
```cmd
/data/data/com.termux/files/usr/bin/mkfs.ntfs -f /dev/block/by-name/win -L Windows
``` 
```cmd
/data/data/com.termux/files/usr/bin/mkfs.fat -F32 -s1 /dev/block/by-name/esp -n ESP
``` 

### Finding the correct Windows index
- Download the Windows **.esd** (or **.wim**) file if you haven't already, and leave it in the **Download** folder of your internal storage
- Run the below command, making sure to replace `XXXX.esd` with the actual name of the **.esd** (or **.wim**) file. Example: **26200.6899.251011-1532.25h2_ge_release_svc_refresh_CLIENTCONSUMER_RET_A64FRE_en-us.esd**
```cmd
/data/data/com.termux/files/usr/bin/wimlib-imagex info /sdcard/Download/XXXX.esd
```
- Look for the **index** number of your desired Windows edition. **Windows 11 Pro** is recommended.

> In the example below, **Windows 11 Pro** has **index number 6**.
![wimlib index](https://raw.githubusercontent.com/n00b69/woa-template/refs/heads/main/guide/images/wimlib-index.png)

### Installing Windows
> Replace `XXXX.esd` with the actual name of the **.esd** file.

> Replace `6` with the actual **index** number of the desired Windows edition.
```cmd
/data/data/com.termux/files/usr/bin/wimlib-imagex apply /sdcard/Download/XXX.esd 6 /dev/block/by-name/win
```

### Flashing pe.img
- Download **pe.img** and leave it in the **Download** folder of your internal storage, then run the below command.
```cmd
dd if=/sdcard/Download/pe.img of=/dev/block/by-name/esp
``` 

### Mounting Windows
- Download and install the **WOA Helper** app, then open it and grant it root access.
- In **WOA Helper**, click on **MOUNT WINDOWS**.
- Verify that Windows has been mounted by trying to access its files in the **Windows** folder in your **internal storage** (or alternatively at **/mnt/Windows**).

> [!Important]
> If Windows could not be mounted (both folders are empty) and/or a "mount failed" popup appears in **WOA Helper**, you may need to change your ROM and/or root method.
>
> Only official **Magisk v28.1+** and **KSU** are supported. Forks such as Magisk Alpha and KSU-Next are not.
>
> At this point of the process you can safely change your ROM, if needed.


### Copying drivers into Windows
- Download the Windows drivers if you haven't already.
- Create a folder in the mounted **Windows** folder named `Drivers`.
- Unzip the drivers into the newly created **Drivers** folder.

### Flashing the UEFI image
- In **WOA Helper**, open the **WOA TOOLBOX** menu and use the **STA CREATOR** option.
- Download the **UEFI image** and place it inside the folder named `UEFI` in your internal storage.
- Press the **QUICKBOOT TO WINDOWS** button in WOA Helper.

### Reboot your device
- After rebooting your device, the installation will continue automatically.

#### HHHH.















