Davinci Data Visualization System

Registration interface: /api/v3/users

Param：{"email": "string","password": "string","username": "string"}

![image](https://github.com/1dreamGN/CVE/assets/112082417/57f486fc-241d-430c-9a30-e0525125d395)

![image](https://github.com/1dreamGN/CVE/assets/112082417/d8fa0e2a-ca41-4dec-bd88-87ed62b9b5e5)

Activation is required after registration Can receive direct mail activation by email

AES encryption using the token returned by the registration interface Key: sM7!tsv?5ygRo;h.

![image](https://github.com/1dreamGN/CVE/assets/112082417/c084f95c-2693-4954-9b4c-3224bdd52c96)

![image](https://github.com/1dreamGN/CVE/assets/112082417/036cfa1c-0525-4297-8474-2ce31403bf7a)

Activation interface: /api/v3/users/active/{token}

The token is the result of encryption

The system also has a weak druid password path to the root directory of the interface. For example, /druid/root/123456

Destination address: http://bi.jxufe.edu.cn:8081/

Access to registration: http://bi.jxufe.edu.cn:8081/#/register

The registered account is admin2/qq123456.

![image](https://github.com/1dreamGN/CVE/assets/112082417/24904c29-d74d-4756-9725-af6ffcda57a7)

![image](https://github.com/1dreamGN/CVE/assets/112082417/f3ad53a3-e7b1-45ef-816f-e68a776a16c6)

http://bi.jxufe.edu.cn:8081/#/project/4/vizs

Here a project test is created

Go in and find that the URL is passed to the interface. projectId=4

It is convenient for the demo to operate directly in the URL

Unauthorized vulnerabilities

Modify the URL to: http://bi.jxufe.edu.cn:8081/#/project/1/vizs

Access to the information of the original administrator

![image](https://github.com/1dreamGN/CVE/assets/112082417/6bd2bac0-ab7b-4858-bd9f-cae1c491198f)

![image](https://github.com/1dreamGN/CVE/assets/112082417/1d563b3f-9d26-49dc-b9fa-f074feba5d23)

8w+ pieces of student information

![image](https://github.com/1dreamGN/CVE/assets/112082417/a8834f35-9b9c-4565-afc2-169acb3c0da0)

6,863 graduate student information includes ID cards

![image](https://github.com/1dreamGN/CVE/assets/112082417/8060c5ac-7316-4629-9c1f-bcaa6a847c61)

1424 electric vehicle information

