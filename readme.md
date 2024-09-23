
# 环境配置与运行

# 1 环境配置

# 1.1 编译安装
+ 基于ubuntu20.04-x86架构
+ 保证eigen, 安装ros会自动安装eigen
~~~python
# 1 依赖
sudo apt install mesa-common-dev freeglut3-dev coinor-libipopt-dev libblas-dev liblapack-dev gfortran liblapack-dev coinor-libipopt-dev cmake gcc build-essential libglib2.0-dev

sudo apt install openjdk-8-jdk libqt5gamepad5-dev

# 2 lcm
cd third-party/lcm-1.5.0
mkdir build && cd build
cmake ..
sudo make install

# 3 拉取源码
git clone https://github.com/linClubs/Cheetah-Software.git
cd Cheetah-Software
mkdir build && cd build

# 4 运行make_types.sh
./../scripts/make_types.sh

# 5 编译 
cmake ..
make -j20
~~~

## 1.2 报错汇总

~~~python
# 1 下载googletest失败
## master改成main
download_project(PROJ googletest
GIT_REPOSITORY https://mirror.ghproxy.com/https://github.com/google/googletest.git
GIT_TAG main   # master 改成main
${UPDATE_DISCONNECTED_IF_AVAILABLE}
QUIET
)

# 2 qt找不到路径
## 2.1 输入qmake -query打印qt相关路径
qmake -query
## 2.2 找到QT_INSTALL_PREFIX
QT_INSTALL_PREFIX:/usr
## 2.3修改qt的CMAKE_PREFIX_PATH路径
## 在./sim/CMakeLists.txt的18行左右find_package(Qt5Core CONFIG REQUIRED)上面添加一下代码
set(CMAKE_PREFIX_PATH /usr)

# 3 fatal error: stropts.h: 没有那个文件或目录
修改/robot/src/rt/rt_serial.cpp文件
注释掉17行#include <asm/termios.h>、24行#include <stropts.h>
#include <asm/termbits.h>
#include <sys/ioctl.h>

# 4 eigen报错
vscode全局搜索，修改2处
/usr/local/include/eigen3改成/usr/include/eigen3
~~~

# 2 运行
~~~python
# 1 都在build目录下执行
cd build

# 2 启动仿真
./sim/sim
# 选择MINI-Cheetah和Simulator，然后点击start

# 3 启动Controller
./user/MIT_Controller/mit_ctrl m s
# use_rc 1 遥控模式
# control_mode 1 到3，4行走，9 后空翻 
~~~
