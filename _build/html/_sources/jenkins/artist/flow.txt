=========================== 
构建策略流程
=========================== 


构建策略流程
-------------

http://192.168.16.3:8000/idd/%E6%B5%8B%E8%AF%95%E8%B5%84%E6%96%99/artist/#g=1&p=%E6%9E%84%E5%BB%BA%E7%AD%96%E7%95%A5%E6%B5%81%E7%A8%8B

.. image:: media/jenkins_flow.png
    :align: center
    :alt: 构建策略流程

错误解决方法
-------------
Failed to execute goal on project artist-access-eureka: Could not resolve dependencies for project batar.artist:artist-access-eureka:jar:0.0.1-SNAPSHOT: Could not find artifact batar.artist:artist-common:jar:0.0.1-SNAPSHOT ->


需要在顶级pom.xml路径下install 