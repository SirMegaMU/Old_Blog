---
layout: post
title: 使用树莓派操控OLED屏
date: 2021-10-10
tags: 杂项
---

### 使用Adafruit_SSD1306操控SSD1306的屏幕

~~~python
import time
import math
import re

import Adafruit_GPIO.SPI as SPI
import Adafruit_SSD1306

from PIL import Image
from PIL import ImageDraw
from PIL import ImageFont

import subprocess
import psutil
import socket
import requests


def get_host_ip():
    """
    查询本机ip地址
    :return: ip
    """
    try:
        s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
        s.connect(('8.8.8.8', 80))
        ip = s.getsockname()[0]
        s.close()
    finally:
        pass

    return ip


def get_time_1():
    """
    获取年月日
    :return: date
    """
    date = time.strftime("      %a  %b  %d", time.localtime())
    return str(date)


def get_time_2():
    """
    获取时分
    :return: day_time
    """
    day_time = time.strftime("      %H  :   %M", time.localtime())
    return str(day_time)

def get_sayings():
    url = "https://v1.hitokoto.cn/"
    headers = {
        "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:91.0) Gecko/20100101 Firefox/91.0"
    }

    try:
        while True:
            response = requests.get(url=url, headers=headers)
            json_text = response.text
            saysing = re.findall('"hitokoto":"(.*?)",', json_text, re.S)[0]
            if len(saysing) <= 16:
                break

        return [saysing[:8:],saysing[8::]]
    except Exception as e:
        return ["Error", str(e)]
    

if __name__ == '__main__':
    # Raspberry Pi pin configuration:
    RST = None
    """RST的使用存疑"""
    # Note the following are only used with SPI:
    DC = 23
    SPI_PORT = 0
    SPI_DEVICE = 0

    # 128x32 display with hardware I2C:
    disp = Adafruit_SSD1306.SSD1306_128_32(rst=RST)

    """初始化"""
    disp.begin()
    disp.clear()
    disp.display()
    """加载字体"""

    font = ImageFont.truetype('Font.ttf', 12)
    font_large = ImageFont.truetype('Font.ttf', 14)

    """记录长宽"""
    width = disp.width
    height = disp.height
    """预先记录一些数据"""
    padding = -2
    top = padding
    bottom = height - padding
    x = 0
    """画空白图"""
    image_blank = Image.new('1', (width, height))
    draw = ImageDraw.Draw(image_blank)
    disp.display()
    """欢迎"""
    disp.display()
    draw.text((x, 5), "Hello  Raspberry  Pi !", font=font, fill=255)
    disp.image(image_blank)
    disp.display()
    time.sleep(2)

    """画图"""
    image = Image.open('text.bmp').resize((disp.width, disp.height), Image.ANTIALIAS).convert('1')
    disp.image(image)
    disp.display()
    time.sleep(3)

    disp.begin()
    disp.clear()
    disp.display()

    try:
        while True:
            
            """时间"""    
            image_blank = Image.new('1', (width, height))
            draw = ImageDraw.Draw(image_blank)
            draw.rectangle((0, 0, width, height), outline=0, fill=0)
            draw.text((x, top), str(get_time_1()), font=font, fill=255)
            draw.text((x, top + 16), str(get_time_2()), font=font, fill=255)

            disp.image(image_blank)
            disp.display()
            time.sleep(8)
            """语录"""
            image_blank = Image.new('1', (width, height))
            draw = ImageDraw.Draw(image_blank)
            draw.rectangle((0, 0, width, height), outline=0, fill=0)
            text = get_sayings()
            draw.text((x, top), str(text[0]), font=font_large, fill=255)
            draw.text((x, top+17), str(text[1]), font=font_large, fill=255)

            disp.image(image_blank)
            disp.display()
            time.sleep(8)
            """状态"""
            i =0
            while True:
                i += 1
                image_blank = Image.new('1', (width, height))
                draw = ImageDraw.Draw(image_blank)
                draw.rectangle((0, 0, width, height), outline=0, fill=0)
                draw.text((x, top), " CPU : " + str(psutil.cpu_percent()) + " %", font=font, fill=255)
                draw.text((x, top +12 ), " IP : "+str(get_host_ip()), font=font, fill=255)

                disp.image(image_blank)
                disp.display()
                time.sleep(0.4)
                if i ==20:
                    break



    except KeyboardInterrupt as e:
        image_blank = Image.new('1', (width, height))
        draw = ImageDraw.Draw(image_blank)
        draw.rectangle((0, 0, width, height), outline=0, fill=0)
        draw.text((x, top), "   "+str(e), font=font, fill=255)
        image_blank = Image.new('1', (width, height))
        draw = ImageDraw.Draw(image_blank)
        draw.rectangle((0, 0, width, height), outline=0, fill=0)
        exit()
        
~~~

累了，不写解析了，哼
