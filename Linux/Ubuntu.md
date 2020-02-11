# Ubuntu Configuration

## Installation

``` bash
$ sudo apt-get update
$ sudo apt-get install -y git vim wget zsh node

# 使用cnpm代替npm
$ npm install -g cnpm --registry=https://registry.npm.taobao.org
```

## Git

``` bash
$ git config --global user.name "fgksgf"
$ git config --global user.email "fgksgf@yahoo.com"
$ ssh-keygen -t rsa -b 4096 -C "fgksgf@yahoo.com"
```

## Zsh

``` bash
# 安装oh-my-zsh
$ wget --no-check-certificate https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | sh

# 替换bash为zsh
$ chsh -s /bin/zsh

# 修改zsh配置文件
$ vim ~/.zshrc

# 修改主题
ZSH_THEME="ys"

# 增加命令别名
alias cls="clear"
alias gst="git status"
alias gadd="git add"
alias vps="ssh ubuntu@xxx.xxx.xxx.xxx"
```

## Vim

```bash
$ vim ~/.vimrc

set nu
set ts=4
syntax on
set encoding=utf-8
set nocompatible
set autoindent
set cindent
set showmatch
set ignorecase
set hlsearch
set showcmd

" 启动显示状态行(1),总是显示状态行(2)
set laststatus=1
" 允许折叠
set foldenable
" 手动折叠
set foldmethod=manual
```

## SSH login without password

```bash
$ ssh-copy-id user@server
```

## Docker

```bash
$ sudo apt-get update

$ sudo apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common

$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

$ sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
   
$ sudo apt-get update
$ sudo apt-get install -y docker-ce docker-ce-cli containerd.io
```

## Docker compose

```bash
$ sudo curl -L "https://github.com/docker/compose/releases/download/1.25.3/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

$ sudo chmod +x /usr/local/bin/docker-compose
```

## File Transfer Tool

```bash
$ sudo apt-get install -y python-pip build-essential python-dev libffi-dev libssl-dev
$ pip install magic-wormhole
```

## Redis Server

1. **添加安全组规则：开放6379端口**
2. 自定义配置，设置密码

```bash
$ mkdir /redis
$ cd /redis
$ vim redis.conf

######################## redis.conf ########################
protected-mode no
port 6379
tcp-backlog 511
timeout 0
tcp-keepalive 300
daemonize no
supervised no
pidfile /var/run/redis_6379.pid

loglevel debug
logfile ""
databases 16

always-show-logo yes
save 900 1
save 300 10
save 60 10000
stop-writes-on-bgsave-error yes
rdbcompression yes
rdbchecksum yes
dbfilename dump.rdb
dir ./

# 密码
requirepass password

replica-serve-stale-data yes
replica-read-only yes
repl-diskless-sync no
repl-diskless-sync-delay 5
repl-disable-tcp-nodelay no
replica-priority 100
lazyfree-lazy-eviction no
lazyfree-lazy-expire no
lazyfree-lazy-server-del no
replica-lazy-flush no

appendonly no
appendfilename "appendonly.aof"

appendfsync everysec
no-appendfsync-on-rewrite no
auto-aof-rewrite-percentage 100
auto-aof-rewrite-min-size 64mb
aof-load-truncated yes
aof-use-rdb-preamble yes
lua-time-limit 5000
slowlog-log-slower-than 10000
slowlog-max-len 128
latency-monitor-threshold 0
notify-keyspace-events ""
hash-max-ziplist-entries 512
hash-max-ziplist-value 64
list-max-ziplist-size -2
list-compress-depth 0
set-max-intset-entries 512
zset-max-ziplist-entries 128
zset-max-ziplist-value 64
hll-sparse-max-bytes 3000
stream-node-max-bytes 4096
stream-node-max-entries 100
activerehashing yes
client-output-buffer-limit normal 0 0 0
client-output-buffer-limit replica 256mb 64mb 60
client-output-buffer-limit pubsub 32mb 8mb 60
hz 10
dynamic-hz yes
aof-rewrite-incremental-fsync yes
rdb-save-incremental-fsync yes
#############################################################
```

3. 拉取镜像并使用自定义配置启动容器
``` bash
$ docker pull redis
$ docker run -d -p 6379:6379  -v /root/redis/redis.conf:/redis.conf redis redis-server /redis.conf
```



# VPS Configuration

## SS

```bash
$ sudo apt-get install -y python-pip
$ sudo pip install shadowsocks
$ vim /etc/shadowsocks.json

{
   "server":"[server ip address]",
   "server_port":8388,
   "local_port":0,
   "password":"[password]",
   "timeout":500,
   "method":"aes-256-cfb"
}

$ sudo ssserver -c /etc/shadowsocks.json -d start
```

## SSR

```bash
$ wget --no-check-certificate https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocksR.sh
$ chmod +x shadowsocksR.sh
./shadowsocksR.sh 2>&1 | tee shadowsocksR.log
```

