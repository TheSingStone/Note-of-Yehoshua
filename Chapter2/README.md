# 第二章 Tool相关

## 2.1 CnPack技巧

1.Shift+F2启用或停用；

2.Ctrl+Shift+V局部变量编辑区域；

3.专家包的source目录里有cnDebug.pas文件，这是一个供运行期间输出调试的接口单元，使用cnDebugViwer查看；

4.代码的自动完成功能：把安装的source目录PSDedEx目录放到 搜索路径中；

## 2.2 Gamma Measure logFile路径设置 ：

~~~C++
logFilePath = sysconfig.get_path(KEY_PATH_ROOT).c_str();

logFilePath += static_cast<AnsiString>("res/log/logFile.txt");

if(logFile != NULL)

  logFile.close();

logFile.open(logFilePath.c_str(),ios::app);

'logFile.clear();
~~~

## 2.3 Tool Global

\1.platform.db蕴含了注册IC的信息——比如说当新增IC的时候，光更新源代码是无法在Tool里增加这个页面的信息的；

\2.当使用BCB的时候Can’t Create CBuilder6.0/Bin/InitCC32.exe的时候，使用右击管理员模式可以打开；

\3.有时候为了获得rBus的信息，用寄存器的虚拟名字搜索不到时，可以考虑搜rBus内部的信息；

也可以使用notepad ++的在文件中搜索的功能，速度会很快。

\4.添加.cpp文件时，除了要包对应的头文件，不要忘记使用Add To Project，同理可添加.lib文件等；

\5. .h文件不可包太多头文件；

 FYI：在整理Global文件中必须的文件时，比较简便的方法是让编辑器告诉你哪些文件缺失，这样整理起来会快一点。

\6. 使Tab不可见：TabSheet1->TabVisible = false;

\7. 使用SecureCRT记得要断掉之后，才能在Tool里进行读写操作。

\8.  测试使用的Tool，可以用platform.db release比较轻便的Tool发给测试人员。

\9. 如果想要最小的测试版的Tool，则使用standalone版本。

\10.查看Tool的Owner直接查看code的log，看看最近上传的人。

## 2.4 在VideoPath中添加PTG步骤

因为BCB版本的VideoPath是用xml写UI部分的，所以修改分为两大部分：

1. D:\QRtice\res\modules\home\VideoPath\merlin5\VideoPath.xml

( 这里修改的是添加的部件的基本属性：

~~~xml
<item class="ptg" caption="memc_mute_ctrl" mode="img/patterns/MEMC/Blue_Screen"/> 
~~~

2. 对应上一步中的路径中的list 文件，描述了部件的选择属性。

3. 修改D:\QRtice\src\modules\independ\VideoPath\block\CIPBlock(IC名称).cpp中的实际操作部分——比如读写寄存器；

PS：最新的VideoPath Q中已经可以直接添加。

## 2.5 在QT中实现读写和加载图片：

### 2.5.1 读写

~~~C++
#include "CMainController.h"
RT_pIo(CMainController);
RT_pc(CMainController);

    bool ferr = false;
    uint regVal = 0, sceneVal = 0;
    pIo->_StopByMode();
    try{
       ferr = pIo->_BurstReadWord(0xb802ca00,&regVal);
    }catch(...){
       pc->setMessage("Connect Fail",'x');
    }
    if(!ferr)
        pc->setMessage("Read Fail,Check Connect",'x');
sceneVal = (regVal) & 0x08000000; /*这里使用按位与来实现特定位读*/

regVal = regVal ^ 0x08000000;
pIo->_BurstWriteWord(0xb802ca00,&regVal); /*这里使用异或来实现特定位写*/

~~~

### 2.5.2 加载图片

~~~C++
QImage *img=new QImage;
/*图片路径可在qrc文件夹里通过右击选择图片路径*/
img->load(":/Spbtn_VIP_Terminal_Close.png");
/*这里通过QImage来实现label加载图片*/
ui->lblScene->setPixmap(QPixmap::fromImage(*img));

~~~

## 2.6 003: Write Error

当StopByMode(true) 与 RunByMode()重叠使用时，会报错误。一定要确保二者夹住的区域不能让再出现它们。

## 2.7 CA 410引起的支线程的混乱问题

1.首先C++ Builder可以标注线程的数目；

2.帮助查看Timer是否会开启支线程？

## 2.8 ScrollBar的滑块闪烁的问题

在窗体上放一个edit然后在ScrollBar的OnScroll事件中让edit获得焦点。

~~~C++
void __fastcall TForm1::ScrollBar1Scroll(TObject *Sender,
   TScrollCode ScrollCode, int &ScrollPos)
{
    **Edit1->SetFocus();**
}
~~~

使用OnChange函数之后，往往会使得焦点失去，通过**SetFocus()**函数重新获得焦点。

## 2.9 打开文件常见的防呆语句

```C++
if(dlgOpen3->Execute()){                   
    file_path = dlgOpen3->FileName.c_str();
    mmo3->Clear();
    mmo3->Lines->LoadFromFile(file_path);
}else{
    return;				/*预防打开后没有选中就关闭*/
}
```
