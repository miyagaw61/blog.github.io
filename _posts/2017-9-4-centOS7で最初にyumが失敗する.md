```
echo "nameserver 8.8.8.8" >> /etc/resolv.conf
service network restart
```
この後手動でWIFIに繋いでから
```
yum -y update
yum -y install kernel-devel kernel-headers gcc gcc-c++
```
んで、guest additionsを入れる
