Davinci数据可视化系统

注册接口：/api/v3/users

Param：{"email": "string","password": "string","username": "string"}
![image](https://github.com/1dreamGN/CVE/assets/112082417/57f486fc-241d-430c-9a30-e0525125d395)

![image](https://github.com/1dreamGN/CVE/assets/112082417/d8fa0e2a-ca41-4dec-bd88-87ed62b9b5e5)

注册后需要激活 能收到邮件直接邮件激活

使用注册接口返回的token进行AES加密 密钥：sM7!tsv?5ygRo;h.

![image](https://github.com/1dreamGN/CVE/assets/112082417/c084f95c-2693-4954-9b4c-3224bdd52c96)

![image](https://github.com/1dreamGN/CVE/assets/112082417/036cfa1c-0525-4297-8474-2ce31403bf7a)

激活接口：/api/v3/users/active/{token}

Token为加密结果

该系统还存在druid弱口令 路径为接口的根目录。如/druid/   root/123456

目标地址：http://bi.jxufe.edu.cn:8081/

访问注册：http://bi.jxufe.edu.cn:8081/#/register

注册账号为admin2/Qq123456.

![image](https://github.com/1dreamGN/CVE/assets/112082417/24904c29-d74d-4756-9725-af6ffcda57a7)

![image](https://github.com/1dreamGN/CVE/assets/112082417/f3ad53a3-e7b1-45ef-816f-e68a776a16c6)

http://bi.jxufe.edu.cn:8081/#/project/4/vizs

这里创建了一个项目 test

进去发现url传值到接口。projectId=4

方便演示直接在url进行操作

越权漏洞

修改url 为：http://bi.jxufe.edu.cn:8081/#/project/1/vizs

访问到原管理员的信息

![image](https://github.com/1dreamGN/CVE/assets/112082417/6bd2bac0-ab7b-4858-bd9f-cae1c491198f)

![image](https://github.com/1dreamGN/CVE/assets/112082417/1d563b3f-9d26-49dc-b9fa-f074feba5d23)

8w+条学生信息

![image](https://github.com/1dreamGN/CVE/assets/112082417/a8834f35-9b9c-4565-afc2-169acb3c0da0)

6863条研究生信息包含身份证

![image](https://github.com/1dreamGN/CVE/assets/112082417/8060c5ac-7316-4629-9c1f-bcaa6a847c61)

1424条电动车信息

