# HomeWork
无线课程第一次课后作业  
## 作业内容  

1. 我到时候新建一个github组，拉大家进来
2. 编写三组不同切入点，不同目的的monkey的脚本：某个应用的压力测试、点击、应用之间的切换
3. 使用ddms，hierarchyviewer工具，上传截图
4. 安装好对应的模拟器
5. 如果是MacOS的话，安装好ideviceinstaller，使用常用的命令并截图。——在线安装 pip  ideviceinstaller  

## ADB命令练习
1. 查看当前连接设备列表  
adb devices
2. 安装、卸载应用   
adb install xxx.apk  install命令后面是apk文件的文件名 
adb uninstall  package   uninstall后面是apk文件的包名（包名唯一）  
3. 连接多台手机时，指定一台设备进行安装  
adb -s <device SN> install/uninstall  xxx
例子：adb -s 750BCL422B72 install XXX.apk  
4. 关闭/开启adb进程  
adb kill-server  
adb start-server
5. 进入已连接的设备的系统  
adb shell  
查看原生应用  cd /system/app  
查看3rd应用  cd /data/data   需要toot权限  
6. 系统内外的文件传输  
adb push /xx /yy   从PC端/xx路径往手机端/yy路径下传文件  
adb pull  /yy/xx    从手机端/yy路径下往PC端/xx路径下传文件  
7. 查看当前系统事实日志  
adb logcat  ——日志打印到终端  
adb logcat | grep xxx  ——根据xxx来过滤显示日志  
adb logcat > XXX/log.txt  ——日志输出到指定路径下的文件中   

```
引申：grep命令相关  
1、grep参数：   
-I ：忽略大小写 -c ：打印匹配的行数   
-l ：从多个文件中查找包含匹配项   
-v ：查找不包含匹配项的行  
-n：打印包含匹配项的行和行标 

2、RE（正则表达式）  
\ 忽略正则表达式中特殊字符的原有含义   
^ 匹配正则表达式的开始行   
$ 匹配正则表达式的结束行   
\< 从匹配正则表达式的行开始   
\> 到匹配正则表达式的行结束   
[ ] 单个字符；如[A] 即A符合要求   
[ - ] 范围 ；如[A-Z]即A，B，C一直到Z都符合要求   
. 所有的单个字符   
'*' 所有字符，长度可以为0 
```
  
## monkey命令  
 1. monkey是什么？   
Monkey是Android中的一个自带的命令行工具，可以运行在模拟器里或实际设备中，使用安卓调试桥(adb)来运行它。它向系统发送伪随机的用户事件流(如按键输入、触摸屏输入、手势输入等)，实现对应用程序进行压力测试。Monkey测试是一种为了测试软件的稳定性、健壮性的快速有效的方法  
2. adb shell monkey-help   

### 三个不同切入点的monkey命令
* 切入点1  
测试多应用组合，常规测试，依据常见的用户操作，滑动、点击、横竖屏、系统键，不忽略异常  
* 切入点2  
针对某一个应用，对某个事件提高很高的的百分比，进行专项测试 例如：--pct-touch 90
* 切入点3  
对某一个应用进行压力测试，30w，忽略一切异常，忽略一切超时，低延时

## DDMS练习
* 命令行中输入 ddmms，打开ddms
* 左上角区域显示当前设备上的安装包信息，root之后可见，未root不可见
* 右上角区域功能不常用，可不管
* 左下角区域可显示创建好的Filter，点击+号可创建新的Filter，用来过滤制定的log信息
* 右下角区域，实时显示设备或某个应用的日志信息

## Hierarchyviewer练习
* 具体来说主要功能有2个：  
	- 从可视化的角度直观地获得UI布局设计结构和各种属性的信息，帮助我们优化布局设计；  
	- 结合debug帮助观察特定的UI对象进行invalidate和requestLayout操作的过程。
* 命令行中输入 hierarchyviewer，打开hierarchyviewer
* 选中某个activity，点击 Load View Hierarchy按钮，进入层次结构图页面
* 选中某个view，可以查看view的具体信息，id信息，渲染时长（便于优化UI性能）
