## Prepare

Prepare user & home directory:
```
export HADOOP_USER_NAME=hdfs
hdfs dfs -mkdir -p /user/nicolobidotti
hdfs dfs -chown nicolobidotti /user/nicolobidotti
hdfs dfs -chgrp nicolobidotti /user/nicolobidotti
export HADOOP_USER_NAME=nicolobidotti
```

Confirm the new user/home dir works: `hdfs dfs -ls`

Create source & target dirs:
```
hdfs dfs -mkdir -p storagelabs/distcp/nicolobidotti/
hdfs dfs -mkdir -p storagelabs/distcp/nicolobidotti2/
```

## Create 500MB file with teragen

Calculation for # of rows: assuming in MB the "mega" is 10^6 and given a row size of 100 bytes, we need to generate 5'000'000 rows.

Command:
```
hadoop jar /opt/cloudera/parcels/CDH/jars/hadoop-examples.jar teragen -Dmapreduce.job.maps=4 5000000 storagelabs/distcp/nicolobidotti/unsorted500MB
```

Output:
```
17/10/18 00:36:01 INFO client.RMProxy: Connecting to ResourceManager at ip-172-31-5-172.eu-central-1.compute.internal/172.31.5.172:8032
17/10/18 00:36:02 INFO terasort.TeraSort: Generating 5000000 using 4
17/10/18 00:36:02 INFO mapreduce.JobSubmitter: number of splits:4
17/10/18 00:36:02 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1508282962007_0003
17/10/18 00:36:02 INFO impl.YarnClientImpl: Submitted application application_1508282962007_0003
17/10/18 00:36:02 INFO mapreduce.Job: The url to track the job: http://ip-172-31-5-172.eu-central-1.compute.internal:8088/proxy/application_1508282962007_0003/
17/10/18 00:36:02 INFO mapreduce.Job: Running job: job_1508282962007_0003
17/10/18 00:36:07 INFO mapreduce.Job: Job job_1508282962007_0003 running in uber mode : false
17/10/18 00:36:07 INFO mapreduce.Job:  map 0% reduce 0%
17/10/18 00:36:16 INFO mapreduce.Job:  map 100% reduce 0%
17/10/18 00:36:16 INFO mapreduce.Job: Job job_1508282962007_0003 completed successfully
17/10/18 00:36:16 INFO mapreduce.Job: Counters: 31
	File System Counters
		FILE: Number of bytes read=0
		FILE: Number of bytes written=489348
		FILE: Number of read operations=0
		FILE: Number of large read operations=0
		FILE: Number of write operations=0
		HDFS: Number of bytes read=337
		HDFS: Number of bytes written=500000000
		HDFS: Number of read operations=16
		HDFS: Number of large read operations=0
		HDFS: Number of write operations=8
	Job Counters 
		Launched map tasks=4
		Other local map tasks=4
		Total time spent by all maps in occupied slots (ms)=21984
		Total time spent by all reduces in occupied slots (ms)=0
		Total time spent by all map tasks (ms)=21984
		Total vcore-seconds taken by all map tasks=21984
		Total megabyte-seconds taken by all map tasks=22511616
	Map-Reduce Framework
		Map input records=5000000
		Map output records=5000000
		Input split bytes=337
		Spilled Records=0
		Failed Shuffles=0
		Merged Map outputs=0
		GC time elapsed (ms)=310
		CPU time spent (ms)=18840
		Physical memory (bytes) snapshot=1391833088
		Virtual memory (bytes) snapshot=6291001344
		Total committed heap usage (bytes)=1641021440
	org.apache.hadoop.examples.terasort.TeraGen$Counters
		CHECKSUM=10735710707299981
	File Input Format Counters 
		Bytes Read=0
	File Output Format Counters 
		Bytes Written=500000000
```

Check resulting directory size (note this uses MiB, not MB):
```
hdfs dfs -du -s -h storagelabs/distcp/nicolobidotti/unsorted500MB
```

Output:
```
476.8 M  1.4 G  storagelabs/distcp/nicolobidotti/unsorted500MB
```

## Copy using distcp

**NOTE:** we copy from/to the same cluster because communication between VPCs in AWS is a nightmare. Having a restrictive security group (no outside access except SSH) and using internal hostnames for hosts makes it pretty much impossible to get distcp working.

Command:
```
hadoop distcp -p hdfs://ip-172-31-5-172.eu-central-1.compute.internal:8020/user/nicolobidotti/storagelabs/distcp/nicolobidotti/unsorted500MB hdfs://ip-172-31-5-172.eu-central-1.compute.internal:8020/user/nicolobidotti/storagelabs/distcp/nicolobidotti2/
```

