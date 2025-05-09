- `whoami` - what user are we running as
- `id` - what groups does our user belong to?
- `hostname` - what is the server named, can we gather anything from the naming convention?
- `ifconfig` or `ip a` - what subnet did we land in, does the host have additional NICs in other subnets?
- `sudo -l` - can our user run anything with sudo (as another user as root) without needing a password? This can sometimes be the easiest win and we can do something like `sudo su` and drop right into a root shell.
- `cat /etc/os-release` - checking out what operating system and version we are dealing with
- `echo $PATH` - view which paths are added for command execution
- `env` - view list of environment variables
- `uname -a` - kernel version information
- `lscpu` - cpu information
- `cat /etc/shells` - list of valid shells on the system
- `getent groups sudo` - list users apart of sudo or any group specified
- `df -h` - listed mounted file systems
- `cat /etc/fstab` - listed mounted drives
- `grep "*sh$" /etc/passwd` - list default shell for users
- `cat /etc/passwd | cut -f1 -d:` - list users on the system
- `cat /etc/groups` - list all groups on system
- `route` - view routing table
- `lsblk` - list block devices connected to the system
- `cat /etc/fstab | grep -v "#" | column -t` - list unmounted file systems

show all hidden files
```shell-session
find / -type f -name ".*" -exec ls -l {} \; 2>/dev/null | grep htb-student
```

show all hidden directories
```shell-session
find / -type d -name ".*" -ls 2>/dev/null
```

show temp files
```shell-session
ls -l /tmp /var/tmp /dev/shm
```
