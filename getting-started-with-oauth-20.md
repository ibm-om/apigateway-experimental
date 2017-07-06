# Getting started with OAuth 2.0 and the new API Gateway

## Overview
The purpose of this guide is to show the user how to setup OAuth in the new API Connect Toolkit.

## Assumptions
The user has succesfully setup the API Connect Toolkit and can test their API's (the README.md file in this project contains the details).

## Steps

### First Step

1. Turn on "experimental mode" in APIC Toolkit 

> ```apic config:set datapower-api-gateway-experimental=true```

2. Set the oauth redirect URI to the localhost so that you may test on your laptop

> ```apic config:set oauth-redirect-uri=https://localhost``` 

4. Edit the configuration

> ``` SKIP_LOGIN=true apic edit```

5. Navigate to the Security Section (Click ```Security'``)

![Image of Datapower Reboot](/images/oauth20/security_section.png)
