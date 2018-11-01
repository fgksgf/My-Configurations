# Ubuntu Configuration

## software installation

``` bash
$ sudo apt-get update
$ sudo apt-get install git vim wget zsh node

# 使用cnpm代替npm
$ npm install -g cnpm --registry=https://registry.npm.taobao.org
```

## git

``` bash
$ git config --global user.name "fgksgf"
$ git config --global user.email "fgksgf@yahoo.com"
$ ssh-keygen -t rsa -b 4096 -C "fgksgf@yahoo.com"
```

## zsh

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

## vim

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



# VPS Configuration

## SS

```bash
$ sudo apt-get install python-pip
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

