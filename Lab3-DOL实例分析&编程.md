#lab3:DOLʵ������&���

###1.���example���ļ��еĺ���
src�ļ����и����̣������ߣ������ߣ�����ģ��ȣ��Ĺ��ܶ��塣
####a.example1.xml
������Ŀ¼���ҵ�example1.xml�ļ���
![tupian](http://a1.qpic.cn/psb?/V10GqHsq2hIHFE/zk3Nql70fS9LSeEiqzeA*F.*G6co7tGbj6woBRYr0GE!/b/dNwAAAAAAAAA&ek=1&kp=1&pt=0&bo=IwNNASMDTQEDCC0!&sce=0-12-12&rf=viewer_311)

example1.xml��ϵͳ�ܹ���ģ�����ӷ�ʽ���塣
���涨����ģ����ģ��֮������ô���ӵģ���������Щ����Щ�ߣ�����A���B����һ����������
�����Ǿ���һ���ˡ�process������Щ��, sw_channel��Щ��, 
connection���ǰ��ߵ���ͷ���������ͷ��  
   
![tupian](http://a1.qpic.cn/psb?/V10GqHsq2hIHFE/0TW7BVf2e8gU2d1PoU5NNoQKjFxLjWxhY2ntrou4Q4c!/c/dAwBAAAAAAAA&ek=1&kp=1&pt=0&bo=mAETAZgBEwEDCC0!&sce=0-12-12&rf=0-18)   
���ǿ�һ�������example1.xml�ǽ��̶��壺  
&lt;process name=��δ֪��1"&gt;  
    &lt;port type=��δ֪��2�� name=��δ֪��3��/&gt;  //�м����˿ھ�Ҫ�м������  
    &lt;port type=��δ֪��2�� name=��δ֪��3��/&gt;  //�������˵��2���˿�  
    &lt;source type=��c�� location=��δ֪��1.c"/&gt;   
&lt;/process&gt; 
δ֪��1==ʵ�ֵ�ģ������֣�����д��xxx.c�������xxx��  
δ֪��2==output����input  
δ֪��3==�˿ڵ����֣���*.h���ļ����棬����ͼ��ʾ:
![tupian](http://a3.qpic.cn/psb?/V10GqHsq2hIHFE/imsAjketIFQ5Z4m.n593E784HuYxOVlShMQPS1TI6I0!/c/dNoAAAAAAAAA&ek=1&kp=1&pt=0&bo=YgI4AWICOAEDCC0!&sce=0-12-12&rf=0-18)  

���濴һ��ͨ�����壬һ���߾���һ��ͨ����  
![tupian](http://a4.qpic.cn/psb?/V10GqHsq2hIHFE/QSV6Xgno3SqNgNkGLYZsRWIS*coOgqSRqynhKdpUgrs!/c/dHcBAAAAAAAA&ek=1&kp=1&pt=0&bo=0gGxANIBsQADCC0!&sce=0-12-12&rf=0-18)  
&lt;sw_channel type=��fifo�� size=��δ֪��1�� name=��δ֪��2"&gt;  
    &lt;port type=��input�� name=��in"/&gt;  
    &lt;port type=��output�� name=��out"/&gt;  
�����˿ڣ�һ���С�in����һ���С�out��  
&lt;/sw_channel&gt;  
δ֪��1��ָ�������Ĵ�С�������10  
δ֪��2�������ߵ����֣����������C2  
  
�������˵������ģ��֮������ô���ӵģ�  
�������ģ��֮�������,һ���߻��Ӧ����connection������A�������ǣ�������ߵ���ߣ������ߵ��ұ�ǣ��B�򡣣���ÿ����Ҫ��2��connection����   
&lt;connection name=��δ֪��1"&gt;   
   &lt;origin name=��δ֪��2��&gt;!!����!!    
       &lt;port name=��δ֪��3"/&gt;  
    &lt;/origin&gt;  
    &lt;target name=��δ֪��4��&gt;!!������!!  
         &lt;port name=��δ֪��5"/&gt;  
     &lt;/target&gt;  
&lt;/connection&gt;  
δ֪��1����θ�������֣�����  
δ֪��2\δ֪��4��ģ�����ͨ��������  
δ֪��3\δ֪��5Ҫ��Ӧprocess����channel�Ķ˿���  

![tupian](http://a3.qpic.cn/psb?/V10GqHsq2hIHFE/62r.GKmd1ZmLsHNGE5IjvvU8ojBNFfnpAc6Szd61I7w!/c/dAoBAAAAAAAA&ek=1&kp=1&pt=0&bo=1wF4AdcBeAEDCC0!&sce=0-12-12&rf=0-18)  

�ٸ����ӣ���������connection�С�g-c�������ӡ�gennerator�����ģ��ġ�1���˿����ӵ�
��c1�����ģ�飨�ߣ��ġ�0���˿ڡ���ʱ����Ҫ��Ӧ�����һ��connection����Ҫ�ӡ�c1�����ģ��
���ߣ��������˿ڣ����ӵ�������ģ���ϡ�   



���濴һ��src�ļ�������Ĵ��룺  
src�ļ�������7���ļ���generator.c , generator.h , consumer.c �� consumer.h ��square.c , square.h , global.h    
* generator.h �� generator.c�����������߽��̡�
typedef struct _local_states{...}; ����Ƕ���һ���ṹ�壬���������������±꣨index����
���ȣ�len������*.c�ļ��У�����void generator_init(DOLProcess *p)������ʼ���˵�ǰ��λ��Ϊ0��
���������߳���ΪLENGTH�������localָ��ָ�����.h�ļ���_local_states�ṹ��int generator_fire(DOLProcess *p)
������һ���źŲ�������������Ĺ����ǣ������ǰλ��С���������ȣ��򽫵�ǰ�±꣨x��д������ˣ�
�������ٽ��̣�ִ��length��֮��ͣ������    

consumer.h��consumer.c:���������н��̡�
typedet struct _local_states{...};����ṹ�嶨��������������һ������Ϊ10��char�����飬
һ���±꣨index����һ�����ȣ�len����void consumer_init(DOLProcess *p)������ʼ��ģ�����֣������λ�ã�
��������ĳ��ȣ�����generatorһ������int consumer_fire(DOLProcess *p)�������ź����Ѻ���������ǰλ��С���趨���ȣ���
����������źţ����Ҵ�ӡ�������������ٽ��̡�  
square.h��square.c������ƽ�����̡�
����Ҳ��һ������ṹ��ĺ���typedef struct _local_states{...}; �����ǰ��ĺ���һ����
��*.c�ļ��У�����void square_init(DOLProcess *p)�����ʼλ��Ϊ0������ΪLENGTH���ں���
int square_fire(DOLProcess *p)���źŴ���������������ź�i������ƽ����д��������ˣ�
Ҳ���ظ�length��֮���ֹͣ�ˡ�  


���������������ǿ�һ��example1�����н����  
![tupian](http://a1.qpic.cn/psb?/V10GqHsq2hIHFE/t69QVFsqFz.eNEDDQKtQ2Ui6.ImkTRVzjWegL1aKqBo!/c/dOQAAAAAAAAA&ek=1&kp=1&pt=0&bo=6QJDAukCQwIDACU!&sce=0-12-12&rf=0-18)  
![tupian](http://a1.qpic.cn/psb?/V10GqHsq2hIHFE/dTy5aVW8YajE1mAAqP*8m9LwpXAZxw.oM5.8WPqI0KU!/c/dNwAAAAAAAAA&ek=1&kp=1&pt=0&bo=.QGHAPkBhwADCC0!&sce=0-12-12&rf=0-18)  

generator ����0-19��������lengthΪ20����ʼֵΪ0��  
square ���������ƽ������  
consumer ������  


example1���񣺰ѽ����������i��ƽ����Ϊi������������������   
���Ǵ���������Ĺ��̿���square.c�ļ��У��Ƚ�i=i*i�����������������������ֱ�Ӱ����ʽ��
��Ϊi=i*i*i ,���������ǾͿ���������������������£�  
![tupian](http://a3.qpic.cn/psb?/V10GqHsq2hIHFE/RVfkCsq2tSaKWWzLwVmT8Ll8rkIFgB7go.udO7FwFiU!/c/dAoBAAAAAAAA&ek=1&kp=1&pt=0&bo=IQNZAiEDWQIDCC0!&sce=0-12-12&rf=0-18)  




####b.example2  
�����̹��ܶ�����example1��ͬ����֮ͬ������example2�ܹ��а���3��square���̣�����������i^8.   


3��squareģ����ͨ������ʵ�����ӵģ�������Ĵ��룬�������ͬexample1����  
![tupian](http://a1.qpic.cn/psb?/V10GqHsq2hIHFE/w3TxlmybhUgYT5jUtJ.0rLZhUshARLeuHy3VUQ6KM7c!/c/dHwBAAAAAAAA&ek=1&kp=1&pt=0&bo=KQLwASkC8AEDCC0!&sce=0-12-12&rf=0-18)  
ͨ��������������connection  
![tupian](http://a3.qpic.cn/psb?/V10GqHsq2hIHFE/*HVO0kWNbahr*FDgBFEEE0w*vg6qZfVbKgdCrs65aYQ!/c/dAoBAAAAAAAA&ek=1&kp=1&pt=0&bo=7AHuAewB7gEDCC0!&sce=0-12-12&rf=0-18)  


�����ȿ�һ��example2���еĽ����  
![tupian](http://a2.qpic.cn/psb?/V10GqHsq2hIHFE/FgQh1qvkZ3DjxAIkLjRdKnDlcF2dmJUlDRCEup2SJvU!/c/dHEBAAAAAAAA&ek=1&kp=1&pt=0&bo=6AHFAegBxQEDACU!&sce=0-12-12&rf=0-18)  
![tupian](http://a4.qpic.cn/psb?/V10GqHsq2hIHFE/mPkuS7siT0YhfmV9mfo7Zy6rwQFjrA8eMfGYYJSLy7Q!/c/dAsBAAAAAAAA&ek=1&kp=1&pt=0&bo=1AJmANQCZgADCC0!&sce=0-12-12&rf=0-18)   


generator ����0~19������  
square ��������ƽ������   
consumer ������  

������3��squareģ����2��  
������ķ������̣����ǿ��Կ����ж���һ��squareģ������ȡ�������&lt;variable value="3" name="N"/&gt;
���Ƶģ���Ϊvalue=��3����������3��squareģ������������ֻ��Ҫ�������3����Ϊ��2���Ϳ����ˡ�  
�ı�����������  
![tupian](http://a2.qpic.cn/psb?/V10GqHsq2hIHFE/jiJ0KNdr0QwbVZNnVvgzhVM8hjBV5dFC9Z33v9G0c4Y!/c/dI0BAAAAAAAA&ek=1&kp=1&pt=0&bo=rAGuAawBrgEDCC0!&sce=0-12-12&rf=0-18)  
![tupian](http://a1.qpic.cn/psb?/V10GqHsq2hIHFE/7kFgw3agomtDy1PijjnEYyuaWXS7mWbSk6W*lSgAjWA!/c/dNwAAAAAAAAA&ek=1&kp=1&pt=0&bo=zQJ7AM0CewADCC0!&sce=0-12-12&rf=0-18)  

### ʵ�����
���ʵ��������˵�ǱȽϼ򵥵ģ�ֻ�Ǹ������䣬�������кܼ尾�������ϴ�ʵ���гɹ��������ļ���
���ǵ�ʱû������example1�����Բ���֪���ҵ����û���������ġ�����example1��ʱ��
���ܳ��ֽ��������Ĵ������ǽ�ͼ�ˣ���ԭ�������õ��������32λ�ģ���һֱ��Ϊ��64λ�ģ�
����֮��ı��ˣ��������г�����ˡ�����Ϊһ�ж����ˣ���Ϊ���ʵ�鲻�ѣ���ʵ���ǡ�
��example1�У�����i=i*i*i ,������������ô�ģ�����Ľ������i��ƽ���Ľ�����Ҿ�����TA��
��˵Ҫ��������example1���ɵĽ��ɾ��������һ�顣���������ǶԵģ�����Щ�ļ����Ǽ������ļ���
�Ҳ���ɾ����������һֱ���Ҹ���ɾ�ļ��ķ������һ��������û����ˣ������ɵ��ļ����ǲ���ɾ����
�����ҷ�����һ���ܼ򵥵ķ��������Ǹı��ļ�������ô���ǾͿ��������µ�example1�ˡ�
![tupian](http://a4.qpic.cn/psb?/V10GqHsq2hIHFE/x*r4SeY5a37b00ECvuUCZwryaTnd7Lg22Mc6PobTOBo!/c/dHcBAAAAAAAA&ek=1&kp=1&pt=0&bo=3gLnAN4C5wADCC0!&sce=0-12-12&rf=0-18)

