## 文件：

| 要获取的默认文件     | 文件存放在 Hadoop 的  jar 包中的位置                      |
| -------------------- | --------------------------------------------------------- |
| [core-default.xml]   | hadoop-common-3.1.3.jar/core-default.xml                  |
| [hdfs-default.xml]   | hadoop-hdfs-3.1.3.jar/hdfs-default.xml                    |
| [yarn-default.xml]   | hadoop-yarn-common-3.1.3.jar/yarn-default.xml             |
| [mapred-default.xml] | hadoop-mapreduce-client-core-3.1.3.jar/mapred-default.xml |

## 配置集群

### （1） 核心配置文件 core-site.xml

```xml
<configuration>
	<!-- 指定 NameNode 的地址 -->
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://hadoop102:8020</value>
    </property>

    <!-- 指定 hadoop 数据的存储目录 -->
    <property>
        <name>hadoop.tmp.dir</name>
        <value>/opt/module/hadoop-3.1.3/data</value>
    </property>

    <!-- 配置 HDFS 网页登录使用的静态用户为 atguigu -->
    <property>
        <name>hadoop.http.staticuser.user</name>
        <value>atguigu</value>
    </property>
</configuration>

```

### （2） HDFS 配置文件 hdfs-site.xml

```xml
<configuration>
	<!-- nn web 端访问地址-->
    <property>
        <name>dfs.namenode.http-address</name>
        <value>hadoop102:9870</value>
    </property>
	<!-- 2nn web 端访问地址-->
    <property>
        <name>dfs.namenode.secondary.http-address</name>
        <value>hadoop104:9868</value>
    </property>
</configuration>

```

### （3）YARN 配置文件yarn-site.xml

```xml
<configuration>
    <!-- 指定 MR 走 shuffle -->
    <property>
        <name>yarn.nodemanager.aux-services</name>
        <value>mapreduce_shuffle</value>
    </property>
    <!-- 指定 ResourceManager 的地址-->
    <property>
        <name>yarn.resourcemanager.hostname</name>
        <value>hadoop103</value>
    </property>
    <!-- 环境变量的继承 hadoop3.2.x版本以上不需要
			Hadoop3.1.x版本需要-->
   <!-- <property>
   	 	<name>yarn.nodemanager.env-whitelist</name>
  		<value>JAVA_HOME,HADOOP_COMMON_HOME,HADOOP_HDFS_HOME,HADOOP_CO
    NF_DIR,CLASSPATH_PREPEND_DISTCACHE,HADOOP_YARN_HOME,HADOOP_MAP
    RED_HOME</value>
    </property>-->
</configuration>
```

### （4） MapReduce 配置文件mapred-site.xml

```xml
<configuration>
	<!-- 指定 MapReduce 程序运行在 Yarn 上 -->
    <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
    </property>
</configuration>

```

### (5)**配置 workers** 

```
#添加集群主机名，如：
Master
slave1
slave2
slave3
```

### （6）将修改好的文件分发到集群中的各个服务器上

## 配置历史服务器

为了查看程序的历史运行情况，需要配置一下历史服务器。

具体配置步骤如下：

###  配置文件mapred-site.xml  ：

 ```xml
 <configuration>   
	<!-- 历史服务器端地址 -->
    <property>
    <name>mapreduce.jobhistory.address</name>
    <value>hadoop102:10020</value>
    </property>

    <!-- 历史服务器 web 端地址 -->
    <property>
    <name>mapreduce.jobhistory.webapp.address</name>
    <value>hadoop102:19888</value>
    </property>
</configuration>
 ```

## 配置日志的聚集

​        可以方便的查看到程序运行详情，方便开发调试。

### 配置 yarn-site.xml

```xml
<configuration>

    <!-- 开启日志聚集功能 -->
    <property>
        <name>yarn.log-aggregation-enable</name>
        <value>true</value>
    </property>
    <!-- 设置日志聚集服务器地址 -->
    <property>
        <name>yarn.log.server.url</name>
        <value>http://hadoop102:19888/jobhistory/logs</value>
    </property>
    <!-- 设置日志保留时间为 7 天 -->
    <property>
        <name>yarn.log-aggregation.retain-seconds</name>
        <value>604800</value>
    </property>

</configuration>
```



