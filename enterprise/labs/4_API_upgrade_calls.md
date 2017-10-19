## Report the latest available version of the API
    
Command:
```
curl -u nicolobidotti:cloudera localhost:7180/api/version
```

Output:
```
v14
```

## Report the CM version

Command:
```
curl -u nicolobidotti:cloudera localhost:7180/api/v14/cm/version
```

Output:
```json
{
  "version" : "5.9.3",
  "buildUser" : "jenkins",
  "buildTimestamp" : "20170627-1506",
  "gitHash" : "23506bb4e114dd460bdac64c57a672e6be631907",
  "snapshot" : false
}
```

## List all CM users

Command:
```
curl -u nicolobidotti:cloudera localhost:7180/api/v14/users/
```

Output:
```json
{
  "items" : [ {
    "name" : "admin",
    "roles" : [ "ROLE_LIMITED" ]
  }, {
    "name" : "minotaur",
    "roles" : [ "ROLE_CONFIGURATOR" ]
  }, {
    "name" : "nicolobidotti",
    "roles" : [ "ROLE_ADMIN" ]
  } ]
}
```

## Report the database server in use by CM

Command:
```
curl -u nicolobidotti:cloudera localhost:7180/api/v14/cm/scmDbInfo
```

Output:
```json
{
  "scmDbType" : "MYSQL",
  "embeddedDbUsed" : false
}
```

**Note:** actual db address, name & credentials are stored in /etc/cloudera-scm-server/db.properties 