# Project status

- Device: <insert device name here>
- Current **Driver** version: v2601.01
- Current **UEFI** version: v2601.10

# Simple status

| Feature                | Notes                                           | Status         |
|------------------------|-------------------------------------------------|----------------|
| 🔊 Audio               |                                                 | ✅            |
| 🔋 Battery             |                                                 | ✅            |
| 🎆 GPU                 |                                                 | ✅            |
| 👆 Touch               |                                                 | ✅            |
| 🪵 USB                 |                                                 | ✅            |
| 🖥 DisplayPort                 |  Works with certain adapters only             | ⚠️            |
| 🗺 DualScreen                 |                                                 | ❌            |
| 🔌 Charging              | Slow charging only                            | ✅            |
| 💾 SD card                 |                                                 | ✅            |
| 🔵 Bluetooth           |                                                 | ✅            |
| 🛜 Wi-Fi                |                                                 | ✅            |
| 📶 Cellular services       | SIM card must be in SIM1, calling does not work             | ✅            |
| ⌨️ Side buttons        |                                                 | ✅            |
| 🖊 Tablet accesoires        | Mostly working, with some limitations                       | ⚠️            |
| 🛡️ TPM                 | Doesn't support versions below Windows 11 22H2, or above Windows 11 24H2 26100.7171 | ✅            |
| 🛰️ GPS                 |                                                 | ✅            |
| 🧭 Sensors              |                                                 | ✅            |
| 📳 Vibration motor     |                                                 | ❌            |
| 🔦 Flashlight          | Accessible only from Windows camera app         | ⚠️            |
| 📸 Camera flash        |                                                 | ⚠️            |
| 📸 Camera              |                                                 | ❌            |


# Detailed status

## 🔊 Audio

| Feature                | Notes                                       | Status         |
|------------------------|---------------------------------------------|----------------|
| 🔉 Bottom speaker       |                                             | ✅            |
| 🔉 Top speaker(s)    |                                             | ✅            |
| 🎧 3.5mm headphone jack |                                             | ✅            |
| 🎙️ Internal top mic    |                                             | ✅            |
| 🎙️ Internal bottom mic |                                             | ✅            |


## 🎆 GPU

| Feature                | Notes                               | Status         |
|------------------------|-------------------------------------|----------------|
| 🔆 Brightness control  |  Brightness might not change properly until screen is turned off and back on        | ✅            |
| 🎆 x64 emulation      |  Only in Windows 11                          | ✅            |


## 🪵 USB & Charging

> [!Note]
> On **SM8150** devices, the device is incapable of switching the USB-mode in Windows, and a [USB Host Mode Switch tool](https://github.com/n00b69/usbhostmode) is required to do so

| Feature                         | Notes                                                            | Status         |
|---------------------------------|------------------------------------------------------------------|----------------|
| 🪵 USB-Fn (Charging & MTP)   | **[Default]**                                                     | ✅            |
| 🪵 USB-Host (OTG)              | Some of the features are work in progress (USB Powerless Dongles) | ⚠️            |
| 🔌 Charging (USB)             | Slow charging only, only in USB-Fn mode                           | ✅            |
| 🔌 Charging (Wireless)             | Slow charging only, only in USB-Fn mode                           | ✅            |
| 🖥 DisplayPort                 |  Works with certain adapters only, only in USB-Host mode             | ⚠️            |
| 🗺 DualScreen                 |                                                 | ❌            |


## 📶 Cellular services

| Feature                | Notes                               | Status         |
|------------------------|-------------------------------------|----------------|
| 📶 Cellular data (2G)   | SIM card must be in SIM1, unsupported in some regions      | ✅            |
| 📶 Cellular data (3G)   | SIM card must be in SIM1, unsupported in some regions      | ✅            |
| 📶 Cellular data (4G)   | SIM card must be in SIM1                    | ✅            |
| 📶 Cellular data (5G)   | SIM card must be in SIM1, unsupported on SM8150                    | ⚠️            |
| 📞 Cellular calls      |                                                 | ❌            |
| 💬 SMS                 | SIM card must be in SIM1                    | ✅            |


## ⌨️ Side buttons

| Feature                | Notes                                       | Status         |
|------------------------|---------------------------------------------|----------------|
| ⌨️ Volume up button       |                                                 | ✅            |
| ⌨️ Volume down button  |                                                 | ✅            |
| ⌨️ Power button               |                                                 | ✅            |
| ⌨️ Assistant button         |  LG                                             | ❌            |
| ⌨️ AI button                      |  Opens start menu / used for DBKP     | ✅            |
| ⌨️ Alert slider                   |  No functionality in Windows / used for DBKP            | ⚠️            |


## 🖊 Tablet accesoires

| Feature                | Notes                                       | Status         |
|------------------------|---------------------------------------------|----------------|
| 🖋 Xiaomi Pen       |                                             | ✅            |
| 🖋 Xiaomi Pen buttons   |                                             | ✅            |
| 🔌 Xiaomi Pen charging           |                                             | ❌            |
| 🖋 Third-party pens        | Only pens compatible with Wacom WGP digitizers will work properly        | ⚠️            |
| 🖋 Third-party pen buttons    | Only if Bluetooth             | ⚠️            |
| ⌨️ Xiaomi Keyboard        |                                             | ✅            |
| 💻 Smart Case Mode           | No clue what this is, I guess it is the automatic switching to the "tablet mode" taskbar when you detach the keyboard?      | ❌            |


## 🧭 Sensors

| Feature                | Notes                                       | Status         |
|------------------------|---------------------------------------------|----------------|
| 🧭 Accelerometer       |                                             | ✅            |
| 🧭 Gyroscope           |                                             | ✅            |
| 🧭 Light sensor        |                                             | ❌            |
| 🧭 Magnetometer        |                                             | ✅            |
| 🧭 Proximity           |                                             | ❌            |
| 🧬 Fingerprint scanner |                                                 | ❌            |
| 🏷️ NFC                 |                                                 | ❌            |
