---
copyright:
years: 2017
lastupdated: "2017-07-10"
author: "Om Goeckermann"
comment: "US Government Users Restricted Rights - Use, duplication, or
disclosure restricted by GSA ADP Schedule Contract with IBM Corp."
---
## Adding a TLS profile to use with the Invoke policy:

### Introduction
The TLS profile can be added to your project as a file in YAML format. You can refer to the defined TLS Profile in an invoke action to enable server
verification, and optionally, client verification.

### The YAML file
The YAML file defining a TLS profile should have the following keys:

**name:** the TLS profile name corresponding to the name used in the Invoke policy.

**title:** a human-readable description of the purpose of this profile.

**public:** a Boolean value indicating if the profile will be shared across API Manager and the Cloud Manager.

**ciphers:** an array of cipher names acceptable with this profile.  
  possible values:  
    SSL_RSA_WITH_AES_256_CBC_SHA  
    SSL_RSA_WITH_AES_128_CBC_SHA  
    SSL_RSA_WITH_3DES_EDE_CBC_SHA  
    SSL_RSA_WITH_RCA_128_SHA  
    SSL_RSA_WITH_RCA_128_MD5  

**protocols:** an array of TLS versions acceptable with this profile.  
  possible values:  
    SSLv2  
    SSLv3  
    TLSv1  
    TLSv11  
    TLSv12  
 
**features:** an array of TLS features of this profile.  
  possible values:  
    DISABLE_SNI  
    PERMIT_INSECURE_SSL  
    ENABLE_COMPRESSION  

**certs:** an array of objects describing certificates used by this profile. Each object contains the following:
  **name:** generic name for the certificate
  **cert-type:** either CLIENT to indicate CA certificate verifying target URL or PUBLIC to indicate client certificate.
  **cert:** content of the certificate in PEM format or an object with the key `$ref` pointing to the file containing the certificate.

**mutual-auth:** a Boolean value indicating if mutual authenticate should be enabled for this profile.

**private-key:** content of the private key corresponding to the client certificate in PEM format, or an object with the key `$ref` pointing to the file containing the private key.

EXAMPLE YAML FILE: tls-profile.yaml
```
name: secure-loopback
title: 'TLS Profile with Mutual Auth'
public: false
ciphers:
    SSL_RSA_WITH_AES_256_CBC_SHA
    SSL_RSA_WITH_AES_128_CBC_SHA
    SSL_RSA_WITH_3DES_EDE_CBC_SHA
    SSL_RSA_WITH_RCA_128_SHA
    SSL_RSA_WITH_RCA_128_MD5
protocols:
    TLSv1
    TLSv11
    TLSv12
features:
    DISABLE_SNI
certs:
    name: Certificate
    cert:
    $ref: cacert.pem
    cert-type: CLIENT
    name: Certificate
    cert:
    $ref: client.pem
    cert-type: PUBLIC
mutual-auth: true
private-key:
    $ref: client.key
```
