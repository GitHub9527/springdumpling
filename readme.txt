һ��Э������
1 @CooperationService,������Spring��@Service
���б��@CooperationService���඼������෽�����Ƿ�������annotation 
    @Publish / @Subscribe     
    @RemotePublish / @RemoteSubscriber 
    @RemoteSynronized 	
    @RemoteNotify / @RemoteWait
    @Process / @Task


2 @Publish,����������
  path�� һ���߼�·��������Ҫ
  ruleExp: ��������ֵ�����ֵ�ı��ʽ�ж��Ƿ���ҪPublish,��������֪ͨ��������. �����rule="returnValue==true"��Ĭ���Ƿ���
  argExp:һ���������ʽ�б����û�У�����������������������Ϊ�����б����ݸ�sub��������ʽ�磺argExp="args[0].orderId,args[1],returnValue;"
  
 
  @Subscribe 
  path�� һ���߼�·��������Ҫ
  runPolicy�� ����ʱ����������ֵ��һ����sameTransacion,��ʾ��publish������ͬһ���������һ����afterCommint,����Ĭ��ֵ����ʾ������ɹ��ύ���첽ִ�У����Publishû�����������������@publish����ִ����Ϻ�����ִ��

 

3 @ClusterSync 
  path��һ���߼�·����һ��������JVM����ȡ����������ռ����������崻�����ʧȥ���ӣ����������������е�ĳһ��ռ��
  allowAcessAsFistTime: false����true��Ĭ��false�����Ϊtrue���������һ�ε��ú�����
  

4 @RemotePublish��ͬPublish�����Ƿ�����Զ��
  path һ��·��
  ruleEx: ��������ֵ�����ֵ�ж��Ƿ���ҪNotify��Ĭ����returnValue!=null ����������֪ͨ��������.�����rule="returnValue==true"
  argExp:һ���������ʽ�б����û�У�����������������������Ϊ�����б����ݸ�sub��������ʽ�磺argExp="arg0=input[0].orderId;arg1=input[0].cash;arg2=returnValue;"
  	
  @RemoteSubscriber
  path:һ��·����

5 @RemoteNotify,Զ��ֻ����һ����ִ��
  path һ��·��
  rule: ��������ֵ�����ֵ�ı��ʽ�ж��Ƿ���ҪNotify����������֪ͨ��������. �����rule="returnValue==true"��Ĭ���Ƿ���
  argExp:һ���������ʽ�б����û�У�����������������������Ϊ�����б����ݸ�sub��������ʽ�磺argExp="arg0=input[0].orderId;arg1=input[0].cash;arg2=returnValue;"
  @RemoteWait ��
  path:һ��·���� 
  

6 @Process
  @Task����


����Э�������ṩ��

ÿ��annotation�������Լ���Э�������ṩ�ߣ����߹���һ��Э�������ṩ�ߣ���������ṩ�߶�֧�֣���
Э�������ṩʱ��Ӧ����ϵͳ�����ɹ���Ҳ����ϵͳ���������ʼ���ɹ���
Remote��Э������ʵ�ֿ���ͨ��JMS��ZK,�������ݿ������ʵ�֡��Ƽ�ʹ��ZK����ZK ��RemotePublish ֧�ֲ����á����ʺ�����ҵ��ֻ�ʺ�һЩ����ͬ���͹����ܡ�
@Publish,@Process�ǻ���Local�ģ�����һ��������Э�������ṩ�ߡ�


����Э�������֣�

ͨ��Spring�Ļ���PostProcessor�������ҵ�ע��Ϊ@CooperationService���࣬Ȼ�����α������������Է�����Щ��Ҫ����ķ�������
Ҳ���ʺϱ�Ŀ�ܣ���û��spring�����

�� Э����
��Ϊ���𷽺ͽ��շ���ͨ������annotation������ʵ��Э����Ҳ����ֱ���ڴ��������Э������API�����㷢�𷽵������Ҫ��.��һ������������Ҫ����Publish����ͬ�ط�
PublicService pub = ctx.get("CooperationService-Pub");pub.send(path1, arglist),pub.send(path2,arglist2)

�� Ӧ�ó���˵��

1 ��̨������ֻ��һ̨��ִ��ĳ��job����ʹ��@RemoteSynronized 
2 ��ҵ����ú�����һЩ��Ҫҵ�񣬲�ϣ����Ҫҵ��Ӱ����ҵ������ܺ�������ά���� ��ҵ��ʹ��@Publish,�����ҵ��ʹ��@Subscribe��
3 ������Ҫͬ������̨�����ϣ�ʹ��@RemotePublish�� @RemoteSubscriber��ǩ
4 ������Ҫ����Զ�̵���һ̨��������ʹ��@RemoteNotifyȻ����@RemoteWait ��ǩһ����
5 ��ҵ��ʹ�Ҫҵ����󣬻�Ҫ�󽻸�Զ��һ���������� ������ʹ��@Publish,@Subscrbie�󣬿��Խ��@RemoteNotify��@RemoteWait ������



  
  
  