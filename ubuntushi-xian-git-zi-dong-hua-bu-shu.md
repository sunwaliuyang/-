# GIT自动部署实现原理

1. git钩子
2. git 实现原理

# 安装 GIT信息

```
sudo apt-get install git
```

查看版本信息

```
git --version
git version 2.17.1
```

# \#添加git账号

```
groupadd git
useradd -d /home/git -m git
```

# 创建git仓库

```
#初始化裸仓库
git --bare init
#配置仓库的权限
chown -R git:git website.git
git init
```