Output:
```
17/10/18 00:41:26 INFO tools.DistCp: Input Options: DistCpOptions{atomicCommit=false, syncFolder=false, deleteMissing=false, ignoreFailures=false, overwrite=false, skipCRC=false, blocking=true, numListstatusThreads=0, maxMaps=20, mapBandwidth=100, sslConfigurationFile='null', copyStrategy='uniformsize', preserveStatus=[REPLICATION, BLOCKSIZE, USER, GROUP, PERMISSION, CHECKSUMTYPE, TIMES], preserveRawXattrs=false, atomicWorkPath=null, logPath=null, sourceFileListing=null, sourcePaths=[hdfs://ip-172-31-5-172.eu-central-1.compute.internal:8020/user/nicolobidotti/storagelabs/distcp/nicolobidotti/unsorted500MB], targetPath=hdfs://ip-172-31-5-172.eu-central-1.compute.internal:8020/user/nicolobidotti/storagelabs/distcp/nicolobidotti2, targetPathExists=true, filtersFile='null'}
17/10/18 00:41:26 INFO client.RMProxy: Connecting to ResourceManager at ip-172-31-5-172.eu-central-1.compute.internal/172.31.5.172:8032
17/10/18 00:41:27 INFO tools.SimpleCopyListing: Paths (files+dirs) cnt = 6; dirCnt = 1
17/10/18 00:41:27 INFO tools.SimpleCopyListing: Build file listing completed.
17/10/18 00:41:27 INFO Configuration.deprecation: io.sort.mb is deprecated. Instead, use mapreduce.task.io.sort.mb
17/10/18 00:41:27 INFO Configuration.deprecation: io.sort.factor is deprecated. Instead, use mapreduce.task.io.sort.factor
17/10/18 00:41:27 INFO tools.DistCp: Number of paths in the copy list: 6
17/10/18 00:41:27 INFO tools.DistCp: Number of paths in the copy list: 6
17/10/18 00:41:27 INFO client.RMProxy: Connecting to ResourceManager at ip-172-31-5-172.eu-central-1.compute.internal/172.31.5.172:8032
17/10/18 00:41:27 INFO mapreduce.JobSubmitter: number of splits:5
17/10/18 00:41:27 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1508282962007_0004
17/10/18 00:41:28 INFO impl.YarnClientImpl: Submitted application application_1508282962007_0004
17/10/18 00:41:28 INFO mapreduce.Job: The url to track the job: http://ip-172-31-5-172.eu-central-1.compute.internal:8088/proxy/application_1508282962007_0004/
17/10/18 00:41:28 INFO tools.DistCp: DistCp job-id: job_1508282962007_0004
17/10/18 00:41:28 INFO mapreduce.Job: Running job: job_1508282962007_0004
17/10/18 00:41:33 INFO mapreduce.Job: Job job_1508282962007_0004 running in uber mode : false
17/10/18 00:41:33 INFO mapreduce.Job:  map 0% reduce 0%
17/10/18 00:41:41 INFO mapreduce.Job:  map 60% reduce 0%
17/10/18 00:41:42 INFO mapreduce.Job:  map 80% reduce 0%
17/10/18 00:41:43 INFO mapreduce.Job:  map 100% reduce 0%
17/10/18 00:41:43 INFO mapreduce.Job: Job job_1508282962007_0004 completed successfully
17/10/18 00:41:43 INFO mapreduce.Job: Counters: 33
	File System Counters
		FILE: Number of bytes read=0
		FILE: Number of bytes written=627175
		FILE: Number of read operations=0
		FILE: Number of large read operations=0
		FILE: Number of write operations=0
		HDFS: Number of bytes read=500003794
		HDFS: Number of bytes written=500000000
		HDFS: Number of read operations=96
		HDFS: Number of large read operations=0
		HDFS: Number of write operations=26
	Job Counters 
		Launched map tasks=5
		Other local map tasks=5
		Total time spent by all maps in occupied slots (ms)=29729
		Total time spent by all reduces in occupied slots (ms)=0
		Total time spent by all map tasks (ms)=29729
		Total vcore-seconds taken by all map tasks=29729
		Total megabyte-seconds taken by all map tasks=30442496
	Map-Reduce Framework
		Map input records=6
		Map output records=0
		Input split bytes=625
		Spilled Records=0
		Failed Shuffles=0
		Merged Map outputs=0
		GC time elapsed (ms)=289
		CPU time spent (ms)=17490
		Physical memory (bytes) snapshot=1141338112
		Virtual memory (bytes) snapshot=7908397056
		Total committed heap usage (bytes)=1389363200
	File Input Format Counters 
		Bytes Read=3169
	File Output Format Counters 
		Bytes Written=0
	org.apache.hadoop.tools.mapred.CopyMapper$Counter
		BYTESCOPIED=500000000
		BYTESEXPECTED=500000000
		COPY=6
```

Browse results:
```
hdfs fsck /user/nicolobidotti/storagelabs/distcp/nicolobidotti/unsorted500MB -files -blocks
hdfs fsck /user/nicolobidotti/storagelabs/distcp/nicolobidotti2/unsorted500MB -files -blocks
```

