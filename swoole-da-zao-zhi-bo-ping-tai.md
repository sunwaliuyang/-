##### 1. 什么是Swoole

异步特性、

#### 2.swoole安装

1. 源码安装swoole
2. 源码安装php
3. php7支持swoole

#### 3. Swoole简介

1. php异步网络通信引擎
2. Swoole 使用纯 C 语言编写，提供了 PHP 语言的异步多线程服务器，异步 TCP/UDP 网络客户端，异步 MySQL，异步 Redis，数据库连接池，AsyncTask，消息队列，毫秒定时器，异步文件读写，异步DNS查询。 Swoole内置了Http/WebSocket服务器端/客户端、Http2.0服务器端。

3. 除了异步 IO 的支持之外，Swoole 为 PHP 多进程的模式设计了多个并发数据结构和IPC通信机制，可以大大简化多进程并发编程的工作。其中包括了并发原子计数器，并发 HashTable，Channel，Lock，进程间通信IPC等丰富的功能特性。

4. Swoole2.0 支持了类似 Go 语言的协程，可以使用完全同步的代码实现异步程序。PHP 代码无需额外增加任何关键词，底层自动进行协程调度，实现异步。

##### 4.PHP 源码安装

```
#下载最新PHP版本
wget https://www.php.net/distributions/php-7.3.12.tar.bz2 
#解压 
tar -jxvf php-7.3.12.tar.bz2
```

源码安装步骤： 解压、configure、make、make install

编译安装

```
./configure  --prefix=/
```

##### 5.使用pecl 安装swoole

```
#安装php7.3
sudo apt-get install php7.3 php7.3-dev php7.3-gd php7.3-cli php7.3-fpm php7.3-mbstring php7.3-mysql php7.3-curl
#适应pecl安装swoole
sudo pecl install swoole
#编辑php.ini,添加swoole扩展
extension = swoole.so
```

demo测试

```
cd ../swoole/examples/server
php echo.php
#监听9501端口
lsof -i : 9501
# php     1211 ubuntu    3u  IPv4 47977979      0t0  TCP *:9501 (LISTEN)
```



