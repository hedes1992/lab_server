1. tmux 配置
* 鉴于所内网络的不稳定，登陆服务器之后应该立马进入一个tmux session（会话）
* 新建tmux 会话: `tmux -2 new -s zhangsan`
* 进入已有会话: `tmux attach -t zhangsan`
* 退出当前会话
    - 会话内休眠当前会话：ctrl-b + d
    - 会话外休眠会话： `tmux detach -t zhangsan`
* 杀死当前会话: `tmux kill-session -t zhangsan`
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