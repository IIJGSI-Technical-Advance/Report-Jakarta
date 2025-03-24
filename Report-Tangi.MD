# Report Business Trip Jakarta Tan'gi

## 1. Selasa 18/03/2025

## 2. Rabu 18/03/2025
- Create new user (disable promt password dan disable user new information)
```
#!/bin/bashh

read -p "input username: " username
sudo useradd -p -c $username
```
- Create script to install package in remote server
```
#!/bin/bashh

ssh sysadmin@192.168.10.80 "sudo yum install -y httpd && sudo yum update"
```
- Create script copy file to remote server
```
#!/bin/bashh

echo "copy file"
scp -o StrictHostKeyChecking=no index.html sysadmin@192.168.10.80:/home/sysadmin
```
## 3. Kamis 18/03/2025
- Create script for nginx (webserver)
```
#!/bin/bash

echo "Install NGINX";
ssh -o StrictHostKeyChecking=no sysadmin@192.168.10.80 "sudo yum install -y nginx"
echo "move html file to nginx"
scp -o StrictHostKeyChecking=no index.html sysadmin@192.168.10.80:/home/sysadmin
echo "insert hostname to html.index"
ssh -o StrictHostKeyChecking=no sysadmin@192.168.10.80 "sudo hostname > /home/sysadmin/index.html"
echo "chown to root"
ssh -o StrictHostKeyChecking=no sysadmin@192.168.10.80 "sudo chown root:root /home/sysadmin/index.html"
echo "Move index.html to nginx"
ssh -o StrictHostKeyChecking=no sysadmin@192.168.10.80 "sudo cp /home/sysadmin/index.html /usr/share/nginx/html/"
echo "start service nginx"
ssh -o StrictHostKeyChecking=no sysadmin@192.168.10.80 "sudo systemctl enable nginx && sudo systemctl start nginx"
```
- Install vCenter and cluster
- Output & file modification (check process id, port, get spesific output we want)