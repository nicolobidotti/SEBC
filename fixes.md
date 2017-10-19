# Fixes applied to errors made

## Phantom packages

In the role assignment phase of the installation wizard, you are unable to proceed as you get an error that says "A package was not selected". As detailed in https://community.cloudera.com/t5/Cloudera-Manager-Installation/Error-A-package-was-not-selected/td-p/58450 it's a browser issue!
 
**Solution:** refresh the page ignoring cache

## Learn2freespace

Being a cheap guy, you skimp on root EBS volume size for your instances and set it to 16GiB. After installing the cluster, a slew of 40+ warnings appear: there's not enough free space in the various log/storage directories for the services.

**Solution:**
0. ~~Shamelessly suppress all warnings~~
1. Stop cluster
2. Stop Cloudera Management Service
3. Stop CM agent
4. Stop CM server
5. Stop instances
6. Snapshot EBS volumes
7. Create new, bigger volumes from snapshots (filesystem in XFS and is automatically grown to new volume size)
8. Detach old volumes and attach the new ones in their place
9. Restart instances
10. Start CM server
11. Start CM agent
12. Start Cloudera Management Service
13. Delete cluster (the data was lost anyway as it was on the instance's ephemeral storage)
14. Reformat/remount instance ephemeral storage
15. Create and start new cluster

## Alternatives disaster

After attempting to move the parcel directory, commands such as hadoop or sqoop do not work anymore; bash complains with a "command not found". Inspecting the executables under /bin/ reveals the reason: the symlinks are wrong and point to the old parcels directory.

The reason is that moving parcel directory to another directory (/mnt/ssd0/parcels), restarting the agent, moving it back to the original position (/opt/cloudera/parcels) and restarting the agent again caused havoc with alternatives. Cloudera agent does not update alternatives for commands anymore resulting in commands not being available because the symlinks point to the old parcels directory. This is due to lingering alternatives configurations in /var/lib/alternatives/. See: https://community.cloudera.com/t5/Cloudera-Manager-Installation/Incorrect-symlinks-being-created-by-cloudera-scm-agent/td-p/18092

**Solution:**
1. Stop cluster
2. Stop agent
3. Delete all Cloudera-related alternatives under /var/lib/alternatives:
    - be careful, they may be different on each node
    - get into alternatives dir: `cd /var/lib/alternatives`
    - list by time: `ls -tl` (because hopefully you should be able to separate them from the others by time)
    - wipe 'em: `rm $(ls -tl | head -n -5 | awk '{print $9}')` (the -5 in `head` drops the last 5 lines which are other alternatives)
4. Start agent
5. Start cluster
6. Cherish your hadoop commands