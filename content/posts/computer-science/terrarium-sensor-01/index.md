---
title: '用樹莓派打造環境監測器[01]：樹莓派的硬體們'
date: 2023-12-11T16:32:32+08:00
summary: '硬體說明'
draft: false
categories: ['Computer Science']
tags: ['Raspberry Pi']
series: ['Terrarium Sensor']
series_order: 1
isCJKLanguage: true
---

## 前言

在瀏覽別人的植物部落格 [^1] 時，看見他用樹莓派監測溫濕度，並遠端控制燈光與風扇。  
突然興起念頭，想用樹莓派做一個溫度警報器，監測到環境高於某個溫度時發送通知到手機。  
平時也會把監測的數據記錄起來，做成圖表方便觀察季節變化。  
因緣際會拿到樹莓派和一些零件，既然東西都有了那就來玩玩看吧。  

在此之前沒有使用過樹莓派，有許多不懂的地方，只好從頭慢慢研究。  
個人沒有相關背景，因此用字遣詞可能和學界、產業有落差，所以此系列不是好的參考資料。  
寫這系列也只是想紀錄過程中學到的知識。  

接下來分別介紹會用到的硬體與其介面。  

## Raspberry Pi Zero W

樹莓派本體。  
Zero 系列是樹莓派的輕便版本，許多接孔 (connector) 需要轉接器 (adapter) 轉成標準尺寸才能使用。  
W 內建了 wifi 和藍芽，因此使用 wifi 透過 SSH 控制的無頭樹莓派  (headless Raspberry Pi)  [^2] 是個好選擇。  

### miniHDMI

為了節省空間使用了 miniHDMI。  
若需要接螢幕可能需要 miniHDMI 轉 HDMI 的轉接器。  

{{< processImage "images/miniHDMI.jpg" "350x" "來源：[Getting Started with the Raspberry Pi Zero Wireless](https://learn.sparkfun.com/tutorials/getting-started-with-the-raspberry-pi-zero-wireless/all)" >}}

### power

只能單純供電的接口。  
透過 microUSB 連接，電壓應在 5-5.25V 範圍內。  

{{< processImage "images/power.jpg" "350x" "來源：[Getting Started with the Raspberry Pi Zero Wireless](https://learn.sparkfun.com/tutorials/getting-started-with-the-raspberry-pi-zero-wireless/all)" >}}

### usb

