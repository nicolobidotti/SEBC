Hostname:
```
hostname -f
```
Output:
```
ip-172-31-6-73.eu-central-1.compute.internal
```
(Corresponds to IP 54.93.243.167, external DNSec2-54-93-243-167.eu-central-1.compute.amazonaws.com)

MySQL version:
```
mysql --version
```
Output:
```
mysql  Ver 14.14 Distrib 5.5.58, for Linux (x86_64) using readline 5.1
```

Database listing:
```
sudo mysql -e 'show databases;'
```
Output:
```
+--------------------+
| Database           |
+--------------------+
| information_schema |
| hive               |
| hue                |
| mysql              |
| oozie              |
| performance_schema |
| rman               |
| scm                |
| sentry             |
| test               |
+--------------------+
```