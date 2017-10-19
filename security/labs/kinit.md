Authenticate user "nicolobidotti":
```
kinit -p nicolobidotti
```
Or, if logged in as "nicolobidotti", simply `kinit`

List credentials and ticket lifetime:
```
klist
```
Output:
```
Ticket cache: FILE:/tmp/krb5cc_1000
Default principal: nicolobidotti@NICOLO.BIDOTTI

Valid starting       Expires              Service principal
19/10/2017 15:18:57  20/10/2017 15:18:57  krbtgt/NICOLO.BIDOTTI@NICOLO.BIDOTTI
	renew until 26/10/2017 15:18:57
```
