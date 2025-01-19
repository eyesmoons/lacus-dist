## 一、目录结构

lacus-docker目录结构如下，将所需的包放入对应位置即可

```shell
lacus-docker/
├── docker-compose.yaml                                        # 容器编排配置文件
├── README.md                                                  # 使用说明文档
│
├── flink/                                                     # Flink 服务
│   ├── Dockerfile
│   └── flink-1.16.2.tar.gz                                    # Flink 客户端
│
├── lacus-backend/                                             # 后端服务
│   ├── Dockerfile
│   ├── data/                                                  # lacus 数据目录
│   ├── flink-1.16.2.tar.gz                                    # Flink 客户端
│   ├── lacus-dist-2.0.0-all.tar.gz                            # lacus 主程序包
│   └── lacus-flink-sql-app-2.0.0.jar                          # Flink SQL 程序包
│
├── lacus-frontend/                                            # 前端服务
│   ├── Dockerfile
│   ├── dist.zip                                               # 前端打包文件
│   └── nginx.conf                                             # Nginx 配置文件
│
├── mysql/                                                     # MySQL 服务
│   ├── conf/
│   │   └── my.cnf                                             # MySQL 配置文件
│   ├── data/                                                  # msyql数据目录
│   └── init/
│       └── lacus.sql                                          # 初始化sql脚本
│
└── redis/                                                     # Redis 服务
    ├── redis-data/                                            # redis 数据目录
    └── redis.conf                                             # Redis 配置文件
```



## 二、构建Docker镜像

### 1. flink

flink-1.16.2.tar.gz

```
cd lacus-docker/flink
docker build -t eyesmoons/flink:1.16.2 .
```

### 2. lacus-backend

flink-1.16.2.tar.gz

lacus-dist-2.0.0-all.tar.gz

lacus-flink-sql-app-2.0.0-jar-with-dependencies.jar

```
cd lacus-docker/lacus-backend
docker build -t eyesmoons/lacus-backend:2.0.0 .
```

### 3. lacus-frontend

dist.zip

nginx.conf

```
cd lacus-docker/lacus-frontend
docker build -t eyesmoons/lacus-frontend:2.0.0 .
```

### 4. redis

redis.conf

### 5. mysql

init/lacus.sql

conf/my.cnf



## 三、启动Docker Compose

```
cd lacus-docker
docker compose up -d
```



## 四、一键启动

上述的 flink，lacus-backend，lacus-frontend 无需自己构建镜像，我已上传至 dockerhub，只需将 docker-compose.yaml 下载到本地，准备好 redis 和 mysql 配置文件，执行如下命令即可：

```shell
docker compose up -d
```

