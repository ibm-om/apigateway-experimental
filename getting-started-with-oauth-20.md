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

---

### Edit the configuration

> ``` apic edit```

1. Sign in or Register at the login screen

2. Navigate to the Security Section (Click ```Security```)

![Image of Datapower Reboot](/images/oauth20/security_section.png)

3. In the Security Section, ensure OAuth Providers is selected and click the Add button on OAuth Providers.

![Image of Datapower Reboot](/images/oauth20/security-oauth.png)

4. The ```Create OAuth Provider``` screen will appear after clicking the Add button

![Image of Datapower Reboot](/images/oauth20/oauth_provider.png)

5. Provide a name say, ```first-oauth-provider``` and give a Base path, say ```/```.

Note: Base path must be unique. No two OAuth Provider objects can have the same base path. This base path will be used to auto generate an API. ( See next steps)

6.	Click save. You can click on the name again to see the details of the API and change any default values if you need to.  The following are the default values:

    1.	Provider type is “APIConnect”, which means APIC will generate the access tokens.
    1.	Scopes: Default is “Scope1”.
    1.	Grants: Both “Application” and “Access Code” grant tyes are enabled by default
    1.	Authorize Endpoint: /oauth2/authorize
    1.	Token Endpoint: /oauth2/token
    1.  APIC Token Secret: oauth-default-key.  This corresponds to the shared secret key object created in DataPower. Toolkit creates a default SS key named “oauth-default-key”. This is not editable from UI at this point. If you need to change this, you have to go to the “definitions” folder in the toolkit and update the yaml, but you should also ensure to create the key file and object in DataPower.
    1.	Access Token TTL: default 3600 seconds
    1.	Maximum consent TTL: default 3600 seconds

7. Start the gateway if it is not already running.

![Image of Datapower Reboot](/images/oauth20/running.png)

8. Once the gateway starts, it will detect that an OAuth Provider Settings object exists and it will auto generate a corresponding API.

![Image of Datapower Reboot](/images/oauth20/provider_exists.png)

This API is like any other API, but in the Assemble action it has an OAuth-generate action that references to the OAuth Provider Settings object.

![Image of Datapower Reboot](/images/oauth20/oauth-generated.png)

Note: Some default parameters and security definitions/requirements are added to this API. But you can edit this API like any other normal API. For example, update the API security definitions or requirements, request and response parameters or add policies to the assembly that needs to be executed before the token generation as per your needs. But you can’t change the base path, authorize endpoint and token endpoint directly in the API. 

---

### Testing

Now you can send a request to test the Client credentials grant type. Use postman or curl


#### Curl

```
curl -k -X POST \
  'https://127.0.0.1:4002/oauth2/token?client_id=default' \
  -H 'client_id: default' \
  -H 'content-type: application/x-www-form-urlencoded' \
  -d 'client_id=default&client_secret=SECRET&grant_type=client_credentials&scope=scope1'
  ```

Note: A default client is created by the toolkit. Its client_id is “default” and client_secret is “SECRET” 
You should get an access token back:

```
{
  "token_type": "bearer",
  "access_token": "AAIHZGVmYXVsdMeldWS6j1KEm0pi0FRbdRm-aOq9y3nt2l3azyZO9XaK4xmiB6YgY_6GtVBHSo9yiU4F3VD2Qlp_UR7_d8OUew0",
  "scope": "scope1",
  "expires_in": 3600,
  "consented_on": 1498852931
}
```

#### Postman

The following instructions are for retrieving the token using the Postman App, not the Postman Chrome App (installed via the Chrome App Store). Postman can be downloaded from [Postman WebSite](https://www.getpostman.com/)

### Disable SSL certificate verification

1. Click the "wrench" at the upper right corner of Postman, select ```Settings``` when the menu options appear

![Image of Datapower Reboot](/images/oauth20/settings.png)

2. The Settings Window will appear after Selecting ```Settings```, make sure to select the ```General``` tab/section.  Clock the ```X``` at the upper right corner to save and dismiss the screen.

![Image of Datapower Reboot](/images/oauth20/cert-verify.png)

### Create a Request
From the Postman Screen

![Image of Datapower Reboot](/images/oauth20/request.png)


1. Add a new Tab if needed by pressing the ```+``` tab.

2. Change the request from ```GET``` to a ```POST```

3. Add the URL ```https://127.0.0.1:4002/oauth2/token``` at ```Enter request URL```

4. Click the Params button, click ```Bulk Edit``` and enter the following value:

```
client_id:default
```

5. Click the ```Headers``` tab/button, click ```Bulk Edit``` and enter the following value:

```
client_id:default
Content-Type:application/x-www-form-urlencoded
```

The screen should look like this:

![Image of Datapower Reboot](/images/oauth20/post-one.png)

6. Next Click the ```Body``` tab/button. click ```Bulk Edit``` and enter the following value:

```
client_id:default
client_secret:SECRET
grant_type:client_credentials
scope:scope1
```

The screen should look like this
![Image of Datapower Reboot](/images/oauth20/post-two.png)

7. Press the Send button when you want to retrieve the token, check the ```Response``` Window for the token

![Image of Datapower Reboot](/images/oauth20/result.png)

















