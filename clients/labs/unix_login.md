Get current Hue conf dir:
```
sudo bash -c 'echo "/var/run/cloudera-scm-agent/process/$(ls -1 /var/run/cloudera-scm-agent/process | grep HUE | sort -n | tail -1)"'
```

Export the answer in HUE_CONF_DIR:
```
export HUE_CONF_DIR=/var/run/cloudera-scm-agent/process/431-hue-HUE_SERVER```
```

**Note:** I did it this way because the commands specified in the doc did not work with sudo & I prefer not to run as root.

Import users:
```
sudo env "HUE_SECRET_KEY=asd" "HUE_CONF_DIR=$HUE_CONF_DIR" "HUE_IGNORE_PASSWORD_SCRIPT_ERRORS=1" "HUE_DATABASE_PASSWORD=hue_password" /opt/cloudera/parcels/CDH/lib/hue/build/env/bin/hue useradmin_sync_with_unix
```

**Note 1:** the "HUE_SECRET_KEY=asd" is neede because otherwise the script used to extract the password complains ("Error: Password not present"), the value can be anything.

**Note 2:** despite what the doc says, the command line options, eg --min-uid 1090 --max-uid 1110 to import just a subset of users, **do not work**!

Finally, go to the User Admin app in Hue and give the new users passwords.