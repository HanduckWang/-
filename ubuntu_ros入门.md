# ubuntu与ros入门
https://blog.csdn.net/weixin_42949808/articledetails/110038095?spm=1001.2014.3001.5506
http://www.autolabor.com.cn/book/ROSTutorials/chapter1/14-ros-ji-cheng-kai-fa-huan-jing-da-jian/142-an-zhuang-vscode.html
## ubuntu基础
* 文件系统：与windows不同，Ubuntu 没有盘符这个概念，只有一个根目录 /，所有文件都在它下面
![Alt text](image.png)
* 常用命令
  * ls查看当前文件夹下的内容，pwd查看当前所在文件夹
  * cd：cd /回到根目录； cd .当前目录；cd ..退回上一级目录；cd ../..退回上两级目录；cd ~，回到用户目录home/
  * mkdir：mkdir -p递归创建多个目录，可选参数为-p

## ros基础
* ros编程 tab补齐
  1. 创建工作空间：mkdir -p 名称/src，cd，catkin_make（此时除了创建的src多出build和devel文件夹）
  2. 创建一个功能包：cd src，catkin_make_pkg 包名 roscpp rospy std_msgs，即src中放功能包（此时会多出一个与包名相同的文件夹即功能包（此文件夹中有include文件夹、src文件夹、CMakelsts.txt、 package.xml），还有一个CMakelists.txt的文件）
  3. 编辑源文件：（在src/包名文件夹/src中创建）
  4. 编辑配置文件：（在src/包名文件夹/CMakelist中），add_executable（任意映射名称 src/源文件名称后缀），target_link_libraries第一个参数改成映射名称
  5. 编译并执行：回到工作空间目录，catkin_make编译，新开窗口启动roscore，输入soure ./devel/setup.bash（固定命令在该窗口下刷新环境变量），执行rosrun 包名 映射名
  * 补充：对于source为了避免每次刷新，在主目录下找到(ctrl+h)隐藏文件.bashrc使用记事本打开添加该刷新命令.换成文件夹名字，在窗口source .bashrc.
  *  对于python，12步骤相同
    3. 编辑源文件：在src/包名文件夹中新建scripts文件夹（与后src平级），添加python文件；注意需要指定解释器；多一步，需要在scripts中使用chmod +x 自定义文件名.后缀 添加可执行权限
    4. 编辑配置文件：（在src/包名文件夹/CMakelist中）catkin_install_python，在scripts/修改名字，noetic之前版本不需配置
    3. 同，rosrun接具体文件名
---
* ros中使用vscode：需要安装c++、py、cmake tools，py解释器选择usr/bin/python3
  1. 创建工作空间：同 ，并在工作空间下启动code .
  补充：配置vscode中配置编译参数ctrl shift b，选择catkin_make:build后方齿轮配置，默认生成.vscode文件（配置3个json），保证之后ctrl shift b编译
  2. 创建功能包：右键src，create catkin package，录入包名，依赖名，生成结果同
  3. 编辑源文件写代码
  4. 编辑配置文件同，txt可以用makefile格式看好看一些
  5. 直接在终端+号roscore
---
* ros常用指令
  * rosnode
  * rostopic
  * rosmsg
  * rosservice
  * rossrv
  * rosparam
---
* ros通信机制
  