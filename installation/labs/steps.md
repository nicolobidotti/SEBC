# Installing Cloudera 5.8.3 on AWS 

## Spawn instances
 
Spawns 5 m3.xlarge instances using "sebc" key and security group 

Uses CentOS rolling 1602 (7.2-based)

Uses bigger root volume (32GiB instead of 8GiB) and attaches instance store volumes (2x40GiB SSDs)

```
aws --profile personal ec2 run-instances --image-id ami-9bf712f4 --security-groups sebc --key-name sebc --instance-type m3.xlarge --count 5 --block-device-mappings "[{\"DeviceName\":\"/dev/sda1\",\"Ebs\":{\"VolumeSize\":32}},{\"DeviceName\":\"/dev/sdb\",\"VirtualName\":\"ephemeral0\"},{\"DeviceName\":\"/dev/sdc\",\"VirtualName\":\"ephemeral1\"}]"
```

## Shell on all hosts

Write IPs of the machines to "ips"

```
TARGETS=""
while read IP
do
    TARGETS="$TARGETS centos@$IP"
done < ips
clusterssh -o '-i ~/Documents/Lavoro/SEBC/sebc.pem' $TARGETS
```

## Update

Only security so we do not change minor CentOS version (just for fun, minor releases are ABI/API compatible... see https://access.redhat.com/discussions/685843 )

```
sudo yum update -y --security
```

## Install stuff

Install useful stuff:
```
sudo yum install -y wget git nmap-ncat
```

Enable EPEL repository:
```
wget http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-10.noarch.rpm
sudo rpm -ihv epel-release-7-10.noarch.rpm
```

Install *top:
```
sudo yum install -y htop iftop iotop
```

## Disable SELinux

From https://www.cloudera.com/documentation/enterprise/5-8-x/topics/install_cdh_disable_selinux.html

```
sudo vi /etc/selinux/config 
```

Change the line SELINUX=enforcing to SELINUX=permissive

```
sudo setenforce 0
```

## Format & mount instance volumes

TODO: fstab

Unmount

```
sudo umount /dev/xvdb
sudo umount /dev/xvdc
```

Format

```
sudo mkfs.ext4 -m 0 /dev/xvdb
sudo mkfs.ext4 -m 0 /dev/xvdc
```

Mkdirs

```
sudo mkdir /mnt/ssd0
sudo mkdir /mnt/ssd1
```

Set permissions to read-only & make immutable. This makes it so nobody can write to mount dirs, not even root, and even root can't simply chmod 777 because of the immutable flag.

```
sudo chmod 600 /mnt/ssd*
sudo chattr +i /mnt/ssd*
```

Leave a little text file telling confused sysadmins why their `sudo chmod` won't work.
```
sudo bash -c 'echo "These are root-owned, read-only mount dirs. They have the immutable flag set, so even root cannot simply \"chmod 777\" or \"rm -rf\" them. Use \"chattr -i\" to remove the immutable flag." > /mnt/README'
```


Mount with noatime

```
sudo mount -t ext4 -o noatime /dev/xvdb /mnt/ssd0
sudo mount -t ext4 -o noatime /dev/xvdc /mnt/ssd1
```

## Check reserved space for ext4 volumes

Commands:
```
sudo tune2fs -l /dev/xvdb
sudo tune2fs -l /dev/xvdc
```

## Fix swappiness

Check status: `cat /proc/sys/vm/swappiness`

Set to 1 in sysctl.conf: `sudo bash -c 'echo "vm.swappiness = 1" >> /etc/sysctl.conf'` 

Set to 1 on running system: `sudo sysctl vm.swappiness=1`

Check again: `cat /proc/sys/vm/swappiness`

## Fix transparent hugepage

Check status:
```
cat /sys/kernel/mm/transparent_hugepage/enabled
cat /sys/kernel/mm/transparent_hugepage/defrag
```

Disable THP at boot by adding to /etc/rc.d/rc.local:
```
sudo bash -c 'echo "echo never > /sys/kernel/mm/transparent_hugepage/enabled" >> /etc/rc.d/rc.local'
sudo bash -c 'echo "echo never > /sys/kernel/mm/transparent_hugepage/defrag" >> /etc/rc.d/rc.local'
chmod +x /etc/rc.d/rc.local
```

Disable THP at boot by modifying GRUB conf:
```
sudo vi /etc/default/grub
```

Add this line to the GRUB_CMDLINE_LINUX options:
```
transparent_hugepage=never
```

Rebuild GRUB config: `sudo grub2-mkconfig -o /boot/grub2/grub.cfg`

Disable THP on running system:
```
sudo bash -c 'echo never > /sys/kernel/mm/transparent_hugepage/enabled'
sudo bash -c 'echo never > /sys/kernel/mm/transparent_hugepage/defrag'
```

Check again:
```
cat /sys/kernel/mm/transparent_hugepage/enabled
cat /sys/kernel/mm/transparent_hugepage/defrag
```

Disable tuned: `sudo tuned-adm off`

Check that tuned is disabled: `sudo tuned-adm list`
 
Stop and disable tuned service:
```
sudo systemctl stop tuned
sudo systemctl disable tuned
```

## Show network interfaces

Command: `ifconfig`

## Check forward & reverse DNS

Use `gentent hosts` on all hostnames/IPs

## Enable nscd

Install & enable:
```
sudo yum install -y nscd
sudo systemctl start nscd
sudo systemctl enable nscd
```

Check it is running; command: `sudo systemctl status nscd`

Check it speeds up lookups; command (run more than once): `time getent hosts www.google.it`

## Enable ntpd

Install & enable:
```
sudo yum install -y ntp
sudo systemctl start ntpd
sudo systemctl enable ntpd
```

Check it is running; command: `sudo systemctl status ntpd`

## Install MariaDB server on master & worker 1

Install MariaDB 5.5 on master and worker1:
```
sudo yum install -y mariadb-server
```

Backup old config & create new one:
```
sudo mv /etc/my.cnf /etc/my.conf.old
sudo vi /etc/my.cnf
```

Paste the following in it:
```
[mysqld]
transaction-isolation = READ-COMMITTED
# Disabling symbolic-links is recommended to prevent assorted security risks;
# to do so, uncomment this line:
# symbolic-links = 0

key_buffer = 16M
key_buffer_size = 32M
max_allowed_packet = 32M
thread_stack = 256K
thread_cache_size = 64
query_cache_limit = 8M
query_cache_size = 64M
query_cache_type = 1

max_connections = 550
#expire_logs_days = 10
#max_binlog_size = 100M

#log_bin should be on a disk with enough free space. Replace '/var/lib/mysql/mysql_binary_log' with an appropriate path for your system
#and chown the specified folder to the mysql user.
log_bin=/var/lib/mysql/mysql_binary_log

binlog_format = mixed

read_buffer_size = 2M
read_rnd_buffer_size = 16M
sort_buffer_size = 8M
join_buffer_size = 8M

# InnoDB settings
innodb_file_per_table = 1
innodb_flush_log_at_trx_commit  = 2
innodb_log_buffer_size = 64M
innodb_buffer_pool_size = 4G
innodb_thread_concurrency = 8
innodb_flush_method = O_DIRECT
innodb_log_file_size = 512M

[mysqld_safe]
log-error=/var/log/mariadb/mariadb.log
pid-file=/var/run/mariadb/mariadb.pid
```

Start & enable:
```
sudo systemctl start mariadb
sudo systemctl enable mariadb
```

Secure the server:
```
sudo /usr/bin/mysql_secure_installation
```

Answer the questions as follows:
- Set password protection for the server
- Revoke permissions for anonymous users
- Permit remote privileged login
- Remove test databases
- Refresh privileges in memory

## Enable replication for servers

### On the master

Modify config to add this: 
```
[mariadb]
server_id=1
log-basename=master1
```

Restart the server: `sudo systemctl restart mariadb`;

Launch a prompt: `mysql -u root -p`

Execute this to grant replication privileges to slave:
```
GRANT REPLICATION SLAVE ON *.* TO replication_user IDENTIFIED BY 'replication_user_password';
```

Get the log coordinates; execute this:
```
FLUSH TABLES WITH READ LOCK;
```

Then, **in another prompt**, execute this:
```
SHOW MASTER STATUS;
```

Note the coordinates.

Unlock the tables in the first prompt by executing:
```
UNLOCK TABLES;
```

Close the prompts.

### On the slave

Modify config to add this: 
```
[mariadb]
server_id=2
```

Restart the server: `sudo systemctl restart mariadb`

Launch a prompt: `mysql -u root -p`

Execute this to configure a connection to the master:
```
CHANGE MASTER TO MASTER_HOST='master host', MASTER_USER='replication_user', MASTER_PASSWORD='replication_user_password', MASTER_LOG_FILE='master file name', MASTER_LOG_POS=master file offset;
```

Then execute this to initiate slave operations on the replica:
```
START SLAVE;
SHOW SLAVE STATUS \G
```

If successful, the `Slave_IO_State` field will read "Waiting for master to send event".

## Install MariaDB & JDBC connector on all nodes

Install MariaDB libs:
```
sudo yum install -y mariadb
```

Download & install MySQL JDBC connector:
```
wget https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.1.44.tar.gz
tar -xzvf mysql-connector-java-5.1.44.tar.gz
sudo mkdir -p /usr/share/java/
sudo cp mysql-connector-java-5.1.44/mysql-connector-java-5.1.44-bin.jar /usr/share/java/mysql-connector-java.jar
```

## Install Cloudera Manager and CDH, path B

### Add Cloudera repositories

Find the correct repository file from https://www.cloudera.com/documentation/enterprise/release-notes/topics/cm_vd.html

Install repo file; for CM/CDH 5.8.3:
```
wget https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/cloudera-manager.repo
```

Edit it:
```
vi cloudera-manager.repo
```

And change baseurl to point to the correct version.

Copy it in the yum repos directory:
```
sudo cp cloudera-manager.repo /etc/yum.repos.d/
```

### Install Java on CM host

Either use the Oracle-provided rpm package or install the one provided in the Cloudera repos.

Install Java 7 from Cloudera repos:
```
sudo yum install -y oracle-j2sdk1.7
```

### Install CM

Install CM using yum:
```
sudo yum install -y cloudera-manager-daemons cloudera-manager-server
```

Do not start the wizard until you completed the next two sections.

### Create databases

Create database for CM:
```
sudo /usr/share/cmf/schema/scm_prepare_database.sh mysql -uroot -proot_password scm scm scm_password
```

Create databases for services. For MySQL/MariaDB, use these statements:
```
CREATE DATABASE hue DEFAULT CHARACTER SET utf8 DEFAULT COLLATE utf8_general_ci;
GRANT ALL ON hue.* TO 'hue'@'%' IDENTIFIED BY 'hue_password';

CREATE DATABASE oozie DEFAULT CHARACTER SET utf8;
GRANT ALL ON oozie.* TO 'oozie'@'%' IDENTIFIED BY 'oozie_password';

CREATE DATABASE sqoop DEFAULT CHARACTER SET utf8;
GRANT ALL ON sqoop.* TO 'sqoop'@'%' IDENTIFIED BY 'sqoop_password';

CREATE DATABASE amon DEFAULT CHARACTER SET utf8;
GRANT ALL ON amon.* TO 'amon'@'%' IDENTIFIED BY 'amon_password';

CREATE DATABASE rman DEFAULT CHARACTER SET utf8;
GRANT ALL ON rman.* TO 'rman'@'%' IDENTIFIED BY 'rman_password';

CREATE DATABASE metastore DEFAULT CHARACTER SET utf8;
GRANT ALL ON metastore.* TO 'hive'@'%' IDENTIFIED BY 'hive_password';

CREATE DATABASE sentry DEFAULT CHARACTER SET utf8;
GRANT ALL ON sentry.* TO 'sentry'@'%' IDENTIFIED BY 'sentry_password';

CREATE DATABASE nav DEFAULT CHARACTER SET utf8;
GRANT ALL ON nav.* TO 'nav'@'%' IDENTIFIED BY 'nav_password';

CREATE DATABASE navms DEFAULT CHARACTER SET utf8;
GRANT ALL ON navms.* TO 'navms'@'%' IDENTIFIED BY 'navms_password';
```

### Start CMS

Command:
```
sudo systemctl start cloudera-scm-server
```

### Install hosts using wizard

Follow these guidelines:
- access the CM Web UI and start the wizard
- choose to install the Data Hub Edition
- add the hosts
- choose to install CDH using parcels
- edit the parcel repositories to install CDH 5.8.3 and not 5.8.5
- choose to install the JDK
- choose to not use Single User Mode
- specify the credentials to access the hosts
- deploy the Core Hadoop of CDH services
- deploy three ZooKeeper instances
- configure databases according to the section on creating databases
- configure settings
- GO!

## Bonus: locally hosted parcel repo

Install & start httpd:
```
sudo yum install -y httpd
sudo systemctl start httpd
```

Download parcels into a temporary directory:
```
mkdir parcelrepo
cd parcelrepo/
wget https://archive.cloudera.com/cdh5/parcels/5.8.3/CDH-5.8.3-1.cdh5.8.3.p0.2-el7.parcel
wget https://archive.cloudera.com/cdh5/parcels/5.8.3/CDH-5.8.3-1.cdh5.8.3.p0.2-el7.parcel.sha1
wget https://archive.cloudera.com/cdh5/parcels/5.8.3/manifest.json
```

Create directory for serving parcels, copy stuff, set permissions: 
```
sudo mkdir -p /var/www/html/cdh5.8.3
sudo cp * /var/www/html/cdh5.8.3/
sudo chmod -R ugo+rX /var/www/html/cdh5.8.3/
```

Check that the server is working:
```
curl localhost:80/cdh5.8.3/
```

Add `http://localhost:80/cdh5.8.3/` to the parcel repository URLs.

