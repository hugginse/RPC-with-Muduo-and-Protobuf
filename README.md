# PRC with Protobuf and Muduo

## 技术栈

* 集群和分布式概念及原理

* RPC远程过程调用原理及实现

* Protobuf数据序列化和反序列化协议

* Zookeeper分布式一致性协调服务应用以及编程

* Muduo网络库编程

* conf配置文件读取

* CMake构建项目集成编译环境

* github项目管理


## 集群和分布式

**集群：**每一个服务器独立运行一个工程的所有模块

**分布式：**一个工程拆分成多个模块，每个模块独立部署在一个服务器上，所有服务器协同工作共同提供服务，每一台服务器称作分布式的一个**节点**，根据节点的并发要求，对一个节点可以再做节点模块集群部署

## RPC通信原理

RPC(Remote Procedure Call Protocol)远程过程调用协议


## 环境配置使用

### 项目代码工程目录

bin：可执行文件

build：项目编译文件

lib：项目库文件

src：项目源文件

test：测试代码

example：框架代码使用范例

CMakeList.txt：顶层的cmake文件

README.md：项目自述文件

autobuild.sh：一键编译脚本

### 网络I/O模型介绍

### Protobuf

**Protobuf**是google开发的一种独立于平台语言数据交换的格式，其提供了java、c#、c++、go和python等语言的实现，并包含了相应语言的编译器以及库文件

由于它是一种**二进制**的格式，效率上比xml(20倍)、json(10倍)高，可以把它应用于分布式应用之间的数据通信或者异构环境下的数据交换。作为一种效率和兼容性都很优秀的二进制数据传输格式，可用于诸如网络传输、配置文件、数据存储等诸多领域

**要求：熟悉Protubu的proto配置文件内容，以及protoc的编译命令**
```proto
syntax = "proto3";      // 声明了protobuf版本

package xxx;    // 声明了代码所在的包(对应c++来说是namespace)

option cc_generic_services = true;

```

```
protoc test.proto --cpp_out=./
```

**<font color = 'red'>Tips:</font>**
> 在使用string时可以直接使用**bytes**类型代替，提升效率


## MPRPC框架设计

 
## Zookeeper分布式协调服务

**znode节点存储格式**