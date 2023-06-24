# CW32常见问题一览
by流浪剑士 2023.6.24<br />
本文档旨在收集新手入门时的遇到各种问题和相应解决方法，芯源官网有个入门手册，建议先看一下，文档中涉及的文件度盘链接：<br />
链接：https://pan.baidu.com/s/1tUGW5rmnOdn8aI2LJ-ICTQ?pwd=d12l <br />
提取码：d12l<br />
![](./Images/1.png)
## 目录
- [CW32系列命名规则](##CW32系列命名规则)
- [开发环境的安装](##开发环境的安装)
MDK C251 C51共存	3
AC5编译器的安装	3
针对AC6编译器的适配	4
用AC6编译有中文的代码会报-Winvalid-source-encoding的警告	6
例程移动之后编译失败	6
不使用例程或模板，从头新建一个CW32的点灯工程	7
编译报cmsis_version.h或__COMPILER_BARRIER的错误	17
编译报找不到assert_failed的错误	18
编译报L6200E:Symbol xxxx multiply defined错误	19
编译报No space in xxxxx的错误	19
编译报incomplete type is not allowed	20
烧录失败，提示Could not load file xxxxx.axf	21
烧录失败	22
如何进行ISP下载	25
饭盒派的屏幕不亮	27
小蓝板没有晶振	27
烧录器指示灯颜色和视频或手册介绍不一样	27
程序烧录完成后不运行	27
编译烧录了从官网下载的gpio_blink例程但是小蓝板指示灯或大学板底板指示灯没有闪烁	27
串口接收到的数据与程序内发送的数据不同	28
设置HSI为1分频后程序不运行	29
PLL倍频后程序不运行	30
KEIL内调用外部编辑器	30
在VSCode中编辑编译和烧录	32
JLINK JFLSH添加CW32的芯片支持	34
VSCode+MSYS2+arm-none-eabi开发环境的搭建	35
VSCode中使用Cortex Debug+JLinkGDBServer进行调试	38

## CW32系列命名规则
![](./Images/2.png)

## 开发环境的安装
开发要用MDK，建议安装5.36版本，这个版本有AC5编译器，之后的版本不再集成<br />
安装CW32的pack包，可以从武汉芯源官网下载固件库<br />
https://www.whxy.com/support/filelist/13<br />
![](./Images/3.png)