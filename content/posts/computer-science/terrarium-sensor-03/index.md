---
title: '用樹莓派打造環境監測器[03]：程式讀取感測器讀數、通知功能'
date: 2023-12-11T16:45:10+08:00
summary: '以 Node JS 讀取溫濕度感測器、螢幕輸出、手機通知'
draft: true
categories: ['Computer Science']
tags: ['Raspberry Pi']
series: ['Terrarium Sensor']
series_order: 3
isCJKLanguage: true
---

## terrarium sensor 03

[Big-Endian 與 Little-Endian 的差異與判斷程式碼](https://blog.gtwang.org/programming/difference-between-big-endian-and-little-endian-implementation-in-c/)

## I2C

- [ref0](https://www.best-microcontroller-projects.com/i2c-tutorial.html)
- [ref1](https://www.semiee.com/file/EOL2/ROHM-BH1750FVI.pdf)
- [ref2](https://ithelp.ithome.com.tw/articles/10269863)
- [ref3](https://www.analog.com/cn/design-center/landing-pages/002/tech-articles-taiwan/i2c-communication-protocol-understanding-i2c-primer-pmbus-and-smbus.html)

## 上拉 & 下拉電阻 (Pull-up & Pull-down resistor)

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

## 從 AM2302 取得溫濕度紀錄

## 從 GY30 取得光度紀錄

## 控制 LCD display

## 做時間對溫濕度的圖

## 發通知到手機

## 參考資料

- [智慧感測與應用實務| 10: 繼電器、雲端智能家電、手機遙控智慧開關](https://medium.com/eric-y-%E8%96%AA%E7%81%AB%E7%9B%B8%E5%82%B3/%E6%99%BA%E6%85%A7%E6%84%9F%E6%B8%AC%E8%88%87%E6%87%89%E7%94%A8%E5%AF%A6%E5%8B%99-10-%E7%B9%BC%E9%9B%BB%E5%99%A8-%E9%9B%B2%E7%AB%AF%E6%99%BA%E8%83%BD%E5%AE%B6%E9%9B%BB-%E6%89%8B%E6%A9%9F%E9%81%99%E6%8E%A7%E6%99%BA%E6%85%A7%E9%96%8B%E9%97%9C-c66fba868089)
