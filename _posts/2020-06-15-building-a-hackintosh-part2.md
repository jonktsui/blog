---
title: "HaxOS #2 OC 0.5.9 + i9-9900k + z390"
date: 2020-05-15T15:34:30-04:00
categories:
  - tech
tags:
  - hackintosh
  - macos
  - asus z390
  - i9-9900k
  - 0.5.9
  - opencore
---



## Introduction
Originally I wasn't planning on upgrading so soon, but one of my siblings became in need of a computer so I had decided to do an upgrade of a few parts. Check out my [previous build][Previous Build] for hardware specs and some basic troubleshooting.

Took me about 2 hours (with dinner in between) to follow the [Opencore Guide][OCGuide] to setup the USB and boot into MacOS. I didn't need to re-install MacOS since I used my existing drive and only had to update the config.plist and kexts.
Also found someone with the same motherboard and followed their [BIOS configuration][biosguide]

## Honourable mention
A _**HUGE**_ thank you to [CrytoTV][crytotvchannel] for helping with the entire build process! Check out the [build video link][livestreambuild] and also visit his channel for live streams of games, tech, and more!

![builditems](/blog/assets/images/2020-06-15-build-components.jpg)

![Night Pic](/blog/assets/images/2020-06-15-night-pic.jpg)

## Hardware

Currently setup on a testbench until the [case I am waiting for][thorzone] is available for purchase.
I did **NOT** replace my wireless card as I didn't purchase a card that would fit with the Asus casing. I do however have bluetooth working with the built in Intel Wireless 9560 card.

``https://ca.pcpartpicker.com/list/zJfWvW``

```
          [CPU] [Intel Core i9-9900K 3.6 GHz 8-Core Processor]
   [CPU Cooler] [Corsair H60 (2018) 57.2 CFM Liquid CPU Cooler]
  [Motherboard] [Asus ROG STRIX Z390-I GAMING Mini ITX LGA1151 Motherboard]
       [Memory] [G.Skill Ripjaws V 64 GB (2 x 32 GB) DDR4-3600 CL18 Memory]
      [Storage] [Samsung 970 Evo 1 TB M.2-2280 NVME Solid State Drive]
   [Video Card] [Sapphire Radeon RX 580 8 GB NITRO+ Video Card]
 [Power Supply] [Corsair SF 600 W 80+ Platinum Certified Fully Modular SFX Power Supply]
```
![neofetch](/blog/assets/images/2020-06-15-neofetch.jpeg)

#### What Works
- Sleep / Wake
- Bluetooth
- iServices
- Virtualization (Bluestacks/Docker)

#### What Does Not
- Airdrop
- Continuity


### Issue encountered
#### No en0 interface

My LAN interface ended up being a en6 interface and since I didn't replace my WiFi card, no working WiFi adapter which is typically en0 on MacOS.
Followed the [Fixing En0 guide][fixen0] and was back up and running upon the next reboot.

Major kudo's to [HackSlav][HackSlav] and the other contributors to writing up the documentation.



## Helpful Links/Resources
- [GenSMBIOS][GenSMBIOS] - Corp's script to generate SMBIOS, serial #, etc.
- [OpenCore Vanilla Guide][OCGuide] written by [u/dracoflar][HackSlav] based on Corp's Guide
- [ProperTree][ProperTree] - Corp's application to edit OpenCore config.plist with EXTREME ease
- [SSDTime][SSDTime] - Corp's Script to create SSDT's
- [USBMap][USBMap] - Corp's Script to create SSDT and Map the USB Ports (ensuring under the 15 port limit)
- The Reddit page ([r/hackintosh][reddithack]) as well as the Discord channel (link in Reddit page) has been very helpful.

# EFI

[EFI Here](https://github.com/jonktsui/hackintosh)

**Note:** my serial #'s have been removed

## Folder structure

```
/EFI/
├── APPLE
│   └── EXTENSIONS
│       └── Firmware.scap
├── BOOT
│   └── BOOTx64.efi
└── OC
    ├── ACPI
    │   ├── SSDT-AWAC.aml
    │   ├── SSDT-EC.aml
    │   ├── SSDT-PLUG.aml
    │   ├── SSDT-PMC.aml
    │   └── SSDT-USBX.aml
    ├── Bootstrap
    │   └── Bootstrap.efi
    ├── Drivers
    │   ├── AudioDxe.efi
    │   ├── CrScreenshotDxe.efi
    │   ├── HfsPlus.efi
    │   └── OpenRuntime.efi
    ├── Kexts
    │   ├── AppleALC.kext
    │   ├── IntelBluetoothFirmware.kext
    │   ├── IntelMausiEthernet.kext
    │   ├── Lilu.kext
    │   ├── NVMeFix.kext
    │   ├── SMCLightSensor.kext
    │   ├── SMCProcessor.kext
    │   ├── SMCSuperIO.kext
    │   ├── USBMap.kext
    │   ├── VirtualSMC.kext
    │   └── WhateverGreen.kext
    ├── OpenCore.efi
    ├── Resources
    │   ├── Audio
    │   ├── Font
    │   ├── Image
    │   └── Label
    ├── Tools
    │   └── OpenShell.efi
    └── config.plist
```


[Previous Build]: https://jonktsui.github.io/blog/tech/building-a-hackintosh/
[thorzone]: https://thor-zone.com/mini-itx/
[intelbtkext]: https://github.com/zxystd/IntelBluetoothFirmware
[biosguide]: https://github.com/czombos/asus-rog-strix-z390-i-gaming-hackintosh
[fixen0]: https://dortania.github.io/OpenCore-Desktop-Guide/post-install/iservices.html#fixing-en0
[livestreambuild]: https://www.youtube.com/watch?v=nOKSz_z9P5c
[crytotvchannel]: https://www.youtube.com/channel/UCbmBqmoQLUzn9OzgimMv9xA

[reddithack]: https://www.reddit.com/r/hackintosh/
[OCGuide]: https://dortania.github.io/OpenCore-Desktop-Guide/
[SSDTime]: https://github.com/corpnewt/SSDTTime
[GenSMBIOS]: https://github.com/corpnewt/GenSMBIOS
[ProperTree]: https://github.com/corpnewt/ProperTree
[Corp]: https://www.reddit.com/user/corpnewt/
[HackSlav]: https://www.reddit.com/user/dracoflar/
[USBMap]: https://github.com/corpnewt/USBMap
