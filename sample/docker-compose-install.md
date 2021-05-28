# docker-compose install

1. docker-compose install
 `sudo curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose`

2. 実行権限を付与
   `sudo chmod +x /usr/local/bin/docker-compose`

3. リンクを作成
   `ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose`

4. バージョンを確認
   `docker-compose --version`