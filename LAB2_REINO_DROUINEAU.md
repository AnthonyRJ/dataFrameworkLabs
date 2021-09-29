# YARN & MapReduce 2

## 1.5 Import projet
  
  + **Generate the JAR using laven lifecycle package:**
      
      output:
        
        [INFO] ------------------------------------------------------------------------
        [INFO] BUILD SUCCESS
        [INFO] ------------------------------------------------------------------------
        [INFO] Total time:  06:25 min
        [INFO] Finished at: 2021-09-28T14:31:54+02:00
        [INFO] ------------------------------------------------------------------------

## 1.6 Send the JAR to the edge node

![image](https://user-images.githubusercontent.com/61497361/135090517-510e5e74-7421-4266-ae64-80b0b7ad2ea7.png)

## 1.6 Run the Job

  + **command to run:** yarn jar hadoop-examples-mapreduce-1.0-SNAPSHOT-jar-with-dependencies.jar wordcount /user/a.drouineau/65045-0.txt /user/a.drouineau/wordcount
  
    output :
        
        21/09/28 15:30:35 INFO mapreduce.Job:  map 100% reduce 100%
        21/09/28 15:30:36 INFO mapreduce.Job: Job job_1630864376208_0967 completed successfully
        21/09/28 15:30:36 INFO mapreduce.Job: Counters: 54
            File System Counters
             FILE: Number of bytes read=159473
             FILE: Number of bytes written=844985
             FILE: Number of read operations=0
             FILE: Number of large read operations=0
             FILE: Number of write operations=0
             HDFS: Number of bytes read=544024
             HDFS: Number of bytes written=115910
             HDFS: Number of read operations=8
             HDFS: Number of large read operations=0
             HDFS: Number of write operations=2
             HDFS: Number of bytes read erasure-coded=0
            Job Counters
             Launched map tasks=1
             Launched reduce tasks=1
             Data-local map tasks=1
             Total time spent by all maps in occupied slots (ms)=19911
             Total time spent by all reduces in occupied slots (ms)=25820
             Total time spent by all map tasks (ms)=6637
             Total time spent by all reduce tasks (ms)=6455
             Total vcore-milliseconds taken by all map tasks=6637
             Total vcore-milliseconds taken by all reduce tasks=6455
             Total megabyte-milliseconds taken by all map tasks=10194432
             Total megabyte-milliseconds taken by all reduce tasks=13219840
            Map-Reduce Framework
             Map input records=9706
             Map output records=90726
             Map output bytes=893537
             Map output materialized bytes=159473
             Input split bytes=106
             Combine input records=90726
             Combine output records=11176
             Reduce input groups=11176
             Reduce shuffle bytes=159473
             Reduce input records=11176
             Reduce output records=11176
             Spilled Records=22352
             Shuffled Maps =1
             Failed Shuffles=0
             Merged Map outputs=1
             GC time elapsed (ms)=179
             CPU time spent (ms)=6010
             Physical memory (bytes) snapshot=1508040704
             Virtual memory (bytes) snapshot=7303237632
             Total committed heap usage (bytes)=1506279424
             Peak Map Physical memory (bytes)=1200455680
             Peak Map Virtual memory (bytes)=3416035328
             Peak Reduce Physical memory (bytes)=307585024
             Peak Reduce Virtual memory (bytes)=3887202304
            Shuffle Errors
             BAD_ID=0
             CONNECTION=0
             IO_ERROR=0
             WRONG_LENGTH=0
             WRONG_MAP=0
             WRONG_REDUCE=0
            File Input Format Counters
             Bytes Read=543918
            File Output Format Counters
             Bytes Written=115910
             
## 1.8.1 Districts containing trees
