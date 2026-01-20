# Dualboot instructions

## Prerequisites
- [UEFI image](https://uefilink.com)

- [WOA Helper app](https://github.com/n00b69/woa-helper/releases/tag/APK)

This guide assumes you are rooted, if you aren't, please do so first.

### Setup - Android
- Download and install the **WOA Helper** app, then open it and grant it root access.
- In **WOA Helper**, open the **WOA TOOLBOX** menu and use the **STA CREATOR** option.
- Download the **UEFI image** and place it inside the folder named `UEFI` in your internal storage.
- Verify that the dualboot files have been copied correctly by navigating to the Windows folder in your internal storage and making sure that there is a folder called `sta`. In rare cases, Windows might also be mounted in **/mnt/Windows**. A root file explorer is needed to access this folder.

<details>
  <summary><strong>Click here if there is no Windows folder, the Windows folder is empty, there is no sta folder, or if a Mount failed popup appears</strong></summary>

> If there is no `/sdcard/Windows` or `/mnt/Windows` folder, they are empty, or there simply is no `sta` folder inside of them, your device does not (properly) support mounting and you will have to do some additional steps.
- Make a backup of your `boot.img` by clicking on **BACK UP BOOT.IMG** in **WOA Helper**. Select the **ANDROID** option.
- Copy the **boot.img** backup (located in your internal storage at `/sdcard/WOAHelper/Backups`) onto a USB stick or upload it to Google Drive or any other cloud space you can easily access later.
- Do the same thing for the `/sdcard/WOAHelper/sta` folder.
- Press the **QUICKBOOT TO WINDOWS** button in WOA Helper to boot into Windows.
- Once booted into Windows, copy the `sta` folder into the root of the **C drive** (`C:\sta`).
- Also copy the **boot.img** into the root of the **C drive** (`C:\boot.img`).
- Create a shortcut to `C:\sta\sta.exe` and copy it to your desktop.

</details>

- Press the **QUICKBOOT TO WINDOWS** button in WOA Helper.

### Setup - Windows
> [!Tip]
> If this is your first time booting Windows and you wish to skip the Microsoft Account login, press the **I don't have internet** button in the WiFi page, then when prompted, press the **Continue with limited setup** button.
>
> If there is no such button, press the **SIM card** button at the top of the screen (the one that says **Connected**), and press **Disconnect**.
- > Remove the above SIM card line if NABU

#### Booting to Android
- Run the new shortcut on your desktop (you can also pin it to your start menu / taskbar for ease of access).

#### Booting to Windows
- Press **QUICKBOOT TO WINDOWS** inside the WOA Helper app, or use the newly created toggle in your quick settings panel.

> [!Important]
> If you ever update or change your Android ROM, make sure to create a new **boot.img** backup (after rooting your phone!) and place it inside the **C:\ folder** in Windows, overwriting the old file.
>
> You can use the **BACK UP BOOT IMAGE** feature in the WOA Helper app to do so.

## Finished!
