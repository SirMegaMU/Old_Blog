---
layout: post
title: 爬取WallHeaven中的壁纸
date: 2021-09-26
tags: Python
---

### WallHeaven的TopList
![img](https://sirmegamu.github.io/images/posts/2021-09-26/01.png)

### 思路

1. 先获取到TopList页面中各个a标签的href属性

   `<a class="preview" href="https://wallhaven.cc/w/72rxqo" target="_blank"></a>`

1. 再使用获取到的href属性请求到每个图片的详情页，获取img标签的src属性

1. 根据获取的src属性请求图片，并进行保存

但是，WallHeaven的反爬还比较严格，我在第一步就卡住了，使用request无法获取到正确的页面。

所以不得不使用selenium进行浏览器操作。

但是，既然都使用selenium了，在图片页面直接使用ActionChain向浏览器进行模拟输入Ctrl+S就可以保存当前网页的源码(也就是那个图片)，这样反而更简单一些。

然而，由于我的Chrome版本的问题，无法去掉保存页面时跳出的弹窗，所以被迫放弃使用快捷键保存页面的办法。

只好使用selenium.webdriver中的page_source来获取页面源码

### 最终版本

~~~python
from selenium import webdriver
import time

def get_tags(num):
    if num < 1:
        num = 1
    url_main = "https://wallhaven.cc/toplist?page={}".format(num)
    browser = webdriver.Chrome(executable_path=r"D:\Documents\Desktop\Others\Tools\chromedriver_win32\chromedriver.exe")
    browser.get(url_main)
    elements = browser.find_elements_by_xpath('/html/body/main/div[1]/section/ul/li/figure/a')
    url_list = list()
    n = 0
    for element in elements:
        n+=1
        pic_tag = element
        pic_tag.click()
        windows = browser.window_handles
        browser.switch_to.window(windows[n]) 
        time.sleep(1.5)
        browser.find_elements_by_xpath('//*[@id="wallpaper"]')
        data_url = browser.find_element_by_xpath('//*[@id="wallpaper"]').get_attribute("src")
        print(data_url)
        url_list.append(data_url)
        browser.switch_to.window(windows[0]) 
    return url_list

def down_pic(url):
    try:
        browser = webdriver.Chrome(executable_path=r"D:\Documents\Desktop\Others\Tools\chromedriver_win32\chromedriver.exe")  
        name_ = "WallHeaven_pics\\" 
        with open(name_+url,'wb') as f:
            browser.get(url)
            time.sleep(2)
            f.write(browser.page_source)
            print('写入成功')
    except Exception as e:
        print(e)   

if __name__  == "__main__":

    pic_url_list = get_tags(1)
    with open(r"WallHeaven_pics\test.txt",'w')as file:
        for url in pic_url_list:
            file.write(url+"\n")
    for url in pic_url_list:
        down_pic(url)


~~~



