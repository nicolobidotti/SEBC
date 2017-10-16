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
yum update -y --security
```

