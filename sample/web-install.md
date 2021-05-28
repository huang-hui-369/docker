# ウェブサーバーの構築

## 1. login to web host by user futari

## 2. docker install
  docker_installドキュメントを参照。
  docker-compose-install.mdを参照。

## 3. docker networkの作成
`docker network create futari-network`

## 4. redis install

1. pull redis image
docker pull redis:6.0.10

2. run redis
docker run -d --name futari-redis --restart=always --network futari-network -p 6379:6379 redis:6.0.10

## 5. spring api install

### 1. ロカールでjarファイルを作成
   `mvn clean install -P pord`

### 2. create spring api work folder in web server
1. create spring api jar folder
   `mkdir -p /home/futari/api/jar`

2. create spring api log folder
   `mkdir -p /home/futari/api/logs`

### 3. 設定ファイルやjarファイルなどWebサーバーへのコピー

1. 設定ファイルをWebサーバーへコピーする。
   `scp spring_api/Dockerfile futari@web_server:/home/futari/api/`

2. jarファイルをWebサーバーへコピーする。
   `scp spring_api/jar/futari.jar futari@web_server:/home/futari/api/jar/app.jar`

### 4. dockerの起動
1．spring-apiのイメージの作成
```
cd /home/futari/api/
docker build -t spring-api .
```

2．futari-springコンテナの起動
`docker run -d --name futari-spring -p 8088:8088 --restart=always --network futari-network -v /home/futari/api/jar:/jar -v /home/futari/api/logs:/logs -v /home/futari/doc:/doc -v /etc/localtime:/etc/localtime -v /home/futari/fonts:/usr/lib/jvm/java-8-openjdk-amd64/jre/lib/fonts futari-api`

## 3. nginx install

### 1. ロカールでvue build 
1. build
   `npm run build:pord`

2. distフォントをdist.zip圧縮する

### 2. create spring api work folder in web server
1. create nginx conf folder
   `mkdir -p /home/futari/nginx/conf/`

2. create nginx ssl-keys folder
   `mkdir -p /home/futari/nginx/conf/ssl_keys/`

3. create vue folder
   `mkdir -p /home/futari/dist/`

4. create doc folder
   `mkdir -p /home/futari/doc/`

5. create fonts folder
   `mkdir -p /home/futari/fonts/`

6. create work folder
   `mkdir -p /home/futari/work/`

### 3. 設定ファイルやvueファイルなどwebサーバーへのコピー

1. 設定ファイルをサーバーへコピーする。
   `scp nginx/conf/default.conf futari@web_server:/home/futari/nginx/conf`

2. ssl-keyファイルをサーバーへコピーする。
   `scp -r nginx/conf/ssl_keys futari@db_server:/home/futari/nginx/conf/ssl_keys`

3. vue distファイルをへコピーする。
   ```
   scp nginx/dist.zip futari@db_server:/home/futari/work/
   cd /home/futari/work/
   unzip dist.zip -d /home/futari/
   ```
### 3. コンテナを作成しスタートする
 ```
 docker pull nginx:1.19.6
 docker run -d --name futari-nginx --net=host  --restart=always -v /home/futari/dist:/dist -v /home/futari/doc:/doc  -v /home/futari/nginx/conf:/etc/nginx/conf.d -v /home/futari/nginx/log:/var/log/nginx nginx:1.19.6
 ```

### 4. サービスの確認

`docker ps -a`

![](img\2021-02-02-20-42-06.png)

`netstat -nptl`

![](img\2021-02-02-20-41-35.png)
