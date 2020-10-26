​                                                            Zookeeper 



1 定义

它是一个分布式服务框架，是Apache Hadoop 的一个子项目，它主要是用来解决分布式应用中经常遇到的一些数据管理问题，如：统一命名服务、状态同步服务、集群管理、分布式应用配置项的管理等。

2 结构

**1、文件系统**

Zookeeper维护一个类似文件系统的数据结构：

![img](https://img-blog.csdn.net/201807121434154?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2phdmFfNjY2NjY=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

每个子目录项如 NameService 都被称作为 znode(目录节点)，和文件系统一样，我们能够自由的增加、删除znode，在一个znode下增加、删除子znode，唯一的不同在于znode是可以存储数据的

- **PERSISTENT-持久化目录节点**

  客户端与zookeeper断开连接后，该节点依旧存在

- **PERSISTENT_SEQUENTIAL-持久化顺序编号目录节点**

  客户端与zookeeper断开连接后，该节点依旧存在，只是Zookeeper给该节点名称进行顺序编号

- **EPHEMERAL-临时目录节点**

  客户端与zookeeper断开连接后，该节点被删除

- **EPHEMERAL_SEQUENTIAL-临时顺序编号目录节点**

  客户端与zookeeper断开连接后，该节点被删除，只是Zookeeper给该节点名称进行顺序编号

**2、 监听通知机制**

客户端注册监听它关心的目录节点，当目录节点发生变化（数据改变、被删除、子目录节点增加删除）时，zookeeper会通知客户端。

