## docker安装及启动
`yum -y install docker`

## 查看docker运行状态
`systemctl status docker`

## 启动docker
`systemctl start docker`

## 设置docker开机启动
`systemctl enable docker`

## 查看docker版本
`docker version`

## 置容器重启策略
我们设置了docker自启动后，docker可以管理各种容器了，对于容器我们也可以设置重启的策略
```
no  不自动重启容器. (默认值)
on-failure  容器发生error而退出(容器退出状态不为0)重启容器,可以指定重启的最大次数，如：on-failure:10
unless-stopped  在容器已经stop掉或Docker stoped/restarted的时候才重启容器
always  在容器已经stop掉或Docker stoped/restarted的时候才重启容器，手动stop的不算
```

## 修改容器的重启策略
`docker update --restart always mynginx`

## ps -aux | grep docker 
## docker ps -a

## 进入docker 内部
docker exec -it futari-spring /bin/bash
docker exec -it futari-mysql /bin/bash

## 查看docker网络
docker network ls

## 查看docker网络详情
docker network inspect 930d53f3312d

## 创建网络
docker network create project1-network

## run 镜像
```
# docker run --name mysql --network wordpress-network -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:5.7
# docker run --name wordpress --network wordpress-network -e WORDPRESS_DB_PASSWORD=my-secret-pw -p 8080:80 -d wordpress
```

## docker容器日志在哪个目录

/var/lib/docker/containers/容器ID/容器ID-json.log

也可以使用以下命令查看容器日志

docker logs 容器ID

## permission denied

