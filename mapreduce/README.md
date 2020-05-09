Try out the following example to familiarize yourself with the mapreduce framework of hadoop
* create a working directory for this examples
`C:\hadoop_mapreduce_examples`
* To run java programs in hadoop we need first to compile them and create executable jar files. find the following jar files in the hadoop installation directory
and copy them in your working directory. 
1. `hadoop-common-2.*.*.jar`
2. `hadoop-mapreduce-client-core-2.*.*.jar`
* copy the wordcount.java in the same directory
and a test input file `example.txt` with some text.
* start hadoop
`start-all`
*change the working directory to the one you created earlier
`cd\`
`cd\hadoop-mapreduce-examples`
* compile the wordcount.java, remember to include classpath
`javac wordcount.java -cp hadoop-common-2.*.*.jar;hadoop-mapreduce-client-core-2.*.*.jar`
* create a jar file
`jar -cvf wordcount.jar wordcount*class`
* create input directroy in fs and put the text file
`hadoop fs -mkdir /wordcount`
`hadoop fs -put example.txt /wordcount`
* run the wordcount example as follows, second and third arguments are the input and output respectively
` hadoop jar wordcount.jar  wordcount /wordcount/wordcount.txt  wordcount_output`
* to view the output inspect the directories for the output
` hadoop fs -ls /user`
* the output should be in the  directory `/user/opt/wordcount_output`
* to view the output
` hadoop fs -cat /user/opt/wordcount_output/part-r-00000`
