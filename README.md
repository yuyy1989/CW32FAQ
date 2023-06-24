---
title: "CW32常见问题一览"
author: "流浪剑士（977066873）"
html:
    toc: true
    toc_depth: 6
    collapsed: true
    smooth_scroll: true
--- 
#CW32常见问题一览  
by流浪剑士 2023.6.24 

目录
---
[TOC]

## 文档编写目的 
本文档旨在收集新手入门时的遇到各种问题和相应解决方法，芯源官网有个入门手册，建议先看一下，文档中涉及的文件度盘链接：  
链接：<https://pan.baidu.com/s/1tUGW5rmnOdn8aI2LJ-ICTQ?pwd=d12l>  
提取码：d12l  
![](./Images/1.png)  


## CW32系列命名规则  
![](./Images/2.png)

## 开发环境的安装  
开发要用MDK，建议安装5.36版本，这个版本有AC5编译器，之后的版本不再集成  
安装CW32的pack包，可以从武汉芯源官网下载固件库  
<https://www.whxy.com/support/filelist/13>  
![](./Images/3.png)  
pack包在压缩包里，直接双击安装即可  
![](./Images/4.png)  

## MDK C251 C51共存  
可以参考群文件里的教程  
![](./Images/5.png)  
不过本人没有按照这个来装，先装了MDK5.38a，印象中是C251和C51装到最后询问是否替换文件时都选了不替换  

## AC5编译器的安装  
CW32要用AC5编译器，用AC6编译会报错，可能是这样的错误，还有一堆的警告  
![](./Images/6.png)  
MDK5.37开始已经不集成AC5了，想用最新版本有两个方法：  
**方法1：** 最简单的方法是先安装5.36再安装最新版本，这样AC5可以自动集成到MDK中。  
**方法2：** 安装最新版本后手动添加AC5编译器  
下载这个文件并解压出来  
![](./Images/7.png)  
安装完MDK后把ARMCC文件夹手动放到keil安装目录的ARM文件夹中  
![](./Images/8.png)  
然后在keil中手动添加，选择刚刚添加的文件夹  
![](./Images/9.png)  
![](./Images/10.png)  

## 针对AC6编译器的适配  
如果不想折腾安装AC5编译器，可以对现有工程代码修改以适应AC6的编译规则  
CW32的例程直接用AC6编译的话一般会报这个错误  
![](./Images/11.png)  
AC6中__weak这个关键字不能被识别，改为__WEAK就好了，关键字的不同可以看这个图  
![](./Images/12.png)  
更多的关于MDK适配AC6的内容可以下载KEIL官方的文档进行查看  
<https://developer.arm.com/documentation/kan298/latest/>  
或者看ARM的AC6介绍，里面也有说明如何从AC5转向AC6  
<https://developer.arm.com/documentation/100068/latest/>  

## 用AC6编译有中文的代码会报-Winvalid-source-encoding的警告  
![](./Images/13.png)  
可以在下方如图位置填入-Wno-invalid-source-encoding 将该警告信息屏蔽  
![](./Images/14.png)  

## 例程移动之后编译失败  
官方例程的库函数文件没有包含在工程目录中，建议复制库函数文件夹到工程目录并删除原来的库函数文件重新添加  
![](./Images/15.png)  
另外还要修改头文件包含路径，以这个工程目录为例  
![](./Images/16.png)  
要修改成这样  
![](./Images/17.png)  
如果懒得自己整合库文件，可以下载群文件或网盘中的工程模板，里面已经整合好库文件  
![](./Images/18.png)  

## 不使用例程或模板，从头新建一个CW32的点灯工程  
先创建一个文件夹，把官方库和启动文件放进去，可以按照自己喜欢的工程创建额外的文件夹  
![](./Images/19.png)  
打开Keil，选择project-new uVision Project  
![](./Images/20.png)  
选择刚才创建的文件夹  
![](./Images/21.png)  
在接下来的窗口中选择你要用到的芯片  
![](./Images/22.png)  
在接下来的窗口中勾选  
![](./Images/23.png)  
按照自己喜好在工程内创建分组  
![](./Images/24.png)  
引入必要的库文件  
![](./Images/25.png)  
选择工程目录下的Libraries\src中的文件  
![](./Images/26.png)  
你可以直接全部添加，也可以只添加自己需要的，其中system_cw32f030.s在工程目录根目录下，这里只添加了点灯必要的  
![](./Images/27.png)  
添加库头文件路径  
![](./Images/28.png)  
![](./Images/29.png)  
这里可以手动输入路径或者点击右面的...选择文件夹  
![](./Images/30.png)  
选择工程目录中的Libraries\inc文件夹  
![](./Images/31.png)  
keil会自动转为相对路径  
![](./Images/32.png)  
![](./Images/33.png)  
如果有自己定义的头文件需要包含，也可以按照上面的流程添加，如果想使用绝对路径直接在这个界面输入路径即可，路径间用英文的;分隔  
![](./Images/34.png)  
接下来配置工程其它参数，仿照官方工程的参数配置即可  
![](./Images/35.png)  
![](./Images/36.png)  
![](./Images/37.png)  
![](./Images/38.png)  
接下来创建一个main.c文件  
![](./Images/39.png)  
![](./Images/40.png)  
在新建的main.c中写好点灯用的代码，编译并烧录运行  
![](./Images/41.png)  

