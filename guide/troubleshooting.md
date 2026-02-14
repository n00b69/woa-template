# Troubleshooting Issues
> Below you will find a list of common problems and their solutions

## Device is not recognized in fastboot or recovery
> This likely means you don't have (proper) USB drivers installed.
- Open Device Manager and find an unknown device or device with errors that may be called **Android**, **ADB Interface**, or **QUSB_BULK**, likely with a ⚠️ yellow warning triangle / question mark.
- Download and extract the contents of **QUD.zip** somewhere.
- Right click on the device and click on **Update driver**. In this example the device is called **QUSB_BULK_CID**, but it may also be called **Android** or something similar.
![device update1](https://raw.githubusercontent.com/n00b69/woa-template/refs/heads/main/guide/images/devmgmt-update1.png)
- Click on **Browse my computer for drivers**, then find and select the **QUD** folder.
![device update2](https://raw.githubusercontent.com/n00b69/woa-template/refs/heads/main/guide/images/devmgmt-update2.png)
![device update3](https://raw.githubusercontent.com/n00b69/woa-template/refs/heads/main/guide/images/devmgmt-update3.png)
- The drivers should automatically start installing.
![device update4](https://raw.githubusercontent.com/n00b69/woa-template/refs/heads/main/guide/images/devmgmt-update4.png)

##### Finished!


## Mass storage mode does not work
> If mass storage mode in the modified recovery does not work, try the below method
- Reboot back into fastboot mode and download [**msc.img**](https://github.com/n00b69/woa-mh2lm/releases/download/Files/msc.img).
- Run the below command, replacing `path\to\msc.img` with the actual path of the image.
```cmd
fastboot boot path\to\msc.img
```
- Once booted into the image, select **UEFI Boot Menu** using your **volume buttons**.
- Select **USB Attached SCSI (UAS) Storage**.
- Press the **power** button twice to confirm.
- Proceed with the Diskpart steps now.

VVV delete this note if device is not LG
> [!Important]
> If mass storage with the above method still does not work, try the below method

## The device reboots in mass storage mode <--- delete this entire category if device is not LG
> This happens for some users, it is unknown why it happens, to bypass this, do the following:
- Reboot back into the modified TWRP and run `adb shell parted /dev/block/sda`, then run `print`.
- Run `set $ esp off` and `set $ msftdata on`, replacing **$** with the actual number of the esp partition (should be 31).
- Boot into fastboot mode using `adb reboot bootloader`, then download [**LGG8XMassStorageBoot.img**](https://github.com/n00b69/woa-mh2lm/releases/download/Files/LGG8XMassStorageBoot.img) and boot into it using `fastboot boot path\to\LGG8XMassStorageBoot.img`.
- After you finish the installation guide, before booting the Windows UEFI, return to TWRP, reopen **parted** and run `set $ esp on` and `set $ msftdata off`.

##### Finished!


## LTE and other network services in Android no longer work <--- delete this entire category if device is not SDM845
> Sometimes Windows may wipe your modem partitions, resulting in the loss of LTE in Android. To fix this, you'll need to restore your modem using the backups that you hopefully made [while partitioning your device](1-partition.md#backing-up-other-important-partitions). If you did not do this step, there is likely no way to recover.
- Boot into any recovery other than the stock recovery (ADB commands do not work there)
- Open CMD in the **platform-tools** folder.
- Restore the four partitions that you backed up using the below commands. Replace `path\to` with the actual path of the images.
```cmd
adb shell dd if=path\to\fsc.bin of=/dev/block/by-name/fsc
```

```cmd
adb shell dd if=path\to\fsg.bin of=/dev/block/by-name/fsg
```

```cmd
adb shell dd if=path\to\modemst1.bin of=/dev/block/by-name/modemst1
```

```cmd
adb shell dd if=path\to\modemst2.bin of=/dev/block/by-name/modemst2
```
- Reboot your device and check if LTE works.
> [!Note]
> If it still does not work, you will have to do some additional steps;
- Download the [stock rom for your device](https://xmfirmwareupdater.com/miui/polaris/)
- Open it, look for a file called **modem.img** and extract it.
- Boot into fastboot mode (`adb reboot bootloader`).
- Flash this **modem.img** with the below command, replacing `path\to\modem.img` with the actual path of the image
```cmd
fastboot flash modem path\to\modem.img
```

##### Finished!


## Cannot mount Windows in Android
If mounting Windows produces an empty folder, you either don't have Windows installed, or your ROM does not have mount support.

**Possible solutions:**
- Update your ROM. Generally, versions below Android 12 lack proper mount support.
- Update your root method; Only official **Magisk v28.1+** is supported.
• If your Magisk version is older, update it.
• If you are using KSU, try a different kernel.
• If you are using KSU Next, try regular KSU.
- Try enabling "Mount Windows to /mnt instead of /sdcard" in WOA Helper settings, if it isn't already enabled.
- Try setting SELinux to permissive mode using the `setenforce 0` commands. On some devices this may be needed.

##### Finished!


## Cannot write to Windows in Android
> This is caused by shutting down Windows instead of restarting it.
- To solve this, boot back into Windows and then use the **Switch to Android** app to switch back to Android.
- If you are using DBKP, instead press "Restart" in Windows, then as the device reboots, switch to Android using the designated DBKP button or medium.

##### Finished!


## USB does not work
- Enable USB host mode using the the [USB Host Mode Switch tool](https://github.com/n00b69/usbhostmode).
- If USB host mode is already enabled, disable and re-enable it.

##### Finished!


## The computer restarted unexpectedly or encountered an unexpected error
- If you stumble upon this error, you may need to redeploy the Windows image. Use the [reinstall guide](reinstall.md) for this.

##### Finished!




















