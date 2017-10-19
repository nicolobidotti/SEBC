# Security Lab steps

Sources:
- https://www.cloudera.com/documentation/enterprise/5-9-x/topics/how_to_configure_cm_tls.html#concept_wk4_jlx_qw
- https://stackoverflow.com/questions/21297139/how-do-you-sign-certificate-signing-request-with-your-certification-authority - warning: something in the config file provided in this link breaks the CA... it can't verify itself!

## Preliminary steps

On all hosts, setup JAVA_HOME adn PATH so thet `keytool` is available. Modify `.bash_profile` and add the following:
```bash
export JAVA_HOME=/usr/java/jdk1.7.0_67-cloudera/

PATH=$PATH:$JAVA_HOME/bin
```

(place it **before** `export PATH`)

Create & cd into a work directory: `mkdir securitylabs/ca && cd securitylabs/ca`

## Enable TLS

### Create a CA

Create an openssl configuration file for the CA, `openssl.cnf`, with the following contents:
```
[ ca ]
default_ca    = CA_default      # The default ca section

###################################################################
[ CA_default ]

default_days     = 365         # how long to certify for
default_md       = sha256       # use public key default MD

base_dir      = .
certificate   = $base_dir/cacert.pem   # The CA certifcate
private_key   = $base_dir/cakey.pem    # The CA private key
new_certs_dir = $base_dir              # Location for new certs after signing
database      = $base_dir/index.txt    # Database index file
serial        = $base_dir/serial.txt   # The current serial number

unique_subject = no  # Set to 'no' to allow creation of
                     # several certificates with same subject.

email_in_dn     = no            # Don't concat the email in the DN
copy_extensions = copy          # Required to copy SANs from CSR to cert

####################################################################
[ signing_policy ]
countryName            = optional
stateOrProvinceName    = optional
localityName           = optional
organizationName       = optional
organizationalUnitName = optional
commonName             = supplied
emailAddress           = optional

####################################################################
[ signing_req ]
subjectKeyIdentifier   = hash
authorityKeyIdentifier = keyid,issuer
basicConstraints       = CA:FALSE
keyUsage               = digitalSignature, keyEncipherment
```

Initialize state:
```
touch index.txt
echo '01' > serial.txt
```

Create the CA:
```
openssl req -x509 -newkey rsa:4096 -sha256 -keyout cakey.pem -out cacert.pem -days 365 -nodes -subj "/C=DE/ST=Hesse/L=Frankfurt am Main/O=SEBC/OU=Security Lab/CN=NicoloBidottiCA"
```

## Add the CA to the JDK's trust store

Copy the JDK cacerts file to jssecacerts:
```
sudo env "JAVA_HOME=$JAVA_HOME" cp $JAVA_HOME/jre/lib/security/cacerts $JAVA_HOME/jre/lib/security/jssecacerts
```

**Note:** the Oracle JDK uses the jssecacerts file for its default truststore if it exists. Otherwise, it uses the cacerts file. Creating the jssecacerts file allows you to trust an internal CA without modifying the cacerts file that is included with the JDK.

Import the root CA certificate into the JDK truststore:
```
sudo env "JAVA_HOME=$JAVA_HOME" "PATH=$PATH" keytool -importcert -alias NicoloBidottiCA \
    -keystore $JAVA_HOME/jre/lib/security/jssecacerts \
    -file $(pwd)/cacert.pem -storepass changeit
```

**Note:** the default password for the jssecacerts/cacerts file is "changeit".

## Copy the trust store to all cluster hosts

Copy the trust store to a reachable location:
```
sudo env "JAVA_HOME=$JAVA_HOME" cp $JAVA_HOME/jre/lib/security/jssecacerts ~/securitylabs/jssecacerts
```

Download to your machine: `scp -i ~/Documents/Lavoro/SEBC/sebc.pem centos@sebcmaster:~/securitylabs/jssecacerts .`

Write IPs of the machines to "ips", then run this snippet:
```
TARGETS=""
while read IP
do
    TARGETS="$TARGETS centos@$IP"
done < ips
```

Upload to all hosts:
```
for i in $TARGETS; do scp -i ~/Documents/Lavoro/SEBC/sebc.pem jssecacerts "$i":. ; done
```

Shell on all hosts:
```
clusterssh -o '-i ~/Documents/Lavoro/SEBC/sebc.pem' $TARGETS
```

Copy to proper dir:
```
sudo env "JAVA_HOME=$JAVA_HOME" cp jssecacerts $JAVA_HOME/jre/lib/security/
```

## Create the Cloudera Manager Server's certificate

On the Cloudera Manager Server host, create the directory:
```
sudo mkdir -p /opt/cloudera/security/pki
```

Create the certificate:
```
sudo env "PATH=$PATH" keytool -genkeypair -alias $(hostname -f)-server \
    -keyalg RSA -keysize 2048 \
    -keystore /opt/cloudera/security/pki/$(hostname -f)-server.jks \
    -dname "CN=$(hostname -f),OU=Security Lab,O=SEBC,L=Frankfurt am Main,ST=Hesse,C=DE" \
    -storepass password -keypass password
```

