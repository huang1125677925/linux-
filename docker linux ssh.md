## 目的

买了一个华为的服务器，因为在香港，ssh连接的时候，网络经常非常慢，而且使用起来经常卡顿；

于是乎，就想在自己的物理机上搭建一个容器化的乌班图，然后开启ssh服务，可以在本机上通过ssh连接

但是通过容器化方法来这样使用linux操作系统，存在部分问题，比如目前systemd不能使用；



## 步骤

1. 

   ```
   docker pull ubuntu 
   ```

2. 下载完成后，可以输入

   ```
   docker images
   ```

   查看是否已经下载镜像到本地

3. 启动一个ubuntu容器，进入bash，

   ```
   docker run -it ubuntu /bin/bash，
   ```

4. 此时应该可以看到 root@bc6a0a7912b1:/# ，证明已经成功开动了容器，并且进入容器的bash

5. 修改容器的root密码：passwd， 直至输入新的密码，例如：123456

6. 安装vim，

   ```
   apt-get install vim -y
   ```

7. 安装容器的openssh-server，输入 

   ```
   apt-get install openssh-server -y
   ```

8. 成功安装后，

   ```
   vim /etc/ssh/sshd_config
   ```

   ，修改下面两个配置

   PermitRootLogin yes  
   UsePAM no

9. 启动ssh服务，

   ```
   service ssh start
   ```

10. 退出容器，输入exit，然后输入

    ```
    docker ps -a
    ```

    查看容器的ID

11. 提交容器成为新的镜像，例如叫做ubuntu-ssh，输入

    ```
    docker commit 容器ID ubuntu-ssh
    ```

12. 启动这个镜像的容器，并映射本地的一个闲置的端口（例如10000）到容器的22端口，并启动容器的ssh d

    ```
    docker run -d -p 10000:22 ubuntu-ssh /usr/sbin/sshd -D
    ```

13. 现在打开新的终端，输入

    ```
    ssh root@127.0.0.1 -p 10000
    ```

    ，如果能链接成功，会要求输入密码的，输入刚才的123456就可以进入容器的终端了

## 安装vim 

在使用docker容器时，有时候里边没有安装vim，敲vim命令时提示说：vim: command not found，这个时候就需要安装vim，可是当你敲apt-get install vim命令时，提示：

```
 Reading package lists... Done
    Building dependency tree    
    Reading state information... Done
    E: Unable to locate package vim
```

 这时候需要敲：apt-get update，这个命令的作用是：同步 /etc/apt/sources.list 和 /etc/apt/sources.list.d 中列出的源的索引，这样才能获取到最新的软件包。

等更新完毕以后再敲命令：apt-get install vim命令即可。

