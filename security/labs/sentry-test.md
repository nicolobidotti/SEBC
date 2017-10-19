## Verify user privileges

Transcript:
```
[nicolobidotti@ip-172-31-5-172 centos]$ kinit
Password for nicolobidotti@NICOLO.BIDOTTI: 
[nicolobidotti@ip-172-31-5-172 centos]$ beeline
Beeline version 1.1.0-cdh5.8.3 by Apache Hive
beeline> !connect jdbc:hive2://localhost:10000/default;principal=hive/ip-172-31-5-172.eu-central-1.compute.internal@REALM.COM
scan complete in 3ms
Connecting to jdbc:hive2://localhost:10000/default;principal=hive/ip-172-31-5-172.eu-central-1.compute.internal@REALM.COM
Enter username for jdbc:hive2://localhost:10000/default;principal=hive/ip-172-31-5-172.eu-central-1.compute.internal@REALM.COM: nicolobidotti
Enter password for jdbc:hive2://localhost:10000/default;principal=hive/ip-172-31-5-172.eu-central-1.compute.internal@REALM.COM: ********
Connected to: Apache Hive (version 1.1.0-cdh5.8.3)
Driver: Hive JDBC (version 1.1.0-cdh5.8.3)
Transaction isolation: TRANSACTION_REPEATABLE_READ
0: jdbc:hive2://localhost:10000/default> SHOW TABLES;
INFO  : Compiling command(queryId=hive_20171019194141_33a9c675-70c9-45a7-bda2-b2182d6ff5e2): SHOW TABLES
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:tab_name, type:string, comment:from deserializer)], properties:null)
INFO  : Completed compiling command(queryId=hive_20171019194141_33a9c675-70c9-45a7-bda2-b2182d6ff5e2); Time taken: 0.928 seconds
INFO  : Executing command(queryId=hive_20171019194141_33a9c675-70c9-45a7-bda2-b2182d6ff5e2): SHOW TABLES
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20171019194141_33a9c675-70c9-45a7-bda2-b2182d6ff5e2); Time taken: 0.277 seconds
INFO  : OK
+-----------+--+
| tab_name  |
+-----------+--+
+-----------+--+
No rows selected (2.557 seconds)
0: jdbc:hive2://localhost:10000/default> 
```

## Create a Sentry role with full authorization

Transcript:
```
0: jdbc:hive2://localhost:10000/default> CREATE ROLE sentry_admin;
INFO  : Compiling command(queryId=hive_20171019194343_f4ff1250-6e51-4767-9402-540c95f536c9): CREATE ROLE sentry_admin
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20171019194343_f4ff1250-6e51-4767-9402-540c95f536c9); Time taken: 0.072 seconds
INFO  : Executing command(queryId=hive_20171019194343_f4ff1250-6e51-4767-9402-540c95f536c9): CREATE ROLE sentry_admin
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20171019194343_f4ff1250-6e51-4767-9402-540c95f536c9); Time taken: 0.749 seconds
INFO  : OK
No rows affected (0.835 seconds)
0: jdbc:hive2://localhost:10000/default> GRANT ALL ON SERVER server1 TO ROLE sentry_admin;
INFO  : Compiling command(queryId=hive_20171019194343_baefca0f-71fe-4934-a874-baeb10ac543a): GRANT ALL ON SERVER server1 TO ROLE sentry_admin
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20171019194343_baefca0f-71fe-4934-a874-baeb10ac543a); Time taken: 0.092 seconds
INFO  : Executing command(queryId=hive_20171019194343_baefca0f-71fe-4934-a874-baeb10ac543a): GRANT ALL ON SERVER server1 TO ROLE sentry_admin
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20171019194343_baefca0f-71fe-4934-a874-baeb10ac543a); Time taken: 0.108 seconds
INFO  : OK
No rows affected (0.208 seconds)
0: jdbc:hive2://localhost:10000/default> GRANT ROLE sentry_admin TO GROUP nicolobidotti;
INFO  : Compiling command(queryId=hive_20171019194444_c078d8f4-5b58-4713-95ec-ecfbcc76b79b): GRANT ROLE sentry_admin TO GROUP nicolobidotti
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20171019194444_c078d8f4-5b58-4713-95ec-ecfbcc76b79b); Time taken: 0.079 seconds
INFO  : Executing command(queryId=hive_20171019194444_c078d8f4-5b58-4713-95ec-ecfbcc76b79b): GRANT ROLE sentry_admin TO GROUP nicolobidotti
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20171019194444_c078d8f4-5b58-4713-95ec-ecfbcc76b79b); Time taken: 0.077 seconds
INFO  : OK
No rows affected (0.165 seconds)
0: jdbc:hive2://localhost:10000/default> SHOW TABLES;
INFO  : Compiling command(queryId=hive_20171019194444_ffbb1458-d4ac-4de4-8e84-99a4f1113593): SHOW TABLES
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:tab_name, type:string, comment:from deserializer)], properties:null)
INFO  : Completed compiling command(queryId=hive_20171019194444_ffbb1458-d4ac-4de4-8e84-99a4f1113593); Time taken: 0.063 seconds
INFO  : Executing command(queryId=hive_20171019194444_ffbb1458-d4ac-4de4-8e84-99a4f1113593): SHOW TABLES
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20171019194444_ffbb1458-d4ac-4de4-8e84-99a4f1113593); Time taken: 0.155 seconds
INFO  : OK
+------------+--+
|  tab_name  |
+------------+--+
| customers  |
| sample_07  |
| sample_08  |
| web_logs   |
+------------+--+
4 rows selected (0.274 seconds)
0: jdbc:hive2://localhost:10000/default> 
```

