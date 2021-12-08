# Linux-Environment
---

## 手把手带你搭建Linux各种环境

---

### 首先搭建一个虚拟机（基于centos7）

1. 下载一个镜像

![镜像](/img/jx.png)

2. 下载一个虚拟机（VMware是一个收费软件可以自己在网上找许可证输入即可我用的是）

![虚拟机](/img/xnj.png)

3. 虚拟机里面安装镜像（傻瓜式安装）

- 这里推荐如果内存够的话分配2048mb的内存

![安装指南](/img/安装指南.png)

4. 等待安装是一个漫长的过程

![等待](/img/等待ing.png)

5. 开始界面

![开始](/img/start.png)

6. 首先我们配置网络（这个和你本地网卡有关）

- 使用root用户打开/etc/sysconfifig/network-scripts/ifcfg-eno16777736文件，添加内容如下：

  ```
  BOOTPROTO=static
  ONBOOT=yes
  IPADDR=192.168.72.128 
  GATEWAY=192.168.72.2
  NETMASK=255.255.255.0
  NETMASK=255.255.255.0 DNS1=114.114.114.114
  ```

- 目的是可以使用xshell连接linux我们直接通过xshell来操作linux

  ![配置网络成功](/img/配置网络成功.png)

7. 你得搞明白linux系统目录有些啥

![linux目录](/img/linux目录.png)

8. 下载xftp用于文件传输

   ![xftp](/img/xftp.png)



---

### JDK->Tomcat->MySql 

#### JDK

- 解压

  ![](/img/jdk1.png)

- 转移到usr/  改名 

  ![](/img/jdk3.png)

  

- 配置环境变量

  ![](/img/jdk2.png)

- 检查是否成功

- ![](/img/jdk6.png)

#### Tomcat

永久关闭防火墙

> 1:查看防火状态
>
> systemctl status firewalld
>
> service  iptables status
>
> 2:暂时关闭防火墙
>
> systemctl stop firewalld
>
> service  iptables stop
>
> 3:永久关闭防火墙
>
> systemctl disable firewalld
>
> chkconfig iptables off
>
> 4:重启防火墙
>
> systemctl enable firewalld
>
> service iptables restart  
>
> 5:永久关闭后重启
>
> //暂时还没有试过
>
> chkconfig iptables on
> 

- 解压

  ![](/img/tomcat1.png)

- 移动以及配置文件

  ![](/img/tomcat3.png)

- 配置环境变量

- ![](/img/tomcat2.png)

#### MySql

- 网络下载包

  ![](/img/mysql1.png)

- 解析包

  ![](/img/mysql2.png)

- 安装包

  ![](/img/mysql3.png)

- 启动并且查询是否启动成功

  ![](/img/mysql4.png)

- 远程连接（各种问题）

  - vi /etc/my.cnf 加入一行skip-grant-tables 跳过验证 忽略授权表 然后Mysql-u第一个修改密码 第二修改权限

  ![](/img/mysql5.png)

  ![](/img/mysql6.png)



---

### Dubbo->Zookeeper->Redis->FastDfS->RabbitMQ

#### Redis

- 安装
 ![](./img/redis1.png)

-  后台运行

  ![](./img/redis2.png)

- 关闭数据库

  ![](./img/redis3.png)

- 监听以及连接

  ![](./img/redis4.png)

- 成功

  ![](./img/redis5.png)






---

### Kafka

---

### Docker



