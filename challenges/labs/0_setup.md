Cloud provider: AWS you are using (AWS, GCE, Azure, other)

Linux release: CentOS 7.2.1511 (ami-9bf712f4)

Disk space on each node:
```
df -kh
```

Output (identical for alla nodes):
```
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda1       32G  928M   32G   3% /
devtmpfs        7,3G     0  7,3G   0% /dev
tmpfs           7,2G     0  7,2G   0% /dev/shm
tmpfs           7,2G   17M  7,2G   1% /run
tmpfs           7,2G     0  7,2G   0% /sys/fs/cgroup
/dev/xvdb        37G   49M   35G   1% /mnt
tmpfs           1,5G     0  1,5G   0% /run/user/1000
tmpfs           1,5G     0  1,5G   0% /run/user/0
```

Repolist:
```
sudo yum repolist enabled
```

Output:
```
Loaded plugins: fastestmirror
base                                                                                                                                           | 3.6 kB  00:00:00     
extras                                                                                                                                         | 3.4 kB  00:00:00     
updates                                                                                                                                        | 3.4 kB  00:00:00     
(1/4): base/7/x86_64/group_gz                                                                                                                  | 156 kB  00:00:00     
(2/4): extras/7/x86_64/primary_db                                                                                                              | 110 kB  00:00:00     
(3/4): updates/7/x86_64/primary_db                                                                                                             | 2.7 MB  00:00:00     
(4/4): base/7/x86_64/primary_db                                                                                                                | 5.7 MB  00:00:00     
Determining fastest mirrors
 * base: mirror.23media.de
 * extras: mirror.imt-systems.com
 * updates: ftp.antilo.de
repo id                                                                        repo name                                                                        status
base/7/x86_64                                                                  CentOS-7 - Base                                                                  9591
extras/7/x86_64                                                                CentOS-7 - Extras                                                                 227
updates/7/x86_64                                                               CentOS-7 - Updates                                                                741
repolist: 10559
```


/etc/passwd entries for new users:
```
ernest:x:2000:2000::/home/ernest:/bin/bash
siwicki:x:3000:3000::/home/siwicki:/bin/bash
```

/etc/group entries for new groups:
```
usa:x:3001:ernest
emea:x:3002:siwicki
```