# YARN

## 1.2 Run the wordcount example

+ yarn jar /usr/odp/current/hadoop-client/src/hadoop-mapreduce-project/hadoop-mapreduce-examples

#### Result : 

    An example program must be given as the first argument.
    Valid program names are:
    aggregatewordcount: An Aggregate based map/reduce program that counts the words in the input files.
    aggregatewordhist: An Aggregate based map/reduce program that computes the histogram of the words in the input files.
    bbp: A map/reduce program that uses Bailey-Borwein-Plouffe to compute exact digits of Pi.
    dbcount: An example job that count the pageview counts from a database.
    distbbp: A map/reduce program that uses a BBP-type formula to compute exact bits of Pi.
    grep: A map/reduce program that counts the matches of a regex in the input.
    join: A job that effects a join over sorted, equally partitioned datasets
    multifilewc: A job that counts words from several files.
    pentomino: A map/reduce tile laying program to find solutions to pentomino problems.
    pi: A map/reduce program that estimates Pi using a quasi-Monte Carlo method.
    randomtextwriter: A map/reduce program that writes 10GB of random textual data per node.
    randomwriter: A map/reduce program that writes 10GB of random data per node.
    secondarysort: An example defining a secondary sort to the reduce.
    sort: A map/reduce program that sorts the data written by the random writer.
    sudoku: A sudoku solver.
    teragen: Generate data for the terasort
    terasort: Run the terasort
    teravalidate: Checking results of terasort
    wordcount: A map/reduce program that counts the words in the input files.
    wordmean: A map/reduce program that counts the average length of the words in the input files.
    wordmedian: A map/reduce program that counts the median length of the words in the input files.
    wordstandarddeviation: A map/reduce program that counts the standard deviation of the length of the words in the input files.

+ yarn jar /usr/odp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount

#### Result :

    Usage: wordcount <in> [<in>...] <out>

+ yarn jar /usr/odp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /user/a.reino.joaquim/davinci.txt /user/a.reino.joaquim/wordcount

 #### Result :
 Many lines that i think it's not relevant to put it in, here the first lines :  
 
    21/09/15 16:28:33 INFO mapreduce.Job:  map 0% reduce 0%
    21/09/15 16:28:41 INFO mapreduce.Job:  map 100% reduce 0%
    21/09/15 16:28:48 INFO mapreduce.Job:  map 100% reduce 100%
    21/09/15 16:28:49 INFO mapreduce.Job: Job job_1630864376208_0191 completed successfully
    21/09/15 16:28:49 INFO mapreduce.Job: Counters: 54
	  File System Counters
		FILE: Number of bytes read=159473
		FILE: Number of bytes written=845111
		FILE: Number of read operations=0
		FILE: Number of large read operations=0
		FILE: Number of write operations=0
		HDFS: Number of bytes read=544028
		HDFS: Number of bytes written=115910
		HDFS: Number of read operations=8
		HDFS: Number of large read operations=0
		HDFS: Number of write operations=2
		HDFS: Number of bytes read erasure-coded=0

 + hdfs dfs -cat /user/a.reino.joaquim/wordcount/part-r-00000
 
 #### Result : 
 Like the last command, there are too much lines to put it in so I show you the first lines : 
 
    lderman,	2
    Aldershot	2
    Alex.	1
    All	23
    Allenby	2
    Allenby's	4
    Allenby,	1
    Alley	1
    Alley,	1
    Allied	6
    Allies	12
    Allies,	4
    Allies.	2
    Allusion	1
    Along	2
    Aloof	1
    Alps	1
    Although	2
    Altogether	5
    Altogether,	1
    America	2
    American	1
    Among	9
    An	18

## 1.3 The Sudoku example
  
 + yarn jar /usr/odp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar sudoku sudoku.dta
 
 #### Result : 
 
    Solving sudoku.dta
    8 5 1 3 9 2 6 4 7 
    4 3 2 6 7 8 1 9 5 
    7 9 6 5 1 4 3 8 2 
    6 1 4 8 2 3 7 5 9 
    5 7 8 9 6 1 4 2 3 
    3 2 9 4 5 7 8 1 6 
    9 4 7 2 8 6 5 3 1 
    1 8 5 7 3 9 2 6 4 
    2 6 3 1 4 5 9 7 8 

    Found 1 solutions

## 1.4 Pi example
 + yarn jar /usr/odp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar pi 16 10000000
  
#### Result : 
The interesting part is :

    Job Finished in 24.132 seconds
    Estimated value of Pi is 3.14159155000000000000

