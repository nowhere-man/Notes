# Linux环境配置

## Ubuntu
### Ubuntu替换apt源
#### 备份
```bash
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
```

#### 查看版本号
```bash
lsb_release -c
```
确认Codename是focal

#### 编辑
```bash
sudo vim /etc/apt/sources.list
```

#### 替换
```
deb https://mirrors.aliyun.com/ubuntu/ focal main restricted universe multiverse
# deb-src https://mirrors.aliyun.com/ubuntu/ focal main restricted universe multiverse

deb https://mirrors.aliyun.com/ubuntu/ focal-security main restricted universe multiverse
# deb-src https://mirrors.aliyun.com/ubuntu/ focal-security main restricted universe multiverse

deb https://mirrors.aliyun.com/ubuntu/ focal-updates main restricted universe multiverse
# deb-src https://mirrors.aliyun.com/ubuntu/ focal-updates main restricted universe multiverse

deb https://mirrors.aliyun.com/ubuntu/ focal-proposed main restricted universe multiverse
# deb-src https://mirrors.aliyun.com/ubuntu/ focal-proposed main restricted universe multiverse

deb https://mirrors.aliyun.com/ubuntu/ focal-backports main restricted universe multiverse
# deb-src https://mirrors.aliyun.com/ubuntu/ focal-backports main restricted universe multiverse
```

#### 更新
```bash
sudo apt-get update
sudo apt-get upgrade
```

### Ubuntu下cpp环境搭建
```bash
sudo apt install build-essential
sudo apt install manpages-dev
sudo apt install gdb
sudo apt install git
sudo apt install cmake
```

### Ubuntu下mysql环境搭建
```bash
sudo apt install mysql-server
sudo apt install libmysqlclient-dev
```