Port
	111
Banner Grabbing
	nmap -sV -sC ip
Info Gathering
	nmap --script nfs* ip
show file shares
	showmount -e ip
mounting fileshare
	sudo mount -t nfs x.x.x.x:/ ./target-NFS/ -o nolock,ver=1