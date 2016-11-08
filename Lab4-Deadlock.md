# lab4：死锁  
#### 死锁就是两个或者多个进程，互相请求对方占有的资源。
#### 产生死锁的四个条件：
* 互斥条件：一个资源每次只能被一个进程使用  
* 请求与保持条件：一个进程因请求资源而阻塞时，对已获得的资源保持不放  
* 不剥夺条件:进程已获得的资源，在末使用完之前，不能强行剥夺  
* 循环等待条件:若干进程之间形成一种头尾相接的循环等待资源关系  

#### 看一下产生死锁的具体过程：
![tupian](http://a4.qpic.cn/psb?/V10GqHsq2hIHFE/ziaovG1vj2ue0zJaoJeTxkCMohRz*9yrRhToOSTQM*c!/c/dHcBAAAAAAAA&ek=1&kp=1&pt=0&bo=ZwHXAGcB1wADCC0!&sce=0-12-12&rf=0-18)  
这里有两个进程A和B，这两个进程都分别占有一个资源，A进程占有橙色小球的资源，进程B占有黑色小球的资源。
同时进程A申请占有黑色小球资源，进程B申请占有橙色小球资源。根据上面产生死锁的条件，进程A申请的黑色小球资源
被进程B占有，所以A不能申请成功；进程B申请的橙色小球被进程A占有，所以不能申请成功。在未完成进程之前，
进程A和进程B都不会释放他们占有的资源，而且其他进程也无法剥夺他们占有的资源。因此，进程A和进程B只能无限
的等待，这就造成了一个死锁。
 
####下面直接看一下Deadlock.java代码：

<pre><code>
class Deadlock implements Runnable{
  A a = new A();
  B b = new B();
  
  //构造函数
  Deadlock(){
    Thread t = new Thread(this);
    int count = 20000 ;
    
    t.start();           //线程start开始
    while(count-- > 0); //等待20000
    a.methodA(b) ;
  }

  //runnable运行时调用的方法
  public void run(){
    b.methodB(a);
  }

  public static void main(String args[]){
    new Deadlock();
  }

}

class A{

  synchronized void methodA(B b){
    b.last();
  }

  synchronized void last(){
    System.out.println("Inside A.last()");
  }
}

class B{

  synchronized void methodB(A a){
    a.last();
  }

  synchronized void last(){
      System.out.println("Inside B.last()");
    }
}
</code></pre>  


我们可以看到上面的class A{...}和class B{...}的类定义，这里用了关键字“synchronized”。
当它用来修饰一个方法或者一个代码块的时候，能够保证在同一时刻最多只有一个线程执行该段代码。
当一个线程访问object的一个synchronized同步代码块或同步方法时，其他线程对object中所有其它synchronized
同步代码块或同步方法的访问将被阻塞。这是为实现死锁而准备的。

在Deadlock里，我们会有两个类a和b，a会调用b的方法，b会调用a的方法，这里的方法可以理解为资源。当a占用a方法，
b占用b方法，同时a调用b方法，b调用a方法，就会出现在上面分析死锁的情况，那么这个进程就会停止而无法继续运行下去。

把上面的代码抄到 Deadlock.java里面,保存 , 运行 javac Deadlock.java    

我们还需要一个Deadlock.bat文件，然将批处理文件放在java程序（Deadlock.class）目录下，双击运行，观察结果。  
<pre><code>  windows系统下：
cd /d %~dp0
@echo off
:start
set /a var+=1
echo %var%
java Deadlock
if %var% leq 1000 GOTO start
pause 

  Linux系统下：
#!/bin/bash/
for((c=1 ; c<=100 ; c++))
do
   echo "$c times"
   java Deadlock
done
</code></pre>  

我是在windows下运行的结果，可以看到当运行到第四次的时候，就出现了死锁的状态而使进程停止。  
![tupian](http://a4.qpic.cn/psb?/V10GqHsq2hIHFE/f32fs4glrf04HXAaQUM94I65JrQsQ4oZa1Io1xu4ugo!/c/dG8BAAAAAAAA&ek=1&kp=1&pt=0&bo=pQLtAaUC7QEDCC0!&sce=0-12-12&rf=0-18)  

####实验感想
死锁的实验并不难，只要学过操作系统的同学都是很容易理解和接受死锁的条件和过程的，这次实验主要是要求
我们实现一个死锁。有些同学可能运行好多遍都不会出现死锁，这就要看运气了。