## 1 - Check vm.swappiness on all your nodes 

Command: `cat /proc/sys/vm/swappiness`

Output:
```
30
```

Set to 1 in sysctl.conf: `sudo bash -c 'echo "vm.swappiness = 1" >> /etc/sysctl.conf'` 

Set to 1 on running system: `sudo sysctl vm.swappiness=1`

Check again: `cat /proc/sys/vm/swappiness`

Output: 
```
1
```

## 2 - Show the mount attributes of all volumes

Command: `mount`

Output:
```
sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime,seclabel)
proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
devtmpfs on /dev type devtmpfs (rw,nosuid,seclabel,size=7599028k,nr_inodes=1899757,mode=755)
securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime)
tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev,seclabel)
devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,seclabel,gid=5,mode=620,ptmxmode=000)
tmpfs on /run type tmpfs (rw,nosuid,nodev,seclabel,mode=755)
tmpfs on /sys/fs/cgroup type tmpfs (ro,nosuid,nodev,noexec,seclabel,mode=755)
cgroup on /sys/fs/cgroup/systemd type cgroup (rw,nosuid,nodev,noexec,relatime,xattr,release_agent=/usr/lib/systemd/systemd-cgroups-agent,name=systemd)
pstore on /sys/fs/pstore type pstore (rw,nosuid,nodev,noexec,relatime)
cgroup on /sys/fs/cgroup/blkio type cgroup (rw,nosuid,nodev,noexec,relatime,blkio)
cgroup on /sys/fs/cgroup/hugetlb type cgroup (rw,nosuid,nodev,noexec,relatime,hugetlb)
cgroup on /sys/fs/cgroup/net_cls type cgroup (rw,nosuid,nodev,noexec,relatime,net_cls)
cgroup on /sys/fs/cgroup/memory type cgroup (rw,nosuid,nodev,noexec,relatime,memory)
cgroup on /sys/fs/cgroup/cpu,cpuacct type cgroup (rw,nosuid,nodev,noexec,relatime,cpuacct,cpu)
cgroup on /sys/fs/cgroup/cpuset type cgroup (rw,nosuid,nodev,noexec,relatime,cpuset)
cgroup on /sys/fs/cgroup/freezer type cgroup (rw,nosuid,nodev,noexec,relatime,freezer)
cgroup on /sys/fs/cgroup/perf_event type cgroup (rw,nosuid,nodev,noexec,relatime,perf_event)
cgroup on /sys/fs/cgroup/devices type cgroup (rw,nosuid,nodev,noexec,relatime,devices)
configfs on /sys/kernel/config type configfs (rw,relatime)
/dev/xvda1 on / type xfs (rw,relatime,seclabel,attr2,inode64,noquota)
rpc_pipefs on /var/lib/nfs/rpc_pipefs type rpc_pipefs (rw,relatime)
selinuxfs on /sys/fs/selinux type selinuxfs (rw,relatime)
systemd-1 on /proc/sys/fs/binfmt_misc type autofs (rw,relatime,fd=27,pgrp=1,timeout=300,minproto=5,maxproto=5,direct)
debugfs on /sys/kernel/debug type debugfs (rw,relatime)
mqueue on /dev/mqueue type mqueue (rw,relatime,seclabel)
hugetlbfs on /dev/hugepages type hugetlbfs (rw,relatime,seclabel)
nfsd on /proc/fs/nfsd type nfsd (rw,relatime)
tmpfs on /run/user/1000 type tmpfs (rw,nosuid,nodev,relatime,seclabel,size=1497312k,mode=700,uid=1000,gid=1000)
/dev/xvdb on /mnt/ssd0 type ext4 (rw,noatime,seclabel,data=ordered)
/dev/xvdc on /mnt/ssd1 type ext4 (rw,noatime,seclabel,data=ordered)
```

## 3 - Show the reserve space of any non-root, ext-based volumes

TOASK: ok to add grep Reserved in pipe?

Commands:
```
sudo tune2fs -l /dev/xvdb
sudo tune2fs -l /dev/xvdc
```

Output 1:

