---

copyright:
years: 2017
lastupdated: "2017-07-10"
author: "Om Goeckermann"

---
# Windows 10 install of the Toolkit preview
Information References
https://www.npmjs.com/package/apiconnect
https://github.ibm.com/apimesh/apiconnect-mgmt-lite-datapower
https://www.ibm.com/support/knowledgecenter/en/SSMNED_5.0.0/com.ibm.apic.toolkit.doc/tapim_apic_test_with_dpdockergateway.html

## Follow these instructions to prepare an environment for the API Connect Toolkit preview.

Install Node.js VERSIONS 4.4+, or 6 + from https://nodejs.org/en/download/.

Docker CD (Community Edition) (Windows 10, OSX, Linux) v1.13 or higher

### Configuration:
Ensure that you configure Docker to allocate at least 4.0 GB of memory and 2 CPU to the images.

### Installation
1. Start Docker.

2. `cd` to your project directory.

3. Enter `npm cache clean` and then `npm uninstall -g apiconnect`.

4. Enter `npm install apiconnect -g --registry http://apim-ci1.rtp.raleigh.ibm.com:4873`

5. Enter `docker login datapower-docker-local.artifactory.swg-devops.com`.

6. Create a new directory for the required loopback project, and `cd` into it.

7. Install a loopback project when you enter the following.
  ```
  apic loopback
  ```
  Loopback presents a series of choices, select the default for each.

8. Prepare API Connect to use the Toolkit preview Docker image by entering `apic config:set datapower-api-gateway-experimental=true`.

9. Start API Connect Designer by entering `apic edit`.

10. In the API Connect Designer, remove any automatically generated Security Definitions.
   - a. Select the **Design** tab.
   - b. Select **Security Definitions** in the left navigation menu.
   - c. Click the trash symbol to delete, and click `Ok` in the popup confirmation.
   - d. Click the **Save** icon.

![Security Definitions step](https://github.com/ibm-apiconnect/apigateway-experimental/images/security_definitions.png "Security Definitions step")

11. In the API Connect Designer, select DataPower Gateway Policies.
   - Click the **Assemble** tab.
   - Click the **Create assembly** button.
   - Select the **Filter policies** icon (striped triangle).
   - Select the **DataPower Gateway Policies**.
   - Click **Save** to complete the step.

### Result
You are now able to run your tests against the DataPower Gateway.
Refer to the __Getting Started__ tutorials, or documentation for more information.

### Using the DataPower Docker container
To find the URL for DataPower enter `docker ps`.

Find the image with `datapower-api-gateway-v6` or in `/bin/drouter`.

Find the Ports entry with 9090/tcp
    • Example : `0.0.0.0:32769->9090/tcp`

To access the DataPower container, open the web page https://0.0.0.0:32769 in your browser, and log in to `drouter` with the default username/password (`admin`/`admin`).

## Results

```
Successfully built 23d09337f161
Successfully tagged ibm-apiconnect-toolkit/datapower-api-gateway-v6:1.0.52
```

![Return to Top Level](../../)
