# Linux_Server_Solution

> 查看版本（ubuntu）

```sh
uname -a

lsb_release -a
```



> 挂载磁盘

```sh
# 查看当前用户磁盘占用情况
df -h ~
# 查看被系统识别的磁盘
lsblk

# 创建目录用来挂载磁盘
mkdir -p ~/mount_file

# 挂载 前面写要挂载的磁盘 后面写挂载到的目录
sudo mount /dev/vdc ~/mount_file

# 检查是否挂载成功
df -h ~/mount_file
```







> pip 换源

```sh
# pip换源
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple --user

# pip查看源
pip config list


# 直接编辑pip.conf文件
# 这个配置文件一般在 ~/.conf/pip/pip.conf
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple

extra-index-url =
    https://mirrors.aliyun.com/pypi/simple/
    https://mirrors.bfsu.edu.cn/pypi/web/simple/
```





> 下载pyenv来管理python版本

```shell
# 这个是下载pyenv
curl https://pyenv.run | bash

# 下面是很重要的一步，我们需要进入当前所使用的sh的rc文件，然后将下面的内容复制进去，这样才能保证我们每次使用shell都有pyenv使用（配置环境变量） 
source ~/.zshrc

export PATH="$HOME/.pyenv/bin:$PATH"
eval "$(pyenv init --path)"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"

source ~/.zshrc
```



> 创建虚拟环境并激活
>
> 虚拟环境可以隔绝系统的python环境进行操作

```sh
# 使用这条命令创建
python -m venv [venv_name]

# 使用这条命令进入虚拟环境激活（需要首先进入含有虚拟环境的目录下）
source [venv_name]/bin/activate
```



> 查看Nvidia显卡

```sh
lspci | grep -i nvidia
```

```sh
# 查看是否安装显卡驱动
nvidia-smi
# 查看推荐安装的驱动版本
ubuntu-driver devices
#自动安装推荐的版本
sudo ubuntu-drivers autoinstall
```



> 下载Anaconda

```sh
# 下载anaconda
wget https://repo.anaconda.com/archive/Anaconda3-2022.10-Linux-x86_64.sh

bash ~/Downloads/Anaconda3-2021.11-Linux-x86_64.sh

# 配置环境变量
export  PATH=$PATH:/home/USERNAME/anaconda3/bin
```

> conda 常用指令

```sh


# 列出所有已创建的虚拟环境
conda env list

# 创建虚拟环境 -n 指定虚拟环境的名字 后面要制定该环境的Python版本 
conda create -n [venv_name] python=[version_name]

# 进入虚拟环境
conda activate [venv_name]

# 推出虚拟环境
conda deactivate

#每次进入终端的时候会默认进入conda的base环境，使用下面的命令取消这个的设置
conda config --set auto_activate_base false

```

> conda 换源（清华）

```sh
# 当前用户目录的conda配置文件
~/.condarc

conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r
conda config --set show_channel_urls yes

# 查看信息
conda info
conda config --show
```

> conda 升级

```sh
# 更新
conda update conda
# 尝试安装最新版本
conda install conda=24.11.0

# 重新安装miniconda升级（安装不同的conda后，不同conda之间的虚拟环境不能相互进入）
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh
# 推出终端
conda --version
```





> Scp 服务器命令行传送文件

```shell
# 传递目录
# 本地 -> 远程
scp -r /xxx/xxx/xxx user@ipaddr:/yyy/yyy/yyy

# 远程 -> 本地
scp -r user@ipaddr:/yyy/yyy/yyy /xxx/xxx/xxx
```

```sh
# 传递文件
```



> ssh

```sh
ssh-add [pub-key path]
```

```sh
# 端口转发（端口映射？）
# 在服务器上运行的一些程序，需要访问特定的端口才能使用，但本地访问不到端口，这个时候我们可以使用端口转发来# # 将服务器上的某个端口运行的服务转发到本地指定的端口

ssh -L [server_port]:127.0.0.1:[local_port] user@server_ip
```

