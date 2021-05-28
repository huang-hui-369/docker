https://coralogix.com/log-analytics-blog/managing-docker-logs-with-elk-and-fluentd/

# 查看log驱动方式

```
docker info | grep Log
WARNING: the devicemapper storage-driver is deprecated, and will be removed in a future release.
WARNING: devicemapper: usage of loopback devices is strongly discouraged for production use.
         Use `--storage-opt dm.thinpooldev` to specify a custom block storage device.
 Logging Driver: json-file
  Log: awslogs fluentd gcplogs gelf journald json-file local logentries splunk syslog

```
docker 默认为json log

# 查看log的目录

```
docker inspect c033ff1ebf6d --format "{{.LogPath}}"

/var/lib/docker/containers/c033ff1ebf6dc7a76cc21b52b6ab144ef4e63883c9242ccd350bdc3cfd2c1cd0/c033ff1ebf6dc7a76cc21b52b6ab144ef4e63883c9242ccd350bdc3cfd2c1cd0-json.log
```

or
```
docker inspect 8f18b6bfb58a | grep 'LogPath'
```


默认的log目录

/var/lib/docker/containers/<CONTAINER ID>/<CONTAINER ID>-json.log


# 查看log

```
docker logs futari-nginx

# 最后十条记录
docker logs --tail=10 -t futari-spring

# 
docker logs --since "2021-05-06T10:08:00Z" -t futari-spring

# 从距现在5h30m到现在为止的log
docker logs --since "5h30m" -t futari-nginx

```

## 分别将错误log，和一般输出log导入文件
```
# To only read the error logs
docker logs NAME_OF_THE_CONTAINER  1>/home/temp/error.log

# To only read the access logs:
docker logs NAME_OF_THE_CONTAINER  2>/home/temp/access.log
```