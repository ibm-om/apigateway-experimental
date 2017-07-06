# Getting started with OAuth 2.0 and the new API Gateway

## Overview
The purpose of this guide is to show the user how to setup OAuth in the new API Connect Toolkit.

## Assumptions
The user has succesfully setup the API Connect Toolkit and can test their API's (the README.md file in this project contains the details).

## Steps

### Enable Experimental Mode

1. Turn on "experimental mode" in APIC Toolkit 

> ```apic config:set datapower-api-gateway-experimental=true```

2. Set the oauth redirect URI to the localhost so that you may test on your laptop

> ```apic config:set oauth-redirect-uri=https://localhost``` 

### Edit the configuration

> ``` SKIP_LOGIN=true apic edit```

1. Navigate to the Security Section (Click ```Security```)

![Image of Datapower Reboot](/images/oauth20/security_section.png)

2. In the Security Section, ensure OAuth Providers is selected and click the Add button on OAuth Providers.

![Image of Datapower Reboot](/images/oauth20/security-oauth.png)

3. The ```Create OAuth Provider``` screen will appear after clicking the Add button

![Image of Datapower Reboot](/images/oauth20/oauth_provider.png)

4. Provide a name say, ```first-oauth-provider``` and give a Base path, say ```/```.
Note: Base path must be unique. No two OAuth Provider objects can have the same base path. This base path will be used to auto generate an API. ( See next steps)

5.	Click save. You can click on the name again to see the details of the API and change any default values if you need to.

