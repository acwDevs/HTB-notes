

##### Prevent User Path Declaration
The most effective thing we can do to reduce file inclusion vulnerabilities is to avoid passing any user-controlled inputs into any file inclusion functions or APIs. The page should be able to dynamically load assets on the back-end, with no user interaction whatsoever.


##### Create Front-End File Whitelist
Create a whitelist that contains all existing paths used in the front-end, and then utilize this list to match the user input. Such a whitelist can have many shapes, like a database table that matches IDs to files, a `case-match` script that matches names to files, or even a static json map with names and files that can be matched.

##### Remove Remote File Inclusion
- In PHP this can be done by setting `allow_url_fopen` and `allow_url_include` to Off
- Run the application within `Docker` to lock webserver to web root directory
- In PHP that can be done by adding `open_basedir = /var/www` in the php.ini file
- Furthermore, you should ensure that certain potentially dangerous modules are disabled, like [PHP Expect](https://www.php.net/manual/en/wrappers.expect.php) [mod_userdir](https://httpd.apache.org/docs/2.4/mod/mod_userdir.html)

##### Using WAF(Web Application Firewall)
ModSecurity
With proper hardening, attackers will leave many more signs, and the organization will hopefully detect these events even quicker
