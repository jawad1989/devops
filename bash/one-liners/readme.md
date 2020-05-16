Create a new file
```
touch index.html
```
Edit any file
```
gedit index.html
vim index.html
nano index.html
```

Check Linux Version
```
cat /etc/system-release
```

List running services using service command on a CentOS/RHEL 6.x or older
The syntax is as follows for CentOS/RHEL 6.x and older (pre systemd systems):
```
service --status-all
service --status-all | more
service --status-all | grep ntpd
service --status-all | less
```
PRINT THE STATUS OF ANY SERVICE

To print the status of apache (httpd) service:
```
service httpd status
```
LIST ALL KNOWN SERVICES (CONFIGURED VIA SYSV)
```
chkconfig --list
```
LIST SERVICE AND THEIR OPEN PORTS
```
netstat -tulpn
```
TURN ON / OFF SERVICE
```
ntsysv
chkconfig service off
chkconfig service on
chkconfig httpd off
chkconfig ntpd on
```