```
tune2fs 1.42.9 (28-Dec-2013)
Filesystem volume name:   <none>
Last mounted on:          <not available>
Filesystem UUID:          29e8ca6e-8f3b-40f7-ba69-be61e0ab3ffd
Filesystem magic number:  0xEF53
Filesystem revision #:    1 (dynamic)
Filesystem features:      has_journal ext_attr resize_inode dir_index filetype needs_recovery extent 64bit flex_bg sparse_super large_file huge_file uninit_bg dir_nlink extra_isize
Filesystem flags:         signed_directory_hash 
Default mount options:    user_xattr acl
Filesystem state:         clean
Errors behavior:          Continue
Filesystem OS type:       Linux
Inode count:              2457600
Block count:              9828352
Reserved block count:     0
Free blocks:              9629018
Free inodes:              2457589
First block:              0
Block size:               4096
Fragment size:            4096
Group descriptor size:    64
Reserved GDT blocks:      1024
Blocks per group:         32768
Fragments per group:      32768
Inodes per group:         8192
Inode blocks per group:   512
Flex block group size:    16
Filesystem created:       Mon Oct 16 14:44:33 2017
Last mount time:          Mon Oct 16 15:05:03 2017
Last write time:          Mon Oct 16 15:05:03 2017
Mount count:              2
Maximum mount count:      -1
Last checked:             Mon Oct 16 14:44:33 2017
Check interval:           0 (<none>)
Lifetime writes:          733 MB
Reserved blocks uid:      0 (user root)
Reserved blocks gid:      0 (group root)
First inode:              11
Inode size:	          256
Required extra isize:     28
Desired extra isize:      28
Journal inode:            8
Default directory hash:   half_md4
Directory Hash Seed:      4d891305-b832-4581-a779-e5aea4f24e14
Journal backup:           inode blocks
```

Output 2:

```
tune2fs 1.42.9 (28-Dec-2013)
Filesystem volume name:   <none>
Last mounted on:          <not available>
Filesystem UUID:          dd540bb5-4add-482f-b98a-a0eaf91a924e
Filesystem magic number:  0xEF53
Filesystem revision #:    1 (dynamic)
Filesystem features:      has_journal ext_attr resize_inode dir_index filetype needs_recovery extent 64bit flex_bg sparse_super large_file huge_file uninit_bg dir_nlink extra_isize
Filesystem flags:         signed_directory_hash 
Default mount options:    user_xattr acl
Filesystem state:         clean
Errors behavior:          Continue
Filesystem OS type:       Linux
Inode count:              2457600
Block count:              9828352
Reserved block count:     0
Free blocks:              9629018
Free inodes:              2457589
First block:              0
Block size:               4096
Fragment size:            4096
Group descriptor size:    64
Reserved GDT blocks:      1024
Blocks per group:         32768
Fragments per group:      32768
Inodes per group:         8192
Inode blocks per group:   512
Flex block group size:    16
Filesystem created:       Mon Oct 16 14:44:37 2017
Last mount time:          Mon Oct 16 15:05:04 2017
Last write time:          Mon Oct 16 15:05:04 2017
Mount count:              2
Maximum mount count:      -1
Last checked:             Mon Oct 16 14:44:37 2017
Check interval:           0 (<none>)
Lifetime writes:          733 MB
Reserved blocks uid:      0 (user root)
Reserved blocks gid:      0 (group root)
First inode:              11
Inode size:	          256
Required extra isize:     28
Desired extra isize:      28
Journal inode:            8
Default directory hash:   half_md4
Directory Hash Seed:      f6d52687-24cb-4cc1-a31a-00388ab134da
Journal backup:           inode blocks
```

## 4 - Disable transparent hugepage support

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

Add this to the GRUB_CMDLINE_LINUX options:
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

## 5 - List your network interface configuration

Command: `ifconfig`

Output:
```
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 9001
        inet 172.31.5.172  netmask 255.255.240.0  broadcast 172.31.15.255
        inet6 fe80::3b:4bff:fec6:f6aa  prefixlen 64  scopeid 0x20<link>
        ether 02:3b:4b:c6:f6:aa  txqueuelen 1000  (Ethernet)
        RX packets 15803  bytes 10346400 (9.8 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 11023  bytes 1519924 (1.4 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 0  (Local Loopback)
        RX packets 70  bytes 5984 (5.8 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 70  bytes 5984 (5.8 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

## 6 - List forward and reverse host lookups using getent or nslookup

Forward DNS, commands:
```
getent hosts ip-172-31-5-172.eu-central-1.compute.internal
getent hosts ip-172-31-12-159.eu-central-1.compute.internal
getent hosts ip-172-31-13-237.eu-central-1.compute.internal
getent hosts ip-172-31-10-208.eu-central-1.compute.internal
getent hosts ip-172-31-3-37.eu-central-1.compute.internal
```
Outputs (merged together):
```
172.31.5.172    ip-172-31-5-172.eu-central-1.compute.internal
172.31.12.159   ip-172-31-12-159.eu-central-1.compute.internal
172.31.13.237   ip-172-31-13-237.eu-central-1.compute.internal
172.31.10.208   ip-172-31-10-208.eu-central-1.compute.internal
172.31.3.37     ip-172-31-3-37.eu-central-1.compute.internal
```

Reverse DNS, commands:
```
getent hosts 172.31.5.172
getent hosts 172.31.12.159
getent hosts 172.31.13.237
getent hosts 172.31.10.208
getent hosts 172.31.3.37
```

Outputs (merged together):
```
172.31.5.172    ip-172-31-5-172.eu-central-1.compute.internal
172.31.12.159   ip-172-31-12-159.eu-central-1.compute.internal
172.31.13.237   ip-172-31-13-237.eu-central-1.compute.internal
172.31.10.208   ip-172-31-10-208.eu-central-1.compute.internal
172.31.3.37     ip-172-31-3-37.eu-central-1.compute.internal
```

## 7 - Show the nscd service is running

Install & enable:
```
sudo yum install -y nscd
sudo systemctl start nscd
sudo systemctl enable nscd
```

Check it is running; command: `sudo systemctl status nscd`

Output:
```
● nscd.service - Name Service Cache Daemon
   Loaded: loaded (/usr/lib/systemd/system/nscd.service; enabled; vendor preset: disabled)
   Active: active (running) since mar 2017-10-17 00:22:18 UTC; 2min 44s ago
 Main PID: 17876 (nscd)
   CGroup: /system.slice/nscd.service
           └─17876 /usr/sbin/nscd

