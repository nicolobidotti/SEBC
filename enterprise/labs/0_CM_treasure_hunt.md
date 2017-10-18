## What is ubertask optimization?

Ubertask optimization (mapreduce.job.ubertask.enable) refers to using a single JVM (that of the AppplicationMaster) for the map & reduce tasks of "sufficiently small" jobs. These jobs are defined by thresholds specifying the maximum number fo mappers, reducers & bytes that they involve (mapreduce.job.ubertask.maxmaps, mapreduce.job.ubertask.maxreduces, and mapreduce.job.ubertask.maxbytes).  

## Where in CM is the Kerberos Security Realm value displayed?

It can be found under Administration / Security or Administration / Settings / Category: Kerberos / "default_realm"

## Which CDH service(s) host a property for enabling Kerberos authentication?

From the Core Hadoop service set, the following services have a property to enable Kerberos:
- Hive
- ZooKeeper
- Hue
- Oozie
- HDFS
- YARN

(All of them)

## How do you upgrade the CM agents?

The CM agents can be upgraded when upgrading the CM server to a newer version by using the upgarde wizard; they can also be upgraded by installing packages directly. The agent version must be <= than the version of the server.

## Give the tsquery statement used to chart Hue's CPU utilization?

Statement:
```
select cpu_system_rate + cpu_user_rate where category=ROLE and serviceName=$SERVICENAME
```

Variables:
```
$SERVICENAME = hue  $CLUSTERID = 1
```

## Name all the roles that make up the Hive service

- Hive Metastore Server
- HiveServer2
- WebHCat Server
- Gateway

**Note:** WebHCat Server was not deployed

## What steps must be completed before integrating Cloudera Manager with Kerberos?

Before enabling Kerberos the following prerequisites must be met:
- TLS/SSL encryption between Cloudera Manager Server and all Cloudera Manager Agent host systems in the cluster must be enabled and working
- a working KDC must be available
- the KDC should be configured to have non-zero ticket lifetime and renewal lifetime
- OpenLdap client libraries should be installed on the Cloudera Manager Server (if using Active Directory)
- Kerberos client libraries should be installed on ALL hosts
- Cloudera Manager needs an account that has permissions to create other accounts in the KDC


