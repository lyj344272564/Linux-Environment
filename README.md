# Linux-Environment
---

## 手把手带你搭建Linux各种环境

---

### 首先搭建一个虚拟机（基于centos7）

1. 下载一个镜像

![镜像](./img/jx.png)

2. 下载一个虚拟机（VMware是一个收费软件可以自己在网上找许可证输入即可我用的是）

![虚拟机](./img/xnj.png)

3. 虚拟机里面安装镜像（傻瓜式安装）

- 这里推荐如果内存够的话分配2048mb的内存

![安装指南](./img/安装指南.png)

4. 等待安装是一个漫长的过程

![等待](./img/等待ing.png)

5. 开始界面

![开始](./img/start.png)

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

- 之后service network restart(重启网络)

- 目的是可以使用xshell连接linux我们直接通过xshell来操作linux

  ![配置网络成功](./img/配置网络成功.png)

7. 你得搞明白linux系统目录有些啥

![linux目录](./img/linux目录.png)

8. 下载xftp用于文件传输

   ![xftp](./img/xftp.png)



---

### JDK->Tomcat->MySql 

#### JDK

- 解压

  ![](./img/jdk1.png)

- 转移到usr/  改名 

  ![](./img/jdk3.png)

  

- 配置环境变量     使用root用户打开配置文件/etc/profifile，向文件末尾追加内容如下：

  ![](./img/jdk2.png)

-  保存退出后让文件生效并验证是否配置成功  source /etc/profil

- 检查是否成功 

- ![](./img/jdk6.png)

在云服务器中，只这样配置是不行的，会报一下错误，是因为缺少环境导致的

![image-20220502204045297](D:\github\Linux-Environment\image-20220502204045297.png)

````java
运行这个就可以解决sudo yum install glibc.i686
````



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

  ![](./img/tomcat1.png)

- 移动以及配置文件

  ![](./img/tomcat3.png)

- 配置环境变量

- ![](./img/tomcat2.png)

#### MySql

- 网络下载包

  ![](./img/mysql1.png)

- 解析包

  ![](./img/mysql2.png)

- 安装包

  ![](./img/mysql3.png)

- 启动并且查询是否启动成功

  ![](./img/mysql4.png)

- 远程连接（各种问题）

  - vi /etc/my.cnf 加入一行skip-grant-tables 跳过验证 忽略授权表 然后Mysql-u第一个修改密码 第二修改权限

  ![](./img/mysql5.png)

  ![](./img/mysql6.png)

在云服务器安装MYSQL8的时候，会出现以下问题：

**解决Mysql8密码验证方式**

````java
mysql 8.0 默认使用 caching_sha2_password 身份验证机制 —— 从原来的 mysql_native_password 更改为 caching_sha2_password。
从 5.7 升级 8.0 版本的不会改变现有用户的身份验证方法，但新用户会默认使用新的 caching_sha2_password 。
客户端不支持新的加密方式。
````

在docker中登录mysql

1. 进入数据库：mysql -uroot -p

   ````mysql
   mysql -u root -p
   ````

2. 设置密码 123456 永不过期：

   ````mysql
   ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY '123456';
   ````

3. 刷新权限：FLUSH PRIVILEGES;

   ````mysql
   FLUSH PRIVILEGES;
   ````

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

![img](D:\github\Linux-Environment\1.png)

---

### Docker

````java
yum install -y docker

````

![image-20220511163847699](D:\github\Linux-Environment\image-20220511163847699.png)

````java
docker run -d --name zookeeper -p 2181:2181 -v /etc/localtime:/etc/localtime wurstmeister/zookeeper

    
 docker run  -d --name kafka -p 9092:9092 -e KAFKA_BROKER_ID=0 -e KAFKA_ZOOKEEPER_CONNECT=10.9.44.11:2181 -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://10.9.44.11:9092 -e KAFKA_LISTENERS=PLAINTEXT://0.0.0.0:9092 -t wurstmeister/kafka


````

如何用tomcat跑一个SpringBoot项目

![image-20220517163321187](D:\github\Linux-Environment\image-20220517163321187.png)

````java
war包、

````

![image-20220517163406077](D:\github\Linux-Environment\image-20220517163406077.png)

````java
1.解压zip文件：unzip -d /解压后放在那个路径  xx.zip
如果提示没有这个命令  那么需要安装unzip这个环境
2.mvn clean package -Dmaven.test.skip=true
````

有了这个target

![image-20220517163532386](D:\github\Linux-Environment\image-20220517163532386.png)

把ROOT.war移动到tomcat的webapps下

![image-20220517163709801](D:\github\Linux-Environment\image-20220517163709801.png)