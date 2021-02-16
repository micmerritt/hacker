# LINUX PRIV
# OS
## Distro
`cat /etc/issue`

`cat /etc/*-release`

`cat /etc/lsb-release #Debian-based`

`cat /etc/redhat-release #Redhat-based`
## Kernel
`cat /proc/version`

`uname -a` or `uname -mrs`

`rpm -q kernel`

`dmesg | grep Linux`

`ls /boot | grep vmlinux-`
## Environmental
`cat /etc/profile`

`cat /etc/bashrc`

`cat ~/.bash_profile`

`cat ~/.bashrc`

`cat ~/.bash_logout`

`env`
## Printer check
`lpstat -a`
#
# Services
`ps aux`

`ps -ef`

`top`

`cat /etc/services`
## Root Services
`ps aux | grep root`

`ps -ef | grep root`
## Versions
`ls -alh /usr/bin/` or `ls -alh /sbin/`

`ls -alh /var/cache/apt/archives`

`dpkg -l`

`rpm -qa`
## Misconfigurations
`cat /etc/syslog.conf`

`cat /etc/chttp.conf`

`cat /etc/lighttpd.conf`

`cat /etc/inetd.conf`

`cat /etc/apache2/apache2.conf`

`ls -aRl /etc/ | awk '$1 ~ /^.*r.*/`
## Cronjobs
`crontab -l`

`ls -alh /var/spool/cron`

`ls -al /etc/ | grep cron`

`cat /etc/cron*`

`cat /etc/at.allow`

`cat /etc/at.deny`

`cat /var/spool/cron/crontabs/root`
## Usernames
`grep -i user [filename]`

`grep -i pass [filename]`

`find . -name "*.php" -print0 | xargs -0 grep -i -n "var $passsword"`
#
# Network Connection
`/sbin/ifconfig -a`

`cat /etc/network/interfaces`

`cat /etc/sysconfig/network`
## Network Configuration
`cat /etc/resolv.conf`

`cat /etc/sysconfig/network`

`cat /etc/networks`

`iptables -L`

`hostname`

`dnsdomainname`
## Communications
`lsof -i` [:port]`

`grep [port] /etc/services`

`netstat -antup` or `netstat -antpx`

`netstat -tulpn`

`chkconfig --list`

`last`

`w`
## Cached Connections
`arp -e`

`route`

`/sbin/route -nee`
## Packet Sniffing
`tcpdump tcp dst [IP] [port] and tcp dst [IP] [port]`
## Port Forwarding
`FPipe.exe -l [localport] -r [remoteport] -s [localport] [localIP]`
### Local Port
`ssh -L [localport]:[remoteIP]:[remoteport] [localuser]@[localIP]`
### Remote Port
`ssh -R [localport]:[remoteIP]:[remoteport] [localuser]@[localIP]`
### Port Relay
`mknod backpipe p ; nc -l -p [remoteport] < backpipe | nc [localIP] [localport] > backpipe`
### Proxy (Port 80 to 8080)
`mknod backpipe p ; nc -l -p 8080 0 & < backpipe | tee -a inflow | nc localhost 80 | tee -a outflow 1>backpipe`
### Proxy Monitor (Port 80 to 8080)
`mknod backpipe p ; nc -l -p 8080 0 & < backpipe | tee -a inflow | nc localhost 80 | tee -a outflow & 1>backpipe`
### Tunneling
`ssh -D 127.0.0.1:[port] -N [username]@[IP]`

`proxychains ifconfig`
#
# Info and Users
## Who are You
`id`

`who`

`last`
### List Users
`cat /etc/passwd | cut -d: -f1`
### List Super Users
`grep -v -E "^#" /etc/passwd | awk -F: '$3 == 0 {print $1}'`

`cat /etc/sudoers`

`sudo -l`
## Files
`cat /etc/passwd` and `cat /etc/shadow`

`cat /etc/group`

`ls -alh /var/mail`
## Directories
`ls -ahlR /root/` or `ls -ahlR /home/`
## User Activities
`cat ~/.bash_history`

`cat ~/.php_history`
## User Info
`cat ~/.bashrc`

`cat ~/.profile`

`cat /var/mail/root` or `cat /var/spool/mail/root`
## Keys
`cat ~/.ssh/authorized_keys`

`cat ~/.ssh/id_rsa`

`cat /etc/ssh/ssh_config` or `cat /etc/sshd/sshd_config`
#
# File Systems
## Break out of Shell
>python -c 'import pty;pty.spawn("/bin/bash")'

>echo os.system('/bin/bash')

>/bin/sh -i
## Writeable
### Anyone
`ls -aRl /etc/ | awk '$1 ~ /^.*w.*/' 2>/dev/null`
### Owner
`ls -aRl /etc/ | awk '$1 ~ /^..w/' 2>/dev/null`
### Group
`ls -aRl /etc/ | awk '$1 ~ /^.....w/' 2>/dev/null`
### Other
`ls -aRl /etc/ | awk '$1 ~ /w.$/' 2>/dev/null`
## Var
`ls -alh /var/log` or `ls -alh /var/mail`

`ls -alh /var/spool`

`cat /var/lib/dhcp3/dhclient.leases`
## Website Hidden Files
`ls -alhR /var/www/`

`ls -alhR /srv/www/htdocs/`

`ls -alhR /usr/local/www/apache22/data/`

`ls -alhR /var/www/html/`
## Logs
`cat /etc/httpd/logs/access_log`
## Mounts
`mount`

`df -h`

`cat /etc/fstab`
## Sticky Bits
### Sticky bit owner of the directory
`find / -perm -1000 -type d 2>/dev/null`
### SGID (chmod 2000) - run as the group
`find / -perm -g=s -type f 2>/dev/null`
### SUID (chmod 4000) - run as the owner
`find / -perm -u=s -type f 2>/dev/null`
### SGID or SUID
`find / -perm -g=s -o -perm -u=s -type f 2>/dev/null`

`for i in 'locate -r "bin$"'; do find $i \( -perm -4000 -o -perm -2000 \) -type f 2>/dev/null; done`
### SGID or SUID, no symbolic, 3 folders deep
`find / -perm -g=s -o -perm -4000 ! -type 1 -maxdepth 3 -exec ls -ld {} \; 2>/dev/null`
