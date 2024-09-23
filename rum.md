# 

+ 保证eigen, 安装ros会自动安装eigen
~~~python
sudo apt install mesa-common-dev freeglut3-dev coinor-libipopt-dev libblas-dev liblapack-dev gfortran liblapack-dev coinor-libipopt-dev cmake gcc build-essential libglib2.0-dev

sudo apt install openjdk-8-jdk libqt5gamepad5-dev

# Could NOT find Java
cd third-party/lcm-1.5.0
mkdir build && cd build
cmake ..
sudo make install

# 
./../scripts/make_types.sh
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