## Create additional test users, create roles, grant privileges

## Test new users/roles

George:
```
[george@ip-172-31-5-172 centos]$ kinit
Password for george@NICOLO.BIDOTTI: 
[george@ip-172-31-5-172 centos]$ beeline
Beeline version 1.1.0-cdh5.8.3 by Apache Hive
beeline> !connect jdbc:hive2://localhost:10000/default;principal=hive/ip-172-31-5-172.eu-central-1.compute.internal@REALM.COM
scan complete in 3ms
Connecting to jdbc:hive2://localhost:10000/default;principal=hive/ip-172-31-5-172.eu-central-1.compute.internal@REALM.COM
Enter username for jdbc:hive2://localhost:10000/default;principal=hive/ip-172-31-5-172.eu-central-1.compute.internal@REALM.COM: george
Enter password for jdbc:hive2://localhost:10000/default;principal=hive/ip-172-31-5-172.eu-central-1.compute.internal@REALM.COM: ******
Connected to: Apache Hive (version 1.1.0-cdh5.8.3)
Driver: Hive JDBC (version 1.1.0-cdh5.8.3)
Transaction isolation: TRANSACTION_REPEATABLE_READ
0: jdbc:hive2://localhost:10000/default> SHOW TABLES;
INFO  : Compiling command(queryId=hive_20171019200707_9b9d7228-58c4-49fc-98fc-fcc4f09b0f54): SHOW TABLES
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:tab_name, type:string, comment:from deserializer)], properties:null)
INFO  : Completed compiling command(queryId=hive_20171019200707_9b9d7228-58c4-49fc-98fc-fcc4f09b0f54); Time taken: 0.083 seconds
INFO  : Executing command(queryId=hive_20171019200707_9b9d7228-58c4-49fc-98fc-fcc4f09b0f54): SHOW TABLES
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20171019200707_9b9d7228-58c4-49fc-98fc-fcc4f09b0f54); Time taken: 0.148 seconds
INFO  : OK
+------------+--+
|  tab_name  |
+------------+--+
| customers  |
| sample_07  |
| sample_08  |
| web_logs   |
+------------+--+
4 rows selected (0.357 seconds)
0: jdbc:hive2://localhost:10000/default> !quit
Closing: 0: jdbc:hive2://localhost:10000/default;principal=hive/ip-172-31-5-172.eu-central-1.compute.internal@REALM.COM
```

Ferdinand:
```
[ferdinand@ip-172-31-5-172 centos]$ kinit
Password for ferdinand@NICOLO.BIDOTTI: 
[ferdinand@ip-172-31-5-172 centos]$ beeline
Beeline version 1.1.0-cdh5.8.3 by Apache Hive
beeline> !connect jdbc:hive2://localhost:10000/default;principal=hive/ip-172-31-5-172.eu-central-1.compute.internal@REALM.COM
scan complete in 4ms
Connecting to jdbc:hive2://localhost:10000/default;principal=hive/ip-172-31-5-172.eu-central-1.compute.internal@REALM.COM
Enter username for jdbc:hive2://localhost:10000/default;principal=hive/ip-172-31-5-172.eu-central-1.compute.internal@REALM.COM: ferdinand
Enter password for jdbc:hive2://localhost:10000/default;principal=hive/ip-172-31-5-172.eu-central-1.compute.internal@REALM.COM: *********
Connected to: Apache Hive (version 1.1.0-cdh5.8.3)
Driver: Hive JDBC (version 1.1.0-cdh5.8.3)
Transaction isolation: TRANSACTION_REPEATABLE_READ
0: jdbc:hive2://localhost:10000/default> SHOW TABLES;
INFO  : Compiling command(queryId=hive_20171019200808_fc1204d2-3e50-4389-953a-4c866df0e0f9): SHOW TABLES
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:tab_name, type:string, comment:from deserializer)], properties:null)
INFO  : Completed compiling command(queryId=hive_20171019200808_fc1204d2-3e50-4389-953a-4c866df0e0f9); Time taken: 0.068 seconds
INFO  : Executing command(queryId=hive_20171019200808_fc1204d2-3e50-4389-953a-4c866df0e0f9): SHOW TABLES
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20171019200808_fc1204d2-3e50-4389-953a-4c866df0e0f9); Time taken: 0.133 seconds
INFO  : OK
+------------+--+
|  tab_name  |
+------------+--+
| sample_07  |
+------------+--+
1 row selected (0.324 seconds)
0: jdbc:hive2://localhost:10000/default> !quit
Closing: 0: jdbc:hive2://localhost:10000/default;principal=hive/ip-172-31-5-172.eu-central-1.compute.internal@REALM.COM
```