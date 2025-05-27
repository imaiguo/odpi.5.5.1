# Oracle Database

##  Oracle 连接

登录到system以创建其他用户

```bash
> sudo docker run -it oracle/database:11.2.0.2-xe  /usr/bin/bash
> sqlplus /nolog
SQL> connect / as sysdba
>
```

## Oracle 用户管理

```bash
SQL> create user username identified by dbuser123;
SQL> alter user dbuser identified by dbuser123;
SQL> drop user dbuser;
>
```

为用户授权角色\撤销授权

oracle提供三种标准角色（role）:connect/resource和dba.

1. connect role(连接角色)
临时用户，特指不需要建表的用户，通常只赋予他们connect role.

connect是使用oracle简单权限，这种权限只对其他用户的表有访问权限，包括select/insert/update和delete等。
拥有connect role 的用户还能够创建表、视图、序列（sequence）、簇（cluster）、同义词(synonym)、回话（session）和其他 数据的链（link)。

2. resource role(资源角色)
更可靠和正式的数据库用户可以授予resource role。

resource提供给用户另外的权限以创建他们自己的表、序列、过程(procedure)、触发器(trigger)、索引(index)和簇(cluster)。

3. dba role(数据库管理员角色)
dba role拥有所有的系统权限

包括无限制的空间限额和给其他用户授予各种权限的能力。

```bash
> grant connect, resource to dbuser;
> revoke connect, resource from dbuser;
>
```

## Oracle SQL语句


## Oracle 运维


