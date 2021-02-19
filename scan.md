## Check the network
`nmap -sn 10.0.0.0/24`
## Scan ports/run OS detection
`nmap -A -oA nmap [IP]`
## Scan all ports, takes forever
`nmap -v -p- -sT [IP]`
## Nikto probe
`nikto -host [IP] -port [port]`
## Directories and Files
`./dirsearch.py -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u [IP] -e php`
## Check nmap scripts
`locate *.nse | grep smb`
## Syntax
`nmap -p [port,port] --script=[scriptname] [IP]`
## Wildcards
`nmap -p [port,port] --script=smb-vuln* [IP]`
## Enum
`enum4linux -a [IP]`
## smbclient
`smbclient \\\\[IP]\\[share]`
## FTP
`ftp [IP]`

`username: anonymous / password: [enter]`
## Banner Grab
`nc [IP] [port]`
## Find Exploit
`searchsploit -u`
`searchsploit [multiple search terms]`
