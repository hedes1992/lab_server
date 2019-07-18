## cuda 安装
1. cuda 安装
- cuda 安装包下载地址(https://developer.nvidia.com/cuda-80-ga2-download-archive)
- example: [cuda8 安装步骤](https://github.com/hedes1992/lab_server/issues/1)
2. cudnn 安装(如无要求可不装..., 装了更快不过)
- cudnn7 安装包下载地址(https://developer.nvidia.com/rdp/cudnn-archive)
- 需要下载适合cuda对应版本的cudnn
3. 多版本cuda的使用
- example: `/usr/local/cuda-8.0` 和 `/usr/local/cuda-10.1` 分别安装了对应版的cuda
- 在自己的 `~/.bashrc` 中加入如下设定
```
export CUDA_PATH=/usr/local/cuda-10.1
export PATH=$CUDA_PATH/bin:$PATH
export LD_LIBRARY_PATH=$CUDA_PATH/lib64:$LD_LIBRARY_PATH
# 以下两行不一定加, 主要有cuda相关操作子的编译时可能用到
export C_INCLUDE_PATH=$CUDA_PATH/include:$C_INCLUDE_PATH
export CPLUS_INCLUDE_PATH=$CUDA_PATH/include:$CPLUS_INCLUDE_PATH
```
## pytorch 安装
### 采用pip安装
* 截至目前, 没有看到pytorch有cuda10.1的编译版本, 不保证在cuda8上的包安装好之后能在cuda10.1的机器上用, 所以一定注意cuda版本, cudnn版本 和 pytorch版本以及python和pip的版本
- 推荐 pip 安装
- pip 设置清华源来加速, 参考[pip x tsinghua](https://mirror.tuna.tsinghua.edu.cn/help/pypi/)
- example1: pip 安装 pytorch1.0.1+cuda80的示例, 参考[pytorch 不同版本](https://pytorch.org/get-started/previous-versions/)
`pip install torch==1.0.1 -f https://download.pytorch.org/whl/cu80/stable`
- example2: pip 安装 pytorch1.1.0+cuda10的示例
```
pip3 install https://download.pytorch.org/whl/cu100/torch-1.1.0-cp37-cp37m-linux_x86_64.whl
pip3 install https://download.pytorch.org/whl/cu100/torchvision-0.3.0-cp37-cp37m-linux_x86_64.whl
```
- 本地安装

```
wget -c https://download.pytorch.org/whl/cu100/torch-1.1.0-cp37-cp37m-linux_x86_64.whl
pip install ./torch-1.1.0-cp37-cp37m-linux_x86_64.whl
pip install torchvision
```
### 采用conda安装
* 参考官网(安装基于cuda10的pytorch 1.0.1版)
`conda install pytorch==1.0.1 torchvision cudatoolkit=10.0 -c pytorch`