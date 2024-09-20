NMAP
	![[Pasted image 20240626130310.png]]
	NFS
		![[Pasted image 20240626132409.png]]		
		Root has privileges so we switch to root and go into file
			Issue with root_squash configuration
		![[Pasted image 20240626132449.png]]
	Using File on all the files in the mounted share shows one with text
		![[Pasted image 20240626132717.png]]
		Found Creds
			 user="alex"
			 password="lol123!mD"

	
	![[Pasted image 20240626132749.png]]	Got an rdp connection with creds
		Found interesting file for admin account with creds
			sa:87N1ns@slls83
		![[Pasted image 20240626134326.png]]
		Found flag after connecting over with admin privilege
		![[Pasted image 20240626135423.png]]