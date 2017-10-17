# Installing Cloudera 5.8.3 on AWS 

## Spawn instances
 
Spawns 5 m3.xlarge instances using "sebc" key and security group 

Uses CentOS rolling 1602 (7.2-based)

Uses bigger root volume (16GiB instead of 8GiB) and attaches instance store volumes (2x40GiB SSDs)

```
aws --profile personal ec2 run-instances --image-id ami-9bf712f4 --security-groups sebc --key-name sebc --instance-type m3.xlarge --count 5 --block-device-mappings "[{\"DeviceName\":\"/dev/sda1\",\"Ebs\":{\"VolumeSize\":16}},{\"DeviceName\":\"/dev/sdb\",\"VirtualName\":\"ephemeral0\"},{\"DeviceName\":\"/dev/sdc\",\"VirtualName\":\"ephemeral1\"}]"
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
sudo yum install -y wget git
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
