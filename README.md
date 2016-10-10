#DOL描述
##### 1. Distributed Operation Layer :
The distributed operation layer (DOL) is a software development framework to 
program parallel applications. The DOL allows to specify applications based on
the Kahn process network model of computation and features a simulation engine
based on SystemC. Moreover, the DOL provides an XML-based specification format 
to describe the implementation of a parallel application on a multi-processor 
systems, including binding and mapping.
<http://www.tik.ee.ethz.ch/~shapes/dol.html>  
![tupian](http://a3.qpic.cn/psb?/V10GqHsq3dYRfO/hajJ3hzpdJPLOWMZxlm0gNiS.JxnF0JDsbqnPdlyQrw!/c/dAoBAAAAAAAA&ek=1&kp=1&pt=0&bo=7wMoAgAAAAAFB.I!&sce=60-2-2&rf=0-0)

##### 2. Make工具简介
* 在Linux和Ubuntu环境中，make工具主要被用来进行工程编译和程序链接
* Makefile文件：告诉make以何种方式编译源代码和链接程序
* make通过比较对应文件（规则的目标和依赖）的最后修改时间，来决定哪些文件需要更新、那些文件不需要更新。

<http://blog.chinaunix.net/uid-9314244-id-2004686.html>  

##### 3. Ant工具简介
* Ant是一种基于Java的build工具。
* Ant用Java的类来扩展。
* Ant本身就是这样一个流程脚本引擎，用于自动化调用程序完成项目的编译，打包，测试等。

<http://blog.163.com/qiangyongbin2000@126/blog/static/77517819201151653423687/>  

##### 4. Ant的优点
* 跨平台性。Ant是纯java语言编写的，所示具有很好的跨平台性。
* 操作简单。Ant是由一个内置任务和可选任务组成的。Ant运行时需要一个XML文件(构建文件)。
* 容易维护和书写，结构清晰。
* Ant可以集成到开发环境中。  

##### 5. Java与javac简介
* 用途：编译或执行java代码
* javac命令用来编译java文件
* java命令可以执行生成的class文件


# DOL安装笔记 

#### 本次实验环境在linux下进行，建议使用虚拟机安装Ubuntu（由于本人之前就安装了Ubuntu，所以不展开说明）
  VMWARE教程：<http://jingyan.baidu.com/article/0320e2c1ef9f6c1b87507bf6.html>  
  VIRTUALBOX教程：<http://jingyan.baidu.com/article/cdddd41c5eea3153ca00e160.html>  
  Ubuntu下载：<http://www.ubuntu.com/download/desktop>
  
## DOL的环境配置
#### 安装一些必要的环境(ubuntu为例)：
  $    sudo apt-get update  
  $	   sudo apt-get install ant  
  $    sudo apt-get install openjdk-7-jdk  
  $	   sudo apt-get install unzip  
  
  
##### 1. 下载文件(使用Vmware虚拟机，也可以从主机拷贝到虚拟机中
  (<http://jingyan.baidu.com/article/c33e3f48a5c153ea15cbb5b2.html>)  
##### systemc-2.3.1安装包下载： <http://www.accellera.org/images/downloads/standards/systemc/systemc-2.3.1.tgz>
##### dol_ethz安装包下载： <http://www.tik.ee.ethz.ch/~shapes/downloads/dol_ethz.zip>
> 如果直接在虚拟机上下载，可以在终端输入： sudo wget 上面的链接  
> 否则在windows下载后，通过U盘把安装包放到虚拟机中。

![tupian](http://a1.qpic.cn/psb?/V10GqHsq3dYRfO/R7sca.F43Ydw8*q7eDN6cSfODrR*XjNr5oqkxJBCyAU!/b/dAgBAAAAAAAA&bo=4AJCAgAAAAAFAIE!&rf=viewer_4)

##### 2. 解压安装包 
新建dol的文件夹   
$    mkdir dol  
将dolethz.zip解压到 dol文件夹中  
$	unzip dol_ethz.zip -d dol  
解压systemc  
$	tar -zxvf systemc-2.3.1.tgz  

##### 3. 编译systemc
解压后进入systemc-2.3.1的目录下  
$    cd systemc-2.3.1  
新建一个临时文件夹objdir  
$	mkdir objdir  
进入该文件夹objdir  
$	cd objdir  
运行configure(能根据系统的环境设置一下参数，用于编译)  
$	../configure CXX=g++ --disable-async-updates  

![tupian](http://a4.qpic.cn/psb?/V10GqHsq3dYRfO/HTdx2mMIGhYciEHH4xSfOggSm1LodjAplGeAusoeIcU!/c/dMcAAAAAAAAA&ek=1&kp=1&pt=0&bo=fQLwAAAAAAAFB6s!&sce=60-2-2&rf=0-0)
编译  
$    sudo make install   
记录当前的工作路径(会输出当前所在路径，记下来，待会有用)  
$    pwd  


##### 4. 编译dol  
进入刚刚dol的文件夹  
$    cd ../dol  
修改build_zip.xml文件  
找到下面这段话，就是说上面编译的systemc位置在哪里，
&lt;property name="systemc.inc" value="YYY/include"/&gt;
&lt;property name="systemc.lib" value="YYY/lib-linux/libsystemc.a"/&gt;
把YYY改成上页pwd的结果（注意，对于  64位 系统的机器，lib-linux要改成lib-linux64） 
然后是编译  
$    ant -f build_zip.xml all  
若成功会显示build successful  

![tupian](http://a3.qpic.cn/psb?/V10GqHsq3dYRfO/QXu.S1f*MwtVDA6JfGhHCAhtDKEpIDsJMwPxmggAjK4!/c/dAoBAAAAAAAA&ek=1&kp=1&pt=0&bo=nAG0AAAAAAAFBw0!&sce=60-2-2&rf=0-0)

接着可以试试运行第一个例子  
进入build/bin/mian路径下  
$    cd build/bin/main  
然后运行第一个例子  
$	ant -f runexample.xml -Dnumber=1  

##### 5. 你很有可能在编译dol时是没有成功的，如下：  
![tupian](http://a1.qpic.cn/psb?/V10GqHsq3dYRfO/rWj5pa0mRlELJd7ERbWDm9r2KkzhZ*EhdJzp7KRIoR8!/b/dMgAAAAAAAAA&ek=1&kp=1&pt=0&bo=OQLKAAAAAAAFB9U!&sce=60-3-3&rf=viewer_4)
这是因为没有jdk  
我们可以回到上面的DOL环境配置安装一些必要的环境那里，
在Ubuntu中跑一遍四条指令即可成功。  
还有一个问题，这四条指令的运行速度可能会很慢很慢，这里也有两个原因，一是你当前的网速
很慢，就要换一个网络环境；二是你的Ubuntu安装源是国外的，这样对导致速度慢，这就需要
我们更改安装源，详细流程<http://jingyan.baidu.com/article/ed2a5d1f55bcb509f6be17cb.html>


# 实验感想和心得
DOL环境配置花费了我很多时间。在前面的步骤都是顺利的，就在最后的dol编译失败了，我重新
配置了很多遍都失败，后来下好了jdk的安装包，重新运行上面的四条指令，发现超慢超慢的。
所以，更换安装源是必需的。  




















