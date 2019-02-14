# virtualBox

https://www.virtualbox.org/  
下载安装  


创建虚拟机  
类型 Linux  
版本 Ubuntu 64  

设置  
网络  
网卡1 默认 NAT  
网卡2 Host-only  
网卡3 桥接  
存储 选择盘片 ubuntu 18  

# ubuntu  
https://www.ubuntu.com/download/server  

### install Ubuntu server 16.04.4

安装 ubuntu 16,  
注意 最后选择安装 OpenSSH 和 postgres  
postgres 也可以用其他方式安装, 安装办法可参考postgres官网  
这里选择用ubuntu自动安装postgres  

Select a language = Englilsh  
Select your location = other - Asia - China  
Configure locales = United States  
Configure the keyboard = English (US)  
Configure the network = Hostname:{any}  
Set up users and password = Encrypt your home directory? No  
Configure the clock  
Partition disk = Manual  
Configure the package manager = http proxy : (null)  
Configure tasksel = Install security updates automatically  
Software selection = OpenSSH server  
Install the GRUB boot loader on a hard disk = Yes  
Finish the installation  

### ubuntu network  
显示ubuntu的网卡  
```
ifconfig -a  
```
该命令显示所有的网卡 show all network  
ubuntu 16.4.3有三个网卡, 与创建虚拟机时的网卡配置对应  
* enp0s3  
* enp0s8  
* enp0s9  

* enp0s8 is virtualBox host-only Ethernet Adapter  
  the host address is 192.168.56.1  
* enp0s9 is bridge to host ethernet adapter  


### Ubuntu Configure network  
配置网络  

打开并编辑配置文件  
```
sudo nano /etc/network/interfaces  
```

编辑文件内容如下  
```  
source /etc/network/interfaces.d/*

# The loopback network interface
auto lo
iface lo inet loopback

# The primary network interface
auto enp0s3
iface enp0s3 inet dhcp

auto enp0s8
iface enp0s8 inet dhcp

auto enp0s9
iface enp0s9 inet dhcp
```

若为静态ip, 则示例如下:  
```
auto enp0s8  
iface enp0s8 inet static  
address 192.168.56.99  
gateway 192.168.56.1  
netmask 255.255.255.0  
```

重启网络, 或者重启虚拟机  
```
sudo /etc/init.d/networking restart  
ifconfig -a   
```

### ubuntu update  
更新操作系统  
```
nano /etc/apt/sources.list  
sudo apt update  
sudo apt dist-upgrade  
sudo shutdown -h now  
```

# odoo  

### download odoo source
下载 odoo 源码从: http://nightly.odoo.com/  
```
wget http://nightly.odoo.com/12.0/nightly/src/odoo_12.0.latest.tar.gz   
```

### add a user for ubuntu
给操作系统增加一个用户, 用户名为odoo, 以后用该用户运行odoo服务  
/opt/odoo 路径是 用户odoo的 home路径  
```
sudo adduser --system --home=/opt/odoo --group odoo  
```

切换用户, 测试该用户创建成功  
```
sudo su - odoo -s /bin/bash  
exit  
```

### unzip source
解压缩上述下载的odoo源码, 到 odoo用户的home路径, /opt/odoo  
odoo源码在 server 文件夹下  
修改所有文件的 owner 为 用户odoo  
复制文件server/setup/odoo 为 server/odoo-bin  
为文件 server/odoo-bin 增加可执行属性
以后执行 server/odoo-bin 以运行 odoo服务 
```
cd /opt/odoo  
sudo tar xvf ~/odoo_10.0.latest.tar.gz  
sudo tar xvf ~/odoo_11.0.latest.tar.gz  
sudo tar xvf ~/odoo_12.0.latest.tar.gz  
sudo chown -R odoo: *  
sudo cp -a odoo-10.0.post20180424 server  
cd server  
sudo cp -a setup/odoo odoo-bin   
sudo chmod 755 odoo-bin   
```

### install python lib
安装 python 依赖包  
所有的依赖包列表, 在文件 server/requirements.txt 中  

切换路径  
```
cd /opt/odoo  
cd server  
```

