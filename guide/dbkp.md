# Dualboot instructions (DualbootKernelPatcher)
> There are two methods listed below, the first one requires root, the second one does not. Use whichever method suits you the most, as they both do the same.

## Prerequisites (method 1: root required)
- [WOA Helper app](https://github.com/n00b69/woa-helper/releases/tag/APK)

### Setup - Android
- Download and install the **WOA Helper** app, then open it and grant it root access.
- Open **WOA Toolbox**, then press the **DUALBOOT KERNEL PATCHER** button.
- Wait for it to finish, then reboot your device.

#### Booting into Windows <--- delete whole category if nabu
- Press and hold the **assistant button** and reboot (or turn on) your device. <--- LG
- Press and hold the **AI button** and reboot (or turn on) your device. <--- Cepheus
- Move the **alert slider** into the top position and reboot (or turn on) your device. <--- hotdog/guacamole

#### Booting into Windows - Magnetic Case method <--- delete whole category if not nabu
- Close the **magnetic case** and reboot (or turn on) your device.

#### Booting into Windows - Volume button method <--- delete whole category if not nabu
- Reboot (or turn on) your device and hold any **volume button** once you see the unlock icon or the Aloha logo (**Λ**).

#### Booting into Android
- Reboot (or turn on) your device while not holding or pressing the **assistant button**. <--- LG
- Reboot (or turn on) your device while not holding or pressing the **AI button**. <--- cepheus
- Move the **alert slider** into the middle or bottom position and reboot (or turn on) your device. <--- hotdog/guacamole
- Open the **magnetic case** and reboot (or turn on) your device. <--- nabu
- If you are using the **volume button** method, simply do not press any volume button while (re)booting the device. <--- nabu

## Finished!


## Prerequisites (method 2: no root required)
- [Modified recovery](https://github.com/)

- [Magiskboot](https://github.com/erdilS/Port-Windows-11-Xiaomi-Pad-5/releases/download/1.0/magiskboot.exe)

- [DualBoot Kernel Patcher](https://github.com/erdilS/Port-Windows-11-Xiaomi-Pad-5/releases/download/1.0/DualBootKernelPatcher.zip)

- [devicename.fd file](https://github.com/n00b69/woa-everything/releases/download/Files/cepheus.fd)

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

```cmd
fastboot boot path\to\modified-recovery.img
```

### Backing up your boot image
> This will back up your boot image in the currently selected **platform-tools** directory.
```cmd
adb pull /dev/block/by-name/boot boot.img
```

### Setting up required files
> GUIDE EDIT REFERENCE: EDIT DEVICENAME.FD
- Download **magiskboot.exe** and move it into the `platform-tools` folder.
- Download **DualBootKernelPatcher.zip** and extract the **DualBootKernelPatcher** folder into the `platform-tools` folder.
- Download **devicename.fd** and move it into the `platform-tools` folder.

### Unpacking your boot image
> Make sure **boot.img** is in the `platform-tools` folder.
```cmd
magiskboot unpack boot.img
```

### Patching your boot image
> GUIDE EDIT REFERENCE: EDIT DEVICENAME.FD
```cmd
DualBootKernelPatcher\bin\Windows\DualBootKernelPatcher-x86_64.exe kernel devicename.fd output DualBootKernelPatcher\Config\DualBoot.Sm8150.cfg DualBootKernelPatcher\ShellCode\ShellCode.Cepheus.bin
```

### Renaming the kernel file
- Delete or rename the **kernel** file in the `platform-tools` folder, then rename the **output** file to `kernel`

### Repacking your boot image
> This will repack your patched boot image into a new file called **new_boot.img**
```cmd
magiskboot repack boot.img
```

### Reboot back into fastboot mode
```cmd
adb reboot bootloader
```

### Flashing the patched boot image
> Replace `path\to\new_boot.img` with the actual path of the image
```cmd
fastboot flash boot path\to\new_boot.img
```

### Reboot your device
```cmd
fastboot reboot
```

#### Booting into Windows <--- delete whole category if nabu
- Press and hold the **assistant button** and reboot (or turn on) your device. <--- LG
- Press and hold the **AI button** and reboot (or turn on) your device. <--- Cepheus
- Move the **alert slider** into the top position and reboot (or turn on) your device. <--- hotdog/guacamole

#### Booting into Windows - Magnetic Case method <--- delete whole category if not nabu
- Close the **magnetic case** and reboot (or turn on) your device.

#### Booting into Windows - Volume button method <--- delete whole category if not nabu
- Reboot (or turn on) your device and hold any **volume button** once you see the unlock icon or the Aloha logo (**Λ**).

#### Booting into Android
- Reboot (or turn on) your device while not holding or pressing the **assistant button**. <--- LG
- Reboot (or turn on) your device while not holding or pressing the **AI button**. <--- cepheus
- Move the **alert slider** into the middle or bottom position and reboot (or turn on) your device. <--- hotdog/guacamole
- Open the **magnetic case** and reboot (or turn on) your device. <--- nabu
- If you are using the **volume button** method, simply do not press any volume button while (re)booting the device. <--- nabu

## Finished!

