ott 17 00:22:18 ip-172-31-5-172 nscd[17876]: 17876 monitoring directory `/etc` (2)
ott 17 00:22:18 ip-172-31-5-172 nscd[17876]: 17876 monitoring file `/etc/services` (6)
ott 17 00:22:18 ip-172-31-5-172 nscd[17876]: 17876 monitoring directory `/etc` (2)
ott 17 00:22:18 ip-172-31-5-172 nscd[17876]: 17876 disabled inotify-based monitoring for file `/etc/netgroup': No such file or directory
ott 17 00:22:18 ip-172-31-5-172 nscd[17876]: 17876 stat failed for file `/etc/netgroup'; will try again later: No such file or directory
ott 17 00:22:18 ip-172-31-5-172 nscd[17876]: 17876 Access Vector Cache (AVC) started
ott 17 00:22:18 ip-172-31-5-172 systemd[1]: Started Name Service Cache Daemon.
ott 17 00:22:37 ip-172-31-5-172 nscd[17876]: 17876 checking for monitored file `/etc/netgroup': No such file or directory
ott 17 00:23:15 ip-172-31-5-172 systemd[1]: Started Name Service Cache Daemon.
ott 17 00:24:36 ip-172-31-5-172 systemd[1]: Started Name Service Cache Daemon.
```

Check it speeds up lookups; command: `time getent hosts www.google.it`

Output, first run:
```
2607:f8b0:400e:c04::5e www.google.it

real	0m0.018s
user	0m0.000s
sys	0m0.001s
```
Ouput, second run:
```
2607:f8b0:400e:c04::5e www.google.it

real	0m0.001s
user	0m0.000s
sys	0m0.001s
```

## 8 - Show the ntpd service is running

Install & enable:
```
sudo yum install -y ntp
sudo systemctl start ntpd
sudo systemctl enable ntpd
```

Check it is running; command: `sudo systemctl status ntpd`

Output:
```
● ntpd.service - Network Time Service
   Loaded: loaded (/usr/lib/systemd/system/ntpd.service; enabled; vendor preset: disabled)
   Active: active (running) since mar 2017-10-17 07:08:59 UTC; 1min 3s ago
  Process: 18907 ExecStart=/usr/sbin/ntpd -u ntp:ntp $OPTIONS (code=exited, status=0/SUCCESS)
 Main PID: 18908 (ntpd)
   CGroup: /system.slice/ntpd.service
           └─18908 /usr/sbin/ntpd -u ntp:ntp -g

ott 17 07:08:59 ip-172-31-5-172 ntpd[18908]: Listen normally on 2 lo 127.0.0.1 UDP 123
ott 17 07:08:59 ip-172-31-5-172 ntpd[18908]: Listen normally on 3 eth0 172.31.5.172 UDP 123
ott 17 07:08:59 ip-172-31-5-172 ntpd[18908]: Listen normally on 4 lo ::1 UDP 123
ott 17 07:08:59 ip-172-31-5-172 ntpd[18908]: Listen normally on 5 eth0 fe80::3b:4bff:fec6:f6aa UDP 123
ott 17 07:08:59 ip-172-31-5-172 ntpd[18908]: Listening on routing socket on fd #22 for interface updates
ott 17 07:08:59 ip-172-31-5-172 systemd[1]: Started Network Time Service.
ott 17 07:08:59 ip-172-31-5-172 ntpd[18908]: 0.0.0.0 c016 06 restart
ott 17 07:08:59 ip-172-31-5-172 ntpd[18908]: 0.0.0.0 c012 02 freq_set kernel 0.000 PPM
ott 17 07:08:59 ip-172-31-5-172 ntpd[18908]: 0.0.0.0 c011 01 freq_not_set
ott 17 07:09:06 ip-172-31-5-172 ntpd[18908]: 0.0.0.0 c614 04 freq_mode
```