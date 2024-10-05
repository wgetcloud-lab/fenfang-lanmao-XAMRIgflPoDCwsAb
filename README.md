[合集 \- Ubuntu强化学习合集(3\)](https://github.com)[1\.命令行gcc \-v和g\+\+ \-v输出版本不一致09\-27](https://github.com/hassle/p/18435916)[2\.crypt.h：No such file or directory 报错处理09\-28](https://github.com/hassle/p/18437045)3\.ROS基础入门——实操教程10\-04收起
## ROS基础入门——实操教程




---


### 前言


本教程实操为主，少说书。[可供参考的文档](https://github.com)中详细的记录了ROS的实操和理论，只是过于详细繁杂了，看得脑壳疼，于是做了这个笔记。




---


[![](https://img2024.cnblogs.com/blog/3382553/202410/3382553-20241004202207569-503292158.jpg)](https://img2024.cnblogs.com/blog/3382553/202410/3382553-20241004202207569-503292158.jpg)
Ruby Rose，放在这里相当合理


---


本文初编辑于2024年10月4日


CSDN主页：[https://blog.csdn.net/rvdgdsva](https://github.com)


博客园主页：[https://github.com/hassle](https://github.com)




---


### 一、安装【virtualbox】【Ubuntu】【ROS】


~~前人栽树，后人乘凉~~


[安装virtualbox教程](https://github.com):[西部世界官网](https://tianchuang88.com)


[安装Ubuntu教程](https://github.com)


[安装ROS教程](https://github.com)


[测试ROS教程](https://github.com)


### 二、文件创建


#### 2\.1创建工作空间和初始化


[此处参考](https://github.com)（选看）


在ubuntu主界面按下(ctrl \+ alt \+ T)打开命令行，然后依次输入下面的命令



```
mkdir -p test（这是自定义空间名称，爱叫什么叫什么）/src
cd test（这是自定义空间名称，爱叫什么叫什么）
catkin_make

```

生成了下面的文件树



```
....    
└── test(文件夹，意为工作空间，第一行代码运行时被创建)
    ├── build(文件夹，意为编译空间，第三行代码运行时被创建)
    │   ├── ...
    ├── devel(文件夹，意为开发空间，第三行代码运行时被创建)
    │   ├── setup.bash
    │   ├── setup.sh
    │   ├── ...
    └── src(文件夹，第一行代码运行时被创建)
        └── CMakeLists.txt （别动这个）

```

#### 2\.2导入包


生成一个基于三个库的ROS包，其中：roscpp是使用C\+\+实现的库，rospy是使用python实现的库，std\_msgs是标准消息库



```
cd src
catkin_create_pkg testpkg（这是ROS包名，爱叫什么叫什么） roscpp rospy std_msgs


```

此时src文件树变动



```
....    
└── test
    ├── build
    │   ├── ...
    ├── devel
    │   ├── setup.bash
    │   ├── setup.sh
    │   ├── ...
    └── src
		└── CMakeLists.txt （别动这个！！！动的是下面那个同名文件，别搞错了）
		└── testpkg
            ├── CMakeLists.txt（执行cpp和py代码需要修改此处）（2.4涉及此处）
            ├── include
            │   └── testpkg
            ├── package.xml
            └── src（此处存放cpp代码）（2.3涉及此处）


```

#### 2\.3 编写Cpp与Py程序


[Cpp详细教程](https://github.com)(教程浓缩成下面一句话了，看完教程感觉脑子很乱的话照着下面的话去做就行)


一句话概括：需要在src（源文件空间）······\> testpkg（ROS包名，爱叫什么叫什么）······\> src文件夹（用于存放cpp文件）中存放编写好的cpp文件


[Py详细教程](https://github.com)（同上）


一句话概括：需要在src（源文件空间）······\> testpkg（ROS包名，爱叫什么叫什么）······\> scripts文件夹（用于存放py文件，需要手动创建该文件夹）中存放编写好的py文件


#### 2\.4 Cmakelist.txt文件改写


##### 2\.4\.1Cpp程序：


在自定义命名包的 CMakeLists.txt（执行cpp和py代码需要修改此处）内修改第136行和第149\-151行 为


具体行数因版本不同可能有所变动


注意映射名（映射名就是随便写的名，别写test就行）可与cpp源文件名相同



```
add_executable(映射名
  src/源文件名.cpp
)
target_link_libraries(映射名
  ${catkin_LIBRARIES}
)


```

##### 2\.4\.2python程序：


在自定义命名包的 CMakeLists.txt（执行cpp和py代码需要修改此处）内修改第162\-165行 为


具体行数因版本不同可能有所变动


注意这里Py程序是**不需要映射名**的



```
catkin_install_python(PROGRAMS scripts/源文件名.py
  DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

```

#### 2\.5编译并运行程序


##### 2\.5\.1Cpp程序：


在自定义空间名称（2\.1中创建的）中按下(ctrl \+ alt \+ T)打开命令行，依次输入



```
catkin_make
roscore

```

在自定义空间名称（2\.1中创建的）中按下(ctrl \+ alt \+ T)打开**另一个**命令行，依次输入



```
source ./devel/setup.bash
rosrun 包名(2.2中创建的) 映射名(2.4中创建的)

```

##### 2\.5\.2Python程序：


在自定义空间名称（2\.1中创建的）中按下(ctrl \+ alt \+ T)打开命令行，依次输入



```
chmod +x 源文件名.py
catkin_make
roscore

```

在自定义空间名称（2\.1中创建的）中按下(ctrl \+ alt \+ T)打开**另一个**命令行，依次输入



```
source ./devel/setup.bash
rosrun testpkg（ROS包名，爱叫什么叫什么，2.2中创建的） 源文件名.py(2.4中创建的)

```

 \_\_EOF\_\_

   El Psy Kongroo!  - **本文链接：** [https://github.com/hassle/p/18447212](https://github.com)
 - **关于博主：** 研二计算机遥感方向转强化学习方向，喜欢英国源神、杀戮尖塔、香蕉锁头、galgame，和下午的一杯红茶。
 - **版权声明：** 本博客所有文章除特别声明外，均采用BY\-NC\-SA 许可协议。转载需要注明出处
 - **声援博主：** 点个赞再走吧，初音未来会护佑每一位虔诚的信徒！
     
