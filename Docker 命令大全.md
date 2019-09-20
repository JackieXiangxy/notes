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



### 3、top



### 4、 attcach



### 5、events



### 6、logs



### 7、wait



### 8、export



### 9、port

















