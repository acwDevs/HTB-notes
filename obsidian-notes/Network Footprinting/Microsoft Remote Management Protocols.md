
RDP
	Port
		3389
	Footrprinting
		nmap --script rdp*
		nmap --packet-trace (detect rdp cookies)
	Tools
		rdp-sec-check.pl https://github.com/CiscoCXSecurity/rdp-sec-check
	Interaction
		xfreerdp /u:user /p:pass /v:x.x.x.x
	trace and inspect
		nmap -sV -sC 10.129.201.248 -p3389 --packet-trace --disable-arp-ping -n
WinRM
	Port
		5985 5986
	Tools
		Test-WsMan
		evilwinrm https://github.com/Hackplayers/evil-winrm
	WMI
		Port 
			135
		Tools
			wmiexec.py https://github.com/SecureAuthCorp/impacket/blob/master/examples/wmiexec.py