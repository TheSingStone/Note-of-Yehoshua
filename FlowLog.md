# 工作日志

NOTE：
T：Task  E：Experience P：Purpose





### 2021/02/01

#### 1.hdmiDebug修改记录

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

