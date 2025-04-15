后台（-d）运行一个容器  （-d不进入容器，进入容器请用exec命令）

```
docker run -itd --name ckks-test ubuntu /bin/bash
```

进入容器 （从这个容器退出，容器不会停止）

``` 
docker exec -it [ID] /bin/bash
```

退出容器

```
exit
```

查看容器

```bash
docker ps -a     # 查看所有容器
```

删除容器

```
docker rm -f [ID]
```

导出容器 （导出容器快照到本地文件）

```
docker export [ID] > ubuntu.tar
```

导入容器快照

```
cat docker/ubuntu.tar | docker import - 
```



mv /etc/apt/sources.list /etc/apt/sources.list.bak

​    echo "deb http://mirrors.163.com/debian/ jessie main non-free contrib" >> /etc/apt/sources.list
​    echo "deb http://mirrors.163.com/debian/ jessie-proposed-updates main non-free contrib" >>/etc/apt/sources.list
​    echo "deb-src http://mirrors.163.com/debian/ jessie main non-free contrib" >>/etc/apt/sources.list
​    echo "deb-src http://mirrors.163.com/debian/ jessie-proposed-updates main non-free contrib" >>/etc/apt/sources.list

