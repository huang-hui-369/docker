# データーベースサーバーの構築

## 1. login to db host by user futari

## 2. docker install
  docker_installドキュメントを参照。
  docker-compose-install.mdを参照。

## 3. mysql install

### 1. create mysql work folder in db server

1. create mysql log folder
   `mkdir -p /home/futari/mysql/log`

2. create mysql data folder
   `mkdir -p /home/futari/mysql/data`

3. create mysql conf folder
   `mkdir -p /home/futari/mysql/conf.d`

4. create mysql init-db folder
   `mkdir -p /home/futari/mysql/initdb.d`

### 2. 設定ファイルやバックアップデーターファイルなどデーターベースサーバーへのコピー

1. バックアップされたデーターをデーターベースサーバーへコピーする。
   `scp backup/futari_bak.sql futari@db_server:/home/futari/mysql/initdb.d/1_futari_data.sql`

2. mysql設定ファイルをデーターベースサーバーへコピーする。
   `scp /mysql/conf.d/my.cnf futari@db_server:/home/futari/mysql/conf.d`

3. 権限設定ファイルをデーターベースサーバーへコピーする。
   `scp /mysql/initdb.d/2_privileges.sql futari@db_server:/home/futari/mysql/initdb.d`

4. dockerファイルをデーターベースサーバーへコピーする。
   `scp /mysql/docker-compose.yml futari@db_server:/home/futari/mysql`



### 3. コンテナを作成しスタートする
 ```
 cd /home/futari/mysql/
 docker-compose up -d
 ```
### 4. mysql サービスの確認

`docker ps -a`

![](img\2021-02-02-19-43-58.png)

`netstat -nptl`

![](img\2021-02-02-19-44-26.png)
