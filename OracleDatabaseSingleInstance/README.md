
# Oracle Database container images

## 1. 下载需要的oracel版本压缩文件包

下载文件 oracle-xe-11.2.0-1.0.x86_64.rpm.zip 放到目录 OracleDatabaseSingleInstance/dockerfiles/11.2.0.2中

数据源1:
https://dw.hanbit.co.kr/Oracle/11gXE/
https://dw.hanbit.co.kr/Oracle/11gXE/oracle-xe-11.2.0-1.0.x86_64.rpm.zip

数据源2:
https://www.mediafire.com/file/fxkpss2lkv854qh/oracle-xe-11.2.0-1.0.x86_64.rpm.zip/file

## 2. 镜像制作

```bash
> # 查看构建帮助说明
> ./buildContainerImage.sh -h
>
> # 构建oracle 11g Express Edition版本镜像
> sudo ./buildContainerImage.sh -i -x -v 11.2.0.2
> sudo ./buildContainerImage.sh -i -x -f -v 11.2.0.2
>
```

## 3. 服务运行

### 运行oracle版本11.2.0.2-xe

```bash
docker run --name oracle11g \
--shm-size=1g \
-p 1521:1521 -p 8080:8080 \
-e ORACLE_PWD=oracle123 \
-v /opt/Data/Service/Oracle11g/oradata:/u01/app/oracle/oradata \
oracle/database:11.2.0.2-xe
```

docker run --name <container name> \
--shm-size=1g \
-p 1521:1521 -p 8080:8080 \
-e ORACLE_PWD=<your database passwords> \
-v [<host mount point>:]/u01/app/oracle/oradata \
oracle/database:11.2.0.2-xe

Parameters:
   --name:        The name of the container (default: auto generated)
   --shm-size:    Amount of Linux shared memory
   -p:            The port mapping of the host port to the container port.
                  Two ports are exposed: 1521 (Oracle Listener), 8080 (APEX)
   -e ORACLE_PWD: The Oracle Database SYS, SYSTEM and PDBADMIN password (default: auto generated)

   -v /u01/app/oracle/oradata
                  The data volume to use for the database.
                  Has to be writable by the Unix "oracle" (uid: 1000) user inside the container!
                  If omitted the database will not be persisted over container recreation.
   -v /u01/app/oracle/scripts/startup | /docker-entrypoint-initdb.d/startup
                  Optional: A volume with custom scripts to be run after database startup.
                  For further details see the "Running scripts after setup and on startup" section below.
   -v /u01/app/oracle/scripts/setup | /docker-entrypoint-initdb.d/setup
                  Optional: A volume with custom scripts to be run after database setup.
                  For further details see the "Running scripts after setup and on startup" section below.

There are two ports that are exposed in this image:

1521 which is the port to connect to the Oracle Database.
8080 which is the port of Oracle Application Express (APEX).

### 更新账户密码

```bash
>
> docker exec <container name> /u01/app/oracle/setPassword.sh <your password>
>
```

### 连接数据库

```bash
>
> sqlplus sys/<your password>@//localhost:1521/XE as sysdba
> sqlplus system/<your password>@//localhost:1521/XE
>
```


## 容器镜像下载

Oracle Express Edition版本
```bash
> docker pull container-registry.oracle.com/database/express:18.4.0-xe
> docker pull container-registry.oracle.com/database/express:21.3.0-xe
>
```


Oracle Free版本
```bash
> docker pull container-registry.oracle.com/database/free:23.8.0.0
> docker pull container-registry.oracle.com/database/adb-free:25.4.4.2-23ai
>
```