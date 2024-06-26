# 好用的Docker应用汇总



> 本文收集一些比较有趣的Docker应用，镜像版本更新可能会导致脚本或配置失效，如果无法使用请发邮件给我。

## 一、安装环境
* 系统 `Ubuntu` 已开启 `BBR加速` [BBR加速开启脚本](https://blog.ylx.me/archives/783.html)
* 安装 `docker` 和 `docker-compose`最新版本 [教程地址](https://www.runoob.com/docker/ubuntu-docker-install.html)

## 二、应用汇总
### zerotier
> [镜像地址](https://hub.docker.com/r/zerotier/zerotier) [教程地址](http://www.360doc.com/content/12/0121/07/11604731_1081143038.shtml)
```yaml
services:
  zerotier:
    image: zerotier/zerotier
    container_name: zerotier
    restart: unless-stopped
    privileged: true
    network_mode: host
    volumes:
      - ./data:/var/lib/zerotier-one
    devices:
      - /dev/net/tun
    environment:
      - TZ=Asia/Shanghai
    cap_add:
      - NET_ADMIN
      - SYS_ADMIN
    command: ["你的网络ID"]
```

### watchtower(自动更新容器)
> [镜像地址](https://hub.docker.com/r/containrrr/watchtower) [教程地址](https://blog.csdn.net/qq_21127151/article/details/129574398)<br>
```yaml
services:
  watchtower:
    image: containrrr/watchtower
    container_name: watchtower
    restart: unless-stopped
    network_mode: host
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
    environment:
      - TZ=Asia/Shanghai
```

### nginx-web-ui
> [镜像地址](https://hub.docker.com/r/cym1102/nginxwebui) [教程地址](https://www.nginxwebui.cn/product.html)<br>
> 首次登录初始化管理员账号密码
```yaml
services:
  nginx-web-ui:
    image: cym1102/nginxwebui
    container_name: nginx-web-ui
    restart: unless-stopped
    network_mode: host
    volumes:
      - ./data:/home/nginxWebUI
      - ./www:/www
    environment:
      - TZ=Asia/Shanghai
      - BOOT_OPTIONS=--server.port=8080 --spring.database.type=mysql --spring.datasource.url=jdbc:mysql://your-mysql-host:3306/nginx-web-ui --spring.datasource.username=root --spring.datasource.password=your-password 
```

### portainer-ce汉化版
> [镜像地址](https://hub.docker.com/r/6053537/portainer-ce) [教程地址](https://imnks.com/3406.html)<br>
> 首次登录初始化管理员账号密码
```yaml
services:
  portainer-ce:
    image: 6053537/portainer-ce
    container_name: portainer-ce
    restart: unless-stopped
    ports:
      - 9000:9000
    volumes:
      - ./data:/data
      - /var/run/docker.sock:/var/run/docker.sock
    environment:
      - TZ=Asia/Shanghai
```

### gitea
> [镜像地址](https://hub.docker.com/r/gitea/gitea) [教程地址](https://docs.gitea.io/zh-cn/installation/install-with-docker/)
```yaml
services:
  gitea:
    image: gitea/gitea
    container_name: gitea
    restart: unless-stopped
    ports:
      - 3000:3000
    volumes:
      - ./data:/data
    environment:
      - TZ=Asia/Shanghai
      - USER_UID=1000
      - USER_GID=1000
```

### gogs
> [镜像地址](https://hub.docker.com/r/gogs/gogs) [教程地址](https://learnku.com/articles/36255)
```yaml
services:
  gogs:
    image: gogs/gogs
    container_name: gogs
    restart: unless-stopped
    ports:
      - 3000:3000
    volumes:
      - ./data:/data
    environment:
      - TZ=Asia/Shanghai
```

### x-ui
> [镜像地址](https://hub.docker.com/r/enwaiax/x-ui)<br>
> 默认账号密码: `admin`/`admin`
```yaml
services:
  xui:
    image: enwaiax/x-ui
    container_name: x-ui
    restart: unless-stopped
    ports:
      - 54321:54321
      - 12345:12345
    volumes:
      - ./data:/etc/x-ui
    environment:
      - TZ=Asia/Shanghai
```

### jenkins
> [镜像地址](https://hub.docker.com/r/jenkins/jenkins) [教程地址](https://segmentfault.com/a/1190000042279781)
```yaml
services:                                      # 集合
  jenkins:
    image: jenkins/jenkins:lts                 # 指定服务所使用的镜像
    container_name: jenkins                    # 容器名称
    restart: unless-stopped                    # 重启方式
    user: root                                 # 为了避免一些权限问题 在这我使用了root
    ports:                                     # 对外暴露的端口定义
      - 8080:8080                              # 访问Jenkins服务端口
      - 50000:50000
    volumes:                                   # 卷挂载路径
      - ./data:/var/jenkins_home               # 这是我们一开始创建的目录挂载到容器内的jenkins_home目录
      - /usr/bin/docker:/usr/bin/docker        # 这是为了我们可以在容器内使用docker命令
      - /var/run/docker.sock:/var/run/docker.sock
      - /usr/local/bin/docker-compose:/usr/local/bin/docker-compose
    environment:
      - TZ=Asia/Shanghai
      - JAVA_OPTS=-server -Xms1024m -Xmx1024m -Xmn512m
```

### minio(单机部署)
> [镜像地址](https://hub.docker.com/r/minio/minio) [旧版教程](https://blog.csdn.net/weixin_45653525/article/details/128842091) [新版教程](https://blog.csdn.net/qq_57581439/article/details/126192492)
```yaml
services:
  minio:
    image: minio/minio:RELEASE.2021-06-17T00-10-46Z
    container_name: minio
    restart: unless-stopped
    ports:
      - 9000:9000
    volumes:
      - ./config:/root/.minio
      - ./data:/data
    environment:
      - TZ=Asia/Shanghai
      - MINIO_ROOT_USER=minio
      - MINIO_ROOT_PASSWORD=your-minio-password
    command: server /data
```

### mysql
> [镜像地址](https://hub.docker.com/_/mysql) [教程地址](https://www.cnblogs.com/Galaxy1/p/17806388.html) [内存优化](https://blog.csdn.net/weixin_43888891/article/details/122518719)<br>
```yaml
services:
  mysql:
    image: mysql
    container_name: mysql
    restart: unless-stopped
    ports:
      - 3306:3306
    volumes:
      - ./config/my.cnf:/etc/mysql/my.cnf
      - ./data:/var/lib/mysql
      - ./log:/var/log/mysql
    environment:
      - TZ=Asia/Shanghai
      # 初始化mysql的root密码
      - MYSQL_ROOT_PASSWORD=your-mysql-password
```
> my.cnf文件，请自行按需修改。
```
[mysqld]
user=mysql
max_connections=1000
mysql-native-password=ON
character-set-server=utf8mb4
collation-server=utf8mb4_general_ci
default-storage-engine=INNODB
default-time_zone='+8:00'
sql_mode=STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION

[client]
default-character-set=utf8mb4

[mysql]
default-character-set=utf8mb4
```

### postgres
> [镜像地址](https://hub.docker.com/_/postgres) [教程地址](https://www.itcto.cn/jc/docker/docker-compose-postgresql/)
```yaml
services:
  postgres:
    image: postgres
    container_name: postgres
    restart: unless-stopped
    ports:
      - 5432:5432
    volumes:
      - ./data:/var/lib/postgresql/data
    environment:
      - TZ=Asia/Shanghai
      - POSTGRES_USER=root
      - POSTGRES_PASSWORD=your-postgres-password
      - POSTGRES_DB=postgres
```

### redis
> [镜像地址](https://hub.docker.com/_/redis) [教程地址](https://www.jianshu.com/p/094078ef4347)
```yaml
services:
  redis:
    image: redis
    container_name: redis
    restart: unless-stopped
    ports:
      - 6379:6379
    volumes:
      - ./config/redis.conf:/etc/redis/redis.conf
      - ./data:/data
    environment:
      - TZ=Asia/Shanghai
    command: redis-server /etc/redis/redis.conf
```

### httpd
> [镜像地址](https://hub.docker.com/_/httpd)
```yaml
services:
  httpd1:
    image: httpd
    container_name: httpd1
    restart: unless-stopped
    ports:
      - 8080:80
    volumes:
      - ./data/web1:/usr/local/apache2/htdocs/
    environment:
      - TZ=Asia/Shanghai
```

### frps
> [镜像地址](https://hub.docker.com/r/snowdreamtech/frps) [参考配置](https://dusays.com/636/)
```yaml
services:
  frps:
    image: snowdreamtech/frps
    container_name: frps
    restart: unless-stopped
    network_mode: host
    volumes:
      - ./config/frps.toml:/etc/frp/frps.toml
    environment:
      - TZ=Asia/Shanghai
```

### frpc
> [镜像地址](https://hub.docker.com/r/snowdreamtech/frpc) [参考配置](https://dusays.com/636/)
```yaml
services:
  frpc:
    image: snowdreamtech/frpc
    container_name: frpc
    restart: unless-stopped
    network_mode: host
    volumes:
      - ./config/frpc.toml:/etc/frp/frpc.toml
    environment:
      - TZ=Asia/Shanghai
```

### alist(预装aria2)
> [镜像地址](https://hub.docker.com/r/xhofe/alist-aria2) [教程地址](https://alist.nn.ci/zh/guide/install/docker.html)<br>
> 获取初始账号密码: 在宿主机执行`docker exec -it 容器ID bash`进入容器, 执行`./alist admin set your-password`手动设置密码
```yaml
services:
  alist:
    image: xhofe/alist-aria2
    container_name: alist
    restart: unless-stopped
    ports:
      - 5244:5244
      - 6800:6800
    volumes:
      - ./data:/opt/alist/data
      - ./mydata:/mydata
    environment:
      - TZ=Asia/Shanghai
      - PUID=0
      - PGID=0
      - UMASK=022
```

### rocketmq(单机部署)
> [镜像地址](https://hub.docker.com/r/rocketmqinc/rocketmq) [教程地址](https://www.jianshu.com/p/9ed30a99a50a) [配置文件解释](https://blog.csdn.net/weixin_44606481/article/details/129780540)<br>
```yaml
services:
  rocketmq-namesrv:
    image: rocketmqinc/rocketmq
    container_name: rocketmq-namesrv
    restart: unless-stopped
    ports:
      - 9876:9876
    volumes:
      - ./data/namesrv/logs:/home/rocketmq/logs
      - ./data/namesrv/store:/home/rocketmq/store
    environment:
      - TZ=Asia/Shanghai
      - JAVA_OPT_EXT=-Duser.home=/home/rocketmq -Xms512M -Xmx512M -Xmn128m
    command: [ "sh","mqnamesrv" ]

  rocketmq-broker:
    image: rocketmqinc/rocketmq
    container_name: rocketmq-broker
    restart: unless-stopped
    ports:
      - 10909:10909
      - 10911:10911
    volumes:
      - ./config/broker.conf:/etc/rocketmq/broker.conf
      - ./data/broker/logs:/home/rocketmq/logs
      - ./data/broker/store:/home/rocketmq/store
    environment:
      - TZ=Asia/Shanghai
      - JAVA_OPT_EXT=-Duser.home=/home/broker -Xms512M -Xmx512M -Xmn128m
    command: [ "sh","mqbroker","-c","/etc/rocketmq/broker.conf","-n","rocketmq-namesrv:9876","autoCreateTopicEnable=true" ]
    depends_on:
      - rocketmq-namesrv

  rocketmq-console:
    image: styletang/rocketmq-console-ng
    container_name: rocketmq-console
    restart: unless-stopped
    ports:
      - 8080:8080
    volumes:
      - ./data/console:/tmp
    environment:
      - TZ=Asia/Shanghai
      - JAVA_OPTS=-Drocketmq.namesrv.addr=rocketmq-namesrv:9876 -Dcom.rocketmq.sendMessageWithVIPChannel=false -Xms512M -Xmx512M -Xmn128m
    depends_on:
      - rocketmq-namesrv
```

### verdaccio(npm私服)
> [镜像地址](https://hub.docker.com/r/verdaccio/verdaccio) [教程地址](https://blog.csdn.net/jxy139/article/details/129198445)
```yaml
services:
  verdaccio:
    image: verdaccio/verdaccio
    container_name: verdaccio
    restart: unless-stopped
    ports:
      - 3005:3005
    volumes:
      - ./data/conf:/verdaccio/conf
      - ./data/plugins:/verdaccio/plugins
      - ./data/storage:/verdaccio/storage
    environment:
      - TZ=Asia/Shanghai
      - VERDACCIO_PORT=3005
      - VERDACCIO_USER_NAME=root
```

### nexus(maven私服)
> [镜像地址](https://hub.docker.com/r/sonatype/nexus3) [教程地址](https://blog.csdn.net/qiaohao0206/article/details/125471721)
```yaml
services:
  nexus:
    image: sonatype/nexus3
    container_name: nexus
    restart: unless-stopped
    ports:
      - 8081:8081
    volumes:
      - ./data:/nexus-data
    environment:
      - TZ=Asia/Shanghai
```

### nacos
> [镜像地址](https://hub.docker.com/r/nacos/nacos-server) [官方文档](https://nacos.io/zh-cn/docs/quick-start-docker.html) [数据库初始化](https://github.com/alibaba/nacos/blob/2bb7193d1b311ec04c844b61612d6a151013ae88/config/src/main/resources/META-INF/mysql-schema.sql) [教程地址](https://www.cnblogs.com/studyjobs/p/18014237)<br>
> 默认的账号和密码都是 nacos，
```yaml
services:
  nacos:
    image: nacos/nacos-server:v2.2.3
    container_name: nacos
    restart: unless-stopped
    ports:
      - 8848:8848
      - 9848:9848
      - 9849:9849
    volumes:
      - ./logs/:/home/nacos/logs
    environment:
      - TZ=Asia/Shanghai
      - MODE=standalone
      - SPRING_DATASOURCE_PLATFORM=mysql
      - MYSQL_SERVICE_HOST=your-mysql-host
      - MYSQL_SERVICE_PORT=3306
      - MYSQL_SERVICE_USER=root
      - MYSQL_SERVICE_PASSWORD=your-mysql-password
      - MYSQL_SERVICE_DB_NAME=nacos
      - MYSQL_SERVICE_DB_PARAM=characterEncoding=utf8&connectTimeout=1000&socketTimeout=3000&autoReconnect=true&useUnicode=true&useSSL=false&serverTimezone=UTC
      - JVM_XMS=512m
      - JVM_XMX=512m
      - JVM_XMN=256m
      - JVM_MS=512m
      - JVM_MMS=512m
      # 启用账号密码验证
      - NACOS_AUTH_ENABLE=true
      # 随便使用一个32个字符组成的字符串，生成 base64 字符串，填写到这里即可
      - NACOS_AUTH_TOKEN=VGhpc0lzTXlDdXN0b21TZWNyZXRLZXkwMTIzNDU2Nzg=
      # 随便填写
      - NACOS_AUTH_IDENTITY_KEY=JobsKey
      # 随便填写
      - NACOS_AUTH_IDENTITY_VALUE=JobsValue
```

### vsftpd(ftp)
> [镜像地址](https://hub.docker.com/r/fauria/vsftpd) [教程地址](http://zongming.net/read-1394/?h=ftp)
```yaml
services:
  vsftpd:
    image: fauria/vsftpd
    container_name: vsftpd
    restart: unless-stopped
    ports:
      - 20:20
      - 21:21
      - 21100-21200:21100-21200
    volumes:
      - ./data:/home/vsftpd
      - ./logs/vsftpd.log:/var/log/vsftpd.log
    environment:
      - TZ=Asia/Shanghai
      - FTP_USER=root
      - FTP_PASS=your-password
      - PASV_MIN_PORT=21100
      - PASV_MAX_PORT=21200
```

### code-server(网页版vscode)
> [镜像地址](https://hub.docker.com/r/codercom/code-server) [github地址](https://github.com/coder/code-server)<br>
> 如果启动失败，日志显示没有权限创建文件或目录，可以试试给`./data`目录提升读写权限。
```yaml
services:
  code-server:
    image: codercom/code-server
    container_name: code-server
    restart: unless-stopped
    ports:
      - 8080:8080
    volumes:
      - ./data:/home/coder
    environment:
      - TZ=Asia/Shanghai
      - PUID=0
      - PGID=0
      - PASSWORD=your-password
      - SUDO_PASSWORD=your-password
```

### samba(samba服务器)
> [镜像地址](https://hub.docker.com/r/dperson/samba) [教程地址](https://juejin.cn/post/7250398315778998327)
```yaml
services:
  samba:
    image: dperson/samba
    container_name: samba
    restart: unless-stopped
    ports:
      - 139:139
      - 445:445
    volumes:
      - ./data:/mount
    environment:
      - TZ=Asia/Shanghai
    command: '-u "username1;password1" -u "username2;password2" -s "share;/mount/;yes;yes;yes;all;none" -s "public;/mount/;yes;no;no;all;none"'
```

### lychee(瀑布流相册)
> [镜像地址](https://hub.docker.com/r/lycheeorg/lychee) [github地址](https://github.com/LycheeOrg/Lychee-Docker/tree/master)
```yaml
services:
  lychee:
    image: lycheeorg/lychee
    container_name: lychee
    restart: unless-stopped
    ports:
      - 8080:80
    volumes:
      - ./config:/conf
      - ./sym:/sym
      - ./data:/uploads
    environment:
      - TZ=Asia/Shanghai
      - PUID=1000
      - PGID=1000
      - DB_CONNECTION=sqlite
```


### lsky-pro(兰空图床)
> [镜像地址](https://hub.docker.com/r/halcyonazure/lsky-pro-docker) [github地址](https://github.com/HalcyonAzure/lsky-pro-docker)
```yaml
services:
  lsky-pro:
    image: halcyonazure/lsky-pro-docker
    container_name: lsky-pro
    restart: unless-stopped
    ports:
      - 8089:8089
    volumes:
      - ./data:/var/www/html
    environment:
      - TZ=Asia/Shanghai
      - WEB_PORT=8089
```

### easyimage(简单图床)
> [镜像地址](https://hub.docker.com/r/ddsderek/easyimage) [github地址](https://github.com/icret/EasyImages2.0)
```yaml
services:
  easyimage:
    image: ddsderek/easyimage:latest
    container_name: easyimage
    restart: unless-stopped
    ports:
      - 8080:80
    volumes:
      - ./config:/app/web/config
      - ./data:/app/web/i
    environment:
      - TZ=Asia/Shanghai
      - PUID=1000
      - PGID=1000
      - DEBUG=false
```

### voce-chat(在线聊天室)
> [镜像地址](https://hub.docker.com/r/privoce/vocechat-server) [官方文档](https://doc.voce.chat/zh-cn/)
```yaml
services:
  voce-chat:
    image: privoce/vocechat-server
    container_name: voce-chat
    restart: unless-stopped
    ports:
      - 3000:3000
    volumes:
      - ./data:/home/vocechat-server/data
    environment:
      - TZ=Asia/Shanghai
```

### uptime-kuma(开源监控工具)
> [镜像地址](https://hub.docker.com/r/louislam/uptime-kuma) [教程地址](https://blog.csdn.net/csdnzxm/article/details/123081322)
```yaml
services:
  uptime-kuma:
    image: louislam/uptime-kuma
    container_name: uptime-kuma
    restart: unless-stopped
    ports:
      - 3001:3001
    volumes:
      - ./data:/app/data
    environment:
      - TZ=Asia/Shanghai
```


### docker-registry(docker仓库)
> [镜像地址](https://hub.docker.com/_/registry) [教程地址](https://blog.csdn.net/qq120631157/article/details/104398209)
```yaml
services:
  docker-registry:
    image: registry
    container_name: docker-registry
    restart: unless-stopped
    ports:
      - 5000:5000
    volumes:
      - ./data:/var/lib/registry
    environment:
      - TZ=Asia/Shanghai
```

### rustdesk-server(RustDesk远程桌面服务端)
> [镜像地址](https://hub.docker.com/r/rustdesk/rustdesk-server) [github地址](https://github.com/rustdesk/rustdesk-server#docker-images)
```yaml
services:
  rustdesk-server:
    image: rustdesk/rustdesk-server-s6
    container_name: rustdesk-server
    restart: unless-stopped
    ports:
      - 21115:21115
      - 21116:21116
      - 21116:21116/udp
      - 21117:21117
      - 21118:21118
      - 21119:21119
    volumes:
      - ./data:/data
    environment:
      - TZ=Asia/Shanghai
      - RELAY=rustdesk.example.com:21117
      - ENCRYPTED_ONLY=1
```

### dosgame(DOS游戏)
> [镜像地址](https://hub.docker.com/r/oldiy/dosgame-web-docker) [github地址](https://github.com/rwv/chinese-dos-games)
```yaml
services:
  dosgame:
    image: oldiy/dosgame-web-docker
    container_name: dosgame
    restart: unless-stopped
    ports:
      - 262:262
    environment:
      - TZ=Asia/Shanghai
```

### kuboard(k8s可视化面板)
> [镜像地址](https://hub.docker.com/r/eipwork/kuboard) [教程地址](https://www.cnblogs.com/a120608yby/p/17354691.html)
```yaml
services:
  kuboard:
    image: eipwork/kuboard:v3
    container_name: kuboard
    restart: unless-stopped
    ports:
      - 8090:80
      - 10081:10081
    volumes:
      - ./data:/data
    environment:
      - TZ=Asia/Shanghai
      - KUBOARD_ENDPOINT=http://ip:8090
      - KUBOARD_AGENT_SERVER_TCP_PORT=10081
```

### kubepi(k8s可视化面板)
> [镜像地址](https://hub.docker.com/r/1panel/kubepi) [官方文档](https://github.com/1Panel-dev/KubePi/wiki)
```yaml
services:
  kubepi:
    image: 1panel/kubepi
    container_name: kubepi
    restart: unless-stopped
    privileged: true
    ports:
      - 8080:80
    environment:
      - TZ=Asia/Shanghai
```

### rainbond(云原生平台)
> [教程地址](https://www.rainbond.com/docs/installation/install-with-ui/)
```yaml
services:
  rainbond:
    image: registry.cn-hangzhou.aliyuncs.com/goodrain/rainbond:v5.15.0-release-allinone
    container_name: rainbond
    restart: unless-stopped
    network_mode: host
    volumes:
      - ./.ssh:/root/.ssh
      - ./data:/app/data
    environment:
      - TZ=Asia/Shanghai
```

### hnet-web(在线网页代理)
> [镜像地址](https://hub.docker.com/r/stilleshan/hideipnetwork-web) [教程地址](https://blog.tanglu.me/web-browser/)
```yaml
services:
  hnet-web:
    image: stilleshan/hideipnetwork-web
    container_name: hnet-web
    restart: unless-stopped
    ports:
      - 56559:56559
    environment:
      - TZ=Asia/Shanghai
```

### memos(备忘录)
> [镜像地址](https://hub.docker.com/r/neosmemo/memos) [github地址](https://github.com/usememos/memos)
```yaml
services:
  memos:
    image: neosmemo/memos:latest
    container_name: memos
    restart: unless-stopped
    ports:
      - 5230:5230
    volumes:
      - ./data:/var/opt/memos
    environment:
      - TZ=Asia/Shanghai
```

### neko(neko远程浏览器)
> [镜像地址](https://hub.docker.com/r/m1k1o/neko) [教程地址](https://blog.tanglu.me/neko/)
```yaml
services:
  neko:
    image: m1k1o/neko:firefox
    container_name: neko
    restart: "unless-stopped"
    shm_size: "2gb"
    ports:
      - 8080:8080
      - 52000-52100:52000-52100/udp
    cap_add:
      - SYS_ADMIN
    environment:
      - TZ=Asia/Shanghai
      - NEKO_SCREEN='1920x1080@60'
      - NEKO_PASSWORD=neko
      - NEKO_PASSWORD_ADMIN=admin
      - NEKO_EPR=52000-52100
      - NEKO_NAT1TO1=127.0.0.1
      - NEKO_FILE_TRANSFER_ENABLED=true
```

### lobe-chat(开源的高性能聊天机器人框架)
> [镜像地址](https://hub.docker.com/r/lobehub/lobe-chat) [github地址](https://github.com/lobehub/lobe-chat) [环境变量](https://github.com/lobehub/lobe-chat/blob/main/src/config/server/provider.ts)
```yaml
services:
  lobe-chat:
    image: lobehub/lobe-chat
    container_name: lobe-chat
    restart: unless-stopped
    ports:
      - 3210:3210
    environment:
      - TZ=Asia/Shanghai
      - ACCESS_CODE=your-password
      - OLLAMA_PROXY_URL=your-ollama-url
      - OPENAI_API_KEY=your-openai-key
      - OPENAI_PROXY_URL=your-openai-url
      - ANTHROPIC_API_KEY=your-anthropic-key
      - ANTHROPIC_PROXY_URL=your-anthropic-url
```

### chatgpt-next-web(跨平台ChatGPT应用)
> [镜像地址](https://hub.docker.com/r/yidadaa/chatgpt-next-web) [教程地址](https://github.com/Yidadaa/ChatGPT-Next-Web)
```yaml
services:
  chatgpt:
    image: yidadaa/chatgpt-next-web
    container_name: chatgpt
    restart: unless-stopped
    ports:
      - 3000:3000
    environment:
      - TZ=Asia/Shanghai
      - OPENAI_API_KEY=your-key
      - CODE=your-password
      - BASE_URL=https://your-openai-api-url/v1
      - OLLAMA_PROXY_URL=https://your-ollama-api-url/v1
```

### pairdrop(在线文件传输)
> [镜像地址](https://hub.docker.com/r/linuxserver/pairdrop) [github地址](https://github.com/schlagmichdoch/PairDrop)
```yaml
services:
  pair-drop:
    image: lscr.io/linuxserver/pairdrop
    container_name: pair-drop
    restart: unless-stopped
    ports:
      - 3000:3000
    environment:
      - TZ=Asia/Shanghai
      - PUID=1000
      - PGID=1000
      - RATE_LIMIT=false
      - WS_FALLBACK=false
```

### it-tools(开发者工具箱)
> [镜像地址](https://hub.docker.com/r/qingfeng2336/it-tools) [github地址](https://github.com/CorentinTh/it-tools)
```yaml
services:
  it-tools:
    image: qingfeng2336/it-tools
    container_name: it-tools
    restart: unless-stopped
    ports:
      - 8080:80
    environment:
      - TZ=Asia/Shanghai
```

### filecodebox(文件快递柜)
> [镜像地址](https://hub.docker.com/r/lanol/filecodebox) [github地址](https://github.com/vastsa/FileCodeBox)
```yaml
services:
  file-code-box:
    image: lanol/filecodebox:beta
    container_name: file-code-box
    restart: unless-stopped
    ports:
      - 12345:12345
    volumes:
      - ./data:/app/data
    environment:
      - TZ=Asia/Shanghai
```

### briefing(WebRTC视频通话)
> [镜像地址](https://hub.docker.com/r/holtwick/briefing) [github地址](https://github.com/holtwick/briefing)
```yaml
services:
  video-chat:
    image: holtwick/briefing
    container_name: video-chat
    restart: unless-stopped
    ports:
      - 8080:8080
    environment:
      - TZ=Asia/Shanghai
```

### emby(emby多媒体服务器-特别版)
> [镜像地址](https://hub.docker.com/r/lovechen/embyserver)
```yaml
services:
  emby:
    image: lovechen/embyserver
    container_name: emby
    restart: unless-stopped
    ports:
      - 8096:8096
      - 8920:8920
      - 1900:1900/udp
      - 7359:7359/udp
    volumes:
      - ./data:/config
      - ./your-media-path:/media
    environment:
      - TZ=Asia/Shanghai
      - UID=0
      - GID=0 
      - GIDLIST=0
      - NVIDIA_VISIBLE_DEVICES=all
    devices:
      - /dev/dri:/dev/dri
```

### plex(plex多媒体服务器)
> [镜像地址](https://hub.docker.com/r/linuxserver/plex) [获取claim](https://plex.tv/claim)
```yaml
services:
  plex:
    image: lscr.io/linuxserver/plex
    container_name: plex
    restart: unless-stopped
    network_mode: host
    volumes:
      - ./data:/config
      - ./your-media-path:/media
    environment:
      - TZ=Asia/Shanghai
      - PUID=1000
      - PGID=1000
      - VERSION=docker
      - PLEX_CLAIM=your-claim
```

### stash(stash多媒体管理)
> [镜像地址](https://hub.docker.com/r/stashapp/stash) [github地址](https://github.com/stashapp/stash)
```yaml
services:
  stash:
    image: stashapp/stash
    container_name: stash
    restart: unless-stopped
    ports:
      - "9999:9999"
    volumes:
      - ./data/config:/root/.stash
      - ./data/generated:/generated
      - ./data/metadata:/metadata
      - ./data/cache:/cache
      - ./your-media-path:/media
    environment:
      - TZ=Asia/Shanghai
      - STASH_GENERATED=/generated/
      - STASH_METADATA=/metadata/
      - STASH_CACHE=/cache/
      - STASH_STASH=/media/
      - STASH_PORT=9999
    logging:
      driver: "json-file"
      options:
        max-file: "10"
        max-size: "2m"
```

### transmission(bt下载工具)
> [镜像地址](https://registry.hub.docker.com/r/linuxserver/transmission) [transmission-web-ui中文增强版](https://github.com/ronggang/transmission-web-control)
```yaml
services:
  transmission:
    image: lscr.io/linuxserver/transmission
    container_name: transmission
    restart: unless-stopped
    ports:
      - 9091:9091
      - 51413:51413
      - 51413:51413/udp
    volumes:
      - ./data:/config
      - ./downloads:/downloads
    environment:
      - TZ=Asia/Shanghai
      - PUID=1000
      - PGID=1000
      - TRANSMISSION_WEB_HOME=/config/transmission-web-ui
      - USER=your-username
      - PASS=your-password
```

### showdoc(在线文档)
> [镜像地址](https://hub.docker.com/r/star7th/showdoc) [帮助文档](https://www.showdoc.com.cn/help/)
```yaml
services:
  showdoc:
    image: star7th/showdoc
    container_name: showdoc
    restart: unless-stopped
    privileged: true
    user: root
    ports:
      - 8080:80
    volumes:
      - ./data:/var/www/html
    environment:
      - TZ=Asia/Shanghai
```

### odoo(开源的商业应用程序)
> [镜像地址](https://hub.docker.com/_/odoo) [教程地址](https://www.cnblogs.com/gzxiaohai/p/17303629.html)<br>
> 安装自定义模块需要配置`odoo.conf`，具体看教程。
```yaml
services:
  odoo:
    image: odoo
    container_name: odoo
    restart: unless-stopped
    ports:
      - 8069:8069
    volumes:
      - ./config:/etc/odoo
      - ./data:/var/lib/odoo
      - ./addons:/mnt/extra-addons
    environment:
      - TZ=Asia/Shanghai
      - HOST=your-postgres-host
      - USER=your-postgres-user
      - PASSWORD=your-postgres-password
```

### onlyoffice-server(onlyoffice在线文档服务端)
> [镜像地址](https://hub.docker.com/r/onlyoffice/documentserver)<br>
> 如果要使用`jwt`，就去除`- JWT_ENABLED=false`
```yaml
services:
  onlyoffice-server:
    image: onlyoffice/documentserver
    container_name: onlyoffice-server
    restart: unless-stopped
    ports:
      - 8080:80
    environment:
      - TZ=Asia/Shanghai
      - JWT_ENABLED=false
```

### nextcloud(自建网盘)
> [镜像地址](https://hub.docker.com/_/nextcloud)
```yaml
services:
  nextcloud:
    image: nextcloud
    container_name: nextcloud
    restart: unless-stopped
    ports:
      - 8080:80
    volumes:
      - ./data:/var/www/html
    environment:
      - TZ=Asia/Shanghai
      - MYSQL_HOST=your-mysql-host
      - MYSQL_USER=your-mysql-user
      - MYSQL_PASSWORD=your-mysql-password
      - MYSQL_DATABASE=nextcloud
```

### kodbox(可道云)
> [镜像地址](https://hub.docker.com/r/kodcloud/kodbox)<br>
> 免费版有10个用户的上限
```yaml
services:
  kodbox:
    image: kodcloud/kodbox
    container_name: kodbox
    restart: unless-stopped
    ports:
      - 8080:80
    volumes:
      - ./data:/var/www/html
    environment:
      - TZ=Asia/Shanghai
```

