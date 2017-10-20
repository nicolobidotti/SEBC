Become ernest, kinit:
```
sudo su - ernest
kinit
```

Terasort as ernest:
```
time hadoop jar /opt/cloudera/parcels/CDH/jars/hadoop-examples.jar terasort tgen512m tsort512m
```
Output:
```
17/10/20 09:51:47 INFO terasort.TeraSort: starting
17/10/20 09:51:48 INFO hdfs.DFSClient: Created token for ernest: HDFS_DELEGATION_TOKEN owner=ernest@NICOLOBIDOTTI.CO.UK, renewer=yarn, realUser=, issueDate=1508493108875, maxDate=1509097908875, sequenceNumber=3, masterKeyId=2 on 172.31.13.131:8020
17/10/20 09:51:48 INFO security.TokenCache: Got dt for hdfs://ip-172-31-13-131.eu-central-1.compute.internal:8020; Kind: HDFS_DELEGATION_TOKEN, Service: 172.31.13.131:8020, Ident: (token for ernest: HDFS_DELEGATION_TOKEN owner=ernest@NICOLOBIDOTTI.CO.UK, renewer=yarn, realUser=, issueDate=1508493108875, maxDate=1509097908875, sequenceNumber=3, masterKeyId=2)
17/10/20 09:51:49 INFO input.FileInputFormat: Total input paths to process : 6
Spent 340ms computing base-splits.
Spent 5ms computing TeraScheduler splits.
Computing input splits took 346ms
Sampling 10 splits of 156
Making 8 from 100000 sampled records
Computing parititions took 731ms
Spent 1080ms computing partitions.
17/10/20 09:51:49 INFO client.RMProxy: Connecting to ResourceManager at ip-172-31-13-131.eu-central-1.compute.internal/172.31.13.131:8032
17/10/20 09:51:50 INFO mapreduce.JobSubmitter: number of splits:156
17/10/20 09:51:50 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1508492543470_0003
17/10/20 09:51:50 INFO mapreduce.JobSubmitter: Kind: HDFS_DELEGATION_TOKEN, Service: 172.31.13.131:8020, Ident: (token for ernest: HDFS_DELEGATION_TOKEN owner=ernest@NICOLOBIDOTTI.CO.UK, renewer=yarn, realUser=, issueDate=1508493108875, maxDate=1509097908875, sequenceNumber=3, masterKeyId=2)
17/10/20 09:51:50 INFO impl.YarnClientImpl: Submitted application application_1508492543470_0003
17/10/20 09:51:50 INFO mapreduce.Job: The url to track the job: http://ip-172-31-13-131.eu-central-1.compute.internal:8088/proxy/application_1508492543470_0003/
17/10/20 09:51:50 INFO mapreduce.Job: Running job: job_1508492543470_0003
17/10/20 09:51:51 INFO mapreduce.Job: Job job_1508492543470_0003 running in uber mode : false
17/10/20 09:51:51 INFO mapreduce.Job:  map 0% reduce 0%
17/10/20 09:51:51 INFO mapreduce.Job: Job job_1508492543470_0003 failed with state FAILED due to: Application application_1508492543470_0003 failed 2 times due to AM Container for appattempt_1508492543470_0003_000002 exited with  exitCode: -1000
For more detailed output, check application tracking page:http://ip-172-31-13-131.eu-central-1.compute.internal:8088/proxy/application_1508492543470_0003/Then, click on links to logs of each attempt.
Diagnostics: Application application_1508492543470_0003 initialization failed (exitCode=255) with output: main : command provided 0
main : run as user is ernest
main : requested yarn user is ernest
Can't create directory /mnt/ssd0/nm/usercache/ernest/appcache/application_1508492543470_0003 - Permission denied
Can't create directory /mnt/ssd1/nm/usercache/ernest/appcache/application_1508492543470_0003 - Permission denied
Did not create any app directories

Failing this attempt. Failing the application.
17/10/20 09:51:51 INFO mapreduce.Job: Counters: 0
17/10/20 09:51:51 INFO terasort.TeraSort: done

real	0m5.293s
user	0m8.472s
sys	0m0.317s
```

**IT FAILS.**

Reason: cache directories created under simple AUTH are owned by yarn:yarn; this will not work after enabling Kerberos because then the actual user must own them!! User siwicki does not suffer the problem because it never had them created as it did not run any job. See https://community.cloudera.com/t5/Batch-Processing-and-Workflow/Can-t-create-directory-yarn-nm-usercache-urika-appcache/td-p/24891
Solution: remove cache directories from all nodes, they will be recreated with the correct permissions.
```
sudo rm -rf /mnt/ssd0/nm/usercache/ernest/
sudo rm -rf /mnt/ssd1/nm/usercache/ernest/
```

