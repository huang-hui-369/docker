mysql 在docker中运行时，会以mysql用户（999:999）运行，所有映射出的host的data目录的所有者为999用户，
如果为了一致，最好在host中创建一个mysql用户。



# docker使用报错：the input device is not a TTY
用以下命令备份mysql时，在定时任务中报 the input device is not a TTY
docker exec -it futari-mysql mysqldump -u${DB_USER} -p${MYSQL_PWD} -B -R futari | gzip > ${MYSQL_BACKUP_FOLDER}/mysql_futari.sql.gz

这个的意思是说后台linux执行的时候没有终端设备。我们一般执行docker里的命令时候都喜欢加上              -it 这个参数，这里的-it 就是表示终端设备。所以，如果我们docker执行后台运行的任务或者程序直接去除 -it 这个参数就不会出现这个报错了！