只有這個孔能傳輸資料且供電。  
支援 OTG 功能 ([On-The-Go](https://en.wikipedia.org/wiki/USB_On-The-Go))，大致上是接口兩邊的裝置，都能作為主機（提供電力，能主動控制連結）或週邊裝置（消耗電力）。  

{{< processImage "images/usb.jpg" "350x" "來源：[Getting Started with the Raspberry Pi Zero Wireless](https://learn.sparkfun.com/tutorials/getting-started-with-the-raspberry-pi-zero-wireless/all)" >}}

### micro SD card slot

micro SD 卡就是插在這邊。  
SD 卡作為儲存設備，需要燒錄作業系統。  

{{< processImage "images/uSDcard.jpg" "350x" "來源：[Getting Started with the Raspberry Pi Zero Wireless](https://learn.sparkfun.com/tutorials/getting-started-with-the-raspberry-pi-zero-wireless/all)" >}}

### General-purpose input/output (GPIO)

樹莓派的重點，每個孔都有已經定義好的各種用途。  
透過這個介面可以實現讀取/提供資料、供電等與外接設備互動的功能。  

GPIO0 和 1 （Pin27 和 28）預留作別用，一般情況不要連接。  

{{< processImage "images/gpio.jpg" "350x" "來源：[Getting Started with the Raspberry Pi Zero Wireless](https://learn.sparkfun.com/tutorials/getting-started-with-the-raspberry-pi-zero-wireless/all)" >}}

#### 各接腳功能

{{< processImage "images/Pi2 GPIO.png" "500x"  "來源：[Raspberry Pi 筆記(2)：GPIO 接腳與 I2C 及 SPI 安裝](https://atceiling.blogspot.com/2014/01/raspberry-pigpio.html)" >}}

可在樹莓派 cli 中輸入 `$ pinout` 查詢接腳。  
另外在 [Raspberry Pi Pinout](https://pinout.xyz/) 也有大致說明各接腳的功能。  
sparkfun 也有比較 [I2C vs UART vs SPI](https://learn.sparkfun.com/tutorials/i2c/all)，對協定原理有興趣時也能看看。  

## GPIO Extension Board

將 GPIO pin 引出到麵包板，以避免頻繁插拔造成損壞。  

{{< processImage "images/Gpi1.jpg" "400x" "擴充板本體。來源：[sunfounder](http://wiki.sunfounder.cc/index.php?title=GPIO_40pin_Breakout_Expansion_Board)" >}}
{{< processImage "images/Gpi2.jpg" "400x" "擴充板接上麵包板，並連接樹莓派。來源：[sunfounder](http://wiki.sunfounder.cc/index.php?title=GPIO_40pin_Breakout_Expansion_Board)" >}}

### 麵包板用法

{{< processImage "images/breadboard.webp" "450x" "來源：[麵包板怎麼用? 超簡單教學!](https://www.davidhuanglab.com/post/breadboard)" >}}

## AM2302(a.k.a. DHT22) humidity & temperature sensor/module

用來感測溫濕度。  

販售的有分成四個 pin 的感測器 (sensor) 還有三個 pin 的模組 (module)。  
如圖，四個 pin 由左到右是電源、訊號、沒用、接地。  
三個 pin 的話則是電源、訊號、接地。  

{{< processImage "images/dht22.png" "450x" "來源：[sparkfun](https://www.sparkfun.com/datasheets/Sensors/Temperature/DHT22.pdf)" >}}

### 其他規格

![dht22 spec](./images/dht22_spec.png "來源：[sparkfun](https://www.sparkfun.com/datasheets/Sensors/Temperature/DHT22.pdf)")

## GY30(a.k.a. BH1750FVI) light intensity sensor (待補)

I2C 介面的光度感測器。

### 感測器外觀

{{< processImage "images/GY-30_1.jpg" "400x" "來源：[sunfounder](http://wiki.sunfounder.cc/index.php?title=GY-30_Digital_Light_Intensity_Measuring_Module)" >}}

### pin

{{< processImage "images/GY-30_2.png" "400x" "來源：[sunfounder](http://wiki.sunfounder.cc/index.php?title=GY-30_Digital_Light_Intensity_Measuring_Module)" >}}

## LCD display 2004A 20x4 with I2C (待補)

- [ref1](https://www.youtube.com/watch?app=desktop&v=fR5XhHYzUK0)
- [ref2](https://circuitdigest.com/microcontroller-projects/interfacing-lcd-with-raspberry-pi-4-to-create-custom-character-and-scrolling-text)
- [ref3](https://phppot.com/web/guide-to-setup-raspberry-pi-with-lcd-display-using-i2c-backpack/)

## 設備連接圖 (待補)

使用 fritzing 來畫。  

## 參考資料

- [Getting Started with the Raspberry Pi Zero Wireless](https://learn.sparkfun.com/tutorials/getting-started-with-the-raspberry-pi-zero-wireless/all)
- [Raspberry Pi 筆記(2)：GPIO接腳與 I2C 及 SPI 安裝](https://atceiling.blogspot.com/2014/01/raspberry-pigpio.html)
- [Raspberry Pi Pinout](https://pinout.xyz/)
- [sparkfun I2C TUTORIALS](https://learn.sparkfun.com/tutorials/i2c/all)
- [麵包板怎麼用? 超簡單教學!](https://www.davidhuanglab.com/post/breadboard)
- [Digital-output relative humidity & temperature sensor/module DHT22 (DHT22 also named as AM2302)](https://www.sparkfun.com/datasheets/Sensors/Temperature/DHT22.pdf)
- [GY-30 Digital Light Intensity Measuring Module](http://wiki.sunfounder.cc/index.php?title=GY-30_Digital_Light_Intensity_Measuring_Module)

[^1]: [Tom's Carnivores](https://tomscarnivores.com/resources/raspberry-pi-terrarium-controller/)
[^2]: 無頭樹莓派：不用額外接螢幕、滑鼠、鍵盤的樹莓派
