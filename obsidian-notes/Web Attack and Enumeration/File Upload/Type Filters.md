
There are two common methods for validating the file content: `Content-Type Header` or `File Content`.

[Content-Type Wordlist](https://github.com/danielmiessler/SecLists/blob/master/Discovery/Web-Content/web-all-content-types.txt)

Limiting Content-Type List
```shell-session
cat web-all-content-types.txt | grep 'image/' > image-content-types.txt
```

Content-Type Header Validation Example
```php
$type = $_FILES['uploadFile']['type'];

if (!in_array($type, array('image/jpg', 'image/jpeg', 'image/png', 'image/gif'))) {
    echo "Only images are allowed";
    die();
}
```

#### MIME-Type Validation
This is usually done by inspecting the first few bytes of the file's content, which contain the [File Signature](https://en.wikipedia.org/wiki/List_of_file_signatures) or [Magic Bytes](https://web.archive.org/web/20240522030920/https://opensource.apple.com/source/file/file-23/file/magic/magic.mime)

We can add magic numbers to our payload in order to upload a file
E.g.
![[Pasted image 20250217204503.png]]
