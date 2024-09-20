Intelligent Platform Management Interface

Port
	623 udp
Version enum
	nmap --script ipmi-version -sU
	msf
		ipmi_version

Default Creds
	![[IPMI-Default-Creds.png]]
Brute Forcing captured hashes 
	hashcat -m 7300 ipmi.txt -a 3 ?1?1?1?1?1?1?1?1 -1 ?d?u
Exploit Tools
	https://www.rapid7.com/db/modules/auxiliary/scanner/ipmi/ipmi_dumphashes/
	ipmitools