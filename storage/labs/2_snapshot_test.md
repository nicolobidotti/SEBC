HDFS Lab: Test HDFS Snapshots

## Create directory & upload file

Commands:
```
hdfs dfs -mkdir precious
hdfs dfs -copyFromLocal SEBC-master.zip precious/
```

## Snapshotting

Enable snapshots:
```
HADOOP_USER_NAME=hdfs hdfs dfsadmin -allowSnapshot /user/nicolobidotti/precious
```

Output:
```
Allowing snaphot on /user/nicolobidotti/precious succeeded
```

Create a snapshot "sebc-hdfs-test":
```
hdfs dfs -createSnapshot /user/nicolobidotti/precious sebc-hdfs-test
```

Output:
```
Created snapshot /user/nicolobidotti/precious/.snapshot/sebc-hdfs-test
```

## Delete & recovery

Delete the directory: `hdfs dfs -rm -r precious`

Output:
```
rm: Failed to move to trash: hdfs://ip-172-31-5-172.eu-central-1.compute.internal:8020/user/nicolobidotti/precious: The directory /user/nicolobidotti/precious cannot be deleted since /user/nicolobidotti/precious is snapshottable and already has snapshots
```

(This is the expected behaviour as snapshots, or rather pointers to them, are "stored" inside .snapshots)

Delete the ZIP file: `hdfs dfs -rm precious/SEBC-master.zip`

Restore the deleted file: `hdfs dfs -cp precious/.snapshot/sebc-hdfs-test/SEBC-master.zip precious`
