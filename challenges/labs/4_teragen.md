Become ernest:
```
sudo su ernest
```

Run teragen:
```
time hadoop jar /opt/cloudera/parcels/CDH/jars/hadoop-examples.jar teragen -Dmapreduce.job.maps=6 -Ddfs.blocksize=33554432 51200000 tgen512m
```
Output (time only):
```
real	0m46.788s
user	0m7.241s
sys	0m0.398s
```
Output (full):
```
17/10/20 09:13:58 INFO client.RMProxy: Connecting to ResourceManager at ip-172-31-13-131.eu-central-1.compute.internal/172.31.13.131:8032
17/10/20 09:13:59 INFO terasort.TeraSort: Generating 51200000 using 6
17/10/20 09:13:59 INFO mapreduce.JobSubmitter: number of splits:6
17/10/20 09:13:59 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1508489352789_0001
17/10/20 09:13:59 INFO impl.YarnClientImpl: Submitted application application_1508489352789_0001
17/10/20 09:14:00 INFO mapreduce.Job: The url to track the job: http://ip-172-31-13-131.eu-central-1.compute.internal:8088/proxy/application_1508489352789_0001/
17/10/20 09:14:00 INFO mapreduce.Job: Running job: job_1508489352789_0001
17/10/20 09:14:07 INFO mapreduce.Job: Job job_1508489352789_0001 running in uber mode : false
17/10/20 09:14:07 INFO mapreduce.Job:  map 0% reduce 0%
17/10/20 09:14:19 INFO mapreduce.Job:  map 12% reduce 0%
17/10/20 09:14:20 INFO mapreduce.Job:  map 24% reduce 0%
17/10/20 09:14:22 INFO mapreduce.Job:  map 29% reduce 0%
17/10/20 09:14:23 INFO mapreduce.Job:  map 34% reduce 0%
17/10/20 09:14:25 INFO mapreduce.Job:  map 40% reduce 0%
17/10/20 09:14:26 INFO mapreduce.Job:  map 47% reduce 0%
17/10/20 09:14:28 INFO mapreduce.Job:  map 50% reduce 0%
17/10/20 09:14:29 INFO mapreduce.Job:  map 54% reduce 0%
17/10/20 09:14:31 INFO mapreduce.Job:  map 61% reduce 0%
17/10/20 09:14:32 INFO mapreduce.Job:  map 66% reduce 0%
17/10/20 09:14:34 INFO mapreduce.Job:  map 71% reduce 0%
17/10/20 09:14:35 INFO mapreduce.Job:  map 73% reduce 0%
17/10/20 09:14:37 INFO mapreduce.Job:  map 82% reduce 0%
17/10/20 09:14:38 INFO mapreduce.Job:  map 86% reduce 0%
17/10/20 09:14:39 INFO mapreduce.Job:  map 88% reduce 0%
17/10/20 09:14:40 INFO mapreduce.Job:  map 94% reduce 0%
17/10/20 09:14:41 INFO mapreduce.Job:  map 97% reduce 0%
17/10/20 09:14:42 INFO mapreduce.Job:  map 100% reduce 0%
17/10/20 09:14:42 INFO mapreduce.Job: Job job_1508489352789_0001 completed successfully
17/10/20 09:14:42 INFO mapreduce.Job: Counters: 31
	File System Counters
		FILE: Number of bytes read=0
		FILE: Number of bytes written=742200
		FILE: Number of read operations=0
		FILE: Number of large read operations=0
		FILE: Number of write operations=0
		HDFS: Number of bytes read=511
		HDFS: Number of bytes written=5120000000
		HDFS: Number of read operations=24
		HDFS: Number of large read operations=0
		HDFS: Number of write operations=12
	Job Counters 
		Launched map tasks=6
		Other local map tasks=6
		Total time spent by all maps in occupied slots (ms)=192882
		Total time spent by all reduces in occupied slots (ms)=0
		Total time spent by all map tasks (ms)=192882
		Total vcore-seconds taken by all map tasks=192882
		Total megabyte-seconds taken by all map tasks=197511168
	Map-Reduce Framework
		Map input records=51200000
		Map output records=51200000
		Input split bytes=511
		Spilled Records=0
		Failed Shuffles=0
		Merged Map outputs=0
		GC time elapsed (ms)=771
		CPU time spent (ms)=102270
		Physical memory (bytes) snapshot=2373246976
		Virtual memory (bytes) snapshot=16758943744
		Total committed heap usage (bytes)=2195718144
	org.apache.hadoop.examples.terasort.TeraGen$Counters
		CHECKSUM=109963291816450258
	File Input Format Counters 
		Bytes Read=0
	File Output Format Counters 
		Bytes Written=5120000000

real	0m46.788s
user	0m7.241s
sys	0m0.398s
```

Listing of tgen512m:
```
hdfs dfs -ls /user/ernest/tgen512m
```
Output:
```
Found 7 items
-rw-r--r--   3 ernest ernest          0 2017-10-20 09:14 /user/ernest/tgen512m/_SUCCESS
-rw-r--r--   3 ernest ernest  853333400 2017-10-20 09:14 /user/ernest/tgen512m/part-m-00000
-rw-r--r--   3 ernest ernest  853333300 2017-10-20 09:14 /user/ernest/tgen512m/part-m-00001
-rw-r--r--   3 ernest ernest  853333300 2017-10-20 09:14 /user/ernest/tgen512m/part-m-00002
-rw-r--r--   3 ernest ernest  853333400 2017-10-20 09:14 /user/ernest/tgen512m/part-m-00003
-rw-r--r--   3 ernest ernest  853333300 2017-10-20 09:14 /user/ernest/tgen512m/part-m-00004
-rw-r--r--   3 ernest ernest  853333300 2017-10-20 09:14 /user/ernest/tgen512m/part-m-00005
```

Blocks associated with tgen512m directory:
```
hdfs fsck -blocks /user/ernest/tgen512m
```
Output:
```
Connecting to namenode via http://ip-172-31-13-131.eu-central-1.compute.internal:50070
FSCK started by ernest (auth:SIMPLE) from /172.31.13.131 for path /user/ernest/tgen512m at Fri Oct 20 09:19:37 UTC 2017
.......Status: HEALTHY
 Total size:	5120000000 B
 Total dirs:	1
 Total files:	7
 Total symlinks:		0
 Total blocks (validated):	156 (avg. block size 32820512 B)
 Minimally replicated blocks:	156 (100.0 %)
 Over-replicated blocks:	0 (0.0 %)
 Under-replicated blocks:	0 (0.0 %)
 Mis-replicated blocks:		0 (0.0 %)
 Default replication factor:	3
 Average block replication:	3.0
 Corrupt blocks:		0
 Missing replicas:		0 (0.0 %)
 Number of data-nodes:		4
 Number of racks:		1
FSCK ended at Fri Oct 20 09:19:37 UTC 2017 in 5 milliseconds


The filesystem under path '/user/ernest/tgen512m' is HEALTHY
```

There are 156 blocks associated with the directory.


**Note:** I noticed that the directory was named 512m (either for "millions" or "mega" or "mebi" disregarding capitalization), but the dataset is actually ~4.8GiB