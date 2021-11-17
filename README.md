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
7. 

   

   

   

---

### JDK->Tomcat->MySql 

---

### Dubbo->Zookeeper->Redis->FastDfS->RabbitMQ

---

### Kafka

---

### Docker



