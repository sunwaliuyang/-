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

安装后报以上错误，原因是使用命令`yun install -y erlang` 安装的`erlang`版本较低，需要高版本支持

`RabbitMQ`不同版本对应的`erlang`版本

```
#查看erlang版本
[root@VM_0_17_centos home]# erl
Erlang R16B03-1 (erts-5.10.4) [source] [64-bit] [async-threads:10] [hipe] [kernel-poll:false]

Eshell V5.10.4  (abort with ^G)
1>
```

重走第一步，安装最新版本erlang

| RabbitMQ Version | Minimum required Erlang/OTP | Maximum supported Erlang/OTP | Notes |
| :--- | :--- | :--- | :--- |
| 3.8.0 | 21.3.x | 22.x | Erlang 22.1 is recommended. |
| 3.7.19 | 21.3x | 22.x | Erlang/OTP 20.3x support  is  discontinued |
| 3.7.18、3.7.17、3.7.16、3.7.15 | 20.3.x | 22.x | [Erlang/OTP22.0compatibility notes](https://groups.google.com/forum/#!topic/rabbitmq-users/vcRLhpUdg_o)[TLSv1.0 and TLSv1.1 support](https://www.rabbitmq.com/ssl.html#tls-versions)is disabled by default on Erlang 22.x |
| 3.7.14、3.7.13、3.7.12、3.7.11、3.7.10、3.7.9、3.7.8、3.7.7 | 20.3.x | 21.3.x | [Erlang/OTP19.3.xsupport is discontinued](https://groups.google.com/forum/#!topic/rabbitmq-users/G4UJ9zbIYHs)For the best TLS support, the latest version of Erlang/OTP 21.3.x is recommended |
| 3.7.6、3.7.5、3.7.4、3.7.3、3.7.2、3.7.1、3.7.0 | 19.3.x | 20.3.x | For the best TLS support, the latest version of Erlang/OTP 20.3.x is recommendedErlang versions prior to 19.3.6.4 have known bugs \(e.g.[ERL-430](https://bugs.erlang.org/browse/ERL-430),[ERL-448](https://bugs.erlang.org/browse/ERL-448)\) that can prevent RabbitMQ nodes from accepting connections \(including from CLI tools\) and stoppingVersions prior to 19.3.6.4 are vulnerable to the[ROBOT attack](https://robotattack.org/)\(CVE-2017-1000385\)On Windows, Erlang/OTP 20.2 changed[default cookie file location](https://www.rabbitmq.com/cli.html) |

[erlang官网](https://www.erlang.org/)

```
#官网下载最新相关版本
wget http://erlang.org/download/otp_src_22.1.tar.gz
#解压
tar -zxvf otp_src_19.3.tar.gz
cd otp_src_19.3
#配置安装目录
./configure --prefix=/usr/lib/erlang
#编译安装
make && make install
```

安装过程中错误提示：`configure: error: No curses library functions found`

原因：未安装`ncurses-devel`扩展

```
yun install ncurses-devel

#编译安装
./configure --prefix=/usr/lib/erlang
make && make install
```

在配置文件中配置环境变量`~/.bash_profile`

```
vim ~/.bash_profile
#添加命令（本地安装目录）
PATH=$PATH:/usr/local/lib/erlang/bin
#使bash_profile生效
source ~/.bash_profile
```

验证erlang是否安装成功

```
erl
```

输出

```
Erlang/OTP 22 [erts-10.5] [source] [64-bit] [smp:1:1] [ds:1:1:10] [async-threads:1] [hipe]

Eshell V10.5  (abort with ^G)
1>
```

说明 erlang版本更新成功

安装RabbitMQ

```
#rpm -ivh --nodeps rabbitmq-server-3.8.0-1.el7.noarch.rpm
warning: rabbitmq-server-3.8.0-1.el7.noarch.rpm: Header V4 RSA/SHA256 Signature, key ID 6026dfca: NOKEY
Preparing...                          ################################# [100%]
Updating / installing...
   1:rabbitmq-server-3.8.0-1.el7      ################################# [100%]

```



