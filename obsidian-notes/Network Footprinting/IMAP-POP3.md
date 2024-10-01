
Use HELO command without creds before running anything else on the mail service
Use EHLO with creds

Ports
	`110`, `143`, `993`, and `995`



![[pop3-cmds.png]]

![[imap-cmds.png]]


Banner Grabbing
	curl -k 'imaps://x.x.x.x' --user user:pass
	SSL enabled
		openssl s_client -connect 10.129.14.128:imaps
	view messages
		fetch <id> body[]

Pop3 footprinting
	SSL 
		openssl s_client -connect 10.129.14.128:pop3s