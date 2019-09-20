#                                                                               docker中安装mysql  （基于centos7）

### 1.安装mysql

```shell
[root@localhost ~]# docker pull mysql     //从docker镜像中拉取mysql的镜像
```

### 2.启动mysql

```shell
[root@localhost ~]# docker run --name mysql01 -d mysql
```

启动以后查看mysql的启动情况，使用一下命令

```shell
[root@localhost ~]#  docker ps
CONTAINER ID     IMAGE     COMMAND     CREATED     STATUS      PORTS     NAMES
```

查看以后我们发现mysql并没有启动起来，继续使用 docker ps  -a 命令来查看所有的启动项

 ```shell
[root@localhost ~]#  docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                     PORTS               NAMES
7d2a1115405f        mysql               "docker-entrypoint..."   3 minutes ago       Exited (1) 3 minutes ago                       mysql01
 ```

此时发现服务并没有启动起来，而是已经被关掉了，所以这个时候就需要到日志中去查看发生了什么。继续使用命令 ：docker logs 7d2a1115405f    *7d2a1115405f*   为日志id，此处为msyql的 CONTAINER ID

```shell
[root@localhost ~]# docker logs 7d2a1115405f
error: database is uninitialized and password option is not specified 
  You need to specify one of MYSQL_ROOT_PASSWORD, MYSQL_ALLOW_EMPTY_PASSWORD and MYSQL_RANDOM_ROOT_PASSWORD

```

在日志中，可以看得出我们并没有指定mysql的密码

也就是说必须指定 MYSQL_ROOT_PASSWORD，MYSQL_ALLOW_EMPTY_PASSWORD ， MYSQL_RANDOM_ROOT_PASSWORD 这三个参数中的一个

> > > 可以到 hub docker  的镜像网站中查看 ,网址：<https://hub.docker.com/>

- ![avatar](D:\资料\笔记\docker_mysql_images\1565076277(1).jpg)

启动方式

![avatar](D:\资料\笔记\docker_mysql_images\1565076922(1).jpg)

也就是说，正常启动需要如下命令：

```shell
docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:tag
说明： --name  mysql的名称
	  -e 带参数
where some-mysql is the name you want to assign to your container, my-secret-pw is the password to be set for the MySQL root user and tag is the tag specifying the MySQL version you want. See the list above for relevant tags

```

也就说，我们需要先删除有问题的容器，继续我们的操作。

先将有问题的容器删除（命令格式: docker rm 容器id）

```
[root@localhost ~]# docker ps -a 
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                         PORTS               NAMES
7d2a1115405f        mysql               "docker-entrypoint..."   About an hour ago   Exited (1) About an hour ago                       mysql01
[root@localhost ~]# docker rm 7d2a1115405f
7d2a1115405f
```

现在，我们就可以正常启动一个容器了

##### 正常启动mysql

```shell
[root@localhost ~]# docker run  --name mysql01 -e MYSQL_ROOT_PASSWORD=admin -d mysql
1b74f7449e223b326bc999b0bef49b16054f8ddcb6fb576ac88ba9f02d946221
```

现在我们就已经可以正常启动mysql了，启动完成以我们来做测试就可以在navcat上对mysql进行连接。

但是在开始连接mysql之前，我们先需要做一下端口映射。

##### mysql端口映射

因为之前的端口没有做端口映射，所以不能通过外部的navcat进行连接

现在需要重新启动一个

```shell
[root@localhost ~]# docker ps        //查看所有端口
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
1b74f7449e22        mysql               "docker-entrypoint..."   6 minutes ago       Up 6 minutes        3306/tcp, 33060/tcp   mysql01
[root@localhost ~]# docker stop 1b74f7449e22    //将之前启动的容器删除
1b74f7449e22
[root@localhost ~]# docker run -p 3306:3306  --name mysql02  -e MYSQL_ROOT_PASSWORD=admin -d mysql     //正常启动一个新的容器   
d3dd9d12feebe521fd603a29f5095558980a195c3f9f7f1f1285b4122f121246
[root@localhost ~]# 
```

现在已经启动一个新的容器了。在这里我们要注意，**新启动的容器名称不能与已经存在的容器名称重复**，否则会报错。

```shell
[root@localhost ~]# docker ps -a 
CONTAINER ID        IMAGE            COMMAND                  CREATED             STATUS                PORTS                               NAMES
d3dd9d12feeb        mysql            "docker-entrypoint..."   3 minutes ago       Up 3 minutes          0.0.0.0:3306->3306/tcp, 33060/tcp   mysql02
1b74f7449e22        mysql            "docker-entrypoint..."   12 minutes ago      Exited (0) 5 minutes ago                                  mysql01
```

现在可以看到mysql02已经正常启动，并且已经将端口映射到3306端口中



### 3.测试连接

启动成功后用navcat测试一下是否正常启动即可

![avata](D:\资料\笔记\docker_mysql_images\1565078695(1).jpg)

现在可以看到可以正常连接mysql了



### 4.后记

更多高级操作详见

<https://hub.docker.com/_/mysql>

在使用docker的时候，我们要经常去 hub.docker.com这个网站

在成功启动mysql后，我们也可以同样的方法启动es 和rabbitmq等工具



