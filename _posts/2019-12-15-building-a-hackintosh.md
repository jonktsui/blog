---
title: "Building a Hackintosh"
date: 2019-12-15T15:34:30-04:00
categories:
  - tech
tags:
  - hackintosh
  - macos
---

## Introduction
So before I get into the details of my build, this is a fun project for myself to work on as a hobby. In no way shape or form do I sell this device to anyone.

There are many tools out there as well that "bundle" installation however, there are so many different configurations for your hardware that it is nearly impossible to have everything setup the exact same way. This is why I'd recommend following the [Clover Vanilla Guide][VanillaGuide] (if you're starting out for the first time) or the [OpenCore Vanilla Guide][OCGuide] (recommended after having a working Hackintosh with Clover).



## Hardware

Hackintosh's have very particular hardware requirements. The more that's deviated from mimic-ing a real Mac, the more issues you'd run into.

Couple places to look to see if your hardware is compatible with being a hackintosh. Read the [Hardware Guide FAQ][HWGuide] or if you prefer, this is what hardware to NOT get [Anti-Hackintosh Buyers Guide][Antibuyer]


### My Hackintosh Hardware

``https://ca.pcpartpicker.com/list/kHWx6R``

```
         [CPU][Intel Core i7-8700K 3.7 GHz 6-Core]
  [CPU Cooler][Noctua NH-L9i CPU Cooler]
 [Motherboard][Gigabyte Z370N WIFI Mini ITX LGA1151]
      [Memory][G.Skill TridentZ RGB 32 GB DDR4-3200]
     [Storage][Samsung 970 Evo 1 TB M.2 NVME SSD (Primary)]
     [Storage][Samsung 860 Evo 1 TB M.2 SSD (Secondary)]
  [Video Card][Sapphire Radeon RX 580 8 GB NITRO+]
        [Case][Fractal Design Node 304 Mini ITX]
[Power Supply][Corsair RMx 750 W 80+ Gold]
[WiFi Adapter][BCM94360CS2 A/E Key NGFF M.2 Adapter Card Module]
   [WiFi Card][Wireless-AC BCM94360CS2 WiFi Bluetooth Card for 13 MacBook Air]
```

### Issues encountered
#### Faulty Hardware
- When installing, I kept running into Kernel Panics. I spent about 2-3 weeks trying to figure out what the problem was with help from the [Discord channel][DiscordURL]. I thought it was a RAM or Motherboard issue, so I had replaced both. Still had same kernel panic error. I tried installing Ubuntu from the same USB which stil resulted in a Panic Error. I was ready to give up but as a last attempt, I tried to install Windows. I wasn't until I was also having issues installing Windows was when I realized it was not my Clover Configuration that was faulty, but rather the CPU was the issue. Long story short, replaced the CPU and Mojave 10.14.1 installed perfectly.
- ***TL;DR: If Installing MacOS on new hardware does not work, try installing Linux or Windows to rule out hardware issues.***

#### USB Drive
- You must use a ***USB 2.0*** port or a ***USB 2.0 drive***
- Must be ***8+ GB*** as you'd need to have MacOS on the drive

If you see it stuck at "Still waiting for root device", it is likely a USB 3 related issue

![USB3 Error](/blog/assets/images/2019-12-15-hackintosh-usb3error.jpg)

When formatting the USB, ensure you're not just formatting the Volume, but the entire drive.

![Format Drives](/blog/assets/images/2019-12-15-hackintosh-showalldevices.png)


## Helpful Links/Resources
### Links used to get started
- [Clover Vanilla Guide][VanillaGuide] written by [u/corpnewt][Corp]
- [GenSMBIOS][GenSMBIOS] - Corp's script to generate SMBIOS, serial #, etc.

### Used when I move to OpenCore
- [OpenCore Vanilla Guide][OCGuide] written by [u/dracoflar][HackSlav] based on Corp's Guide
- [ProperTree][ProperTree] - Corp's application to edit OpenCore config.plist with EXTREME ease
- [SSDTime][SSDTime] - Corp's Script to create SSDT's
- [USBMap][USBMap] - Corp's Script to create SSDT and Map the USB Ports (ensuring under the 15 port limit)

### Other
- CorpNewt has a ton of scripts in his [github page][CorpGithub]. Definitely take a look there for other useful scripts.
- The Reddit page ([r/hackintosh][reddithack]) as well as the Discord channel (link in Reddit page) has been very helpful.


[reddithack]: https://www.reddit.com/r/hackintosh/
[VanillaGuide]: https://hackintosh.gitbook.io/-r-hackintosh-vanilla-desktop-guide/
[DiscordURL]: https://discord.gg/u8V7N5C
[OCGuide]: https://khronokernel-2.gitbook.io/opencore-vanilla-desktop-guide/
[SSDTime]: https://github.com/corpnewt/SSDTTime
[GenSMBIOS]: https://github.com/corpnewt/GenSMBIOS
[ProperTree]: https://github.com/corpnewt/ProperTree
[Corp]: https://www.reddit.com/user/corpnewt/
[CorpGithub]: https://github.com/corpnewt?tab=repositories
[HackSlav]: https://www.reddit.com/user/dracoflar/
[USBMap]: https://github.com/corpnewt/USBMap
[WifiCards]: https://khronokernel-7.gitbook.io/wireless-buyers-guide/
[HWGuide]: https://www.reddit.com/r/hackintosh/wiki/faq#wiki_ok.21_i_fulfil_some_points.2C_what_now.3F
[Antibuyer]:https://github.com/khronokernel/Anti-Hackintosh-Buyers-Guide/blob/master/README.md
