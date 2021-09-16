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

## 1.5 10GB GraySort example
 + yarn jar /usr/odp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapred.map.tasks=50 100000000 /user/a.reino.joaquim/data/10GB-sort-input
 
 + yarn jar /usr/odp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapred.tasks=50 -Dmapred.reduce.tasks=25 /user/a.reino.joaquim/data/10GB-sort-input /user/a.reino.joaquim/data/10GB-sort-output
 
 + yarn jar /usr/odp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /user/a.reino.joaquim/data/10GB-sort-output /user/a.reino.joaquim/data/10GB-sort-validate
 
 #### Result : 
 Many lines in java
 
 # MapReduce2

### mapper.py
	#! /usr/bin/env python
	"""mapper.py"""

	import sys

	#input comes from STDIN (standard input)
	for line in sys.stdin:
	    #remove leading and trailing whitespace
	    line = line.strip()
	    #split the line into words
	    words = line.split()

	    for word in words :
		#write the results to STDOUT (standard output);
		#what we output here will be the input for the 
		#Reduce step, i.e. the input for reducer.py
		#
		#tab-delimited; the trivial word count is 1
		print '%s\t%s' % (word,1)

### reducer.py

	#! /usr/bin/env python
	"""reducer.py"""

	from operator import itemgetter
	import sys

	current_word = None
	current_count = 0
	word = None

	#input comes from STDIN
	for line in sys.stdin:
	    #remove the leading and trailing whitespace
	    line = line.strip()

	    #parse the input we got from mapper.py
	    word, count = line.split('\t', 1)

	    #convert count (currently a string) to int 
	    count = int(count)

	    #this IF-switch only works because Hadoop sorts map output
	    #by key (here : word) before it is passed to the reducer
	    if current_word == word:
	       currrent_word += count
	    else:
	       if current_word:
		  sys.stdout.write(current_word, current_count)
	       current_count = count
	       current_word = word

	#do not forget to output the last word if needed !
	if current_word == word:
	    sys.stdout.write(current_word, current_count)

## 2.3.3 Test your code (cat data | map | sort | reduce)
 + echo "foo foo quux labs foo bar quux" | /home/a.reino.joaquim/mapper.py

#### Result : 
	foo	1
	foo	1
	quux	1
	labs	1
	foo	1
	bar	1
	quux	1

+ echo "foo foo quux labs foo bar quux" | /home/a.reino.joaquim/mapper.py | sort -k1,1 | /home/a.reino.joaquim/reducer.py
#### Result :
	bar	1
	foo	3
	labs	1
	quux	2

If we use it on the previous davinci.txt, we get this result (I only show a little part) : 

	Abadie	3
	Abadie,	1
	abandon	1
	abandoned	11
	abandoned,	4
	abandonment	1
	abeyance	1
	abhor.	1
	abide	2
	able	24
	abnormally	2
	abounded	1
	about	66
	About	14
	above	8
	
## Running the python code on hadoop


