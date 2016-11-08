#lab3:DOL实例分析&编程

###1.理解example各文件夹的含义
src文件夹中各进程（生产者，消费者，处理模块等）的功能定义。
####a.example1.xml
在下面目录中找到example1.xml文件：
![tupian](http://a1.qpic.cn/psb?/V10GqHsq2hIHFE/zk3Nql70fS9LSeEiqzeA*F.*G6co7tGbj6woBRYr0GE!/b/dNwAAAAAAAAA&ek=1&kp=1&pt=0&bo=IwNNASMDTQEDCC0!&sce=0-12-12&rf=viewer_311)

example1.xml：系统架构即模块连接方式定义。
里面定义了模块与模块之间是怎么连接的，就是有哪些框，哪些线，比如A框跟B框用一根线连起来
，他们就在一起了。process就是那些框, sw_channel那些线, 
connection就是把线的那头连到框的那头。  
   
![tupian](http://a1.qpic.cn/psb?/V10GqHsq2hIHFE/0TW7BVf2e8gU2d1PoU5NNoQKjFxLjWxhY2ntrou4Q4c!/c/dAwBAAAAAAAA&ek=1&kp=1&pt=0&bo=mAETAZgBEwEDCC0!&sce=0-12-12&rf=0-18)   
我们看一下上面的example1.xml是进程定义：  
&lt;process name=“未知数1"&gt;  
    &lt;port type=“未知数2” name=“未知数3”/&gt;  //有几个端口就要有几行这个  
    &lt;port type=“未知数2” name=“未知数3”/&gt;  //这里就是说有2个端口  
    &lt;source type=“c” location=“未知数1.c"/&gt;   
&lt;/process&gt; 
未知数1==实现的模块的名字，比如写了xxx.c这里就是xxx了  
未知数2==output或者input  
未知数3==端口的名字，在*.h的文件里面，如下图所示:
![tupian](http://a3.qpic.cn/psb?/V10GqHsq2hIHFE/imsAjketIFQ5Z4m.n593E784HuYxOVlShMQPS1TI6I0!/c/dNoAAAAAAAAA&ek=1&kp=1&pt=0&bo=YgI4AWICOAEDCC0!&sce=0-12-12&rf=0-18)  

下面看一下通道定义，一条线就是一条通道：  
![tupian](http://a4.qpic.cn/psb?/V10GqHsq2hIHFE/QSV6Xgno3SqNgNkGLYZsRWIS*coOgqSRqynhKdpUgrs!/c/dHcBAAAAAAAA&ek=1&kp=1&pt=0&bo=0gGxANIBsQADCC0!&sce=0-12-12&rf=0-18)  
&lt;sw_channel type=“fifo” size=“未知数1” name=“未知数2"&gt;  
    &lt;port type=“input” name=“in"/&gt;  
    &lt;port type=“output” name=“out"/&gt;  
两个端口，一个叫”in”，一个叫”out”  
&lt;/sw_channel&gt;  
未知数1是指缓冲区的大小，左边是10  
未知数2是这条线的名字，比如左边是C2  
  
下面举例说明各个模块之间是怎么连接的：  
定义各个模块之间的连接,一条线会对应两个connection，就是A框的右手牵着这条线的左边，这条线的右边牵着B框。！！每条线要有2个connection！！   
&lt;connection name=“未知数1"&gt;   
   &lt;origin name=“未知数2”&gt;!!从这!!    
       &lt;port name=“未知数3"/&gt;  
    &lt;/origin&gt;  
    &lt;target name=“未知数4”&gt;!!连到这!!  
         &lt;port name=“未知数5"/&gt;  
     &lt;/target&gt;  
&lt;/connection&gt;  
未知数1是这段感情的名字，随便填。  
未知数2\未知数4是模块或者通道的名字  
未知数3\未知数5要对应process或者channel的端口名  

![tupian](http://a3.qpic.cn/psb?/V10GqHsq2hIHFE/62r.GKmd1ZmLsHNGE5IjvvU8ojBNFfnpAc6Szd61I7w!/c/dAoBAAAAAAAA&ek=1&kp=1&pt=0&bo=1wF4AdcBeAEDCC0!&sce=0-12-12&rf=0-18)  

举个例子，上面这条connection叫“g-c”；它从”gennerator”这个模块的”1”端口连接到
“c1”这个模块（线）的”0”端口。此时还需要对应另外的一条connection，它要从“c1”这个模块
（线）的其他端口，连接到其他的模块上。   



下面看一下src文件夹里面的代码：  
src文件夹里有7个文件：generator.c , generator.h , consumer.c ， consumer.h ，square.c , square.h , global.h    
* generator.h 和 generator.c：定义生产者进程。
typedef struct _local_states{...}; 这个是定义一个结构体，包含两个变量，下标（index），
长度（len）。在*.c文件中，函数void generator_init(DOLProcess *p)函数初始化了当前的位置为0，
设置生产者长度为LENGTH，这里的local指针指向的是.h文件的_local_states结构。int generator_fire(DOLProcess *p)
函数是一个信号产生函数，这里的过程是，如果当前位置小于生产长度，则将当前下标（x）写入输出端，
否则销毁进程，执行length次之后停下来。    

consumer.h和consumer.c:定义消费中进程。
typedet struct _local_states{...};这个结构体定义了三个变量，一个长度为10的char型数组，
一个下标（index），一个长度（len）。void consumer_init(DOLProcess *p)函数初始化模块名字，最初的位置，
消费者最长的长度（理解和generator一样）。int consumer_fire(DOLProcess *p)函数是信号消费函数，若当前位置小于设定长度，则
读出输入端信号，并且打印出来，否则销毁进程。  
square.h和square.c：定义平方进程。
这里也有一个定义结构体的函数typedef struct _local_states{...}; 意义和前面的函数一样。
在*.c文件中，函数void square_init(DOLProcess *p)定义初始位置为0，长度为LENGTH。在函数
int square_fire(DOLProcess *p)是信号处理函数读入输入端信号i，将其平方后写出到输出端，
也是重复length次之后就停止了。  


在上面分析完后，我们看一下example1的运行结果：  
![tupian](http://a1.qpic.cn/psb?/V10GqHsq2hIHFE/t69QVFsqFz.eNEDDQKtQ2Ui6.ImkTRVzjWegL1aKqBo!/c/dOQAAAAAAAAA&ek=1&kp=1&pt=0&bo=6QJDAukCQwIDACU!&sce=0-12-12&rf=0-18)  
![tupian](http://a1.qpic.cn/psb?/V10GqHsq2hIHFE/dTy5aVW8YajE1mAAqP*8m9LwpXAZxw.oM5.8WPqI0KU!/c/dNwAAAAAAAAA&ek=1&kp=1&pt=0&bo=.QGHAPkBhwADCC0!&sce=0-12-12&rf=0-18)  

generator 产生0-19的整数（length为20，初始值为0）  
square 对输入进行平方操作  
consumer 输出结果  


example1任务：把结束的输出从i的平方改为i的立方，并输出结果：   
我们从上面分析的过程看在square.c文件中，先将i=i*i，在这个结果输出，所以我们直接把这个式子
改为i=i*i*i ,就这样我们就可以输出立方。输出结果如下：  
![tupian](http://a3.qpic.cn/psb?/V10GqHsq2hIHFE/RVfkCsq2tSaKWWzLwVmT8Ll8rkIFgB7go.udO7FwFiU!/c/dAoBAAAAAAAA&ek=1&kp=1&pt=0&bo=IQNZAiEDWQIDCC0!&sce=0-12-12&rf=0-18)  




####b.example2  
各进程功能定义与example1相同，不同之处在于example2架构中包含3个square进程，故输出结果是i^8.   


3个square模块是通过迭代实现连接的：看下面的代码，代码分析同example1相似  
![tupian](http://a1.qpic.cn/psb?/V10GqHsq2hIHFE/w3TxlmybhUgYT5jUtJ.0rLZhUshARLeuHy3VUQ6KM7c!/c/dHwBAAAAAAAA&ek=1&kp=1&pt=0&bo=KQLwASkC8AEDCC0!&sce=0-12-12&rf=0-18)  
通过迭代生成链接connection  
![tupian](http://a3.qpic.cn/psb?/V10GqHsq2hIHFE/*HVO0kWNbahr*FDgBFEEE0w*vg6qZfVbKgdCrs65aYQ!/c/dAoBAAAAAAAA&ek=1&kp=1&pt=0&bo=7AHuAewB7gEDCC0!&sce=0-12-12&rf=0-18)  


现在先看一下example2运行的结果：  
![tupian](http://a2.qpic.cn/psb?/V10GqHsq2hIHFE/FgQh1qvkZ3DjxAIkLjRdKnDlcF2dmJUlDRCEup2SJvU!/c/dHEBAAAAAAAA&ek=1&kp=1&pt=0&bo=6AHFAegBxQEDACU!&sce=0-12-12&rf=0-18)  
![tupian](http://a4.qpic.cn/psb?/V10GqHsq2hIHFE/mPkuS7siT0YhfmV9mfo7Zy6rwQFjrA8eMfGYYJSLy7Q!/c/dAsBAAAAAAAA&ek=1&kp=1&pt=0&bo=1AJmANQCZgADCC0!&sce=0-12-12&rf=0-18)   


generator 生成0~19的整数  
square 经过三次平方操作   
consumer 输出结果  

任务：让3个square模块变成2个  
在上面的分析过程，我们可以看到有多少一个square模块相连取决于语句&lt;variable value="3" name="N"/&gt;
控制的，因为value=“3”，所以有3个square模块相连，我们只需要把这个“3”改为“2”就可以了。  
改变后的输出结果：  
![tupian](http://a2.qpic.cn/psb?/V10GqHsq2hIHFE/jiJ0KNdr0QwbVZNnVvgzhVM8hjBV5dFC9Z33v9G0c4Y!/c/dI0BAAAAAAAA&ek=1&kp=1&pt=0&bo=rAGuAawBrgEDCC0!&sce=0-12-12&rf=0-18)  
![tupian](http://a1.qpic.cn/psb?/V10GqHsq2hIHFE/7kFgw3agomtDy1PijjnEYyuaWXS7mWbSk6W*lSgAjWA!/c/dNwAAAAAAAAA&ek=1&kp=1&pt=0&bo=zQJ7AM0CewADCC0!&sce=0-12-12&rf=0-18)  

### 实验感想
这次实验总体来说是比较简单的，只是改了两句，但过程中很煎熬。我在上次实验中成功的配置文件，
但是当时没有运行example1，所以并不知道我的配置还是有问题的。我跑example1的时候，
不能出现结果（具体的错误忘记截图了），原来我配置的虚拟机是32位的，我一直以为是64位的，
所以之后改变了，就能运行出结果了。我以为一切都好了，因为这次实验不难，其实不是。
在example1中，改了i=i*i*i ,但是无论我怎么改，输出的结果都是i的平方的结果。我就问了TA，
他说要把我运行example1生成的结果删掉再运行一遍。恩，这样是对的，但这些文件都是加锁的文件，
我不能删掉。所以我一直再找各种删文件的方法，我还重新配置环境了，但生成的文件还是不能删掉。
后来我发下了一个很简单的方法，就是改变文件名，那么我们就可以生成新的example1了。
![tupian](http://a4.qpic.cn/psb?/V10GqHsq2hIHFE/x*r4SeY5a37b00ECvuUCZwryaTnd7Lg22Mc6PobTOBo!/c/dHcBAAAAAAAA&ek=1&kp=1&pt=0&bo=3gLnAN4C5wADCC0!&sce=0-12-12&rf=0-18)

