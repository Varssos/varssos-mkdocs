# Certificates-practical commands

## Extracting pfx file to CA certificate, public key, private key

Let's imagine that you have a `domain.pfx` file. You can use the `openssl` command to extract the CA certificate, public key and private key from it. Each command below will prompt for the pfx password.

CA certificate:
```bash
openssl pkcs12 -in domain.pfx -nodes -nokeys -cacerts -out ca.crt
```

Public key:
```bash
openssl pkcs12 -in domain.pfx -clcerts -nokeys -out cert.crt
```

Private key:
```bash
openssl pkcs12 -in domain.pfx -nocerts -nodes -out private.key
```

## Wget with certs

### Files .crt and .key

If you have such cert files:
```bash
user@user:~/.certs$ ls -la
-rw------- 1 user user 1245 Jul  5 11:48 ca.crt
-rw------- 1 user user 1326 Jul  5 11:48 cert.crt
-rw------- 1 user user 1704 Jul  5 11:49 private.key
```

There is an example of wget:
```bash
wget --ca-certificate=$HOME/.certs/ca.crt --certificate=$HOME/.certs/cert.crt --private-key=$HOME/.certs/private.key 'link'
```

You can create a script to handle this:
```bash
user@user:~# echo '#!/bin/sh
wget --ca-certificate=$HOME/.certs/ca.crt --certificate=$HOME/.certs/cert.crt --private-key=$HOME/.certs/private.key $*' > /bin/wget-ca
user@user:~# chmod +x /bin/wget-ca
```

