---
title: request模块
tags:
  - 爬虫
  - python
abbrlink: 16dd4349
date: 2018-05-24 20:47:32
categories:
copyright:
password:
---
## request模块的学习
 
### 使用前
 	- pip install requests

### 发送get，post请求，获取响应
- response = request.get(url)       #发送get请求，请求url地址对应的响应
- response = request.post(url,data={请求体的字典})    #发送post请求

### response的方法
- response.text
	- 该方式往往会出现乱码，出现乱码使用response.encoding="utf-8"
- response.content.decode()
	- 把响应的二进制字节类型转化为str型
- response.request.url #发送请求的url地址
- response.rul  #response响应的url地址
- response.erquest.headers  #请求头
- response.headers  #响应请求

### 获取网页源码的正确打开方式
- 1.response.content.decode()
- 2.response.content.decode("gbk") 
- 3.response.text

### 发送带harder的请求
- 为了模拟浏览器，获取和浏览器一样的内容
```python
headers = {
"User-Agent":"Mozilla/5.0 (Linux; Android 5.0; SM-G900P Build/LRX21T) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Mobile Safari/537.36",
"Referer":"https://fanyi.baidu.com/?aldtype=16047"}

response = requests.get(url,headers=hesders)
```
### 使用超时参数
- requests.get(url,headers=headers,timeout=3) #3秒内必须返回响应，否则报错

### retrying模块
  - pip install retrying
 ```python
 from retrying import retry
 
 @retry(stop_max_attempt_number=3)
 def fun1():
 	print("this is fun1")
	raise ValueError("this is error")
 ```




### 处理cookie相关请求

- 直接携带cookie请求url地址
	- 1.cookie放在headers中
	  ```python
	  headers = {"User-Agent":".......","Cookie":"cookie 字符串"}
	  ```
	- 2.cookie字典传给cookies参数
		- requests.get(url,cookies=cookie_dict)
	
	- 先发送post请求，获取cookie，带上cookie请求登陆后的页面
		- 1. session = requests.session()  #session具有的方法和requests一样
		- 2. session.post(url,data,headers) #服务器设置在本地的cookie会保存在session
		- 3. session.get(url) #会带上之前保存在session中的cookie，能够请求成功
		