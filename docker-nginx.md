## 运行的用户

nginx 的主进程是用 root用户启动的
        work process 进程是用 nginx用户（101）运行的。

![](img\2021-05-06-13-19-20.png)

/etc/nginx/nginx.confというファイルに設定

```
user  nginx;
worker_processes  1;

...

```

## 主なディレクトリ構成

| ファイル/ディレクトリ          | 説明                                                             |
| ------------------------------ | ---------------------------------------------------------------- |
| /etc/nginx/nginx.conf          | 起点となる設定ファイルで、他の設定ファイルはここから読み込まれる |
| /etc/nginx/conf.d/default.conf | webサーバの設定ファイル                                          |
| /etc/nginx/mime.types          | MIME のマッピングファイル                                        |
| /usr/share/nginx/html/         | webサーバのドキュメントルート                                    |
| /etc/logrotate.d/nginx         | ログローテーションの設定ファイル                                 |
| /var/log/nginx/ ログ           | ファイルの出力先ディレクトリ                                     |
| /var/cache/nginx/              | キャッシュファイルが格納先ディレクトリ                           |


## 映射的log

所以映射出的log是root所有

![](img\2021-05-06-13-48-37.png)

