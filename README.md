这一次做的是通过ARP欺骗的方式进行MITM的实验。此次使用的是sslsplit工具。
基本步骤如下：
1.在git上下载源码：
git clone https://github.com/droe/sslsplit.git   /opt/sslsplit
apt-get install libssl-dev libevent-dev
安装成功：![](https://raw.githubusercontent.com/vsmile0601/2Pictures/master/完整版一.bmp) 
2.利用小学期所讲授的知识，使用openssl生成一份数字证书：
openssl genrsa -out ca.key 2048
openssl req -new -x509 -days 1096 -key ca.key -out ca.crt
![](https://raw.githubusercontent.com/vsmile0601/2Pictures/master/完整版二.bmp)
![](https://raw.githubusercontent.com/vsmile0601/2Pictures/master/完整版三.bmp)
3.在进行端口转发之前，打开ip_forward功能：
首先输入：iptables -F 清除原有设置
echo 1 > /proc/sys/net/ipv4/ip_forward
使用iptables进行流量转发：
![](https://raw.githubusercontent.com/vsmile0601/2Pictures/master/打开ip_forward转发并且用sslstrip监听10000端口.bmp)
查看当前设置：
![](https://raw.githubusercontent.com/vsmile0601/2Pictures/master/完整版四.bmp)
![](https://raw.githubusercontent.com/vsmile0601/2Pictures/master/完整版五.bmp)
4.ARP欺骗：
![](https://raw.githubusercontent.com/vsmile0601/2Pictures/master/完整版六.bmp)
其中192.168.1.103为物理机IP，192.168.1.1为物理机和虚拟机的网关。本实验的目的是攻击物理机。
（PS:其中，为了让物理主机与虚拟机的IP在同一网段，我们进行了如下修改：)
![](https://raw.githubusercontent.com/vsmile0601/2Pictures/master/解决方法（arp%20spoof）.bmp)
![](https://raw.githubusercontent.com/vsmile0601/2Pictures/master/重启network.bmp)
5.启动SSLSplit：
![](https://raw.githubusercontent.com/vsmile0601/2Pictures/master/完整版2.bmp)
