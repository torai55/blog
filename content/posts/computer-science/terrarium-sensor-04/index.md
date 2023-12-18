---
title: '用樹莓派打造環境監測器[04]：遺珠之憾系列'
date: 2023-12-11T16:48:07+08:00
summary: '未來可擴充之功能及延伸閱讀'
draft: false
categories: ['Computer Science']
tags: ['Raspberry Pi']
series: ['Terrarium Sensor']
series_order: 4
isCJKLanguage: true
---

## 遺珠之憾

這裡記錄各種待消化的雜項資料。  
有些是未來可擴充功能、有些是延伸閱讀、有些是查完待歸類的資料。  

### 未來可擴充：手機控制

接上繼電器，透過 MQTT 使手機可遠端操控繼電器開關。

- [智慧感測與應用實務| 10: 繼電器、雲端智能家電、手機遙控智慧開關](https://medium.com/eric-y-%E8%96%AA%E7%81%AB%E7%9B%B8%E5%82%B3/%E6%99%BA%E6%85%A7%E6%84%9F%E6%B8%AC%E8%88%87%E6%87%89%E7%94%A8%E5%AF%A6%E5%8B%99-10-%E7%B9%BC%E9%9B%BB%E5%99%A8-%E9%9B%B2%E7%AB%AF%E6%99%BA%E8%83%BD%E5%AE%B6%E9%9B%BB-%E6%89%8B%E6%A9%9F%E9%81%99%E6%8E%A7%E6%99%BA%E6%85%A7%E9%96%8B%E9%97%9C-c66fba868089)

### 未來可擴充：發送通知到手機

監測到溫度之類的讀數異常時，直接使用 LINE Notify （或使用 IFTTT 之類的服務）送通知到手機。  

- [LINE Notify API doc](https://notify-bot.line.me/doc/en/)
- [IFTTT doc](https://ifttt.com/docs)

## 延伸閱讀：I2C

對 I2C protocol 有興趣的話可以看硬體的文件，說明硬體怎麼使用時會提到。  
或者直接上網查教學文也行。  

- [ref0](https://www.best-microcontroller-projects.com/i2c-tutorial.html)
- [BH1750 doc](https://www.mouser.com/datasheet/2/348/bh1750fvi-e-186247.pdf)
- [ref2](https://ithelp.ithome.com.tw/articles/10269863)
- [ref3](https://www.analog.com/cn/design-center/landing-pages/002/tech-articles-taiwan/i2c-communication-protocol-understanding-i2c-primer-pmbus-and-smbus.html)

## 待歸類：上拉 & 下拉電阻 (Pull-up & Pull-down resistor)

研究 I2C 的時候有提到不認識的名詞，查完之後不知道放哪。  

上拉電阻是把電阻接在電源，在電路斷開時輸入會是 High，電路閉合時拿到 Low；  
下拉電阻是把電阻接在接地，在電路斷開時輸入會是 Low，電路閉合時拿到 High。  

![open](./images/Pull-up&Pull-down%20resistor_open.png "電路斷開圖示，來源：[上拉電阻&下拉電阻 - GPIO新手入門必知【明富其識】](https://youtu.be/k_GAuSONCqo?t=68)")
![close](./images/Pull-up&Pull-down%20resistor_close.png "電路閉合圖示，來源：[上拉電阻&下拉電阻 - GPIO新手入門必知【明富其識】](https://youtu.be/k_GAuSONCqo?t=71)")

樹莓派有內建上拉 & 下拉電阻，可用下列範例程式碼控制：  

```python
# 下拉電阻
GPIO.setup(port_or_pin, GPIO.IN, pull_up_down=GPIO.PUD_DOWN)

# 上拉電阻
GPIO.setup(port_or_pin, GPIO.IN, pull_up_down=GPIO.PUD_UP)
```
