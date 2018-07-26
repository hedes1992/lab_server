# 620 lab server
## 1. 服务器使用
### 1.1 现有服务器统计
本实验室现有可用服务器3台
1. P900
内外部IP：见邮件，可以外网ssh访问
cpu kernel: 32
memory: 157G
nvidia gpu: 1, GTX Titan X, 12G
user list:
2. wgw
内外部IP：见邮件，可以外网ssh访问
cpu kernel: 56
memory: 64G
nvidia gpu: 2, GTX Titan X, 12G
user list:
3. 624
内部IP：见邮件，外网不可访问，亦不可访问外网（需要配置代理，见section1.5）
cpu kernel: 48
memory: 252G
nvidia gpu: 4, GTX 1080 Ti, 12G

### 1.2 如何登陆服务器
1. 登陆软件：推荐Mobaxterm[官网的免费版下载地址](https://mobaxterm.mobatek.net/download.html)
2. 文件下载软件：mobaxterm本身可以进行文件上传下载，这里推荐FileZilla[下载地址](https://filezilla-project.org/)
2. 登陆命令：
shell 内登陆： ssh 账号@ip
Mobaxterm内登陆：基本用法[百度经验：mobaxterm ssh使用](https://jingyan.baidu.com/article/6dad5075223635a123e36ec9.html); 更多使用[博客：windows 全能终端](https://www.isharebest.com/mobaxterm.htm)
3. 个人账户：
由系统管理员分配(sudo adduser 账号名; 再在ssh配置中添加白名单)
注意624的机器上各个账户的home目录有20G的空间限制，所以大家应该把 数据和自己的代码程序 放在 /media/账户名/ 中，然后软连接到 自己的home下,以张三为例
`shell
mkdir /media/zhangsan/projects;
ln -s /media/zhangsan/projects /home/zhangsan/
`

### 1.3 linux 基础命令
1. 基本教程(国内教程链接)[http://www.runoob.com/linux/linux-tutorial.html]
2. ssh [基本教程链接](https://www.wikihow.com/Use-SSH)
3. vim [交互式教程](https://www.openvim.com/)
### 1.4 基本配置 
1. tmux 配置
* 鉴于所内网络的不稳定，登陆服务器之后应该立马进入一个tmux session（会话）
* 新建tmux 会话: tmux -2 new -s zhangsan
* 进入已有会话: tmux attach -t zhangsan
* 退出当前会话
    - 会话内休眠当前会话：ctrl-b + d
    - 会话外休眠会话： tmux detach -t zhangsan
* 杀死当前会话: tmux kill-session -t zhangsan
* 好用的 tmux 的配置
    - 参考[一本tmux的电子书](https://aquaregia.gitbooks.io/tmux-productive-mouse-free-development_zh/content/book-content/Appendix.html)
    - 保留原始快捷键 ctrl-b
    - 参考本项目中的 tmux.conf, 将其放在自己的home目录中，即 /home/账户名/，并改在文件名之前加点号
    - 完成tmux的配置
    - 纵向切割： ctrl-b + |
    - 横向切割： ctrl-b + -
    - 面板内的移动： ctrl-b + h或l(左右移动);ctrl-b + j或k(上下移动)
    - 查看面板历史： ctrl-b + esc; 然后按 jk可上下移动
    - 这里的移动完全是参考vim的移动
    - 创建新面板： ctrl-b + c
    - 切换到面板1：ctrl-b + 1
    - 切换到下个面板： ctrl-b + n
2. miniconda/anaconda 安装与配置
* [miniconda 下载地址](https://conda.io/miniconda.html)
* [anaconda 下载地址](https://www.anaconda.com/download/#linux)
* 下载下来的是sh文件，直接执行 sh 文件名.sh 即可
* 安装位置：以624机器安装miniconda2为例, 安装地址则为：/media/账户名/miniconda2
* 安装完成后用 which python和 which conda 以及 which pip 查看是否安装成功
* 为加速python 包的安装速度，建议安装清华源：
    - conda [清华源配置方法](https://mirrors.tuna.tsinghua.edu.cn/help/anaconda/)
    - pip [清华源配置方法](https://mirror.tuna.tsinghua.edu.cn/help/pypi/)
    - 也可以选择中科大ustc和aliyun的源
3. ~/.bashrc 文件配置
* .bashrc 文件，注意它和.tmux.conf 之前都有一个点号，并且同样放在自身的home目录下
    - 参考本项目中的 bashrc，将下方增加的部分放入自己的.bashrc 中即可
* 这其中用于配置个人的系统变量
    - PATH：系统路径
    - LD_LIBRARY_PATH：动态库路径
    - 等
* 对624用户来说，因为无法访问外网，所以需要配置 http_proxy等变量，同样参考本项目的bashrc即可
* vim 打开，修改，保存退出后, source ~/.bashrc 即完成新变量的加载

## 服务器管理
### 系统安装
### GPU cuda安装
### 网络管理