Become siwicki, kinit:
```
sudo su - siwicki
kinit
```

Run pi:
```
time hadoop jar /opt/cloudera/parcels/CDH/jars/hadoop-examples.jar pi 6 10000
```
Output:
```
Number of Maps  = 6
Samples per Map = 10000
Wrote input for Map #0
Wrote input for Map #1
Wrote input for Map #2
Wrote input for Map #3
Wrote input for Map #4
Wrote input for Map #5
Starting Job
17/10/20 10:01:18 INFO client.RMProxy: Connecting to ResourceManager at ip-172-31-13-131.eu-central-1.compute.internal/172.31.13.131:8032
17/10/20 10:01:18 INFO hdfs.DFSClient: Created token for siwicki: HDFS_DELEGATION_TOKEN owner=siwicki@NICOLOBIDOTTI.CO.UK, renewer=yarn, realUser=, issueDate=1508493678257, maxDate=1509098478257, sequenceNumber=5, masterKeyId=2 on 172.31.13.131:8020
17/10/20 10:01:18 INFO security.TokenCache: Got dt for hdfs://ip-172-31-13-131.eu-central-1.compute.internal:8020; Kind: HDFS_DELEGATION_TOKEN, Service: 172.31.13.131:8020, Ident: (token for siwicki: HDFS_DELEGATION_TOKEN owner=siwicki@NICOLOBIDOTTI.CO.UK, renewer=yarn, realUser=, issueDate=1508493678257, maxDate=1509098478257, sequenceNumber=5, masterKeyId=2)
17/10/20 10:01:18 INFO input.FileInputFormat: Total input paths to process : 6
17/10/20 10:01:18 INFO mapreduce.JobSubmitter: number of splits:6
17/10/20 10:01:18 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1508492543470_0005
17/10/20 10:01:18 INFO mapreduce.JobSubmitter: Kind: HDFS_DELEGATION_TOKEN, Service: 172.31.13.131:8020, Ident: (token for siwicki: HDFS_DELEGATION_TOKEN owner=siwicki@NICOLOBIDOTTI.CO.UK, renewer=yarn, realUser=, issueDate=1508493678257, maxDate=1509098478257, sequenceNumber=5, masterKeyId=2)
17/10/20 10:01:19 INFO impl.YarnClientImpl: Submitted application application_1508492543470_0005
17/10/20 10:01:19 INFO mapreduce.Job: The url to track the job: http://ip-172-31-13-131.eu-central-1.compute.internal:8088/proxy/application_1508492543470_0005/
17/10/20 10:01:19 INFO mapreduce.Job: Running job: job_1508492543470_0005
17/10/20 10:01:26 INFO mapreduce.Job: Job job_1508492543470_0005 running in uber mode : false
17/10/20 10:01:26 INFO mapreduce.Job:  map 0% reduce 0%
17/10/20 10:01:33 INFO mapreduce.Job:  map 17% reduce 0%
17/10/20 10:01:35 INFO mapreduce.Job:  map 33% reduce 0%
17/10/20 10:01:36 INFO mapreduce.Job:  map 50% reduce 0%
17/10/20 10:01:39 INFO mapreduce.Job:  map 100% reduce 0%
17/10/20 10:01:44 INFO mapreduce.Job:  map 100% reduce 100%
17/10/20 10:01:44 INFO mapreduce.Job: Job job_1508492543470_0005 completed successfully
17/10/20 10:01:44 INFO mapreduce.Job: Counters: 49
	File System Counters
		FILE: Number of bytes read=84
		FILE: Number of bytes written=876541
		FILE: Number of read operations=0
		FILE: Number of large read operations=0
		FILE: Number of write operations=0
		HDFS: Number of bytes read=1818
		HDFS: Number of bytes written=215
		HDFS: Number of read operations=27
		HDFS: Number of large read operations=0
		HDFS: Number of write operations=3
	Job Counters 
		Launched map tasks=6
		Launched reduce tasks=1
		Data-local map tasks=6
		Total time spent by all maps in occupied slots (ms)=50281
		Total time spent by all reduces in occupied slots (ms)=2900
		Total time spent by all map tasks (ms)=50281
		Total time spent by all reduce tasks (ms)=2900
		Total vcore-seconds taken by all map tasks=50281
		Total vcore-seconds taken by all reduce tasks=2900
		Total megabyte-seconds taken by all map tasks=51487744
		Total megabyte-seconds taken by all reduce tasks=2969600
	Map-Reduce Framework
		Map input records=6
		Map output records=12
		Map output bytes=108
		Map output materialized bytes=210
		Input split bytes=1110
		Combine input records=0
		Combine output records=0
		Reduce input groups=2
		Reduce shuffle bytes=210
		Reduce input records=12
		Reduce output records=0
		Spilled Records=24
		Shuffled Maps =6
		Failed Shuffles=0
		Merged Map outputs=6
		GC time elapsed (ms)=513
		CPU time spent (ms)=5870
		Physical memory (bytes) snapshot=2841493504
		Virtual memory (bytes) snapshot=19540238336
		Total committed heap usage (bytes)=2806513664
	Shuffle Errors
		BAD_ID=0
		CONNECTION=0
		IO_ERROR=0
		WRONG_LENGTH=0
		WRONG_MAP=0
		WRONG_REDUCE=0
	File Input Format Counters 
		Bytes Read=708
	File Output Format Counters 
		Bytes Written=97
Job Finished in 26.588 seconds
Estimated value of Pi is 3.14200000000000000000

real	0m29.545s
user	0m8.109s
sys	0m0.371s
```