Create a signing request:
```
sudo env "PATH=$PATH" keytool -certreq -alias $(hostname -f)-server \
    -keystore /opt/cloudera/security/pki/$(hostname -f)-server.jks \
    -file /opt/cloudera/security/pki/$(hostname -f)-server.csr \
    -storepass password -keypass password
```

Copy the request over to the CA directory:
```
sudo cp /opt/cloudera/security/pki/$(hostname -f)-server.csr .
```

Sign the certificate:
```
openssl ca -config openssl.cnf -policy signing_policy -extensions signing_req -keyfile cakey.pem -cert cacert.pem -out $(hostname -f)-server.pem -infiles $(hostname -f)-server.csr
```

Append the CA certificate to the server certificate:
```
cat cacert.pem >> $(hostname -f)-server.pem
```

Copy the signed certificate over:
```
sudo cp $(hostname -f)-server.pem /opt/cloudera/security/pki/
```

Import it:
```
sudo env "PATH=$PATH" keytool -importcert -alias $(hostname -f)-server \
    -file /opt/cloudera/security/pki/$(hostname -f)-server.pem \
    -keystore /opt/cloudera/security/pki/$(hostname -f)-server.jks
```

## Create the Cloudera Manager Agents' certificates

On all Cloudera Manager Agent hosts, create the directory:
```
sudo mkdir -p /opt/cloudera/security/pki
```

Create the certificate:
```
sudo env "PATH=$PATH" keytool -genkeypair -alias $(hostname -f)-agent \
    -keyalg RSA -keysize 2048 \
    -keystore /opt/cloudera/security/pki/$(hostname -f)-agent.jks \
    -dname "CN=$(hostname -f),OU=Security Lab,O=SEBC,L=Frankfurt am Main,ST=Hesse,C=DE" \
    -storepass password -keypass password
```

Create a signing request:
```
sudo env "PATH=$PATH" keytool -certreq -alias $(hostname -f)-agent \
    -keystore /opt/cloudera/security/pki/$(hostname -f)-agent.jks  \
    -file /opt/cloudera/security/pki/$(hostname -f)-agent.csr  \
    -ext EKU=serverAuth,clientAuth  \
    -storepass password -keypass password
```

Download all signing requests to your machine, upload to CM host for signing, sign them, download certificates to you machine, upload to all hosts, copy & simlink them following these next steps.

On your machine, write IPs of the machines to "ips", then run this snippet:
```
TARGETS=""
while read IP
do
    TARGETS="$TARGETS centos@$IP"
done < ips
```

Download requests from all hosts:
```
for i in $TARGETS; do scp -i ~/Documents/Lavoro/SEBC/sebc.pem "$i":/opt/cloudera/security/pki/*.csr . ; done
```

Upload to CH host:
```
scp -i ~/Documents/Lavoro/SEBC/sebc.pem *-agent.csr centos@sebcmaster:~/securitylabs/ca
```

On the CM host, sign the certificates:
```
for CSR in *-agent.csr; do openssl ca -config openssl.cnf -policy signing_policy -extensions signing_req -keyfile cakey.pem -cert cacert.pem -out ${CSR::-4}.pem -infiles $CSR; done
```

On your machine, download the signed certificates:
```
scp -i ~/Documents/Lavoro/SEBC/sebc.pem centos@sebcmaster:~/securitylabs/ca/*-agent.pem .
```

Upload all certificates to all hosts (for ease):
```
for i in $TARGETS; do scp -i ~/Documents/Lavoro/SEBC/sebc.pem *-agent.pem "$i":. ; done
```

On each host, copy its own signed certificate over to the pki directory:
```
sudo cp $(hostname -f)-agent.pem /opt/cloudera/security/pki/$(hostname -f)-agent.pem
```

Symlink its own signed certificate:
```
sudo ln -s /opt/cloudera/security/pki/$(hostname -f)-agent.pem /opt/cloudera/security/pki/agent.pem
sudo ln -s /opt/cloudera/security/pki/$(hostname -f)-agent.jks /opt/cloudera/security/pki/agent.jks
```

This allows you to use the same /etc/cloudera-scm-agent/config.ini file on all agent hosts rather than maintaining a file for each agent.

## Enabling TLS/SSL

Follow the steps from https://www.cloudera.com/documentation/enterprise/5-9-x/topics/how_to_configure_cm_tls.html#xd_583c10bfdbd326ba-7dae4aa6-147c30d0933--7a61
up to https://www.cloudera.com/documentation/enterprise/5-9-x/topics/how_to_configure_cm_tls.html#topic_3

# Kerberizing the cluster

## Installing MIT KDC 

## Install (server)

```
sudo yum install krb5-server krb5-workstation
```

## Configure (server)

See krb5.conf.md, kdc.conf.md, kadm5.acl.md

## Init (server)

Create db:
```
sudo kdb5_util create -s
```
Set password to "password".

Setup principals:
```
sudo kadmin.local
```

In the shell, execute:
```
addprinc nicolobidotti/admin
addprinc nicolobidotti
addprinc cloudera-scm/admin
exit
```

Use password "cloudera" for both principals.

## Configure (hosts)

Copy /etc/krb5.conf form the server to all hosts.

## Start

Start & enable services:
```
sudo systemctl start krb5kdc
sudo systemctl start kadmin
sudo systemctl enable krb5kdc
sudo systemctl enable kadmin
```

## Kerberize

Use the wizard in CM.