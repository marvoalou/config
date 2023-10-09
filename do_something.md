### zsh不显示conda环境名称

原因是主题覆盖
找到powerlevel9k(我的主题)的theme文件，其中**defined POWERLEVEL9K_LEFT_PROMPT_ELEMENTS**参数表明了美化栏的内容，在context前加一个anaconda
zsh通过配置文件source文件来调用主题和插件

### 禁用

创建文件/etc/modprobe.d/blacklist-nouveau.conf，添加如下文本：
blacklist nouveau
options nouveau modeset=0
重新生成initramfs
sudo update-initramfs -u

## use nvidia and cuda

forbid the nouveau first(in the config file)

install nvidia driver
use `nvidia-smi` can see the version of your computer's GPU

install cuda (make sure the version is correct)

meet the error:

- `lsmod | grep nvidia` to configure the model which is nvidia in use
- shutdown the model and uninstall nvidia driver
- reinstall nvidia driver and go on

*one problem is that the cuda version is not match to the real GPU version*
solution:
neglect the driver selection when you install cuda

## 无法使用中文
ubuntu20.02 fcitx导致
`sudo apt-get remove fcitx*` 
`sudo apt-get purge fcitx*`
卸载,reboot

## tmux配置文件
手动创建.tmux.conf
`sudo cat /usr/share/tmux/tmux_example.conf >> ~/.tmux.conf`

## 配置zsh自动补全
需要创建zsh文件

## 安装deb

`sudo dpkg -i <package>`
依赖问题
`sudo apt-get install -f`

## tensorflow和cuda,cudnn版本不兼容
多版本cuda：

x CUDA Installer se Agreement                                                  x
x - [ ] Driver                                                                 x
x      [ ] 418.39                                                              x
x + [X] CUDA Toolkit 10.1                                                      x
x   [ ] CUDA Samples 10.1                                                      x
x   [ ] CUDA Demo Suite 10.1                                                   x
x   [ ] CUDA Documentation 10.1                                                x
x   Install                                                                    x
x   Options  

修改软连接：
`sudo ln -snf /usr/local/cuda-10.1 /usr/local/cuda`

修改配置：
#cuda
export PATH=/usr/local/cuda-10.0/bin:$PATH  
export LD_LIBRARY_PATH=/usr/local/cuda-10.0/lib64:$LD_LIBRARY_PATH

发现：nvcc -V现在使用的cuda版本和软连接(stat cuda)不一致  
solve：$PATH的前后优先级

## cudnn install
下载  
`tar -xvf`解压
`sudo cp include/cudnn*.h /usr/local/cuda-12.2/include`
`sudo cp -P lib/libcudnn* /usr/local/cuda-12.2/lib64`
`sudo chmod a+r /usr/local/cuda-12.2/include/cudnn*.h /usr/local/cuda-12.2/lib64/libcudnn*`
放到对应的cuda版本里  
修改配置文件

查看  
`cat /usr/local/cuda/include/cudnn_version.h | grep CUDNN_MAJOR -A 2`

## tensorflow-gpu
一个深度学习框架
`pip install tensorflow-gpu==2.3.0`

## 修改keras的运行的框架
配置文件(json)修改backend

## env用于查看环境变量

## one-hot编码
深度学习为了计算距离，需要将特征值数字化，并且不能是连续离散值，所以几个特征值用几维向来表示空间中的位置

## markdown换行
结尾空格*2