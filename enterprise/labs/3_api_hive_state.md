## Hive start/stop

Start command: `curl -X POST -u nicolobidotti:cloudera localhost:7180/api/v12/clusters/nicolobidotti/services/hive/commands/start`

Output:
```json
{
  "id" : 919,
  "name" : "Start",
  "startTime" : "2017-10-18T15:11:42.062Z",
  "active" : true,
  "serviceRef" : {
    "clusterName" : "cluster",
    "serviceName" : "hive"
  }
}
```

Stop command: `curl -X POST -u nicolobidotti:cloudera localhost:7180/api/v12/clusters/nicolobidotti/services/hive/commands/stop`

Output:
```json
{
  "id" : 915,
  "name" : "Stop",
  "startTime" : "2017-10-18T15:10:15.338Z",
  "active" : true,
  "serviceRef" : {
    "clusterName" : "cluster",
    "serviceName" : "hive"
  }
}
```

## Hive state check

Command: `curl -u nicolobidotti:cloudera localhost:7180/api/v12/clusters/nicolobidotti/services/hive`

Output:
```json
{
  "name" : "hive",
  "type" : "HIVE",
  "clusterRef" : {
    "clusterName" : "cluster"
  },
  "serviceUrl" : "http://ip-172-31-5-172.eu-central-1.compute.internal:7180/cmf/serviceRedirect/hive",
  "roleInstancesUrl" : "http://ip-172-31-5-172.eu-central-1.compute.internal:7180/cmf/serviceRedirect/hive/instances",
  "serviceState" : "STARTED",
  "healthSummary" : "GOOD",
  "healthChecks" : [ {
    "name" : "HIVE_HIVEMETASTORES_HEALTHY",
    "summary" : "GOOD",
    "suppressed" : false
  }, {
    "name" : "HIVE_HIVESERVER2S_HEALTHY",
    "summary" : "GOOD",
    "suppressed" : false
  } ],
  "configStalenessStatus" : "FRESH",
  "clientConfigStalenessStatus" : "FRESH",
  "maintenanceMode" : false,
  "maintenanceOwners" : [ ],
  "displayName" : "Hive",
  "entityStatus" : "GOOD_HEALTH"
}
```