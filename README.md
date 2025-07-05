![](https://views.whatilearened.today/views/github/lmq8267/rttys.svg)

### 帮助信息

```
rttys -h
名称：
   rttys - rtty的服务端程序

用法：
   rttys [全局选项] 命令 [命令选项]

版本：
   4.4.5

命令：
   run      运行rttys
   token    生成一个令牌
   help, h  显示命令列表或某个命令的帮助信息

全局选项：
   --help, -h     显示帮助信息
   --version, -v  输出版本信息

```

### Docker部署

- CMD

`docker run --name rttys -p 5913:5913 -e TZ=Asia/Shanghai restart=always -d ghcr.io/lmq8267/rttys run`

- compose.yaml

```
version: "3.9"
services:
  rttys:
    image: ghcr.io/lmq8267/rttys
    container_name: rttys
    ports:
      - "5913:5913"        # 映射主机5913端口到容器
    environment:
      - TZ=Asia/Shanghai   # 设置容器时区
    volumes:
      - "/你外部文件夹:/app" #挂载主机文件夹到容器的/app目录 用来保存db数据库
    restart: always        # 自动重启策略
    command: run           # 容器启动后执行的命令

```

- 创建token

等待容器成功运行后，执行命令 `docker exec -it rttys rttys token`
  
[客户端程序](https://github.com/lmq8267/rtty)
