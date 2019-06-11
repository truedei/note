# 三、Docker

## 1、安装Docker步骤

```sh
1、检查内核版本，必须为3.0以上
[root@izm5e2w1juq9pmq37ceyvbz ~]# uname -r
3.10.0-693.2.2.el7.x86_64
2、安装
[root@izm5e2w1juq9pmq37ceyvbz ~]# 
[root@izm5e2w1juq9pmq37ceyvbz ~]# yum -y install docker
3、启动Docker
[root@izm5e2w1juq9pmq37ceyvbz ~]# systemctl start docker
4、查看Docker的版本
[root@izm5e2w1juq9pmq37ceyvbz ~]# docker -v
Docker version 1.13.1, build 07f3374/1.13.1
5、开机启动Docker
[root@izm5e2w1juq9pmq37ceyvbz ~]# systemctl enable docker
Created symlink from /etc/systemd/system/multi-user.target.wants/docker.service to /usr/lib/systemd/system/docker.service.
6、停止Docker
[root@izm5e2w1juq9pmq37ceyvbz ~]# systemctl stop docker


```

## 2、常用操作

### 1、镜像操作

| 操作 | 命令                                              | 说明                                                         |
| ---- | :------------------------------------------------ | ------------------------------------------------------------ |
| 检索 | docker  serch 关键字<br />eg: docker search mysql | 检索应用。也可以去[docker hub](https://hub.docker.com/)上检索镜像的详细信息。 |
| 拉取 | docker pull 镜像名:tag                            | :tag是可选的，tag表示标签，多为软件的版本，默认是latest      |
| 列表 | docker images                                     | 查看所有本地镜像                                             |
| 删除 | docker rmi image-id                               | 删除指定的本地镜像                                           |

#### 1、检索：

```shell
[root@izm5e2w1juq9pmq37ceyvbz ~]# docker search mysql
INDEX       NAME    DESCRIPTION    STARS    OFFICIAL   AUT

INDEX:索引      
NAME:镜像的名字（看斜杠后面的就行） 
DESCRIPTION:镜像的描述  
STARS:有多少人关注了这个镜像（以k为单位） 
OFFICIAL:是不是官方发布的  
AUT:是不是自动化配置的

```

#### 2、拉取(下载数据)

##### #1、使用默认的tag标签，拉取mysql数据。

```shell
[root@izm5e2w1juq9pmq37ceyvbz ~]# docker pull mysql
Using default tag: latest  #latest是默认的标签呢
Trying to pull repository docker.io/library/mysql ... 
latest: Pulling from docker.io/library/mysql
5e6ec7f28fb7: Pull complete 
4140e62498e1: Pull complete 
e7bc612618a0: Pull complete 
1af808cf1124: Pull complete 
ff72a74ebb66: Pull complete 
3a28cb03e3dc: Pull complete 
2b52dda3bd7d: Pull complete 
dc89e81122ad: Pull complete 
ecba98b7a588: Pull complete 
109b011a27be: Pull complete 
5f380f98ab52: Pull complete 
cdda841f5c5c: Pull complete 
Digest: sha256:048c2c616866c47c8a9fb604548d32ce842be292b56fba3d90fc07e0e143dac4
Status: Downloaded newer image for docker.io/mysql:latest
[root@izm5e2w1juq9pmq37ceyvbz ~]# 

		
```

##### #2、使用已知的tag标签，拉取mysql数据

#1)、先到https://hub.docker.com
#2)、输入要查询的镜像，例如：mysql

![1549297499945](typora-user-images\1549297499945.png)

#3)、点击需要的镜像

![1549297680548](typora-user-images\1549297680548.png)

#4)、选择所需要的tag标签

![1549297817581](typora-user-images\1549297817581.png)

#5)、拉取数据

例如：拉取mysql为5.5版本的数据

```shell
[root@izm5e2w1juq9pmq37ceyvbz ~]# docker pull mysql:5.5
Trying to pull repository docker.io/library/mysql ... 
5.5: Pulling from docker.io/library/mysql
5e6ec7f28fb7: Already exists 
4140e62498e1: Already exists 
e7bc612618a0: Already exists 
1af808cf1124: Already exists 
ff72a74ebb66: Already exists 
852cfe5dca55: Pull complete 
e27e60fa86d5: Pull complete 
ab7c1c7d8dd6: Pull complete 
bb9fcaf41441: Pull complete 
0c4bda3739a6: Pull complete 
e22ee1bc1b20: Pull complete 
Digest: sha256:0510ece613362e5d91ee9eb28db30a588c04117ae8c59ec31a5981f83e8e9d13
Status: Downloaded newer image for docker.io/mysql:5.5
```



#### 3、查看docker本地所有的镜像

```shell
[root@izm5e2w1juq9pmq37ceyvbz ~]# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
docker.io/mysql     5.5                 2ffcfa755f19        12 days ago         205 MB
docker.io/mysql     latest              71b5c7e10f9b        12 days ago         477 MB
[root@izm5e2w1juq9pmq37ceyvbz ~]# 
```

#### 4、删除已有的镜像

```shell
[root@izm5e2w1juq9pmq37ceyvbz ~]# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
docker.io/mysql     5.5                 2ffcfa755f19        12 days ago         205 MB
docker.io/mysql     latest              71b5c7e10f9b        12 days ago         477 MB
[root@izm5e2w1juq9pmq37ceyvbz ~]# 
[root@izm5e2w1juq9pmq37ceyvbz ~]# docker rmi 2ffcfa755f19
Untagged: docker.io/mysql:5.5
Untagged: docker.io/mysql@sha256:0510ece613362e5d91ee9eb28db30a588c04117ae8c59ec31a5981f83e8e9d13
Deleted: sha256:2ffcfa755f192485577ce54816e5a5fc38b880eff31c0dc2ce9a425730e8e351
Deleted: sha256:b439e68db56fc1ca79409e978e19443641cb63ddfef1f0129c4d7b1af7e77386
Deleted: sha256:f6e12603450f563cbb2e4979b3afab9ab8314005fb5712e327225686c4369bb4
Deleted: sha256:5e6e2a28d59a931e3c0d82fb35731bac997eb7c0134ab2b7af2eb292261b1122
Deleted: sha256:4a6e35c63f532934bf456bc819d6257e908e9c80259585a3b498a2e9ed70bcd1
Deleted: sha256:f2c9078a7321c7087b31e48f59b503d935e74fb670970a5166b430a3298ae2db
Deleted: sha256:c5cda0da6c45607d3e832f96841eb1764f0897abdf273634089a20347be47e98
[root@izm5e2w1juq9pmq37ceyvbz ~]# 
[root@izm5e2w1juq9pmq37ceyvbz ~]# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
docker.io/mysql     latest              71b5c7e10f9b        12 days ago         477 MB
[root@izm5e2w1juq9pmq37ceyvbz ~]# 
```

## 3、容器操作

常用的：

| 操作     | 命令                                                         | 说明                                                         |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 运行     | docker run --name container-name -d image-name<br />eg:docker run -name myredis -d redis | --name:自定义容器名<br />-d:后台运行<br />image-name:指定镜像模板 |
| 列表     | docker ps(查看运行中的容器)                                  | 加上-a；可以查看所有的容器                                   |
| 停止     | docker stop container-name/container-id                      | 停止当前你运行的容器                                         |
| 启动     | docker start container-name/container-id                     | 启动容器                                                     |
| 删除     | docker rm  container-id                                      | 删除指定容器                                                 |
| 端口映射 | -p 6379:6379<br />eg:docker run -d -p 6379:6379 --name myredis docker.io/redis | -p:主机端口（映射到）容器内部的端口                          |
| 容器日志 | docker  logs  container-name/container-id                    |                                                              |
| 更多命令 | https://docs.docker.com/engine/reference/commandline/docker/ |                                                              |



软件镜像（QQ的安装程序）......运行镜像.....产生一个容器（正在运行的软件，运行的QQ）；



步骤：

1、搜索镜像

```shell
[root@izm5e2w1juq9pmq37ceyvbz ~]# docker search tomcat
```

2、拉取镜像

```shell
[root@izm5e2w1juq9pmq37ceyvbz ~]# docker pull tomcat
```

3、查看已知的容器

```shell
[root@izm5e2w1juq9pmq37ceyvbz ~]# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
docker.io/tomcat    latest              7ee26c09afb3        12 days ago         462 MB
docker.io/mysql     latest              71b5c7e10f9b        12 days ago         477 MB
[root@izm5e2w1juq9pmq37ceyvbz ~]#
```

4、运行容器

```shell
[root@izm5e2w1juq9pmq37ceyvbz ~]# docker run --name mytomcat -d tomcat:latest
20fa4ca33dcdc3656c91983bcf76c07621066cff554a1f50c181c3ef08c7b43c
[root@izm5e2w1juq9pmq37ceyvbz ~]# 
```

5、查看正在运行的所有的容器

```shell
[root@izm5e2w1juq9pmq37ceyvbz ~]# docker ps
CONTAINER ID  IMAGE  COMMAND  CREATED    STATUS     PORTS        NAMES
20fa4ca33dcd  tomcat:latest  "catalina.sh run"  2 minutes ago  Up 2 minutes 8080/tcp  mytomcat
[root@izm5e2w1juq9pmq37ceyvbz ~]# 
```

6、停止运行中的容器

```shell
[root@izm5e2w1juq9pmq37ceyvbz ~]# 
[root@izm5e2w1juq9pmq37ceyvbz ~]# docker stop 20fa4ca33dcd
20fa4ca33dcd
[root@izm5e2w1juq9pmq37ceyvbz ~]# docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
[root@izm5e2w1juq9pmq37ceyvbz ~]# 
```

7、查看所有的容器的状态

```shell
[root@izm5e2w1juq9pmq37ceyvbz ~]# docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                        PORTS               NAMES
20fa4ca33dcd        tomcat:latest       "catalina.sh run"   4 hours ago         Exited (143) 18 seconds ago                       mytomcat
[root@izm5e2w1juq9pmq37ceyvbz ~]# 
```

8、删除

```shell
[root@izm5e2w1juq9pmq37ceyvbz ~]# docker rm 20fa4ca33dcd 
20fa4ca33dcd
[root@izm5e2w1juq9pmq37ceyvbz ~]# docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
[root@izm5e2w1juq9pmq37ceyvbz ~]# 
```

9、启动一个做了端口映射的tomcat

```shell
[root@izm5e2w1juq9pmq37ceyvbz ~]# docker run -d -p 8888:8080 tomcat
7e90ece93835100ab3a05d8dd34a580bba7d838a8dca2741a97081cf6123aa70
[root@izm5e2w1juq9pmq37ceyvbz ~]# 

-d:后台运行
-p:将主机的端口映射到容器的一个端口   主机端口：容器端口

[root@izm5e2w1juq9pmq37ceyvbz ~]# netstat -ntpl |grep 8888
tcp6       0      0 :::8888                 :::*                    LISTEN      12365/docker-proxy- 
[root@izm5e2w1juq9pmq37ceyvbz ~]# 
```

10、查看容器日志

```shell
[root@izm5e2w1juq9pmq37ceyvbz ~]# docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS                    NAMES
7e90ece93835        tomcat              "catalina.sh run"   2 minutes ago       Up 2 minutes        0.0.0.0:8888->8080/tcp   nifty_wescoff
[root@izm5e2w1juq9pmq37ceyvbz ~]# 
[root@izm5e2w1juq9pmq37ceyvbz ~]# docker logs 7e90ece93835
```

## 4、Docker安装Mysql

### 1、错误的启动方式：

```shell
1、查看所有的镜像
[root@izm5e2w1juq9pmq37ceyvbz ~]# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
docker.io/tomcat    latest              7ee26c09afb3        13 days ago         462 MB
docker.io/mysql     latest              71b5c7e10f9b        13 days ago         477 MB
[root@izm5e2w1juq9pmq37ceyvbz ~]# 
[root@izm5e2w1juq9pmq37ceyvbz ~]# 

2、运行mysql
[root@izm5e2w1juq9pmq37ceyvbz ~]# docker run --name mysql -d -p 80:8080 mysql
1c178a4b747a87044b058fe7cda3a70ad19e22c8b6e30f3551fd18c0a9648366
[root@izm5e2w1juq9pmq37ceyvbz ~]# 

3、查看所有的镜像的状态
[root@izm5e2w1juq9pmq37ceyvbz ~]# docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                      PORTS               NAMES
1c178a4b747a        mysql               "docker-entrypoint..."   11 seconds ago      Exited (1) 10 seconds ago                       mysql
[root@izm5e2w1juq9pmq37ceyvbz ~]# 

4、查看日志（错误日志）
在运行中没有指定密码
[root@izm5e2w1juq9pmq37ceyvbz ~]# docker logs 1c178a4b747a
error: database is uninitialized and password option is not specified 
  You need to specify one of MYSQL_ROOT_PASSWORD, MYSQL_ALLOW_EMPTY_PASSWORD and MYSQL_RANDOM_ROOT_PASSWORD
[root@izm5e2w1juq9pmq37ceyvbz ~]# 

MYSQL_ROOT_PASSWORD：mysql数据的root用户的密码
MYSQL_ALLOW_EMPTY_PASSWORD：mysql数据库允许空密码
MYSQL_RANDOM_ROOT_PASSWORD：
必须是这三个中的一个


```

### 2、正确的启动：

如果有问题就先删掉，重新配置

正确的启动mysql的步骤：

做了端口映射的启动mysql

```shell
[root@izm5e2w1juq9pmq37ceyvbz ~]# 
[root@izm5e2w1juq9pmq37ceyvbz ~]# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
docker.io/tomcat    latest              7ee26c09afb3        13 days ago         462 MB
docker.io/mysql     5.5                 2ffcfa755f19        13 days ago         205 MB
docker.io/mysql     latest              71b5c7e10f9b        13 days ago         477 MB
[root@izm5e2w1juq9pmq37ceyvbz ~]# 
[root@izm5e2w1juq9pmq37ceyvbz ~]# 
[root@izm5e2w1juq9pmq37ceyvbz ~]# docker run --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 -d mysql:5.5
a1cf4de79a4cda467333448361736f35ea194df576f021c53dd3e32326724094
[root@izm5e2w1juq9pmq37ceyvbz ~]# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
docker.io/tomcat    latest              7ee26c09afb3        13 days ago         462 MB
docker.io/mysql     5.5                 2ffcfa755f19        13 days ago         205 MB
docker.io/mysql     latest              71b5c7e10f9b        13 days ago         477 MB
[root@izm5e2w1juq9pmq37ceyvbz ~]# docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                    NAMES
a1cf4de79a4c        mysql:5.5           "docker-entrypoint..."   5 seconds ago       Up 4 seconds        0.0.0.0:3306->3306/tcp   mysql
[root@izm5e2w1juq9pmq37ceyvbz ~]#
```

链接测试：

![1549366741260](typora-user-images\1549366741260.png)



几个其他的高级操作：

```shell
docker run --name mysql-01 -v /my/custom:/etc/mysql/conf.d -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:tag
把筑基的/my/custom文件夹挂在到mysql Docker容器/etc/mysql/conf.d文件夹里面
改mysql的配置文件，就需要把配置文件放在/my/custom下就好了
```

