# ubuntu安装Go环境

### 1.下载Go语言安装包

官网：[下载地址](https://golang.google.cn/dl/)

### 2. 获取安装包

```
 wget https://studygolang.com/dl/golang/go1.13.4.linux-amd64.tar.gz
 #解压文件
  tar xfz go1.13.4.linux-amd64.tar.gz -C /usr/local
```

### 3. 配置全局变量

```
#修改~/.bashrc
vim ~/.bashrc
#添加Gopath路径
export GOPATH=/usr/local/go
export PATH=$GOPATH/bin:$PATH
```