#### for odoo10
odoo10 是 python2.7,  需要安装python-pip  

```
sudo apt-get install python-pip  

sudo apt-get install zlib1g-dev

sudo apt-get install libxml2-dev libxslt-dev libevent-dev libsasl2-dev libldap2-dev  
sudo pip install -r requirements.txt  
```

#### for odoo11
odoo11 是 python3, 需要安装 python3-pip  
需要 升级 pip3 才能 ..... ? 理由不记得了. 下次安装时补充上.  

```
sudo apt-get install python3-pip  
sudo apt install python3-pip  
sudo -H pip3 install --upgrade pip  


sudo apt-get install libxml2-dev libxslt-dev libevent-dev libsasl2-dev libldap2-dev  
sudo pip install -r requirements.txt  
```

#### for odoo12

安装 python3-pip,   
安装 python 的依赖包  

```
sudo apt install python3-pip  

sudo apt install libldap2-dev libsasl2-dev  
sudo pip3 install -r requirements.txt  
```

安装过程中可能出错, 需要配置下 local  
ubuntu 16 安装后 缺少 local, 需要设置下  
```
locale  
export LC_ALL=en_US.UTF-8  
```


### Create User "odoo" in database

在数据库中创建一个用户 odoo  
```
sudo su - postgres -c "createuser -s odoo"  
```
need not to set password,   
but we access database from pgAdmin with user and password  

设置密码 alter user password  
* 进入数据库命令行方式  
* 执行更新密码语句  
* 退出数据库命令行方式  
```
sudo -u postgres -s /bin/bash  
psql  
ALTER USER odoo WITH PASSWORD 'odoo11';  
\q 
exit
```

### postgre configure, so  pgAmin  access database  
修改数据库配置, 可以在其他机器上访问数据库  

打开并编辑文件  
```
sudo nano /etc/postgresql/9.5/main/pg_hba.conf  
```

行92,  line 92  
```
# IPv4 local connections:  
host all all 0.0.0.0/0  md5  
```

打开并编辑文件  
```
sudo nano /etc/postgresql/9.5/main/postgresql.conf  
```
行58  line 58  
```
listen_addresses = '*'  
```

重启数据库服务  
```
sudo /etc/init.d/postgresql restart  
```


### run odoo
* 切换用户  
* 运行odoo
```
sudo su - odoo -s /bin/bash  
server/odoo-bin -s  
```
用 ctrl + C  退出 odoo 服务  
此时 odoo 服务自动创建一个文件默认的配置文件 /opt/odoo/.odoorc  

### run odoo with conf

创建配置文件  
```
sudo mkdir /etc/odoo  
sudo cp -a /opt/odoo/.odoorc /etc/odoo/odoo.conf  
```
测试运行odoo  
```
sudo su - odoo -s /bin/bash  
server/odoo-bin -c /etc/odoo/odoo.conf  
#ctrl + C 退出odoo  
exit
```

打开并编辑配置文件    
```
sudo nano  /etc/odoo/odoo.conf  
```

配置运行日志文件  
```
logfile = /var/log/odoo/odoo.log  
logrotate = True  
```

创建日志文件需要的文件夹  
```
sudo mkdir /var/log/odoo  
sudo chown odoo:root /var/log/odoo  
```

测试运行odoo  
```
sudo su - odoo -s /bin/bash  
server/odoo-bin -c /etc/odoo/odoo.conf  
#ctrl + C 退出odoo  
exit
```

### 配置 odoo 服务

准备好一个自动运行odoo的文件  
https://github.com/odooht/odoo-docs/blob/master/install/odoo-server  

```
sudo cp ~/odoo-server /etc/init.d/odoo-server  
sudo chmod 755  /etc/init.d/odoo-server  
sudo chown root:  /etc/init.d/odoo-server  
```

测试启动 停止 odoo 服务  
```
sudo /etc/init.d/odoo-server start  
sudo /etc/init.d/odoo-server stop  
```

将odoo 服务设置为 开机自动启动  
```
sudo update-rc.d odoo-server defaults  
```

查看odoo 是否运行  
```
ps aux | grep odoo  
```



