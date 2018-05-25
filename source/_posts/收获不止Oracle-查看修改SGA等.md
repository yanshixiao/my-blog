---
title: 收获不止Oracle-查看修改SGA等
date: 2018-05-25 14:30:21
categories: 收获不止Oracle
tags: Oracle
---

### 查看并修改SGA、PGA等大小
#### 查看
##### sga和pga
![15](/images/shouhuo/15.png)

###### 共享池和数据缓冲区
![1527047874661](/images/shouhuo/1527047874661.png)
可以看到共享池和数据缓冲区大小都为0，这是因为Oracle默认采用SGA自动分配的策略，其中sga_target表示优先分配多少，sga_max_size表示如果不够用，最大能分配多少。如果想要手动，则把sga_target设为0，shared_pool_size和db_cache_size设为非0。

##### 日志缓冲区
![1527048541785](/images/shouhuo/1527048541785.png)
日志缓冲区大概只有15M左右，它不是由SGA自动管理的，只能手动管理，不过由于log_buffer每满1M就写一次，每满1/3也会写一次，给太大也没有意义。

#### 修改
ALTER SYSTEM 命令增加了一个新的选项scope。scope参数有三个可选值：memory、spfile、both。
- memory：只改变当前实例运行，重启后失效。
- spfile：不改变spfile的设置，不改变当前实例运行，重启后生效。
- both：同时改变实例和spfile，当前更改立即生效，重启数据库仍然生效。

1.如果当前实例使用的是pfile而非spfile，则scope=spfile或scope=both会产生错误；
2.如果实例以pfile启动，则scpoe的默认值为memory，若以spfile启动，则默认值为both；
3.有些参数必须重启才能生效，如log_buffer；
4.scope不写默认表示是both。

log_buffer必须重启才能生效，所以修改log_buffer时scope只能是spfile，memory和both都会报错。
