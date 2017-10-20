Create roles, grant permissions:
```
1: jdbc:hive2://localhost:10000/default> !connect jdbc:hive2://localhost:10000/default;principal=hive/ip-172-31-13-131.eu-central-1.compute.internal@NICOLOBIDOTTI.CO.UK
Connecting to jdbc:hive2://localhost:10000/default;principal=hive/ip-172-31-13-131.eu-central-1.compute.internal@NICOLOBIDOTTI.CO.UK
Connected to: Apache Hive (version 1.1.0-cdh5.9.3)
Driver: Hive JDBC (version 1.1.0-cdh5.9.3)
Transaction isolation: TRANSACTION_REPEATABLE_READ
2: jdbc:hive2://localhost:10000/default> CREATE ROLE fce1;
INFO  : Compiling command(queryId=hive_20171020101515_fcf4751d-db7b-41cc-b20c-4c7938d0e35d): CREATE ROLE fce1
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20171020101515_fcf4751d-db7b-41cc-b20c-4c7938d0e35d); Time taken: 0.615 seconds
INFO  : Executing command(queryId=hive_20171020101515_fcf4751d-db7b-41cc-b20c-4c7938d0e35d): CREATE ROLE fce1
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20171020101515_fcf4751d-db7b-41cc-b20c-4c7938d0e35d); Time taken: 0.76 seconds
INFO  : OK
No rows affected (1.744 seconds)
2: jdbc:hive2://localhost:10000/default> GRANT ALL ON DATABASE default TO ROLE fce1;
INFO  : Compiling command(queryId=hive_20171020101616_aa8b3ef7-d805-4af5-906f-1db6eb5d8166): GRANT ALL ON DATABASE default TO ROLE fce1
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20171020101616_aa8b3ef7-d805-4af5-906f-1db6eb5d8166); Time taken: 0.241 seconds
INFO  : Executing command(queryId=hive_20171020101616_aa8b3ef7-d805-4af5-906f-1db6eb5d8166): GRANT ALL ON DATABASE default TO ROLE fce1
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20171020101616_aa8b3ef7-d805-4af5-906f-1db6eb5d8166); Time taken: 0.164 seconds
INFO  : OK
No rows affected (0.436 seconds)
2: jdbc:hive2://localhost:10000/default> GRANT ROLE fce1 TO GROUP usa;
INFO  : Compiling command(queryId=hive_20171020101616_6273c98a-0887-4939-b5ce-524f8dc8bcce): GRANT ROLE fce1 TO GROUP usa
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20171020101616_6273c98a-0887-4939-b5ce-524f8dc8bcce); Time taken: 0.067 seconds
INFO  : Executing command(queryId=hive_20171020101616_6273c98a-0887-4939-b5ce-524f8dc8bcce): GRANT ROLE fce1 TO GROUP usa
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20171020101616_6273c98a-0887-4939-b5ce-524f8dc8bcce); Time taken: 0.083 seconds
INFO  : OK
No rows affected (0.164 seconds)
2: jdbc:hive2://localhost:10000/default> CREATE ROLE fce2;
INFO  : Compiling command(queryId=hive_20171020101616_7aaab342-e718-43f9-b725-2583e0c85d06): CREATE ROLE fce2
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20171020101616_7aaab342-e718-43f9-b725-2583e0c85d06); Time taken: 0.056 seconds
INFO  : Executing command(queryId=hive_20171020101616_7aaab342-e718-43f9-b725-2583e0c85d06): CREATE ROLE fce2
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20171020101616_7aaab342-e718-43f9-b725-2583e0c85d06); Time taken: 0.031 seconds
INFO  : OK
No rows affected (0.104 seconds)
2: jdbc:hive2://localhost:10000/default> GRANT SELECT ON DATABASE default TO ROLE fce1;
INFO  : Compiling command(queryId=hive_20171020101616_b94298d7-f3ba-40b8-93bb-d51744395378): GRANT SELECT ON DATABASE default TO ROLE fce1
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20171020101616_b94298d7-f3ba-40b8-93bb-d51744395378); Time taken: 0.068 seconds
INFO  : Executing command(queryId=hive_20171020101616_b94298d7-f3ba-40b8-93bb-d51744395378): GRANT SELECT ON DATABASE default TO ROLE fce1
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20171020101616_b94298d7-f3ba-40b8-93bb-d51744395378); Time taken: 0.038 seconds
INFO  : OK
No rows affected (0.123 seconds)
2: jdbc:hive2://localhost:10000/default> GRANT ROLE fce2 TO GROUP emea;
INFO  : Compiling command(queryId=hive_20171020101717_f8d89d75-8fff-4181-b2c8-413d18118193): GRANT ROLE fce2 TO GROUP emea
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20171020101717_f8d89d75-8fff-4181-b2c8-413d18118193); Time taken: 0.068 seconds
INFO  : Executing command(queryId=hive_20171020101717_f8d89d75-8fff-4181-b2c8-413d18118193): GRANT ROLE fce2 TO GROUP emea
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20171020101717_f8d89d75-8fff-4181-b2c8-413d18118193); Time taken: 0.04 seconds
INFO  : OK
No rows affected (0.125 seconds)
```

Show tables as ernest:
```
2: jdbc:hive2://localhost:10000/default> SHOW TABLES;
INFO  : Compiling command(queryId=hive_20171020101717_8cbd0ea6-d1c0-4417-838f-02e61e8ab8a9): SHOW TABLES
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:tab_name, type:string, comment:from deserializer)], properties:null)
INFO  : Completed compiling command(queryId=hive_20171020101717_8cbd0ea6-d1c0-4417-838f-02e61e8ab8a9); Time taken: 0.225 seconds
INFO  : Executing command(queryId=hive_20171020101717_8cbd0ea6-d1c0-4417-838f-02e61e8ab8a9): SHOW TABLES
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20171020101717_8cbd0ea6-d1c0-4417-838f-02e61e8ab8a9); Time taken: 0.294 seconds
INFO  : OK
+------------+--+
|  tab_name  |
+------------+--+
| customers  |
| sample_07  |
| sample_08  |
| web_logs   |
+------------+--+
4 rows selected (0.671 seconds)
```

Show tables as siwicki:
```

```