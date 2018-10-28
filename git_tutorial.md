# Git 使用教程
为方便大家熟悉和使用git, 撰写以下教程
## 1. 为什么要用Git
(姿势水平)更高, (写论文, 对比实验)更快, 更强(多人合作)
### 1.1 Git是什么
[Git](https://www.wikiwand.com/zh-sg/Git) 是一个分布式版本控制软件...
主要对文本文件(.txt, .c, py, .tex 等)的内容变化进行跟踪, 记录.
下面是我的粗浅理解
#### 1.1.1 版本控制
Git最开始是为了对Linux的内核代码进行管理. 这样庞大的项目可能每周都会上线或下线新的功能, 这意味着项目的代码随时都处于变动之中. 管理员希望能备份每一版代码, 以方便后续的Bug管理等. 有如下方案:
1. 每一个版本的代码都copy一份, 然后按照存储的时间进行命名
2. 对项目代码中的文件进行追踪控制, 记录每一版本中发生变化的文件以及对应的变化
前者存储的代码虽然可以直接运行, 但十分占用硬盘, 并且很难分析出版本之间的变化; 后者的方案则更好, 只对变化进行记录, 然后从当前最新版本开始, 通过反向操作, 可以回退到特定版本.
具体地, 记录的版本变化主要包含: 文件的增删, 文件的修改(增加或删除或修改哪些行哪些列)
#### 1.1.2 分布式
我理解的分布式:
1. 是指Git可以在任何位置存储版本变化的信息, 主要是在 ./.git 子文件夹中.
2. 不同位置的代码的版本可以不同, 也可以通过命令随时切换到新的版本
### 1.2 Git与github, gitlab, gitee的区别
1. Git 是软件, 帮助我们进行版本管理
2. github 是一种基于Git的代码分享网站, 戏称全球最大同性交友平台. 因为上面有很多程序员公开分享的代码, 是我们复现paper的主要代码来源...
3. gitlab 是一种基于Git的仓库管理工具, 可以下载社区版进行实验室级别的部署, 也可以付费使用企业级. Gitlab 上可以做代码分享(尤其是巨硬收购github之后)
4. gitee 可以理解为国内版的github.
    1. github 虽然好, 但是免费用户上传的代码只能被公开(即都是公有仓库), 不过采用edu邮箱可以申请学生账号(应该可以创建5个免费私有仓库); 此外, 在服务器上clone github上代码的速度很感人(GFW的锅吧)
    2. gitee 之前应该是开源中国开发的, 后来不知为什么就变成了 "码云". 它的优势是: 访问速度很快; 可以建立N多免费私有仓库...
    3. 本教程目前部署在gitee上...
5. 本实验室目前在wgw-1018的机器上部署了gitlab 社区版的服务, 可以通过所内网路访问 http://172.18.34.20/ 即可创建自己的账号
### 1.3 Git可以帮我们做什么
参考[知乎回答: 深度学习科研，如何高效进行代码和实验管理?](https://www.zhihu.com/question/269707221/answer/350542551)
我理解Git主要用于管理自己的代码, 主要是对DL中用到的超参进行管理.
此外, 还可以对写paper的tex进行管理.
## 2. Git的基本命令
### 2.1 比较好的git教程资源
1. [廖雪峰的Git](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)
2. [Pro-git 使用-中文版](https://git-scm.com/book/zh/v2)
3. [Github的Guides](https://guides.github.com/activities/hello-world/)
4. [Github上的中文Git教程](https://github.com/geeeeeeeeek/git-recipes)
### 2.2 常用的命令
1. A 和 B 机器上都从代码分享网站上下载著名的代码: `git clone https://github.com/pytorch/pytorch.git`
2. A 机器上改动代码后需要进行提交
    1. `cd pytorch` # 先进入pytorch文件夹
    2. `git status` 查看当前产生的改动, 假如有file1, file2, file3
    3. `git diff `  查看当前改动的具体情况, 即file1, file2, file3中文本的增删情况
    4. `git diff file2` # 查看特定文件file2的变动情况
    5. `git add file1` # 加入 file1
    6. `##git add .` # 如果将所有文件都加入, 慎用 
    7. `git add file3` # 加入 file3
    8. `git commit -m 'modify learning rate to 0.001'` # 决定commit, -m 后面的信息代表这次提交的改动的意义: 修改了学习率
    9. `git push origin master` # 将改动提交到远程地址(gitee或者Github等)
3. B机器上下载最新的代码改动
    1. `git pull origin master` # 另一台机器上下载当前最新的代码改动
### 2.3 远程仓库, 分支, 版本, 标签, commid_id 等
1. 远程仓库
    参考[远程仓库的使用](https://git-scm.com/book/zh/v1/Git-%E5%9F%BA%E7%A1%80-%E8%BF%9C%E7%A8%8B%E4%BB%93%E5%BA%93%E7%9A%84%E4%BD%BF%E7%94%A8)
    远程仓库代表存储当前代码的网站地址, 默认是origin. 可以有不同名的多个远程仓库.
    1. `git clone https://github.com/pytorch/pytorch.git` 之后, 此时项目的默认远程仓库origin 代表 `https://github.com/pytorch/pytorch.git`
    2. `git remote show origin` #查看远程仓库origin的信息
    3. `git remote show` # 查看当前项目的所有远程仓库名字
    4. `git remote add gitee gitee上自己的pytorch地址` #将gitee上自己的pytorch地址作为名字为gitee的远程仓库
        1. 这一步的前提是先在gitee上的自己的账户里创建名为pytorch的地址, 如果创建好了(例如 `https://gitee.com/hedes/pytorch.git`)
    5. `git push gitee master` #创建好之后可以将本地的master分支推送到gitee上
        1. 注意这里无法push到origin, 因为origin的地址是pytorch官方的, 不是你自己的账户, 因此会被github.com 拒绝
2. 分支
    参考[分支的新建](https://git-scm.com/book/zh/v1/Git-%E5%88%86%E6%94%AF-%E5%88%86%E6%94%AF%E7%9A%84%E6%96%B0%E5%BB%BA%E4%B8%8E%E5%90%88%E5%B9%B6)
    1. 一个项目可能由多人协作开发, 每一个人一般会在自己的分支进行修改, 然后再push到远程, 提交merge request之后, 由boss负责将其余分支融合主分支master.

    2. 对自己的实验来讲, 一般只需要一个分支. 不过也可以创建不同分支(例如自己的代码需要apply到不同的项目领域: 虽然涉及到不同的数据, 但训练和测试的逻辑是一致的. 这时对不同应用分别建立分支是很好的选择)
    
    3. 项目被clone下来之后默认的分支是master, 代表主分支.
        1. `git branch` #查看当前分支
        2. `git checkout master` # 切换回主分支
        3. `git branch hedes-dev` #创建hedes-dev分支
        4. `git checkout hedes-dev` # 切换到hedes-dev分支
        5. `git push gitee hedes-dev` # 如果在hedes-dev分支做了改动, 可以提交到远程仓库gitee上
3. 版本
    在某一个分支内, 版本的变化主要通过commit_id来表示.
    1. `git log` # 每次的commit都会产生commit_id, log显示了截止目前为止本地的commit历史
    2. `git checkout hdsed2` # 切换到commit_id的前6位为hdsed2的版本, 常见于DL代码中要求使用特定commit_id的mxnet或者tensorflow
4. 标签
    1. 参考[Git-打标签](https://git-scm.com/book/zh/v1/Git-%E5%9F%BA%E7%A1%80-%E6%89%93%E6%A0%87%E7%AD%BE)
    不同于commit的频繁推进, 我们希望在完成主要的功能(例如baseline版, state-of-art版)之后, 可以打上不同的标签. 方便进行快速版本回退
    1. `git tag -a v0.1 -m 'my version 0.1'` 给自己的代码打标签
    2. `git push gitee v0.1` #将v0.1标签推送到gitee上
### 2.4 一些trick
TODO
## 3. 实验室配置的git
地址是: [wgw-1018主机](http://172.18.34.20/)