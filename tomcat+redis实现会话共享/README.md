#### 项目源码
[tomcat-redis-session-manager](https://github.com/jcoleman/tomcat-redis-session-manager)
#### 用法

将以下内容添加到Tomcat context.xml中（或适用时，server.xml的上下文块）。

    <Valve className="com.orangefunction.tomcat.redissessions.RedisSessionHandlerValve" />
    <Manager className="com.orangefunction.tomcat.redissessions.RedisSessionManager"
         host="localhost" <!-- optional: defaults to "localhost" -->
         port="6379" <!-- optional: defaults to "6379" -->
         database="0" <!-- optional: defaults to "0" -->
         maxInactiveInterval="60" <!-- optional: defaults to "60" (in seconds) -->
         sessionPersistPolicies="PERSIST_POLICY_1,PERSIST_POLICY_2,.." <!-- optional -->
         sentinelMaster="SentinelMasterName" <!-- optional -->
         sentinels="sentinel-host-1:port,sentinel-host-2:port,.." <!-- optional --> />
The Valve must be declared before the Manager.

Copy the following files into the TOMCAT_BASE/lib directory:

tomcat-redis-session-manager-VERSION.jar
jedis-2.5.2.jar
commons-pool2-2.2.jar

Reboot the server, and sessions should now be stored in Redis.
重新启动服务器，会话现在应该存储在Redis中。
