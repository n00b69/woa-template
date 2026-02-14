# Project status

- Device: <insert device name here>

> [!Important]
> **This description is for reference only. It does not represent any commitment to develop Windows on this device in any way, nor does it mean that all functions will be available in the future or that development will continue indefinitely. You should not buy this device for the purpose of using Windows on it, and hope that it will have complete functions in the end. The functions available today should be considered as the most you can get. Take this into consideration when purchasing this device.**

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