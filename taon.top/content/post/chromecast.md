---
title: "Chromecast"
date: 2022-03-16T16:54:33+08:00
---
### **ChromeCast google TV 无法联网原因之一**

最近，因为手贱把chromecast google tv 版重置了以后，死活无法联网激活，用尽各种办法，什么全局科学\劫持DNS等等都不行,经过无数次的尝试，终于找到可能的原因：**wifi无线的加密方式** 包含wpa3的就会连接不上，改成**WPA+WPA2**混合就可以了。
