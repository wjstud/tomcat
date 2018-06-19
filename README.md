### xdaili tomcat示例
在tomcat/bin/catalina.sh中添加
    JAVA_OPTS=-Djava.awt.headless=true #启用java图形处理
    JAVA_OPTS="$JAVA_OPTS -server -Xms1024m -Xmx2048m -XX:PermSize=512M -XX:MaxNewSize=512m -XX:MaxPermSize=2048m"
    JAVA_OPTS="$JAVA_OPTS $LOGGING_MANAGER -Djava.security.egd=file:/dev/./urandom" #加快tomcat启动速度
### tomcat 优化
#### 内存优化
    JAVA_OPTS="$JAVA_OPTS -server -Xms1024m -Xmx4096m -XX: PermSize=512M -XX:MaxNewSize=2048m -XX:MaxPermSize=4096m"
-server 启用jdk 的 server 版
-Xms java虚拟机初始化时的最小内存
-Xmx java虚拟机可使用的最大内存
-XX: PermSize 内存永久保留区域
-XX:MaxPermSize 内存最大永久保留区域
#### 并发优化
在Tomcat 配置文件 server.xml 中的
    <Connector port="9027"
    protocol="HTTP/1.1"
    maxHttpHeaderSize="8192"
    minProcessors="100"
    maxProcessors="1000"
    acceptCount="1000"
    redirectPort="8443"
    disableUploadTimeout="true"/>
调整连接器connector的并发处理能力
1>参数说明
maxThreads 客户请求最大线程数
minSpareThreads Tomcat初始化时创建的 socket 线程数
maxSpareThreads Tomcat连接器的最大空闲 socket 线程数
enableLookups 若设为true, 则支持域名解析，可把 ip 地址解析为主机名
redirectPort 在需要基于安全通道的场合，把客户请求转发到基于SSL 的 redirectPort 端口
acceptAccount 监听端口队列最大数，满了之后客户请求会被拒绝（不能小于maxSpareThreads ）
connectionTimeout 连接超时
minProcessors 服务器创建时的最小处理线程数
maxProcessors 服务器同时最大处理线程数
URIEncoding URL统一编码
2>Tomcat中的配置示例
    <Connector port="9027"
    protocol="HTTP/1.1"
    maxHttpHeaderSize="8192"
    maxThreads="1000"
    minSpareThreads="100"
    maxSpareThreads="1000"
    minProcessors="100"
    maxProcessors="1000"
    enableLookups="false"
    URIEncoding="utf-8"
    acceptCount="1000"
    redirectPort="8443"
    disableUploadTimeout="true"/>
#### 缓存优化
1>参数说明
compression 打开压缩功能
compressionMinSize 启用压缩的输出内容大小，这里面默认为2KB
compressableMimeType 压缩类型
connectionTimeout 定义建立客户连接超时的时间. 如果为 -1, 表示不限制建立客户连接的时间
2>Tomcat中的配置示例
    <Connector port="9027"　　
    protocol="HTTP/1.1"
    maxHttpHeaderSize="8192"
    maxThreads="1000"
    minSpareThreads="100"
    maxSpareThreads="1000"
    minProcessors="100"
    maxProcessors="1000"
    enableLookups="false"
    compression="on"
    compressionMinSize="2048"
    compressableMimeType="text/html,text/xml,text/javascript,text/css,text/plain"
    connectionTimeout="20000"
    URIEncoding="utf-8"
    acceptCount="1000"
    redirectPort="8443"
    disableUploadTimeout="true"/>
3>参考配置
    <Connector port="9027"
    protocol="HTTP/1.1"
    maxHttpHeaderSize="8192"
    maxThreads="1000"
    minSpareThreads="25"
    maxSpareThreads="75"
    enableLookups="false"
    compression="on"
    compressionMinSize="2048"
    compressableMimeType="text/html,text/xml,text/javascript,text/css,text/plain"
    connectionTimeout="20000"
    URIEncoding="utf-8"
    acceptCount="200"
    redirectPort="8443"
    disableUploadTimeout="true" />
4>后来发现在访问量达到3 百万多的时候出现性能瓶颈。更改后的配置
    <Connector port="9027"
    protocol="HTTP/1.1"
    maxHttpHeaderSize="8192"
    maxThreads="1000"
    minSpareThreads="100"
    maxSpareThreads="1000"
    minProcessors="100"
    maxProcessors="1000"
    enableLookups="false"
    compression="on"
    compressionMinSize="2048"
    compressableMimeType="text/html,text/xml,text/javascript,text/css,text/plain"
    connectionTimeout="20000"
    URIEncoding="utf-8"
    acceptCount="1000"
    redirectPort="8443"
    disableUploadTimeout="true"/>
