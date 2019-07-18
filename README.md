# 620 lab server
## 1. 服务器使用
### 1.1 [现有服务器](./server_list.md)

### 1.2 如何登陆服务器
1. 登陆软件：推荐Mobaxterm[官网的免费版下载地址](https://mobaxterm.mobatek.net/download.html)
- win10 升级至1903版并安装最新更新后可用windows应用商店中的windows terminal
- 第三方软件 [Terminus](https://github.com/Eugeny/terminus)
2. 文件下载软件：mobaxterm本身可以进行文件上传下载，这里推荐FileZilla[下载地址](https://filezilla-project.org/)
3. 登陆命令：
* shell 内登陆： `ssh 账号@ip`
* Mobaxterm内登陆：基本用法[百度经验：mobaxterm ssh使用](https://jingyan.baidu.com/article/6dad5075223635a123e36ec9.html)
* 更多使用[博客：windows 全能终端](https://www.isharebest.com/mobaxterm.htm)
4. 个人账户：
由系统管理员分配(sudo adduser 账号名; 再在ssh配置中添加白名单)
注意624的机器上各个账户的home目录有20G的空间限制，所以大家应该把 数据和自己的代码程序 放在 `/media/账户名/` 中，然后软连接到 自己的home下,以张三为例
```
mkdir /media/zhangsan/projects
ln -s /media/zhangsan/projects /home/zhangsan/
```

### 1.3 linux 基础命令
1. 基本教程(国内教程链接)[http://www.runoob.com/linux/linux-tutorial.html]
2. ssh [基本教程链接](https://www.wikihow.com/Use-SSH)
3. vim [交互式教程](https://www.openvim.com/)
### 1.4 基本配置 
1. [tmux 命令使用](./tmux.md)
2. [miniconda/anaconda 安装与配置](./python_conda.md)
3. ~/.bashrc 文件配置
* .bashrc 文件，注意它和.tmux.conf 之前都有一个点号，并且同样放在自身的home目录下
    - 参考本项目中的 bashrc，将下方增加的部分放入自己的.bashrc 中即可
* 这其中用于配置个人的系统变量
    - PATH：系统路径
    - LD_LIBRARY_PATH：动态库路径
    - 等
* 对624用户来说，因为无法访问外网，所以需要配置 http_proxy等变量，同样参考本项目的bashrc即可
* vim 打开，修改，保存退出后, `source ~/.bashrc` 即完成新变量的加载
## 2. [git 使用](./git_tutorial.md)
## 3. 服务器管理
1. 新用户添加
- 使用命令来添加用户 zhangsan
    管理员完成`sudo adduser zhangsan` 后续按照提示输入选好的密码
- 将 zhangsan 加入ssh白名单,以备ssh访问
    管理员完成`sudo vim /etc/ssh/sshd_config` 在内部添加 zhangsan 即可
### 4. [GPU cuda 环境搭建](./gpu_cuda.md)
### 5. 网络管理