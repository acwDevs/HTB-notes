
Banner grabbing
	nmap -sV -sC
	nc -nv ip port
	telnet ip port

Over SSL 
	openssl s_client -connect <FQDN/IP>:21 -starttls ftp

Get all files from ftp server
	wget -m --no-passive ftp://anonymous:anonymous@<target>