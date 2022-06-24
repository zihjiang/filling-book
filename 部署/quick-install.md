# docker部署

## 先决条件

- [Docker](https://docs.docker.com/engine/install/) 1.13.1+
- [Docker Compose](https://docs.docker.com/compose/) 1.11.0+

## 如何使用 Docker 镜像

有 2 种方式可以快速试用 Filling

### 一、docker-compose 的方式启动 Filling(推荐)

这种方式需要先安装 [docker-compose](https://docs.docker.com/compose/), docker-compose 的安装网上已经有非常多的资料，请自行安装即可

对于 Windows 7-10，你可以安装 [Docker Toolbox](https://github.com/docker/toolbox/releases)。对于 Windows 10 64-bit，你可以安装 [Docker Desktop](https://docs.docker.com/docker-for-windows/install/)，并且注意[系统要求](https://docs.docker.com/docker-for-windows/install/#system-requirements)

#### 0、请配置内存不少于 4GB

对于 Mac 用户，点击 `Docker Desktop -> Preferences -> Resources -> Memory`

对于 Windows Docker Toolbox 用户，有两项需要配置：

- **内存**：打开 Oracle VirtualBox Manager，如果你双击 Docker Quickstart Terminal 并成功运行 Docker Toolbox，你将会看到一个名为 `default` 的虚拟机. 点击 `设置 -> 系统 -> 主板 -> 内存大小`
- **端口转发**：点击 `设置 -> 网络 -> 高级 -> 端口转发 -> 添加`. `名称`，`主机端口` 和 `子系统端口` 都填写 `12345`，不填 `主机IP` 和 `子系统IP`

对于 Windows Docker Desktop 用户

- **Hyper-V 模式**：点击 `Docker Desktop -> Settings -> Resources -> Memory`
- **WSL 2 模式**：参考 [WSL 2 utility VM](https://docs.microsoft.com/zh-cn/windows/wsl/wsl-config#configure-global-options-with-wslconfig)

### 1、编译文件docker-compose.yml

```yml
version: '2.2'
services:
  filling:
    image: zihjiang/filling:latest
    container_name: filling
    depends_on:
      - jobmanager
      - taskmanager
#     volumes:
#       - ./data/db:/home/filling/target/h2db/db
    environment:
      - _JAVA_OPTIONS=-Xmx1g -Xms1g
      - JHIPSTER_SLEEP=10 # gives time for the JHipster Registry to boot before the application
      - SPRING_PROFILES_ACTIVE=docker
      - application_flink_url=http://jobmanager:8081
    ports:
      - "8080:8080"
  jobmanager:
    image: flink:1.14.3-scala_2.11-java11
    ports:
      - "8081:8081"
    command: jobmanager
    environment:
      - |
        FLINK_PROPERTIES=
        jobmanager.rpc.address: jobmanager
  taskmanager:
    image: flink:1.14.3-scala_2.11-java11
    depends_on:
      - jobmanager
    command: taskmanager
    scale: 4
    environment:
      - |
        FLINK_PROPERTIES=
        jobmanager.rpc.address: jobmanager
        taskmanager.numberOfTaskSlots: 3
```

### 2、 启动

```shell
docker-compose up -d
```

或

#### 1、下载源码包

请下载源码包 filling，下载地址: [下载](https://github.com/zihjiang/filling)

#### 2、拉取镜像并启动服务

> 对于 Mac 和 Linux 用户，打开 **Terminal** 对于 Windows Docker Toolbox 用户，打开 **Docker Quickstart Terminal** 对于 Windows Docker Desktop 用户，打开 **Windows PowerShell**

```shell
$ unzip filling.zip
$ cd filling
$ mvn install -DskipTests
$ docker-compose  -f app.yml up -d --build
```
