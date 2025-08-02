---
title: 'Python爬虫之无头浏览器'
date: 2022-02-15 16:36:20
tags: [Python]
published: true
hideInList: false
feature: 
isTop: false
categories: 'Python'
id: 'python-crawler-headless-browser'
---


## Linux安装chrome

```shell
yum install https://dl.google.com/linux/direct/google-chrome-stable_current_x86_64.rpm
或者
yum install google-chrome-stable.x86_64
```

安装必要的库：

```shell
yum install mesa-libOSMesa-devel gnu-free-sans-fonts wqy-zenhei-fonts
```

## 谷歌无头浏览器下载

https://chromedriver.chromium.org/

解压 

```shell
unzip chromedriver_linux64.zip
```

给执行权限

```shell
chmod +x /usr/bin/chromedriver
```

## 获取元素方法

```shell
#使用下面的方法，查找指定的元素进行操作即可
    find_element_by_id            根据id找节点
    find_elements_by_name         根据name找
    find_elements_by_xpath        根据xpath查找
    find_elements_by_tag_name     根据标签名找
    find_elements_by_class_name   根据class名字查找
    
bd_input = browser.find_element_by_id('kw').send_keys('小猪配齐')
#在此截屏
browser.save_screenshot(r'phantomjs\xiaozhu.png')
time.sleep(3)

bd_sous = browser.find_element_by_id('su').click()
#在此截屏
browser.save_screenshot(r'phantomjs\sous.png')
time.sleep(3)
```

<!-- more -->

## 示例：

```py
# 获取drm价格
import time
from selenium import webdriver
from selenium.webdriver.chrome.options import Options

#这个是一个用来控制chrome以无界面模式打开的浏览器
#创建一个参数对象，用来控制chrome以无界面的方式打开
chrome_options = Options()
#后面的两个是固定写法 必须这么写
chrome_options.add_argument('--headless')
chrome_options.add_argument('--disable-gpu')
chrome_options.add_argument('--no-sandbox') #关闭弹窗
chrome_options.add_argument('--disable-dev-shm-usage')
chrome_options.add_argument('blink-settings=imagesEnabled=false') #不加载图片
chrome_options.add_argument('--hide-scrollbars') #隐藏滚动条, 应对一些特殊页面
#驱动路径 谷歌的驱动存放路径
path = r'/usr/bin/chromedriver'

#创建浏览器对象
browser = webdriver.Chrome(executable_path=path,chrome_options=chrome_options)

url ='https://www.yokaiswap.com/info/token/0x81e60a955dc8c4d25535c358fcfe979351d102b5'
browser.get(url)
time.sleep(10)
# browser.save_screenshot('drm.png') #截图
drmprice = browser.find_elements_by_xpath('//*[@id="root"]/div[1]/div[3]/div/div[2]/div[2]/div[1]/div[2]/div[1]')
print(drmprice[0].text)
#print(browser.page_source) #打印获取的网页内容
browser.quit()

```

示例运行结果

```shell
[root@VM-16-2-centos yokai]# python3 getdrmprice.py
$139.14
```



## 报错解决

```shell
[root@VM-16-2-centos yokai]# python3 getdrmprice.py
Traceback (most recent call last):
  File "getdrmprice.py", line 18, in <module>
    browser = webdriver.Chrome(executable_path=path,chrome_options=chrome_options)
  File "/usr/local/lib/python3.6/site-packages/selenium/webdriver/chrome/webdriver.py", line 81, in __init__
    desired_capabilities=desired_capabilities)
  File "/usr/local/lib/python3.6/site-packages/selenium/webdriver/remote/webdriver.py", line 157, in __init__
    self.start_session(capabilities, browser_profile)
  File "/usr/local/lib/python3.6/site-packages/selenium/webdriver/remote/webdriver.py", line 252, in start_session
    response = self.execute(Command.NEW_SESSION, parameters)
  File "/usr/local/lib/python3.6/site-packages/selenium/webdriver/remote/webdriver.py", line 321, in execute
    self.error_handler.check_response(response)
import time
  File "/usr/local/lib/python3.6/site-packages/selenium/webdriver/remote/errorhandler.py", line 242, in check_response
    raise exception_class(message, screen, stacktrace)
selenium.common.exceptions.WebDriverException: Message: unknown error: Chrome failed to start: exited abnormally.
  (unknown error: DevToolsActivePort file doesn't exist)
  (The process started from chrome location /usr/bin/google-chrome is no longer running, so ChromeDriver is assuming that Chrome has crashed.)

修改 /usr/bin/ 目录下的 google-chrome 配置文件

vim /usr/bin/google-chrome

找到 exec -a "$0" "$HERE/chrome" "$@" 将其注释掉

并添加一行 exec -a "$0" "$HERE/chrome" "$@" --user-data-dir --no-sandbox

解决

```