```
[libdefaults]
  default_realm = NICOLO.BIDOTTI
  dns_lookup_kdc = false
  dns_lookup_realm = false
  ticket_lifetime = 86400
  renew_lifetime = 604800
  forwardable = true
  default_tgs_enctypes = rc4-hmac
  default_tkt_enctypes = rc4-hmac
  permitted_enctypes = rc4-hmac
  udp_preference_limit = 1
  kdc_timeout = 3000

[realms]
  NICOLO.BIDOTTI = {
    kdc = ip-172-31-12-159.eu-central-1.compute.internal
    admin_server = ip-172-31-12-159.eu-central-1.compute.internal
  }
```