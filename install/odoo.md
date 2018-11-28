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
ifconfig -a  
show all network  
ubuntu 16.4.3  

enp0s3  
enp0s8  
enp0s9  

### Ubuntu Configure network  
sudo nano /etc/network/interfaces  
  
  #enp0s3 is virtualBox host-only Ethernet Adapter  
  # the host address is 192.168.56.1  
  auto enp0s8  
  iface enp0s8 inet static  
  address 192.168.56.99  
  gateway 192.168.56.1  
  netmask 255.255.255.0  

  #enp0s9 is bridge to host ethernet adapter  
  auto enp0s9  
  iface enp0s9 inet dhcp  

sudo /etc/init.d/networking restart  
ifconfig -a   


### ubuntu update  
nano /etc/apt/sources.list  
sudo apt update  
sudo apt dist-upgrade  
sudo shutdown -h now  



# odoo  

http://nightly.odoo.com/  

wget http://nightly.odoo.com/12.0/nightly/src/odoo_12.0.latest.tar.gz   

---- add user  
sudo adduser --system --home=/opt/odoo --group odoo  

sudo su - odoo -s /bin/bash  
exit  


cd /opt/odoo  
sudo tar xvf ~/odoo_10.0.latest.tar.gz  
sudo tar xvf ~/odoo_11.0.latest.tar.gz  
sudo tar xvf ~/odoo_12.0.latest.tar.gz  
sudo chown -R odoo: *  
sudo cp -a odoo-10.0.post20180424 server  
cd server  
sudo cp -a setup/odoo odoo-bin   
sudo chmod 755 odoo-bin   



-----  for odoo10 ---- pip  
sudo apt-get install python-pip  
---------------------------------

-----for odoo11 install pip3 ----  
sudo apt-get install python3-pip  
sudo apt install python3-pip  
sudo -H pip3 install --upgrade pip  
----------------------------------------

-----only for odoo10 -----------------------------------  
sudo apt-get install zlib1g-dev

-----python lib ---  
sudo apt-get install libxml2-dev libxslt-dev libevent-dev libsasl2-dev libldap2-dev  
sudo pip install -r requirements.txt  
-----------------------------------------------

-----for odoo12 install pip3 ----  
sudo apt install python3-pip  
sudo apt install libldap2-dev libsasl2-dev  
sudo pip3 install -r requirements.txt  

locale  
export LC_ALL=en_US.UTF-8  


###in database Create User "odoo" #####################
sudo su - postgres -c "createuser -s odoo"  
##  need not to set password,   
##  but we access database from pgAdmin with user and password  

#### alter user password  
sudo -u postgres psql  
ALTER USER odoo WITH PASSWORD 'odoo11';  

### to quit
\q 


####  postgre configure, so  pgAmin  access database  
sudo nano /etc/postgresql/9.5/main/pg_hba.conf  
##line 92  
    # IPv4 local connections:  
    host all all 0.0.0.0/0  md5  

sudo nano /etc/postgresql/9.5/main/postgresql.conf  
##line 58  
    listen_addresses = '*'  

sudo /etc/init.d/postgresql restart  

########################################
---- run odoo, and create conf file:   /opt/odoo/.odoorc  
sudo su - odoo -s /bin/bash  
server/odoo-bin -s  
----- quit ----
ctrl + C  
exit  

---- conf ---  
sudo mkdir /etc/odoo  
sudo cp -a /opt/odoo/.odoorc /etc/odoo/odoo.conf  
---- run with conf  
sudo su - odoo -s /bin/bash  
server/odoo-bin -c /etc/odoo/odoo.conf  
---- quit ----  
ctrl + C  

---- to modify odoo.conf  
sudo nano  /etc/odoo/odoo.conf  
----to modify log conf-----  
logfile = /var/log/odoo/odoo.log  
logrotate = True  
------  
#####------ mkdir  log folder  
sudo mkdir /var/log/odoo  
sudo chown odoo:root /var/log/odoo  

########################################  
sudo su - odoo -s /bin/bash  
server/odoo-bin -c /etc/odoo/odoo.conf  

#################################################  
sudo cp ~/odoo-server /etc/init.d/odoo-server  

sudo chmod 755  /etc/init.d/odoo-server  
sudo chown root:  /etc/init.d/odoo-server  

################################################  
sudo /etc/init.d/odoo-server start  
sudo /etc/init.d/odoo-server stop  

##################################################  
sudo update-rc.d odoo-server defaults  
ps aux | grep odoo  




