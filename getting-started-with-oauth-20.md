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

5.	Click save. You can click on the name again to see the details of the API and change any default values if you need to.  The following are the default values:

    1.	Provider type is “APIConnect”, which means APIC will generate the access tokens.
    1.	Scopes: Default is “Scope1”.
    1.	Grants: Both “Application” and “Access Code” grant tyes are enabled by default
    1.	Authorize Endpoint: /oauth2/authorize
    1.	Token Endpoint: /oauth2/token
    1.  APIC Token Secret: oauth-default-key.  This corresponds to the shared secret key object created in DataPower. Toolkit creates a default SS key named “oauth-default-key”. This is not editable from UI at this point. If you need to change this, you have to go to the “definitions” folder in the toolkit and update the yaml, but you should also ensure to create the key file and object in DataPower.
    1.	Access Token TTL: default 3600 seconds
    1.	Maximum consent TTL: default 3600 seconds

6. Start the gateway if it is not already running.

![Image of Datapower Reboot](/images/oauth20/running.png)

7. Once the gateway starts, it will detect that an OAuth Provider Settings object exists and it will auto generate a corresponding API.

![Image of Datapower Reboot](/images/oauth20/provider_exists.png)

This API is like any other API, but in the Assemble action it has an OAuth-generate action that references to the OAuth Provider Settings object.

![Image of Datapower Reboot](/images/oauth20/oauth-generated.png)

Note: Some default parameters and security definitions/requirements are added to this API. But you can edit this API like any other normal API. For example, update the API security definitions or requirements, request and response parameters or add policies to the assembly that needs to be executed before the token generation as per your needs. But you can’t change the base path, authorize endpoint and token endpoint directly in the API. 











