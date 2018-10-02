# idea发布项目到远程tomcat

1，	在编辑tomcat/bin下的catalina.sh，添加配置信息
---

	export CATALINA_OPTS="-Dcom.sun.management.jmxremote
	-Dcom.sun.management.jmxremote.port=1099
	-Dcom.sun.management.jmxremote.ssl=false
	-Dcom.sun.management.jmxremote.authenticate=false
	-Djava.rmi.server.hostname=110.110.110.110"
	
	export JAVA_OPTS="-Dcom.sun.management.jmxremote=
	-Dcom.sun.management.jmxremote.rmi.port=1099
	-Dcom.sun.management.jmxremote.port=1099
	-Dcom.sun.management.jmxremote.ssl=false
	-Dcom.sun.management.jmxremote.authenticate=false"
	
	export CATALINA_OPTS="$CATALINA_OPTS -server -Xdebug -Xnoagent -Djava.compiler=NONE -Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=5005"

说明：

	110.110.110.110换成你服务器的ip
	很多教程没有-Dcom.sun.management.jmxremote.rmi.port=1099这一句配置，会出现
	Error running 'remoteMvc'
	Unable to connect to the 111.230.226.20:1099, reason:
	java.rmi.ConnectException: Connection refused to host: 111.230.226.20; nested exception is: 
	java.net.ConnectException: Connection timed out: connect



开放服务器的1099,8080,22,5005端口

2，在idea中添加远程服务器
---

![](G:\库\Desktop\text\技术类\pic\ideaRemoteTomcat1.png)

![](G:\库\Desktop\text\技术类\pic\ideaRemoteTomcat2.png)

类型选择：sftp 
	(sftp由ssh支持,因此不必再额外安装ftp服务，而且自己配置ftp的话会有很多权限和路径的问题)
![](G:\库\Desktop\text\技术类\pic\ideaRemoteTomcat3.png)

![](G:\库\Desktop\text\技术类\pic\ideaRemoteTomcat4.png)

端口号选择5005，与catalina.sh 添加的配置是最后一行的端口号保持一致

![](G:\库\Desktop\text\技术类\pic\ideaRemoteTomcat5.png)

Deployment 中选择 exploded而不是war

3，在服务器上运行 tomcat/bin/catalina.sh run
---

​	运行后通过浏览器查看

![](G:\库\Desktop\text\技术类\pic\ideaRemoteTomcat6.png)

再在idea上进行发布

![](G:\库\Desktop\text\技术类\pic\ideaRemoteTomcat7.png)

然后就可以访问了


![](G:\库\Desktop\text\技术类\pic\ideaRemoteTomcat8.png)