Output 1:
```
Connecting to namenode via http://ip-172-31-5-172.eu-central-1.compute.internal:50070
FSCK started by nicolobidotti (auth:SIMPLE) from /172.31.5.172 for path /user/nicolobidotti/storagelabs/distcp/nicolobidotti/unsorted500MB at Wed Oct 18 00:46:06 UTC 2017
/user/nicolobidotti/storagelabs/distcp/nicolobidotti/unsorted500MB <dir>
/user/nicolobidotti/storagelabs/distcp/nicolobidotti/unsorted500MB/_SUCCESS 0 bytes, 0 block(s):  OK

/user/nicolobidotti/storagelabs/distcp/nicolobidotti/unsorted500MB/part-m-00000 125000000 bytes, 1 block(s):  OK
0. BP-227085658-172.31.5.172-1508247742232:blk_1073743183_2359 len=125000000 Live_repl=3

/user/nicolobidotti/storagelabs/distcp/nicolobidotti/unsorted500MB/part-m-00001 125000000 bytes, 1 block(s):  OK
0. BP-227085658-172.31.5.172-1508247742232:blk_1073743185_2361 len=125000000 Live_repl=3

/user/nicolobidotti/storagelabs/distcp/nicolobidotti/unsorted500MB/part-m-00002 125000000 bytes, 1 block(s):  OK
0. BP-227085658-172.31.5.172-1508247742232:blk_1073743184_2360 len=125000000 Live_repl=3

/user/nicolobidotti/storagelabs/distcp/nicolobidotti/unsorted500MB/part-m-00003 125000000 bytes, 1 block(s):  OK
0. BP-227085658-172.31.5.172-1508247742232:blk_1073743186_2362 len=125000000 Live_repl=3

Status: HEALTHY
 Total size:	500000000 B
 Total dirs:	1
 Total files:	5
 Total symlinks:		0
 Total blocks (validated):	4 (avg. block size 125000000 B)
 Minimally replicated blocks:	4 (100.0 %)
 Over-replicated blocks:	0 (0.0 %)
 Under-replicated blocks:	0 (0.0 %)
 Mis-replicated blocks:		0 (0.0 %)
 Default replication factor:	3
 Average block replication:	3.0
 Corrupt blocks:		0
 Missing replicas:		0 (0.0 %)
 Number of data-nodes:		4
 Number of racks:		1
FSCK ended at Wed Oct 18 00:46:06 UTC 2017 in 4 milliseconds


The filesystem under path '/user/nicolobidotti/storagelabs/distcp/nicolobidotti/unsorted500MB' is HEALTHY
```

Output 2:
```
Connecting to namenode via http://ip-172-31-5-172.eu-central-1.compute.internal:50070
FSCK started by nicolobidotti (auth:SIMPLE) from /172.31.5.172 for path /user/nicolobidotti/storagelabs/distcp/nicolobidotti2/unsorted500MB at Wed Oct 18 00:46:24 UTC 2017
/user/nicolobidotti/storagelabs/distcp/nicolobidotti2/unsorted500MB <dir>
/user/nicolobidotti/storagelabs/distcp/nicolobidotti2/unsorted500MB/_SUCCESS 0 bytes, 0 block(s):  OK

/user/nicolobidotti/storagelabs/distcp/nicolobidotti2/unsorted500MB/part-m-00000 125000000 bytes, 1 block(s):  OK
0. BP-227085658-172.31.5.172-1508247742232:blk_1073743210_2386 len=125000000 Live_repl=3

/user/nicolobidotti/storagelabs/distcp/nicolobidotti2/unsorted500MB/part-m-00001 125000000 bytes, 1 block(s):  OK
0. BP-227085658-172.31.5.172-1508247742232:blk_1073743209_2385 len=125000000 Live_repl=3

/user/nicolobidotti/storagelabs/distcp/nicolobidotti2/unsorted500MB/part-m-00002 125000000 bytes, 1 block(s):  OK
0. BP-227085658-172.31.5.172-1508247742232:blk_1073743211_2387 len=125000000 Live_repl=3

/user/nicolobidotti/storagelabs/distcp/nicolobidotti2/unsorted500MB/part-m-00003 125000000 bytes, 1 block(s):  OK
0. BP-227085658-172.31.5.172-1508247742232:blk_1073743212_2388 len=125000000 Live_repl=3

Status: HEALTHY
 Total size:	500000000 B
 Total dirs:	1
 Total files:	5
 Total symlinks:		0
 Total blocks (validated):	4 (avg. block size 125000000 B)
 Minimally replicated blocks:	4 (100.0 %)
 Over-replicated blocks:	0 (0.0 %)
 Under-replicated blocks:	0 (0.0 %)
 Mis-replicated blocks:		0 (0.0 %)
 Default replication factor:	3
 Average block replication:	3.0
 Corrupt blocks:		0
 Missing replicas:		0 (0.0 %)
 Number of data-nodes:		4
 Number of racks:		1
FSCK ended at Wed Oct 18 00:46:24 UTC 2017 in 3 milliseconds


The filesystem under path '/user/nicolobidotti/storagelabs/distcp/nicolobidotti2/unsorted500MB' is HEALTHY
```

