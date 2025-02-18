
##### Backend blacklist extension filtering

[Extension Wordlist](https://raw.githubusercontent.com/danielmiessler/SecLists/refs/heads/master/Discovery/Web-Content/web-extensions.txt)
[PHP Extensions](https://raw.githubusercontent.com/swisskyrepo/PayloadsAllTheThings/refs/heads/master/Upload%20Insecure%20Files/Extension%20PHP/extensions.lst)
[.NET Extensions](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Upload%20Insecure%20Files/Extension%20ASP)

##### Backend whitelist extension filtering

Using double extensions (e.g. `shell.jpg.php`)
or Reverse double extensions (e.g. `shell.php.jpg`)

Filter example
```php
$fileName = basename($_FILES["uploadFile"]["name"]);

if (!preg_match('^.*\.(jpg|jpeg|png|gif)', $fileName)) {
    echo "Only images are allowed";
    die();
}
```

##### Character Injection

Character Injection List (e.g. shell.php%00.jpg)
- `%20`
- `%0a`
- `%00`
- `%0d0a`
- `/`
- `.\`
- `.`
- `…`
- `:`

Injection permutation script
```bash
for char in '%20' '%0a' '%00' '%0d0a' '/' '.\\' '.' '…' ':'; do
    for ext in '.php' '.phps'; do
        echo "shell$char$ext.jpg" >> ext_wordlist.txt
        echo "shell$ext$char.jpg" >> ext_wordlist.txt
        echo "shell.jpg$char$ext" >> ext_wordlist.txt
        echo "shell.jpg$ext$char" >> ext_wordlist.txt
    done
done
```

