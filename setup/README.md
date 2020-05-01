#### installation
This file provides a step by step guide for installing hadoop on a windows machine, for this guide windows 7 was used.
You can adopt the same configurations for other versions of windows.

#### Tools
A JDk tool is needed for hadoop as most of hadoop programs are in java. Install and configure a jdk tool to a preferred location on your machine
Also required is a tool to unpack the hadoop rar file.

#### Downloading
Download a  stable versionn of hadoop from apache and unpack it. You might get errors while unpacking which you can just ingore.

#### configurations
* create a directory `C:\hadoop` and transfer the unpacked hadoop files into this folder
* create a folder `data` in this directory and inside this folder create two subfolders `namenode' and `datanode` this is where blocks fo data for hadoop will be stored.

* setup enviroment variables as follows
navigate to `computer>properties>advanced system settings> environment variables` . Add `HADOOP_HOME` to user variables and path as `C:\hadoop`
add the variable `JAVA_HOME` and path as the installation directory of your jdk tool eg `C:\java\jdk1.8.0_221`

Edit the user variable PATH to include the following `C:\hadoop\bin` and `C:\java\jdk1.8.0_221\bin`

* Editing the xml files
navigate to `C:\hadoop\etc\hadoop` and edit the following xml files.

core-site.xml as follows
```<configuration>
     <property>
         <name>fs.defaultFS</name>
         <value>hdfs://localhost:9000</value>
     </property>
</configuration>
```


hdfs-site.xml as follows
```<configuration>
     <property>
         <name>dfs.replication</name>
         <value>1</value>
     </property>
     <property>
         <name>dfs.namenode.name.dir</name>
         <value>C:\hadoop\data\namenode</value>
     </property>
     <property>
         <name>dfs.datanode.data.dir</name>
         <value>C:\hadoop\data\datanode</value>
     </property>
     <property>
        <name>dfs.permissions.enabled</name> 
        <value>false</value>
    </property> 
 </configuration>
 ```

Create copy of the mapred-site.template and rename it as mapred.xml now add the following configurations
```<configuration>
     <property>
         <name>mapred.framework.name</name>
         <value>yarn</value>
     </property>
 </configuration>
```

edit the yarn-site.xml as follows
```<configuration>
     <property>
         <name>yarn.nodemanager.aux-services</name>
         <value>mapreduce_shuffle</value>
     </property>
     <property>
         <name>yarn.nodemanager.aux-services.mapreduce.shuffle.class</name>
         <value>org.apache.hadoop.mapred.ShuffleHandler</value>
     </property>
 </configuration>
 ```

Finally edit the `hadoop-env.cmd` the variable JAVA_HOME should point to the path of your jdk installation
` set JAVA_HOME="C:\java\jdk1.8.0_221"` use double quotes for longer paths

* Replace the bin files in the hadoop directory with windows compatible files provided test the installation as follows:

#### Testing installation
open the windows native shell and  use the following commands
`hdfs namenode -format` for formatting the data block that hadoop will use
`start-all` to start hadoop daemons: namenode,datanode,nodemanager,resourcemanager
create a directory in the fs and try to put a file into it 
`hadoop fs -mkdir /input
`hadoop fs -put C:\example.txt  /input`
confirm that the file has been copied
`hadoop fs -ls /input`
Try to remove the file from the directory
`hadoop fs -rm -r /input/example.txt`

The following will give you  a list of useful commands
`hadoop fs -help` or just `hadoop fs`

#### Your first mapreduce program
hadoop has number of mapreduce examples that you can try. Use the following command to see available examples
` hadoop jar C:\hadoop\share\hadoop\mapreduce\hadoop-mapreduce-examples-2.*.*.jar`
Run the PI example  as follows
` hadoop jar C:\hadoop\share\hadoop\mapreduce\hadoop-mapreduce-examples-2.*.*.jar pi 4 1000`

To stop the daemons use 
`stop-all`
The web UI for  resource manager and namenode can be accessed through
`localhost:8088`
`localhost:50070`

* documentation
[https://hadoop.apache.org/release.html] 
[https://hadoop.apache.org/docs/r2.9.2/]

