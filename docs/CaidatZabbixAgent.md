# Hướng dẫn cài đặt Zabbix Agent
-----------------------------------------------------------
# Mục lục
## [I. Giới thiệu](#gt)
## [II. Cài đặt Zabbix Agent](#cd)
### [2.1 Cài đặt Zabbix Agent trên Ubuntu 16.04/14.04 và Debian 8/7](#21)
### [2.2 Cài đặt Zabbix Agent trên Centos 7/6/5](#22)
### [2.3 Add Host trên Zabbix Server](#23)

<a name=gt></a>
## I. Giới thiệu

Cài đặt Zabbix Agent trên tất cả hệ thống từ xa là việc cần thiết để giám sát thông qua Zabbix server. Zabbix Agent thu thập các nguồn tài nguyên sử dụng và các dữ liệu ứng dụng trên hệ thống máy khách và cung cấp một số thông tin tới Zabbix server trên những yêu cầu của Zabbix Server.

Có 2 loại cấu hình kiểm tra giữa Zabbix Server và Zabbix Agent :
- Passive Check : Zabbix Agent chỉ gửi những dữ liệu đến Zabbix Server khi Zabbix Server có yêu cầu.
- Active Check : Zabbix Agent tự động gửi dữ liệu định kì tới Zabbix Server.

Sau khi cài đặt Zabbix Server trên hệ thống của bạn, chúng ta tiến hành cài đặt Zabbix Agent lên các hệ thống cần giám sát, sau đó tiến hành thêm các hệ thống đó trên Zabbix Server.

<a name=cd></a>
## II. Cài đặt Zabbix Agent

<a name=21></a>
### 2.1 Cài đặt Zabbix Agent trên Ubuntu 16.04/14.04 và Debian 8/7

- Bước 1 : Add Apt Repository

```

For Ubuntu 16.04 LTS:
$ wget http://repo.zabbix.com/zabbix/3.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_3.0-1+xenial_all.deb
$ sudo dpkg -i zabbix-release_3.0-1+xenial_all.deb
$ sudo apt update

For Ubuntu 14.04 LTS:

$ wget http://repo.zabbix.com/zabbix/3.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_3.0-1+trusty_all.deb
$ sudo dpkg -i zabbix-release_3.0-1+trusty_all.deb
$ sudo apt-get update

For Ubuntu 12.04 LTS:

$ wget http://repo.zabbix.com/zabbix/2.2/ubuntu/pool/main/z/zabbix-release/zabbix-release_2.2-1+precise_all.deb
$ sudo dpkg -i zabbix-release_2.2-1+precise_all.deb
$ sudo apt-get update

For Debian 8:

$ wget http://repo.zabbix.com/zabbix/3.0/debian/pool/main/z/zabbix-release/zabbix-release_3.0-1+jessie_all.deb
$ sudo dpkg -i zabbix-release_3.0-1+jessie_all.deb
$ sudo apt-get update


For Debian 7:

$ http://repo.zabbix.com/zabbix/3.0/debian/pool/main/z/zabbix-release/zabbix-release_3.0-1+wheezy_all.deb
$ sudo dpkg -i zabbix-release_3.0-1+wheezy_all.deb
$ sudo apt-get update

```

- Bước 2 : Cài đặt Zabbix Agent

Sau khi đã thêm các Reponsiroty , chúng ta tiến hành cài Zabbix Agent

```
$ sudo apt-get install zabbix-agent

```

- Bước 3 : Chỉnh sửa các thông số trong tệp tin cấu hình

Sau khi cài đặt Zabbix Agent , chúng ta tiến hành chỉnh sửa file cấu hình tại `/etc/zabbix/zabbix_agentd.conf` để cập nhật địa chỉ Zabbix Server và Hostname Zabbix Agent .

```
#Server=[zabbix server ip]
#Hostname=[Hostname of client system ]

Server=172.16.69.163
Hostname=ubuntu
```
- Bước 4 : Khởi động lại dịch vụ Zabbix Agent

Sau khi chỉnh sửa cấu hình thành công, chúng ta tiến hành khởi động lai dịch vụ Zabbix Agent để cập nhật lại cấu hình.

```
# /etc/init.d/zabbix-agent restart

hoặc

# /etc/init.d/zabbix-agent start
# /etc/init.d/zabbix-agent stop

```

Việc cấu hình tại máy cần giám sát dừng tại đây.Tiến hành Add host tại Zabbix Server.

<a name=22></a>
## 2.2 Cài đặt Zabbix Agent trên Centos 7/6/5

- Bước 1 : Add Required Repository

```
CentOS/RHEL 7:
# rpm -Uvh http://repo.zabbix.com/zabbix/3.0/rhel/7/x86_64/zabbix-release-3.0-1.el7.noarch.rpm

CentOS/RHEL 6:
# rpm -Uvh http://repo.zabbix.com/zabbix/3.0/rhel/6/x86_64/zabbix-release-3.0-1.el6.noarch.rpm

CentOS/RHEL 5:
# rpm -Uvh http://repo.zabbix.com/zabbix/3.0/rhel/5/x86_64/zabbix-release-3.0-1.el5.noarch.rpm

```

- Bước 2 : Cài đặt Zabbix Agent

Sau khi thêm các Repository bắt buộc, chúng ta tiến hành cài Zabbix Agent lên các hệ thống cần giám sát.

```
# yum install zabbix zabbix-agent
```

- Bước 3 : Chỉnh sửa file cấu hình Zabbix Agent tại `/etc/zabbix/zabbix_agentd.conf` để cập nhật địa chỉ Zabbix Server và hostname Zabbix Agent.

```
#Server=[zabbix server ip]
#Hostname=[ Hostname of client system ]

Server=172.16.69.163
Hostname=centos
```

- Bước 4 : Khởi động lại dịch vụ Zabbix Agent

Sau khi chỉnh sửa các cấu hình cho Zabbix Agent , Cần khởi động lại dịch vụ để cập nhật lại các cấu hình.

```
# /etc/init.d/zabbix-agent restart

 hoặc

# /etc/init.d/zabbix-agent stop
# /etc/init.d/zabbix-agent start

```

<a name=23></a>
### 2.3 Add Host trên Zabbix Server

Sau khi đã thiết lập và cài đặt các thông số trên các Zabbix Agent , chúng ta tiến hành thêm các host đó trên Zabbix Server để tiến hành giám sát.

- Tại giao diện Dashboard của Zabbix server

![za](/images/config.png)

- Chọn Tab `Config`/`Hosts`

![za](/images/confighost.png)

- Chọn Tab `Create host` phía trên bên phải :

Giao diện Create Host hiện ra

![za](/images/hostcreat.png)

Ví dụ mình thêm 1 host Ubuntu 1604, có địa chỉ IP là 172.16.69.160 có hostname là kma. Ta tiến hành điền các thông số như sau :

![za](/images/hostkma.png)

- Sau khi đã thêm host thành công, tiến hành kết nối đến các Template để  thu thập các thông tin từ thiết bị cần giám sát.

![za](/images/hosttemplate.png)

- Sau khi thêm Template ,trạng thái Host sẽ như sau :

![za](/images/hostaddsuccess.png)

Vậy là chúng ta đã tiến hành thêm 1 host ubuntu thành công, Các phiên bản khác tương tự như vậy.
