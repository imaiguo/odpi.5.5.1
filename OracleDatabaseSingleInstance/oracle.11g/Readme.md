

#  修改文件用户组

```bash
> # 用户id是1000，根据进入容器里查看系统用户oracle的id
> sudo docker run -it oracle/database:11.2.0.2-xe  /usr/bin/bash
> cat /etc/passwd
> mkdir oradata
> sudo chown -R 1000:1000 oradata
>
```

# 启动服务

```bash
>
> sudo docker compose up -d
> sudo docker compose down
```
