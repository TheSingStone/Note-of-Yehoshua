# 工作日志

NOTE：
T：Task  E：Experience P：Purpose

### 2021.04.07

各个IP在driver里的位置：

搜索命令：

1.Gamma：scaler_vpqdev.c



<img src="F:%5C5GitProgram%5C1Notes%5Cpics%5Cimage-20210407174747418.png" alt="image-20210407174747418" style="zoom:67%;" />

写入数据库耗费时间过长；

### 2021.03.29

Z:\merlin6\rtk\kernel\linux\linux-4.14\drivers\rtk_kdriver\rtice\core\rtk_ice.c

~/merlin6/rtk/kernel/linux/linux-4.14/drivers/rtk_kdriver/tvscalercontrol/vip

构造函数默认参数必须最后？



### 2021/02/25-2021/03/01

T1. Mac6P Burn => 为了在6P上实验QGammaTool；=> Fail(没有找到解决办法)，后续决定使用Mac7P做实验；

T2. Mark2 Tool 的验证工作与解决：

​      2.1 Measure Y2R失败；=>确认是IC的问题。LG的Data Path不走Y2R

​      2.2 inv_out_Gamma enable看不出效果；=>在新IC上有效果；

​      2.3 osd_Gamma gamma1R/W失败且看不出画面效果；=>在新IC上有效果；
T3. QGammaMeasure[Beta] 

​     3.0 Daily Task

​     3.1 使用Inventor画出GIF=>导入msgBox；

​     3.2 使用NoteBook实现=>弹出打panel的窗口；

​     3.3 把新算法拆开CStrategy；

T4. QGammaMeasure

​     4.1 实现调整Gamma View曲线功能；

​    		1.初步实现<img src="F:%5C5GitProgram%5C1Notes%5Cpics%5Cimage-20210305143627475.png" alt="image-20210305143627475" style="zoom:33%;" />

​			2.实现legend markers



​     4.2 bug:negative_squared_cross_mark::outputGamma port以现有的LUT作为Base；

​     4.2 Fast Search ： 4.2.1 Retry 二分法；

​                                     4.2.2 更强的规律性；

T5.Merlin7

T6.Mark2:    Output Gamma=>Done；

​     				 OSD Gamma=>Done

​    

T7.Mac7P： OSD Gamma Tools => Done;​​

E1:In the front data path, many IP are processed in YUV color domain to panel. But the IP afterwards, such Contrast, Brightness, sRGB, **Gamma**, Dither, are **processed in RGB color domain**. 

​     

### 2021/02/01

#### Q1.hdmiDebug修改记录

只是删掉 QT       += xlsx 这个声明。

为什么没发现呢？在WIN10上面确实提出这个错误了。但是在jenkins发来的邮件上却没有这个报错。

### 2021/02/02 - 2021/02/05

| Task                                 | Status | comment                                                      |
| ------------------------------------ | ------ | ------------------------------------------------------------ |
| 1.Gamma cmodel修改                   | doing  | 已经询问                                                     |
| 2.Sub Gamma cmodel修改               | doing  |                                                              |
| 3.接屏                               | todo   |                                                              |
| 4.gamma merlin7 FPGA相关case整理     | done   | 其中有两支Case需要和魏存师兄讨论下                           |
| 5.hdmiDebug 最新版更新不到           | done   | 后续修改db存储方式=>只使用vth作为标志，phase按照顺序进行排列即可 |
| 6.QGammaMeasure[Beta]  - QMessageBox |        | 1.建立MessageBox；2.熟悉数据库操作；                         |

QGmmaMeasureBeta:

T1：完成Measure过程中所有需要用户交互的对话框类。
       =>目前完成了窗口的类的构建和放入UnitTest测试

​      问题：

​                  1.图片的路径改变后，加载失败了，还未找到原因；
​      改进想法：

​                    1.加入计时功能，比如如果10s不选择，就会自动进入下面的Flow；

​                    2.窗口的Text部分能否换成html格式，这样一些字样可以加粗，标上颜色；

​                    3.能否把png换成加载GIF格式；

#### E1. 烧录Merlin6的经验：

1.选择的是不带devel的epk，且不需要烧录带rescue的bin档，至少路了for-rtice的bin档；

2.使用ftp7获取micom文件的方法：

<img src="F:%5C5GitProgram%5C1Notes%5Cpics%5Cimage-20210205095245695.png" alt="image-20210205095245695" style="zoom:80%;" />



#### E2. 我们ic代号基本如下：

2875: merlin6
 2874: merlin5
 2873: merlin4 6557
 2873A: merlin6
 2872: Merlin3
 2831: M5P
 2851: MAC6P
 2851M: Merlin5 2020年6月底之前量产 TCL
 2852: MAC6
 2871: Merline2
 2851A(4K): MAC7P 叫做2851A (4K)

2851A (2K)

2833A: mac7P

2823/2824 = MAc7p 2K TV 版本 (沒有 AI PQ)
 2833A = MAc7p 4K TV 版本 (有 AI PQ, DDR4)

2991: M1

2936: MAC4 6583

2841: mac5p
 2861:
 2862: K w memc

2893: H5X
 2892X (TCL) :H5C2

E3.