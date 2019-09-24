# [Docker 命令大全](https://www.runoob.com/docker/docker-command-manual.html)

## 一、容器生命周期管理

run start/stop/restart  kill rm pause/unpause create exec

### 1、run/create 

**docker run ：**创建一个新的容器并运行一个命令

**docker create ：**创建一个新的容器但不启动它

语法：

```shell
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
docker create [OPTIONS] IMAGE [COMMAND] [ARG...]
```

OPTIONS说明：

- **-a stdin:** 指定标准输入输出内容类型，可选 STDIN/STDOUT/STDERR 三项；

- **-d:** 后台运行容器，并返回容器ID；

- **-i:** 以交互模式运行容器，通常与 -t 同时使用；

- **-P:** 随机端口映射，容器内部端口**随机**映射到主机的高端口

- **-p:** 指定端口映射，格式为：**主机(宿主)端口:容器端口**

- **-t:** 为容器重新分配一个伪输入终端，通常与 -i 同时使用；

- **--name="nginx-lb":** 为容器指定一个名称；

- **--dns 8.8.8.8:** 指定容器使用的DNS服务器，默认和宿主一致；

- **--dns-search example.com:** 指定容器DNS搜索域名，默认和宿主一致；

- **-h "mars":** 指定容器的hostname；

- **-e username="ritchie":** 设置环境变量；

- **--env-file=[]:** 从指定文件读入环境变量；

- **--cpuset="0-2" or --cpuset="0,1,2":** 绑定容器到指定CPU运行；

- **-m :**设置容器使用内存最大值；

- **--net="bridge":** 指定容器的网络连接类型，支持 bridge/host/none/container: 四种类型；

- **--link=[]:** 添加链接到另一个容器；

- **--expose=[]:** 开放一个端口或一组端口；

- **--volume , -v:** 绑定一个卷

  

### 2、start/stop/restart

**docker start** :启动一个或多个已经被停止的容器

**docker stop** :停止一个运行中的容器

**docker restart** :重启容器

语法：

```shell
docker start [OPTIONS] CONTAINER [CONTAINER...]    //启动
docker stop [OPTIONS] CONTAINER [CONTAINER...]     //停止
docker restart [OPTIONS] CONTAINER [CONTAINER...]  //重启
```

### 3、kill

**docker kill** :杀掉一个运行中的容器。

语法

```shell
docker kill [OPTIONS] CONTAINER [CONTAINER...]
```

OPTIONS说明：

- **-s :**向容器发送一个信号

### 4、rm

**docker rm ：**删除一个或多少容器

语法

```shell
docker rm [OPTIONS] CONTAINER [CONTAINER...]
```

OPTIONS说明：

- **-f :**通过SIGKILL信号强制删除一个运行中的容器
- **-l :**移除容器间的网络连接，而非容器本身
- **-v :**-v 删除与容器关联的卷

### 5 、pause/unpause

语法

```shell
docker pause [OPTIONS] CONTAINER [CONTAINER...]

docker unpause [OPTIONS] CONTAINER [CONTAINER...]
```

### 6、exec 

**docker exec ：**在运行的容器中执行命令

语法

```shell
docker exec [OPTIONS] CONTAINER COMMAND [ARG...]
```

OPTIONS说明：

- **-d :**分离模式: 在后台运行
- **-i :**即使没有附加也保持STDIN 打开
- **-t :**分配一个伪终端

## 二、容器操作

ps inspect top attach events logs wait export port

### 1、ps 

**docker ps :** 列出容器

语法

```shell
docker ps [OPTIONS]
```

OPTIONS说明：

- **-a :**显示所有的容器，包括未运行的。

- **-f :**根据条件过滤显示的内容。

- **--format :**指定返回值的模板文件。

- **-l :**显示最近创建的容器。

- **-n :**列出最近创建的n个容器。

- **--no-trunc :**不截断输出。

- **-q :**静默模式，只显示容器编号。

- **-s :**显示总的文件大小。

  

### 2、inspect

**docker inspect :** 获取容器/镜像的元数据。

语法

```shell
docker inspect [OPTIONS] NAME|ID [NAME|ID...]
```

OPTIONS说明：

- **-f :**指定返回值的模板文件。
- **-s :**显示总的文件大小。
- **--type :**为指定类型返回JSON。



### 3、top

**docker top :**查看容器中运行的进程信息，支持 ps 命令参数。

语法

```shell
docker top [OPTIONS] CONTAINER [ps OPTIONS]
```

容器运行时不一定有/bin/bash终端来交互执行top命令，而且容器还不一定有top命令，可以使用docker top来实现查看container中正在运行的进程。



### 4、 attcach

**docker attach :**连接到正在运行中的容器。

语法

```shell
docker attach [OPTIONS] CONTAINER
```

要attach上去的容器必须正在运行，可以同时连接上同一个container来共享屏幕（与screen命令的attach类似）。官方文档中说attach后可以通过CTRL-C来detach，但实际上经过我的测试，如果container当前在运行bash，CTRL-C自然是当前行的输入，没有退出；如果container当前正在前台运行进程，如输出nginx的access.log日志，CTRL-C不仅会导致退出容器，而且还stop了。这不是我们想要的，detach的意思按理应该是脱离容器终端，但容器依然运行。好在attach是可以带上--sig-proxy=false来确保CTRL-D或CTRL-C不会关闭容器。



### 5、events

**docker events :** 从服务器获取实时事件

语法

```shell
docker events [OPTIONS]
```

OPTIONS说明：

- **-f ：**根据条件过滤事件；
- **--since ：**从指定的时间戳后显示所有事件;
- **--until ：**流水时间显示到指定的时间为止；



### 6、logs

**docker logs :** 获取容器的日志

语法

```shell
docker logs [OPTIONS] CONTAINER
```

OPTIONS说明：

- **-f :** 跟踪日志输出
- **--since :**显示某个开始时间的所有日志
- **-t :** 显示时间戳
- **--tail :**仅列出最新N条容器日志



### 7、wait

**docker wait :** 阻塞运行直到容器停止，然后打印出它的退出代码。

语法

```shell
docker wait [OPTIONS] CONTAINER [CONTAINER...]
```



### 8、export

**docker export :**将文件系统作为一个tar归档文件导出到STDOUT。

语法

```shell
docker export [OPTIONS] CONTAINER
```

OPTIONS说明：

- **-o :**将输入内容写到文件。



### 9、port

** docker port : **列出指定的容器的端口映射，或者查找将PRIVATE_PORT NAT到面向公众的端口。

语法

```shell
docker port [OPTIONS] CONTAINER [PRIVATE_PORT[/PROTO]]
```

















