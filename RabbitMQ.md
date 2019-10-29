# 1.RabbitMQ简介

# 2. Centos7.6 安装RabbitMQ环境

### 1.安装RabbitMQ环境依赖 --erlang

```
yum install -y erlang
```

### 2. 安装RabbitMQ

下载对应环境的RabbitMQ安装包 [官网](https://www.rabbitmq.com/)

下载最新的安装包

```
wget https://dl.bintray.com/rabbitmq/rpm/rabbitmq-server/v3.8.x/el/7/noarch/rabbitmq-server-3.8.0-1.el7.noarch.rpm
```

下载完成后，安装

```
[root@VM_0_17_centos home]# rpm -ivh rabbitmq-server-3.8.0-1.el7.noarch.rpm 
warning: rabbitmq-server-3.8.0-1.el7.noarch.rpm: Header V4 RSA/SHA256 Signature, key ID 6026dfca: NOKEY
error: Failed dependencies:
	erlang >= 21.3 is needed by rabbitmq-server-3.8.0-1.el7.noarch
	socat is needed by rabbitmq-server-3.8.0-1.el7.noarch
[root@VM_0_17_centos home]#
```

安装后报以上错误，原因是使用命令`yun install -y erlang ` 安装的`erlang`版本较低，需要高版本支持

```
#查看erlang版本
[root@VM_0_17_centos home]# erl
Erlang R16B03-1 (erts-5.10.4) [source] [64-bit] [async-threads:10] [hipe] [kernel-poll:false]

Eshell V5.10.4  (abort with ^G)
1> 

```

```
重走第一步，安装最新版本
```

