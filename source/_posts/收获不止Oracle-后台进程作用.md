---
title: 收获不止Oracle-后台进程作用
date: 2018-05-25 14:43:47
tags: Oracle
categories: 收获不止Oracle
---

#### 后台进程的作用

##### PMON
Processes Monitor进程监视器。更新时崩溃，该进程会自动回滚操作。还可以干预后台进程，比如RECO异常失败了，PMON会重启RECO进程。

##### SMON
System Monitor系统监视器，SMON关注的是系统级的操作而非单个进程，重点工作在于`instance recovery`，除此之外，还有清理临时表空间、清理回滚段表空间、合并空闲时间等。

##### LCKn
仅使用于RAC数据库，最多可以有10个进程（LCK0,LCK1,...,,LCK9），用于实例间的封锁。

##### RECO
Distributed Database Recovery用于分布式数据库的恢复，适用于两阶段提价的应用场景。比如某个应用跨越三个数据库A、B、C，在发起的过程中，需要ABC都提交成功，事务才会成功，只要有一个失败，全部回滚。

##### CKPT
由Oracle的`FAST_START_MTTR_TARGET`参数控制，用于出发DBWR从数据缓冲区中写出数据到磁盘。CKPT执行越频繁，DBWR写出越频繁，越不能显示批量特性，性能就越低，但是数据库异常恢复的时间就会越迅速。

##### DBWR
把数据写入到磁盘中

##### LGWR
把日志缓冲区的数据从内存中写入到磁盘的REDO文件中，完成数据库对象创建、更新数据等操作过程的记录。REDO文件和后续对应的归档文件可以用来做数据库的异常恢复。

LGWR：

  1.每隔三秒钟，LGWR运行一次。
  2.任何COMMIT触发LGWR运行一次。
  3.DBWR要把数据从数据缓存写入到磁盘，触发LGWR运行一次。
  4.日志缓冲区满三分之一或者记录满1MB，触发LGWR运行一次。
  5.联机日志文件切换也将触发LGWR。