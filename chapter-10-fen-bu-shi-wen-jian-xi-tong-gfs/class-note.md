# Class note

## Distributed File System (Google File System)

* 怎么有效存储数据
* No SQL底层需要一个File system
* GFS vs HDFS
  * GFS: Google
  * HDFS: Yahoo(Altaba) open source of GFS

### Scenario

*   需求1

    • 用户写入一个文件，用户读取一个文件. • 支持多大的文件?

    • 越大越好?比如>1000T
*   需求2

    • 多台机器存储这些文件 • 支持多少台机器?

    • 越多越好?

### Service

Client + Server

* 怎么沟通？
  * 社会主义：所有server平级
    * P2P
    * BitComet, Cassandra
  * 资本主义：master+slave
* GFS使用的是master+slave。单master挂了重启就是。

### Storage

* 大文件存在**硬盘**
* 设计GFS
  * File contains file content & Metadata
* Master+slave
  * Master
    * store Metadata
    * store Index
    * chunk的Offset偏移量可以不存在master上面
    * Master 存储10P 文件的metadata需要多少容量 -> 1 chunk = 64MB needs 64B ->10P chunk needs 10G
  * Slave: store chunk of file content

### File Read and Write

#### How to write a file

1. client告诉master file name和index
2. master告诉client分配的server
3. client直接找分配到的server写入文件
4. client告诉client\&master写入完成

一次Write，多次Read

#### 如果要修改文件怎么办？

先删掉`/gfs/home/file_name.mp4`，重新把整个文件重写一份

#### How to read a file

拆成多份多次读

#### Client怎么知道文件被切成了多少块

1. client ask master
2. master gives a chunk list
3. client read to each server
4. combine all chunk and return data

### Scale

* 单Master 够不够?
  * 工业界90%的系统都采用单master
* Checksum
  * use to identify whether a chunk on the disk is broken
  * MD5加密
  * Checksum size
    * 1 chunk (64MB) has 1 checksum (4bytes=32bit)
    * 1P/64MB\*32bit=62.5MB
* Replica
  * avoid data loss when a ChunkServer is down/fail
  * 存**三个**备份，两个备份相对比较近，另一个放在较远的地方
* How to recover when a chunk is broken
  * ask **master** for help
* How to find whether a ChunkServer is down?
  * Heartbeat
    * chunk servers向master汇报
* How to solve Client bottleneck
  * 选队长chunk server，队长chunk server传给其他chunk server（内网更快，比client单独给每个server传更快）
  * 如何选队长
    * 选最近的（快）
    * 选现在不干活的（平衡traffic）
    * 每次选的队长可能会不一样
  * How to solve Chunk Server failure
    * Tell everyone, including master that server is failed
    * Get new server
    * Retry

### 总结

* 存储
  * 普通文件（100G）存储：metadata, block
  * 大文件存储：metadata, block -> chunk
  * 多台机器超大文件：chunk server, master
* 写入
  * master + client + chunk server沟通流程
  * master维护metadata和chunk server
* 读出
  * master+client+chunk server沟通流程

1台电脑通常是2个硬盘：

**A PC can actually use more than one hard drive**, but the extent to which you can increase the number of hard drives in your PC depends on its motherboard. Most motherboards have just 4 SATA ports and can therefore be connected to 2 hard drives and 2 DVD drives, or you have 1 DVD drive and three hard drives

## Bigtable = No-SQL DB

* 怎么连接底层存储和上层数据

## Map Reduce

* 怎么快速处理数据
