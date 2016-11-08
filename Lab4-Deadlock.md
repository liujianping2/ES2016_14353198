# lab4������  
#### ���������������߶�����̣���������Է�ռ�е���Դ��
#### �����������ĸ�������
* ����������һ����Դÿ��ֻ�ܱ�һ������ʹ��  
* �����뱣��������һ��������������Դ������ʱ�����ѻ�õ���Դ���ֲ���  
* ����������:�����ѻ�õ���Դ����ĩʹ����֮ǰ������ǿ�а���  
* ѭ���ȴ�����:���ɽ���֮���γ�һ��ͷβ��ӵ�ѭ���ȴ���Դ��ϵ  

#### ��һ�²��������ľ�����̣�
![tupian](http://a4.qpic.cn/psb?/V10GqHsq2hIHFE/ziaovG1vj2ue0zJaoJeTxkCMohRz*9yrRhToOSTQM*c!/c/dHcBAAAAAAAA&ek=1&kp=1&pt=0&bo=ZwHXAGcB1wADCC0!&sce=0-12-12&rf=0-18)  
��������������A��B�����������̶��ֱ�ռ��һ����Դ��A����ռ�г�ɫС�����Դ������Bռ�к�ɫС�����Դ��
ͬʱ����A����ռ�к�ɫС����Դ������B����ռ�г�ɫС����Դ�����������������������������A����ĺ�ɫС����Դ
������Bռ�У�����A��������ɹ�������B����ĳ�ɫС�򱻽���Aռ�У����Բ�������ɹ�����δ��ɽ���֮ǰ��
����A�ͽ���B�������ͷ�����ռ�е���Դ��������������Ҳ�޷���������ռ�е���Դ����ˣ�����A�ͽ���Bֻ������
�ĵȴ�����������һ��������
 
####����ֱ�ӿ�һ��Deadlock.java���룺

<pre><code>
class Deadlock implements Runnable{
  A a = new A();
  B b = new B();
  
  //���캯��
  Deadlock(){
    Thread t = new Thread(this);
    int count = 20000 ;
    
    t.start();           //�߳�start��ʼ
    while(count-- > 0); //�ȴ�20000
    a.methodA(b) ;
  }

  //runnable����ʱ���õķ���
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


���ǿ��Կ��������class A{...}��class B{...}���ඨ�壬�������˹ؼ��֡�synchronized����
������������һ����������һ��������ʱ���ܹ���֤��ͬһʱ�����ֻ��һ���߳�ִ�иöδ��롣
��һ���̷߳���object��һ��synchronizedͬ��������ͬ������ʱ�������̶߳�object����������synchronized
ͬ��������ͬ�������ķ��ʽ�������������Ϊʵ��������׼���ġ�

��Deadlock����ǻ���������a��b��a�����b�ķ�����b�����a�ķ���������ķ����������Ϊ��Դ����aռ��a������
bռ��b������ͬʱa����b������b����a�������ͻ��������������������������ô������̾ͻ�ֹͣ���޷�����������ȥ��

������Ĵ��볭�� Deadlock.java����,���� , ���� javac Deadlock.java    

���ǻ���Ҫһ��Deadlock.bat�ļ���Ȼ���������ļ�����java����Deadlock.class��Ŀ¼�£�˫�����У��۲�����  
<pre><code>  windowsϵͳ�£�
cd /d %~dp0
@echo off
:start
set /a var+=1
echo %var%
java Deadlock
if %var% leq 1000 GOTO start
pause 

  Linuxϵͳ�£�
#!/bin/bash/
for((c=1 ; c<=100 ; c++))
do
   echo "$c times"
   java Deadlock
done
</code></pre>  

������windows�����еĽ�������Կ��������е����Ĵε�ʱ�򣬾ͳ�����������״̬��ʹ����ֹͣ��  
![tupian](http://a4.qpic.cn/psb?/V10GqHsq2hIHFE/f32fs4glrf04HXAaQUM94I65JrQsQ4oZa1Io1xu4ugo!/c/dG8BAAAAAAAA&ek=1&kp=1&pt=0&bo=pQLtAaUC7QEDCC0!&sce=0-12-12&rf=0-18)  

####ʵ�����
������ʵ�鲢���ѣ�ֻҪѧ������ϵͳ��ͬѧ���Ǻ��������ͽ��������������͹��̵ģ����ʵ����Ҫ��Ҫ��
����ʵ��һ����������Щͬѧ�������кö�鶼����������������Ҫ�������ˡ