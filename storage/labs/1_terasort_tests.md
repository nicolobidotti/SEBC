## Create Linux user

Command: `sudo useradd --create-home nicolobidotti`

No need to create HDFS home, it was done in the previous lab.

Become new user: `sudo su - nicolobidotti`

## Create a 10 GB file using teragen

Calculation for # of rows: assuming in GB the "giga" is 10^9 and given a row size of 100 bytes, we need to generate 100'000'000 rows.

Command:
```
time hadoop jar /opt/cloudera/parcels/CDH/jars/hadoop-examples.jar teragen -Dmapreduce.job.maps=20 -Ddfs.blocksize=33554432 100000000 storagelabs/terasort/unsorted10GB
```

Output:
```
17/10/18 01:22:36 INFO client.RMProxy: Connecting to ResourceManager at ip-172-31-5-172.eu-central-1.compute.internal/172.31.5.172:8032
17/10/18 01:22:37 INFO terasort.TeraSort: Generating 100000000 using 20
17/10/18 01:22:37 INFO mapreduce.JobSubmitter: number of splits:20
17/10/18 01:22:37 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1508282962007_0007
17/10/18 01:22:37 INFO impl.YarnClientImpl: Submitted application application_1508282962007_0007
17/10/18 01:22:37 INFO mapreduce.Job: The url to track the job: http://ip-172-31-5-172.eu-central-1.compute.internal:8088/proxy/application_1508282962007_0007/
17/10/18 01:22:37 INFO mapreduce.Job: Running job: job_1508282962007_0007
17/10/18 01:22:43 INFO mapreduce.Job: Job job_1508282962007_0007 running in uber mode : false
17/10/18 01:22:43 INFO mapreduce.Job:  map 0% reduce 0%
[...]
17/10/18 01:23:47 INFO mapreduce.Job:  map 100% reduce 0%
17/10/18 01:23:48 INFO mapreduce.Job: Job job_1508282962007_0007 completed successfully
17/10/18 01:23:48 INFO mapreduce.Job: Counters: 31
	File System Counters
		FILE: Number of bytes read=0
		FILE: Number of bytes written=2446610
		FILE: Number of read operations=0
		FILE: Number of large read operations=0
		FILE: Number of write operations=0
		HDFS: Number of bytes read=1713
		HDFS: Number of bytes written=10000000000
		HDFS: Number of read operations=80
		HDFS: Number of large read operations=0
		HDFS: Number of write operations=40
	Job Counters 
		Launched map tasks=20
		Other local map tasks=20
		Total time spent by all maps in occupied slots (ms)=608803
		Total time spent by all reduces in occupied slots (ms)=0
		Total time spent by all map tasks (ms)=608803
		Total vcore-seconds taken by all map tasks=608803
		Total megabyte-seconds taken by all map tasks=623414272
	Map-Reduce Framework
		Map input records=100000000
		Map output records=100000000
		Input split bytes=1713
		Spilled Records=0
		Failed Shuffles=0
		Merged Map outputs=0
		GC time elapsed (ms)=3670
		CPU time spent (ms)=254350
		Physical memory (bytes) snapshot=7355805696
		Virtual memory (bytes) snapshot=31532584960
		Total committed heap usage (bytes)=7896301568
	org.apache.hadoop.examples.terasort.TeraGen$Counters
		CHECKSUM=214760662691937609
	File Input Format Counters 
		Bytes Read=0
	File Output Format Counters 
		Bytes Written=10000000000

real	1m14.645s
user	0m6.225s
sys	0m0.303s
```

## Run terasort

Command:
```
time hadoop jar /opt/cloudera/parcels/CDH/jars/hadoop-examples.jar terasort storagelabs/terasort/unsorted10GB storagelabs/terasort/orted10GB
```

Output:
```
17/10/18 01:25:11 INFO terasort.TeraSort: starting
17/10/18 01:25:12 INFO input.FileInputFormat: Total input paths to process : 20
Spent 256ms computing base-splits.
Spent 6ms computing TeraScheduler splits.
Computing input splits took 262ms
Sampling 10 splits of 300
Making 8 from 100000 sampled records
Computing parititions took 878ms
Spent 1143ms computing partitions.
17/10/18 01:25:13 INFO client.RMProxy: Connecting to ResourceManager at ip-172-31-5-172.eu-central-1.compute.internal/172.31.5.172:8032
17/10/18 01:25:14 INFO mapreduce.JobSubmitter: number of splits:300
17/10/18 01:25:14 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1508282962007_0008
17/10/18 01:25:14 INFO impl.YarnClientImpl: Submitted application application_1508282962007_0008
17/10/18 01:25:14 INFO mapreduce.Job: The url to track the job: http://ip-172-31-5-172.eu-central-1.compute.internal:8088/proxy/application_1508282962007_0008/
17/10/18 01:25:14 INFO mapreduce.Job: Running job: job_1508282962007_0008
17/10/18 01:25:19 INFO mapreduce.Job: Job job_1508282962007_0008 running in uber mode : false
17/10/18 01:25:19 INFO mapreduce.Job:  map 0% reduce 0%
[...]
17/10/18 01:30:44 INFO mapreduce.Job:  map 100% reduce 100%
17/10/18 01:30:44 INFO mapreduce.Job: Job job_1508282962007_0008 completed successfully
17/10/18 01:30:44 INFO mapreduce.Job: Counters: 50
	File System Counters
		FILE: Number of bytes read=4447371230
		FILE: Number of bytes written=8828460044
		FILE: Number of read operations=0
		FILE: Number of large read operations=0
		FILE: Number of write operations=0
		HDFS: Number of bytes read=10000056400
		HDFS: Number of bytes written=10000000000
		HDFS: Number of read operations=924
		HDFS: Number of large read operations=0
		HDFS: Number of write operations=16
	Job Counters 
		Launched map tasks=300
		Launched reduce tasks=8
		Data-local map tasks=299
		Rack-local map tasks=1
		Total time spent by all maps in occupied slots (ms)=2550521
		Total time spent by all reduces in occupied slots (ms)=846931
		Total time spent by all map tasks (ms)=2550521
		Total time spent by all reduce tasks (ms)=846931
		Total vcore-seconds taken by all map tasks=2550521
		Total vcore-seconds taken by all reduce tasks=846931
		Total megabyte-seconds taken by all map tasks=2611733504
		Total megabyte-seconds taken by all reduce tasks=867257344
	Map-Reduce Framework
		Map input records=100000000
		Map output records=100000000
		Map output bytes=10200000000
		Map output materialized bytes=4342931372
		Input split bytes=56400
		Combine input records=0
		Combine output records=0
		Reduce input groups=100000000
		Reduce shuffle bytes=4342931372
		Reduce input records=100000000
		Reduce output records=100000000
		Spilled Records=200000000
		Shuffled Maps =2400
		Failed Shuffles=0
		Merged Map outputs=2400
		GC time elapsed (ms)=33537
		CPU time spent (ms)=1464280
		Physical memory (bytes) snapshot=145117515776
		Virtual memory (bytes) snapshot=486747873280
		Total committed heap usage (bytes)=172803751936
	Shuffle Errors
		BAD_ID=0
		CONNECTION=0
		IO_ERROR=0
		WRONG_LENGTH=0
		WRONG_MAP=0
		WRONG_REDUCE=0
	File Input Format Counters 
		Bytes Read=10000000000
	File Output Format Counters 
		Bytes Written=10000000000
17/10/18 01:30:44 INFO terasort.TeraSort: done

real	5m34.822s
user	0m9.457s
sys	0m0.399s
```
