# Preparing your device for partitioning

## Prerequisites
- Unlocked bootloader

- [Qfil](https://github.com/n00b69/woa-mh2lm/releases/tag/Qfil)

- [Engineering ABL](https://github.com/n00b69/woa-mh2lm/releases/download/Files/engabl_ab.bin)

### Setting up Qfil
- Open **Qfil**.
- In "Select Build Type", select **flat build**.
![qfil build type](https://raw.githubusercontent.com/n00b69/woa-template/refs/heads/main/guide/images/qfil-buildtype.png)
- In "Select programmer", select the downloaded firehose.
![qfil firehose](https://raw.githubusercontent.com/n00b69/woa-template/refs/heads/main/guide/images/qfil-firehose.png)
- In "Configuration" > "FireHose Configuration", make sure the "Device Type" is set to **UFS**.
![qfil options](https://raw.githubusercontent.com/n00b69/woa-template/refs/heads/main/guide/images/qfil-options.png)

### Boot into EDL
- Open **Device Manager** on your PC
- With the phone turned off, hold **volume down** + **power**.
- After the LG logo appears, while still holding **volume down** + **power**, start rapidly pressing the **volume up** button.
- Keep doing this until you hear a USB connection sound on your PC, or when **Qualcomm HS-USB QDLoader 9008** appears in the **Ports (COM & LPT)** category of Device Manager.
![device manager 9008](https://raw.githubusercontent.com/n00b69/woa-template/refs/heads/main/guide/images/devmgmt-9008.png)

> [!Note]
> If the device is called **QUSB_BULK_CID** or has a ⚠️ yellow warning triangle / question mark, and is located in any other category (for example **Other devices**), you need to install EDL drivers first.
![device manager yellow triangle](https://raw.githubusercontent.com/n00b69/woa-template/refs/heads/main/guide/images/devmgmt-yellowtriangle.png)

<details>
  <summary><strong>Click here for EDL driver installation instructions</strong></summary> 

### Installing EDL drivers
- Extract the contents of **QUD.zip** somewhere.
- Right click on **QUSB_BULK_CID** and click on **Update driver**.
![device update1](https://raw.githubusercontent.com/n00b69/woa-template/refs/heads/main/guide/images/devmgmt-update1.png)
- Click on**Browse my computer for drivers**, then find and select the **QUD** folder.
![device update2](https://raw.githubusercontent.com/n00b69/woa-template/refs/heads/main/guide/images/devmgmt-update2.png)
![device update3](https://raw.githubusercontent.com/n00b69/woa-template/refs/heads/main/guide/images/devmgmt-update3.png)
- The drivers should automatically start installing.
![device update4](https://raw.githubusercontent.com/n00b69/woa-template/refs/heads/main/guide/images/devmgmt-update4.png)

</details>

### Making sure Qfil works
- In **Qfil**, make sure the correct port is selected. If it says `Please Select an Existing Port`, click on "Select Port ..." and select the **Qualcomm HS-USB QDLoader 9008** port.
![qfil port](https://raw.githubusercontent.com/n00b69/woa-template/refs/heads/main/guide/images/qfil-selectport.png)
- At the top, select "Tools" > "Partition manager", and click **Ok**.
> [!Note]
> If you see a **Download Fail:Sahara Fail** or **Download Fail:FireHose Fail:FHLoader Fail:Process Fail** error, make sure your cable stays connected and reboot to EDL again by holding **volume down** + **power**, then start rapidly pressing the **volume up** button once the LG logo appears.
![qfil sahara error](https://raw.githubusercontent.com/n00b69/woa-template/refs/heads/main/guide/images/qfil-saharaerror.png)
- Once you're back in EDL, try opening the Partition manager again.
- If it still fails, try to repeat the last step a few times. You can also try rebooting your phone and PC.

### Backing up your partitions
- In the Partition manager, search for **abl_a**.
![qfil partitions](https://raw.githubusercontent.com/n00b69/woa-template/refs/heads/main/guide/images/qfil-partitions.png)
- Right click **abl_a**, select **Manage Partition Data** and then press **Read Data**.
![qfil readdata](https://raw.githubusercontent.com/n00b69/woa-template/refs/heads/main/guide/images/qfil-readdata.png)
- Do the same thing for **ftm**, **fsg**, **fsc**, **modemst1** and **modemst2**.

> [!Important]
> Navigate to `C:\Users\YOURNAME\AppData\Roaming\Qualcomm\QFIL\COMPORT_#\` and rename the backed up partitions one by one as you back them up. Qfil does not name the backups, and if you don't rename them, it'll be impossible to figure out which files are which. You can restore them later with the **Load Image** function, if needed.
![qfil partitionname](https://raw.githubusercontent.com/n00b69/woa-template/refs/heads/main/guide/images/qfil-partitionname.png)

### Flashing engineering ABL
- In **Qfil**, select Tools > Partition manager, and click **Ok**.
- Right click on **abl_a** > **Manage Partition Data** and press **Load Image**.
![qfil loadimage](https://raw.githubusercontent.com/n00b69/woa-template/refs/heads/main/guide/images/qfil-loadimage.png)
- Select and flash the **engabl_ab.bin** file.
- Do the same thing for **abl_b**.

### Reboot your device
- Reboot your phone by holding the **volume down** + **power** buttons for around 20 seconds until it shows the LG logo, then release the buttons.

## [Next step: Partitioning your device](1-partition.md)































