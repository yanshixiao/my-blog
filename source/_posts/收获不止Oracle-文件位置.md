---
title: 收获不止Oracle-文件位置
date: 2018-05-25 14:37:00
tags: Oracle
categories: 收获不止Oracle
---

#### 参数文件位置
```
SQL> show parameter spfile;

NAME                                 TYPE        VALUE
------------------------------------ ----------- ------------------------------
spfile                               string      C:\APP\YS\PRODUCT\11.2.0\DBHOM
                                                 E_1\DATABASE\SPFILEORCL.ORA
```

![show parameter spfile](/images/shouhuo/9.png)

#### 控制文件位置
```
SQL> show parameter control;

NAME                                 TYPE        VALUE
------------------------------------ ----------- ------------------------------
control_file_record_keep_time        integer     7
control_files                        string      C:\APP\YS\ORADATA\ORCL\CONTROL
                                                 01.CTL, C:\APP\YS\FLASH_RECOVE
                                                 RY_AREA\ORCL\CONTROL02.CTL
control_management_pack_access       string      DIAGNOSTIC+TUNING
```

![控制文件](/images/shouhuo/10.png)

#### 数据文件位置
```
SQL> select file_name from dba_data_files;

FILE_NAME
------------------------------------
C:\APP\YS\ORADATA\ORCL\USERS01.DBF
C:\APP\YS\ORADATA\ORCL\UNDOTBS01.DBF
C:\APP\YS\ORADATA\ORCL\SYSAUX01.DBF
C:\APP\YS\ORADATA\ORCL\SYSTEM01.DBF
C:\APP\YS\ORADATA\ORCL\EXAMPLE01.DBF
```

![数据文件](/images/shouhuo/11.png)

#### 日志文件位置：
```
SQL> set linesize 100
SQL> col group# for a50
SQL> col member for a50
SQL> select group#,member from v$logfile;

    GROUP# MEMBER
---------- --------------------------------------------------
########## C:\APP\YS\ORADATA\ORCL\REDO03.LOG
########## C:\APP\YS\ORADATA\ORCL\REDO02.LOG
########## C:\APP\YS\ORADATA\ORCL\REDO01.LOG

```
不知道为什么GROUP#那一列格式化后就变成了\#\#\#\#\#\#，本身是1,2,3。

![日志文件](/images/shouhuo/12.png)

#### 归档文件位置
```
SQL> show parameter recovery

NAME                                 TYPE        VALUE
------------------------------------ ----------- ------------------------------
db_recovery_file_dest                string      C:\app\YS\flash_recovery_area
db_recovery_file_dest_size           big integer 3912M
recovery_parallelism                 integer     0
```

![归档文件](/images/shouhuo/13.png)


#### 告警日志文件（位于bdump目录下，以alert打头的文件）
```SQL
SQL> show parameter dump

NAME                                 TYPE        VALUE
------------------------------------ ----------- ------------------------------
background_core_dump                 string      partial
background_dump_dest                 string      c:\app\ys\diag\rdbms\orcl\orcl
                                                 \trace
core_dump_dest                       string      c:\app\ys\diag\rdbms\orcl\orcl
                                                 \cdump
max_dump_file_size                   string      unlimited
shadow_core_dump                     string      none
user_dump_dest                       string      c:\app\ys\diag\rdbms\orcl\orcl
                                                 \trace
```

![告警日志](/images/shouhuo/14.png)