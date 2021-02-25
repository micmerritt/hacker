# Enumeration
## Nmap Basics
- nmap -Pn -p- -vv IP
- nmap -Pn -p- -sU -vv IP
## Nmap version and vulnerability scan
- nmap -Pn -sV -O -pT:ports,U:ports -script *vuln* IP
## Grab banners
- nc -nv IP port
## Web
- Nikto -port ports -host IP -o file.txt
- Nikto -- if LFI/RFI -- fimap -u IP
- Dirb http://x.x.x.x:port /usr/share/wordlist/dirb/commmon/small/vulns.txt
- Gobuster -u http://x.x.x.x -w /usr/share/seclists/discovery/web_content/common.txt
## Netbios/SMB/RPC
- enum4linux -a x.x.x.x
- rpcclient x.x.x.x -U "" -N
- rpcinfo -p x.x.x.x
- showmount -e x.x.x.x/port
- mount -t cifs //x.x.x.x/share local-directory -o username="guest",password=""
- rlogin x.x.x.x
- smbclient -L \\x.x.x.x -U "" -N
- nbtscan -r x.x.x.x
- net use \\x.x.x.x\$share "" /u:""
- net view \\x.x.x.x
## SNMP
- onesixtyone -c listfile -l x.x.x.x
- snmpwalk -c string -v1 version x.x.x.x
## FTP
- ftp://x.x.x.x
## Password Cracking/Brute Force
- unshadow passwd-file shadow-file > unshadowed.txt
- john -rules -wordlist=file unshadowed.txt

- hydra -L userfile - P passwordfile -v x.x.x.x ssh
- medusa -h x.x.x.x -u userfile -P passwordfile -M http -m DIR:/admin -T 30
- hashcat -m 400 -a 0 hashfile wordlist
## Packet Sniffing
- tcpdump -i tap0 host x.x.x.x tcp port xx and not arp and not icmp -vv