## 编译报cmsis_version.h或__COMPILER_BARRIER的错误  
![](./Images/42.png)  
![](./Images/43.png)  
这两个都和CMSIS CORE有关，要勾选如下选项，例程里应该已经默认勾选了，注意CORE的版本，低于5.1.0勾上也还会报错，可以尝试安装网盘或群文件里的ARM.CMSIS.5.9.0.pack或者直接升级MDK  
![](./Images/44.png)  
ARM.CMSIS.5.9.0.pack的发布地址  
<https://github.com/ARM-software/CMSIS_5/releases>  
或者  
<https://www.keil.arm.com/packs/cmsis-arm/versions/>  

## 编译报找不到assert_failed的错误  
![](./Images/45.png)  
多见于自己新建的工程，两个解决方法：  
**方法1：** main.c中添加  
\#ifdef  USE_FULL_ASSERT  
void assert_failed(uint8_t *file, uint32_t line)  
{  
}  
\#endif   
**方法2：** 在base_types.h中注释掉下面的内容  
![](./Images/46.png)  

## 编译报L6200E:Symbol xxxx multiply defined错误
**第1种**  
![](./Images/47.png)  
上图的错误是某个函数被重复定义了，例如你在a.c里定义了函数void func()，在b.c里也定义了一个void func()编译时就会出现这个错误，可以根据提示到相应的源文件里修改或删除重复定义的函数。对于图中这个示例是usart.c和interrupt_cw32f030.c中都定义了UART1_IRQHandler这个函数，删掉一个即可。interrupt_cw32f030.c是官方例程提供的一个统一的中断函数入口，如果你在编程中想要在自己的文件重处理中断可以删除这个文件来避免重复定义的问题。  
**第2种**
![](./Images/48.png)  
这个图的错误是system_cw32f030.c在工程中被重复包含了，删除重复的只保留一个即可  

## 编译报No space in xxxxx的错误  
![](./Images/49.png)  
检查一下这里的配置，如果和下图配置一样的话还有这个错误那可能真的是代码超了，想办法精简一下代码  
![](./Images/50.png)  

## 编译报incomplete type is not allowed  
![](./Images/51.png)  
如果报错发生在库函数中，有可能是工程设置中的C99 Mode没勾选  
![](./Images/52.png)  

## 烧录失败，提示Could not load file xxxxx.axf  
检查是否已经编译成功，一些新入门不熟悉开发环境的可能打开工程后直接烧录就会出现这个错误  
![](./Images/53.png)  
在编辑完代码后要先点击编译，编译成功后才能烧录  
![](./Images/54.png)  
编译失败会显示Target not created，如下图  
![](./Images/55.png)  
这时候就需要按照提示的错误信息修改代码并重新编译，编译成功如下图，这时就可以进行烧录了  
![](./Images/56.png)  

## 烧录失败  
查看是否选择了正确的烧录器  
![](./Images/57.png)  
烧录器的设置，端口这里要选SW  
![](./Images/58.png)  
检查连线，SWD(SWIO)接PA13 SWCK连接PA14  
![](./Images/59.png)  
连接正确这里会显示  
![](./Images/60.png)  
再查看是否选择了正确的烧录算法  
![](./Images/61.png)  
如果烧录时提示找不到FLM文件  
![](./Images/62.png)  
有两个解决方法：  
**方法1：** 可以手动复制FLM文件到这个文件夹  
![](./Images/63.png)  
安装完pack文件后flm文件可以在这个位置找到  
![](./Images/64.png)  
**方法2：** 把原来的算法文件删掉重新添加，列表里找不到CW32的请确认是否安装了pack，如果已安装请确认device标签中芯片是否选择正确，如果芯片也选择正确尝试点击ok关闭工程配置窗口后再重新打开  
![](./Images/65.png)   
![](./Images/66.png)  

## 如何进行ISP下载  
如果PA13 PA14被配置成普通IO导致SWD烧录不能识别，或者手头没有SWD的烧录器，可以通过串口进行ISP下载  
要进入ISP烧录模式<font color=#FF0000>需要将BOOT引脚上拉后再通电</font>  
![](./Images/67.png)  
PA13连接串口工具的TX，PA14连接串口工具的RX  
<font color=#FF0000>注意：针对F030要多用一根线连接串口工具的RST或DTR到芯片的RST，请注意使用的串口工具是否有RST引脚，烧录全程需要保持BOOT上拉</font>  
打开CW32_Pragrammer，这个软件可以在武汉芯源官网下载，网盘里也有，官网下载地址<https://www.whxy.com/support/filelist/18>  
![](./Images/68.png)  
选择串口后点击连接  
![](./Images/69.png)  
选择好芯片和固件后点击在线编程即可完成烧录  
![](./Images/70.png)  
<font color=#FF0000>注意：针对F030供电连接那里要选择 目标芯片自供电，RST复位</font>  
烧录成功，感觉比用daplink还快  
![](./Images/71.png)  

## 饭盒派的屏幕不亮  
烧录器SWD的3.3V带不动屏幕背光，用TYPE-C数据线外接个5V供电即可  

## 小蓝板没有晶振  
没有晶振不影响使用，使用芯片内置时钟就够了，绝大部分例程也都是用的内部时钟  

## 烧录器指示灯颜色和视频或手册介绍不一样  
指示灯颜色不影响烧录器功能，能正常烧录就行  

## 程序烧录完成后不运行  
检查一下这个选项有没有勾上，没勾上的话需要手动复位或重新上电  
![](./Images/72.png)  