Run again, output:
```
17/10/20 09:56:02 INFO terasort.TeraSort: starting
17/10/20 09:56:03 INFO hdfs.DFSClient: Created token for ernest: HDFS_DELEGATION_TOKEN owner=ernest@NICOLOBIDOTTI.CO.UK, renewer=yarn, realUser=, issueDate=1508493363473, maxDate=1509098163473, sequenceNumber=4, masterKeyId=2 on 172.31.13.131:8020
17/10/20 09:56:03 INFO security.TokenCache: Got dt for hdfs://ip-172-31-13-131.eu-central-1.compute.internal:8020; Kind: HDFS_DELEGATION_TOKEN, Service: 172.31.13.131:8020, Ident: (token for ernest: HDFS_DELEGATION_TOKEN owner=ernest@NICOLOBIDOTTI.CO.UK, renewer=yarn, realUser=, issueDate=1508493363473, maxDate=1509098163473, sequenceNumber=4, masterKeyId=2)
17/10/20 09:56:03 INFO input.FileInputFormat: Total input paths to process : 6
Spent 320ms computing base-splits.
Spent 5ms computing TeraScheduler splits.
Computing input splits took 326ms
Sampling 10 splits of 156
Making 8 from 100000 sampled records
Computing parititions took 760ms
Spent 1088ms computing partitions.
17/10/20 09:56:04 INFO client.RMProxy: Connecting to ResourceManager at ip-172-31-13-131.eu-central-1.compute.internal/172.31.13.131:8032
17/10/20 09:56:04 INFO mapreduce.JobSubmitter: number of splits:156
17/10/20 09:56:05 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1508492543470_0004
17/10/20 09:56:05 INFO mapreduce.JobSubmitter: Kind: HDFS_DELEGATION_TOKEN, Service: 172.31.13.131:8020, Ident: (token for ernest: HDFS_DELEGATION_TOKEN owner=ernest@NICOLOBIDOTTI.CO.UK, renewer=yarn, realUser=, issueDate=1508493363473, maxDate=1509098163473, sequenceNumber=4, masterKeyId=2)
17/10/20 09:56:05 INFO impl.YarnClientImpl: Submitted application application_1508492543470_0004
17/10/20 09:56:05 INFO mapreduce.Job: The url to track the job: http://ip-172-31-13-131.eu-central-1.compute.internal:8088/proxy/application_1508492543470_0004/
17/10/20 09:56:05 INFO mapreduce.Job: Running job: job_1508492543470_0004
17/10/20 09:56:13 INFO mapreduce.Job: Job job_1508492543470_0004 running in uber mode : false
17/10/20 09:56:13 INFO mapreduce.Job:  map 0% reduce 0%
17/10/20 09:56:21 INFO mapreduce.Job:  map 1% reduce 0%
17/10/20 09:56:27 INFO mapreduce.Job:  map 4% reduce 0%
17/10/20 09:56:28 INFO mapreduce.Job:  map 6% reduce 0%
17/10/20 09:56:31 INFO mapreduce.Job:  map 7% reduce 0%
17/10/20 09:56:32 INFO mapreduce.Job:  map 9% reduce 0%
17/10/20 09:56:35 INFO mapreduce.Job:  map 12% reduce 0%
17/10/20 09:56:37 INFO mapreduce.Job:  map 14% reduce 0%
17/10/20 09:56:43 INFO mapreduce.Job:  map 15% reduce 0%
17/10/20 09:56:44 INFO mapreduce.Job:  map 17% reduce 0%
17/10/20 09:56:45 INFO mapreduce.Job:  map 19% reduce 0%
17/10/20 09:56:46 INFO mapreduce.Job:  map 21% reduce 0%
17/10/20 09:56:47 INFO mapreduce.Job:  map 22% reduce 0%
17/10/20 09:56:50 INFO mapreduce.Job:  map 23% reduce 0%
17/10/20 09:56:53 INFO mapreduce.Job:  map 24% reduce 0%
17/10/20 09:56:54 INFO mapreduce.Job:  map 25% reduce 0%
17/10/20 09:56:55 INFO mapreduce.Job:  map 26% reduce 0%
17/10/20 09:56:56 INFO mapreduce.Job:  map 29% reduce 0%
17/10/20 09:56:57 INFO mapreduce.Job:  map 31% reduce 0%
17/10/20 09:57:02 INFO mapreduce.Job:  map 32% reduce 0%
17/10/20 09:57:03 INFO mapreduce.Job:  map 33% reduce 0%
17/10/20 09:57:04 INFO mapreduce.Job:  map 35% reduce 0%
17/10/20 09:57:05 INFO mapreduce.Job:  map 37% reduce 0%
17/10/20 09:57:08 INFO mapreduce.Job:  map 39% reduce 0%
17/10/20 09:57:11 INFO mapreduce.Job:  map 42% reduce 0%
17/10/20 09:57:13 INFO mapreduce.Job:  map 43% reduce 0%
17/10/20 09:57:14 INFO mapreduce.Job:  map 44% reduce 0%
17/10/20 09:57:16 INFO mapreduce.Job:  map 45% reduce 0%
17/10/20 09:57:18 INFO mapreduce.Job:  map 48% reduce 0%
17/10/20 09:57:19 INFO mapreduce.Job:  map 49% reduce 0%
17/10/20 09:57:20 INFO mapreduce.Job:  map 50% reduce 0%
17/10/20 09:57:21 INFO mapreduce.Job:  map 51% reduce 0%
17/10/20 09:57:23 INFO mapreduce.Job:  map 52% reduce 0%
17/10/20 09:57:24 INFO mapreduce.Job:  map 53% reduce 0%
17/10/20 09:57:26 INFO mapreduce.Job:  map 54% reduce 0%
17/10/20 09:57:28 INFO mapreduce.Job:  map 56% reduce 0%
17/10/20 09:57:29 INFO mapreduce.Job:  map 57% reduce 0%
17/10/20 09:57:30 INFO mapreduce.Job:  map 60% reduce 0%
17/10/20 09:57:32 INFO mapreduce.Job:  map 61% reduce 0%
17/10/20 09:57:35 INFO mapreduce.Job:  map 62% reduce 0%
17/10/20 09:57:37 INFO mapreduce.Job:  map 65% reduce 0%
17/10/20 09:57:40 INFO mapreduce.Job:  map 68% reduce 0%
17/10/20 09:57:41 INFO mapreduce.Job:  map 69% reduce 0%
17/10/20 09:57:44 INFO mapreduce.Job:  map 71% reduce 0%
17/10/20 09:57:46 INFO mapreduce.Job:  map 72% reduce 0%
17/10/20 09:57:47 INFO mapreduce.Job:  map 73% reduce 0%
17/10/20 09:57:48 INFO mapreduce.Job:  map 74% reduce 0%
17/10/20 09:57:51 INFO mapreduce.Job:  map 77% reduce 0%
17/10/20 09:57:52 INFO mapreduce.Job:  map 78% reduce 0%
17/10/20 09:57:54 INFO mapreduce.Job:  map 80% reduce 0%
17/10/20 09:57:56 INFO mapreduce.Job:  map 81% reduce 0%
17/10/20 09:57:58 INFO mapreduce.Job:  map 83% reduce 0%
17/10/20 09:58:00 INFO mapreduce.Job:  map 84% reduce 0%
17/10/20 09:58:02 INFO mapreduce.Job:  map 85% reduce 0%
17/10/20 09:58:03 INFO mapreduce.Job:  map 87% reduce 0%
17/10/20 09:58:04 INFO mapreduce.Job:  map 88% reduce 0%
17/10/20 09:58:05 INFO mapreduce.Job:  map 89% reduce 0%
17/10/20 09:58:06 INFO mapreduce.Job:  map 90% reduce 0%
17/10/20 09:58:09 INFO mapreduce.Job:  map 90% reduce 4%
17/10/20 09:58:11 INFO mapreduce.Job:  map 91% reduce 4%
17/10/20 09:58:12 INFO mapreduce.Job:  map 91% reduce 7%
17/10/20 09:58:13 INFO mapreduce.Job:  map 91% reduce 10%
17/10/20 09:58:14 INFO mapreduce.Job:  map 92% reduce 14%
17/10/20 09:58:15 INFO mapreduce.Job:  map 92% reduce 21%
17/10/20 09:58:16 INFO mapreduce.Job:  map 93% reduce 25%
17/10/20 09:58:17 INFO mapreduce.Job:  map 93% reduce 26%
17/10/20 09:58:18 INFO mapreduce.Job:  map 94% reduce 26%
17/10/20 09:58:19 INFO mapreduce.Job:  map 96% reduce 27%
17/10/20 09:58:21 INFO mapreduce.Job:  map 96% reduce 28%
17/10/20 09:58:24 INFO mapreduce.Job:  map 97% reduce 28%
17/10/20 09:58:26 INFO mapreduce.Job:  map 99% reduce 28%
17/10/20 09:58:27 INFO mapreduce.Job:  map 99% reduce 29%
17/10/20 09:58:28 INFO mapreduce.Job:  map 100% reduce 29%
17/10/20 09:58:29 INFO mapreduce.Job:  map 100% reduce 30%
17/10/20 09:58:30 INFO mapreduce.Job:  map 100% reduce 37%
17/10/20 09:58:31 INFO mapreduce.Job:  map 100% reduce 48%
17/10/20 09:58:32 INFO mapreduce.Job:  map 100% reduce 51%
17/10/20 09:58:33 INFO mapreduce.Job:  map 100% reduce 61%
17/10/20 09:58:34 INFO mapreduce.Job:  map 100% reduce 67%
17/10/20 09:58:35 INFO mapreduce.Job:  map 100% reduce 68%
17/10/20 09:58:36 INFO mapreduce.Job:  map 100% reduce 73%
17/10/20 09:58:37 INFO mapreduce.Job:  map 100% reduce 77%
17/10/20 09:58:38 INFO mapreduce.Job:  map 100% reduce 80%
17/10/20 09:58:39 INFO mapreduce.Job:  map 100% reduce 82%
17/10/20 09:58:40 INFO mapreduce.Job:  map 100% reduce 86%
17/10/20 09:58:41 INFO mapreduce.Job:  map 100% reduce 89%
17/10/20 09:58:42 INFO mapreduce.Job:  map 100% reduce 92%
17/10/20 09:58:43 INFO mapreduce.Job:  map 100% reduce 94%
17/10/20 09:58:46 INFO mapreduce.Job:  map 100% reduce 97%
17/10/20 09:58:48 INFO mapreduce.Job:  map 100% reduce 99%
17/10/20 09:58:49 INFO mapreduce.Job:  map 100% reduce 100%
17/10/20 09:58:50 INFO mapreduce.Job: Job job_1508492543470_0004 completed successfully
17/10/20 09:58:50 INFO mapreduce.Job: Counters: 49
	File System Counters
		FILE: Number of bytes read=2269390303
		FILE: Number of bytes written=4513565638
		FILE: Number of read operations=0
		FILE: Number of large read operations=0
		FILE: Number of write operations=0
		HDFS: Number of bytes read=5120024492
		HDFS: Number of bytes written=5120000000
		HDFS: Number of read operations=492
		HDFS: Number of large read operations=0
		HDFS: Number of write operations=16
	Job Counters 
		Launched map tasks=156
		Launched reduce tasks=8
		Data-local map tasks=156
		Total time spent by all maps in occupied slots (ms)=1237516
		Total time spent by all reduces in occupied slots (ms)=306126
		Total time spent by all map tasks (ms)=1237516
		Total time spent by all reduce tasks (ms)=306126
		Total vcore-seconds taken by all map tasks=1237516
		Total vcore-seconds taken by all reduce tasks=306126
		Total megabyte-seconds taken by all map tasks=1267216384
		Total megabyte-seconds taken by all reduce tasks=313473024
	Map-Reduce Framework
		Map input records=51200000
		Map output records=51200000
		Map output bytes=5222400000
		Map output materialized bytes=2223514105
		Input split bytes=24492
		Combine input records=0
		Combine output records=0
		Reduce input groups=51200000
		Reduce shuffle bytes=2223514105
		Reduce input records=51200000
		Reduce output records=51200000
		Spilled Records=102400000
		Shuffled Maps =1248
		Failed Shuffles=0
		Merged Map outputs=1248
		GC time elapsed (ms)=23714
		CPU time spent (ms)=804660
		Physical memory (bytes) snapshot=77527003136
		Virtual memory (bytes) snapshot=457970769920
		Total committed heap usage (bytes)=77873545216
	Shuffle Errors
		BAD_ID=0
		CONNECTION=0
		IO_ERROR=0
		WRONG_LENGTH=0
		WRONG_MAP=0
		WRONG_REDUCE=0
	File Input Format Counters 
		Bytes Read=5120000000
	File Output Format Counters 
		Bytes Written=5120000000
17/10/20 09:58:50 INFO terasort.TeraSort: done

real	2m49.840s
user	0m10.318s
sys	0m0.458s
```