==============================
安装Jenkins
==============================

系统安装
--------
	CentOS-6.8-x86_64-minimal

	下载地址:http://mirrors.aliyun.com/centos/6.8/isos/x86_64/CentOS-6.8-x86_64-minimal.iso
	ps:虚拟机安装用户root:Hexiaoyun128.

启用网卡信息 
------------
	* 文件路径： 
	.. code-block:: shell 

		/etc/sysconfig/network-scripts/ifcfg-eth0 

	* 修改网卡信息，将ONBOOT=no改为ONBOOT=yes
	.. code-block:: shell 

		DEVICE=eth0  
		HWADDR=08:00:27:B5:97:CE 
		TYPE=Ethernet 
		UUID=06beb802-ad1e-41da-bff2-a42d95e3aca2 
		ONBOOT=yes 
		NM_CONTROLLED=yes 
		BOOTPROTO=dhcp 
maven配置
-----------
	* 下载maven
	.. code-block:: shell 

		wget https://mirrors.tuna.tsinghua.edu.cn/apache/maven/maven-3/3.5.0/binaries/apache-maven-3.5.0-bin.tar.gz
	* 解压
	.. code-block:: shell 

		tar zxvf apache-maven-3.5.0-bin.tar.gz  
		mv apache-maven-3.5.0 /usr/local/
		 

jdk配置
--------
	* 下载地址：

		http://192.168.1.7/jdk-8u111-linux-x64.tar.gz?fid=Sz8HfSSYTUEE7nuDfgMFJPrLx0A3l9AKAAAAAB6JNf4ch7h0BdTpSQCgtCpPRYyN&mid=666&threshold=150&tid=268209DF4960588CC23F42A3D18C19C5&srcid=119&verno=1
	* 执行命令
		.. code-block:: shell  

			tar zxvf jdk-8u111-linux-x64.tar.gz  
			mv jdk1.8.0_111 /usr/local/

	* 在/.bashrc后面追加下面的内容:
		.. code-block:: shell 

			export MAVEN_HOME=/usr/local/apache-maven-3.5.0
			export JAVA_HOME=/usr/local/jdk1.8.0_111
			export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
			export PATH=$JAVA_HOME/bin:$MAVEN_HOME/bin:$PATH
			export JRE_HOME=$JAVA_HOME/jre

	* 更新
	.. code-block:: shell 

		source .bashrc

git安装(已安装则忽略)
---------------------
.. code-block:: shell

	yum install git-core -y

安装Jenkins:
----------------------------

	* Jenkins安装
		.. code-block:: shell

			yum install wget -y 
			wget -O /etc/yum.repos.d/jenkins.repo http://jenkins-ci.org/redhat/jenkins.repo
			rpm --import http://pkg.jenkins-ci.org/redhat/jenkins-ci.org.key
			yum install jenkins -y
		
	* 修改jenkins配置信息:
		.. code-block:: shell

			vi /etc/init.d/jenkins 

		在70行左右的candidates中增加下面的代码(前面安装jdk时的java路径)

		.. code-block:: shell
			
			/usr/local/jdk1.8.0_111/bin/java

	* 启动 jenkins
	.. code-block:: shell

		service jenkins start 

	* 开放8080 端口
	.. code-block:: shell

		vi /etc/sysconfig/iptables 
	* 添加下面的内容(放到开放端口22下面)

		.. code-block:: shell

			-A INPUT -m state --state NEW -m tcp -p tcp --dport 8080 -j ACCEPT
		* 重启防火墙
		.. code-block:: shell

			/etc/init.d/iptables restart 

	* 修改jenkins的用户
	.. code-block:: shell

		vi  /etc/sysconfig/jenkins
		JENKINS_USER="root"

查看初始密码：
--------------
.. code-block:: shell

	tail /var/lib/jenkins/secrets/initialAdminPassword


浏览器登录
----------
http://192.168.21.201:8080/
输入前面查看到的密码

.. image:: media/init.png
    :align: center
    :alt: 初始页面

安装推荐插件
------------

.. image:: media/intall_suggested_plugins.png
    :align: center
    :alt: 安装推荐插件

进度查看
------------

.. image:: media/progress_check.png
    :align: center
    :alt: 进度查看

用户和密码设置
---------------
	输入用户名batar
	输入密码：batar

.. image:: media/jenkins_user.png
    :align: center
    :alt: 用户和密码设置

后续默认操作即可进入jenkins页面


.. image:: media/jenkins_first.png
    :align: center
    :alt: jenkins页面



