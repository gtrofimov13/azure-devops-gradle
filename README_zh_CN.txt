���ڶ� Ant��Maven �� Gradle ���ɵ���������������·����ȡ��
https://docs.parasoft.com/display/JTEST1043/Integrating+with+Build+Systems

���ĵ����������ʹ�� Jtest ִ�о�̬���������в����Լ��ռ�
��������Ϣ - ʹ�ò�Ʒ�и����� "demo" ��Ŀ��

��ע�⣬����Ŀ�ķ�����ʹ�� demo.properties �ļ���ָ��
���������õġ����ļ�λ�� [INSTALL]/examples/demo Ŀ¼�С�


ǰ������
-------------------------------------------------
1. �� Jtest ��װĿ¼�е� jtestcli.properties �ļ������� Jtest ���֤��


Jtest �����ļ�
-------------------------------------------------
1. ���� "Recommended Rules" �������ã���ֱ��ִ�о�̬�����������κι���ϵͳ��- ʹ���������
   Windows:
     ..\..\jtestcli.exe -config "builtin://Recommended Rules" -data demo.data.json -report report
   UNIX:
     ../../jtestcli -config "builtin://Recommended Rules" -data demo.data.json -report report


Ant
-------------------------------------------------
1. ��ȷ�����·���ϴ��ڿ��õ� "ant"��

2. ���� "Demo Configuration"����ִ�о�̬���������ռ���Ԫ���Եĸ����ʣ�

     ant -file jtest.xml -Djtest.config="builtin://Demo Configuration"

   ������ "demo" ��Ŀ�����е�Ԫ���ԡ� Ant �� Jtest ����ռ�Դ����������ݺͰ��������ʵĵ�Ԫ���Խ������ִ�з��������ɱ��档

   ע�⣺

   �������о�̬��������ʹ���������

     ant -file jtest.xml jtest-sae

   �������е�Ԫ���ԣ���ʹ���������

     ant -file jtest.xml jtest-utc

   jtest.xml ��ָ�������� - ����� "jtest", "jtest-sae", �� "jtest-utc" Ŀ�ꡣ


Maven
-------------------------------------------------
1. ��ȷ�����·���ϴ��ڿ��õ� "mvn"��
2. ����� Jtest �û�ָ��������� Maven ���ã�
   https://docs.parasoft.com/display/JTEST1043/Configuring+the+Jtest+Plugin+for+Maven

3. ���� "Demo Configuration" ��ִ�о�̬���������ռ����ڵ�Ԫ���Եĸ����ʣ�

     mvn clean test-compile jtest:agent test jtest:jtest -Djtest.config="builtin://Demo Configuration"

   ������ "demo" ��Ŀ�������е�Ԫ���ԡ� Maven �� Jtest ����ռ�Դ����������ݺ�
   ���������ʵĲ��Խ������ִ�з��������ɱ��档

   ע�⣺

   �������о�̬��������ʹ���������

     mvn jtest:jtest

   Ĭ��ʹ�� "Recommended Rules" �������á�

   �������е�Ԫ���ԣ���ʹ���������

     mvn clean test-compile jtest:agent test jtest:jtest -Djtest.config="builtin://Unit Tests"


Gradle
-------------------------------------------------
1. ������ Jtest ��װ��������������õ������ű��� "jtest" �顣

2. ���� "Demo Configuration"����ִ�о�̬���������ռ����ڵ�Ԫ���Եĸ����ʣ�

     gradlew clean jtest-agent test jtest -Djtest.config="builtin://Demo Configuration"

   ������ "demo" ��Ŀ�������е�Ԫ���ԡ�Gradle �� Jtest ������ռ�Դ����������ݺͲ��Խ������ִ�к����ɱ��档

   ע�⣺

   �������о�̬��������ʹ���������

     gradlew clean assemble jtest

   Ĭ��ʹ�� "Recommended Rules" ���á�

   �������е�Ԫ���ԣ���ʹ���������

     gradlew clean jtest-agent test jtest -Djtest.config="builtin://Unit Tests"


=================================================

����Ӱ�����

Maven �� Gradle ֧�ֲ���Ӱ�������

Windows:

1. ʹ�� Maven �� Gradle ���в��ԣ����ռ����ڲ��Ժ͸����ʵĻ������ݣ�
   mvn clean test-compile jtest:agent test jtest:jtest -Djtest.config="builtin://Unit Tests" -Djtest.report=cbt
   ��
   gradlew clean jtest-agent test jtest -Djtest.config="builtin://Unit Tests" -Djtest.report=cbt

   ע�⣺��ˣ�report.xml �� cover .xml �ļ����� 'cbt' ���ļ����д����� 

2. �޸Ĳ��Է�Χ�е�Դ�ļ���
   src\main\java\examples\mock\FileExample.java

3. ��������������ִ���ܸ���Ӱ��Ĳ��ԣ�
   mvn clean cbt:affected-tests test -Dparasoft.coverage.file=cbt/coverage.xml -Dparasoft.test.file=cbt/report.xml
   ��
   gradlew clean affectedTests test -Dparasoft.coverage.file=cbt/coverage.xml -Dparasoft.test.file=cbt/report.xml --no-daemon

   ���ܴ����޸�Ӱ��Ĳ��Բ���ִ�С�

UNIX:

1. ʹ�� Maven �� Gradle ���в��ԣ����ռ����Ժ͸����ʵĻ������ݣ�
   mvn clean test-compile jtest:agent test jtest:jtest -Djtest.config="builtin://Unit Tests" -Djtest.report=cbt
   ��
   ./gradlew clean jtest-agent test jtest -Djtest.config="builtin://Unit Tests" -Djtest.report=cbt

   ע�⣺��ˣ�report.xml �� coverage.xml �ļ����� 'cbt' ���ļ����д�����

2. �޸Ĳ��Է�Χ�е�Դ�ļ�:
   src/main/java/examples/mock/FileExample.java

3. ��������������ִ���ܸ���Ӱ��Ĳ��ԣ�
   mvn clean cbt:affected-tests test -Dparasoft.coverage.file=cbt/coverage.xml -Dparasoft.test.file=cbt/report.xml
   ��
   ./gradlew clean affectedTests test -Dparasoft.coverage.file=cbt/coverage.xml -Dparasoft.test.file=cbt/report.xml --no-daemon

   ���ܴ����޸�Ӱ��Ĳ��Բ���ִ�С�


�йظ������飬����ģ�
   https://docs.parasoft.com/display/JTEST1043/Testing+and+Analysis+with+Maven
   https://docs.parasoft.com/display/JTEST1043/Testing+and+Analysis+with+Gradle

=================================================

�ռ�Ӧ�ó��򸲸���

Windows:

1. ����Ӧ�ó����ռ�������������
     ant -file jtest.xml clean jtest-monitor
     ��
     mvn clean package jtest:monitor    
     ��
     gradlew clean assemble jtest-monitor
     
   ע�⣺��ˣ���Ӧ�û�� monitor.zip �ļ���

2. ����Ӧ�ó����ռ�����������
     
   a) �� monitor.zip �鵵�ļ���ѹ�� "demo" Ŀ¼�У���������Ŀ¼ "monitor"����
      ant:
        Archive path: parasoft\jtest-monitor\monitor.zip
      mvn:
        Archive path: target\jtest\monitor\monitor.zip
      gradle:
        Archive path: build\jtest\monitor.zip
     
   b) ���� agent.bat
      cd monitor
      agent.bat
      cd ..
      
   c) ʹ�� b) �����ɵ� Java VM ��������Ӧ�ó���
      ant
        java -cp demo.jar [paste argument generated in point b] examples.stackmachine.RunnableStackMachine
      mvn:
        java -cp target\Demo.jar [paste argument generated in point b] examples.stackmachine.RunnableStackMachine
      gradle:
        java -cp build\libs\demo.jar [paste argument generated in point b] examples.stackmachine.RunnableStackMachine

   d) ʹ�� "Stack Machine Example" Ӧ�ó���ִ�ж��������
      - ������ 123 ���뵽 "Input" �ֶ���
      - ��ѹ "push" ��ť 5 ��
      - ��ѹ "+", "-", "x" �� "/" ��ť
      - �˳�Ӧ�ó���

3. ���ɸ����ʱ���

     ..\..\jtestcli.exe -config "builtin://Calculate Application Coverage" -staticcoverage monitor\static_coverage.xml -runtimecoverage monitor\runtime_coverage

     �����ʵ���ϸ��Ϣ������ report.html ���ҵ�

UNIX:

1. ����Ӧ�ó����ռ��������������
     ant -file jtest.xml clean jtest-monitor
     ��
     mvn clean package jtest:monitor    
     ��
     ./gradlew clean build jtest-monitor
     
   ע�⣺��ˣ���Ӧ�û�� monitor.zip �ļ���

2. ����Ӧ�ó����ռ�����������
   
   a) �� monitor.zip �鵵�ļ���ѹ�� demo ·���ϣ���������Ŀ¼���ӣ�
      ant:
        unzip ./parasoft/jtest-monitor/monitor.zip
      mvn: 
        unzip ./target/jtest/monitor/monitor.zip
      gradle:
        unzip ./build/jtest/monitor.zip
     
   b) ���� agent.sh
      ./monitor/agent.sh
      
   c) ʹ�� b) �����ɵ� Java VM ��������Ӧ�ó���
      ant
        java -cp ./demo.jar [paste argument generated in point b] examples.stackmachine.RunnableStackMachine
      mvn:
        java -cp ./target/Demo.jar [paste argument generated in point b] examples.stackmachine.RunnableStackMachine
      gradle:
        java -cp ./build/libs/demo.jar [paste argument generated in point b] examples.stackmachine.RunnableStackMachine

   d) ʹ�� "Stack Machine Example" Ӧ�ó���ִ���������
      - ������ 123 ���뵽 "Input" �ֶ���
      - ��ѹ "push" ��ť 5 ��
      - ��ѹ "+", "-", "x" �� "/" ��ť
      - �˳�Ӧ�ó���

3. ���ɸ����ʱ���

     ../../jtestcli -config "builtin://Calculate Application Coverage" -staticcoverage ./monitor/static_coverage.xml -runtimecoverage ./monitor/runtime_coverage

     �����ʵ���ϸ��Ϣ������ report.html ���ҵ�


�йظ������飬����� https://docs.parasoft.com/display/JTEST1043/Application+Coverage
