cat /etc
Tools
	SSH
		sshaudit - https://github.com/jtesta/ssh-audit.git
	RSYNC
		nmap
		nc
		rsync
RSYNC
	Port
		873
	Scanning
		nmap
	Probing shares
		nc
	Enumeration
		rsync -av --list-only rsync://127.0.0.1/dev
	
R-Services
	POI
		hosts.equiv
		.rhosts
	Port
		512,513,514
	Interaction
		rlogin
	User Enum
		rusers -al
		rwo
	Commands
		- rcp (`remote copy`)
		- rexec (`remote execution`)
		- rlogin (`remote login`)
		- rsh (`remote shell`)
		- rstat
		- ruptime
		- rwho (`remote who`)
		Vulnerable Commands
				![[rservices-vuln-cmds.png]]