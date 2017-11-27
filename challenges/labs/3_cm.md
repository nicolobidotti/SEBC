List HDFS /user dir:
```
HADOOP_USER_NAME=hdfs hdfs dfs -ls /user
```
Output:
```
Found 6 items
drwxr-xr-x   - ernest  ernest           0 2017-10-20 08:57 /user/ernest
drwxrwxrwx   - mapred  hadoop           0 2017-10-20 08:49 /user/history
drwxrwxr-t   - hive    hive             0 2017-10-20 08:50 /user/hive
drwxrwxr-x   - hue     hue              0 2017-10-20 08:50 /user/hue
drwxrwxr-x   - oozie   oozie            0 2017-10-20 08:50 /user/oozie
drwxr-xr-x   - siwicki siwicki          0 2017-10-20 08:57 /user/siwicki
```

Hosts API call:
```
curl admin:admin@localhost:7180/api/v14/hosts
```
Output:
```json
{
  "items" : [ {
    "hostId" : "i-04ac7acddb92727f3",
    "ipAddress" : "172.31.13.131",
    "hostname" : "ip-172-31-13-131.eu-central-1.compute.internal",
    "rackId" : "/default",
    "hostUrl" : "http://ip-172-31-13-131.eu-central-1.compute.internal:7180/cmf/hostRedirect/i-04ac7acddb92727f3",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "commissionState" : "COMMISSIONED",
    "numCores" : 4,
    "numPhysicalCores" : 2,
    "totalPhysMemBytes" : 15332438016
  }, {
    "hostId" : "i-0cdf130fee7b2def2",
    "ipAddress" : "172.31.15.174",
    "hostname" : "ip-172-31-15-174.eu-central-1.compute.internal",
    "rackId" : "/default",
    "hostUrl" : "http://ip-172-31-13-131.eu-central-1.compute.internal:7180/cmf/hostRedirect/i-0cdf130fee7b2def2",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "commissionState" : "COMMISSIONED",
    "numCores" : 4,
    "numPhysicalCores" : 2,
    "totalPhysMemBytes" : 15332438016
  }, {
    "hostId" : "i-08c764cab4f7d3ab4",
    "ipAddress" : "172.31.5.211",
    "hostname" : "ip-172-31-5-211.eu-central-1.compute.internal",
    "rackId" : "/default",
    "hostUrl" : "http://ip-172-31-13-131.eu-central-1.compute.internal:7180/cmf/hostRedirect/i-08c764cab4f7d3ab4",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "commissionState" : "COMMISSIONED",
    "numCores" : 4,
    "numPhysicalCores" : 2,
    "totalPhysMemBytes" : 15332438016
  }, {
    "hostId" : "i-02fd7c1466776687f",
    "ipAddress" : "172.31.6.73",
    "hostname" : "ip-172-31-6-73.eu-central-1.compute.internal",
    "rackId" : "/default",
    "hostUrl" : "http://ip-172-31-13-131.eu-central-1.compute.internal:7180/cmf/hostRedirect/i-02fd7c1466776687f",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "commissionState" : "COMMISSIONED",
    "numCores" : 4,
    "numPhysicalCores" : 2,
    "totalPhysMemBytes" : 15332438016
  }, {
    "hostId" : "i-08aa7c7bc7e5fce79",
    "ipAddress" : "172.31.9.149",
    "hostname" : "ip-172-31-9-149.eu-central-1.compute.internal",
    "rackId" : "/default",
    "hostUrl" : "http://ip-172-31-13-131.eu-central-1.compute.internal:7180/cmf/hostRedirect/i-08aa7c7bc7e5fce79",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "commissionState" : "COMMISSIONED",
    "numCores" : 4,
    "numPhysicalCores" : 2,
    "totalPhysMemBytes" : 15332438016
  } ]
}
```
.
