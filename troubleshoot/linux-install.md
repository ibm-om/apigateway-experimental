---
copyright:
years: 2017
lastupdated: "2017-08-15"
author: "Om Goeckermann"
comment: "US Government Users Restricted Rights - Use, duplication, or
disclosure restricted by GSA ADP Schedule Contract with IBM Corp."
---
# Linux install of the Toolkit preview
Information References
https://www.npmjs.com/package/apiconnect
https://www.ibm.com/support/knowledgecenter/en/SSMNED_5.0.0/com.ibm.apic.toolkit.doc/tapim_apic_test_with_dpdockergateway.html

## Follow these instructions to prepare an environment for the API Connect Toolkit preview.

Install Node.js VERSIONS 4.4+, or 6 + from https://nodejs.org/en/download/.

Install git. For more information, see: https://help.github.com/articles/set-up-git/.

Ensure that you have installed Docker Community Edition (CE) on Centos and Fedora, or Enterprise Edition (EE)) on Redhat. For more information, see "Download from Docker Store" at https://www.docker.com/community-edition#/download.
    Note: You may need to add $USER to `docker group`. For more information, see:  https://docs.docker.com/engine/installation/linux/linux-postinstall/#manage-docker-as-a-non-root-user


**Note: If you are using a proxy, follow additional instructions at the bottom of the page.**

### To install Docker on Ubuntu follow the steps

Install and verify Docker-Compose version 1.12.0 or higher with the following steps.
  1. Use the Docker-Compose installation instructions at: https://docs.docker.com/compose/install/.
  2. After installation is complete, enter `which docker-compose` and make a note of the Docker-Compose install directory.
  3. Ensure version 1.12.0 or higher is installed by entering `docker-compose –v`.
    Note: If the `-v` output contains version but no build information, replace Docker Compose with the directory information determined in step 2, and instructions found at the following link: https://github.com/docker/compose/releases

You might need to disable your firewall while you are testing API Connect components until you know which ports you need to secure or expose. Your system may be using firewalld, ufw or iptables. Disable them for now.
For example:
    • `sudo ufw disable`
    • `systemctl disable firewalld`
 Note: If you turn off `ufw` (ubuntu firewall), you should renable `ssh` with `sudo ufw allow ssh`. `sudo ufw enable` restores Ubuntu back to defaults.

### Docker Configuration

Ensure that you configure Docker to allocate at least 4.0 GB of memory and 2 CPU to the images.

### Installation
1. Start Docker.

2. `cd` to your project directory.

3. Enter `npm cache clean` and then `npm uninstall -g apiconnect`.

4. Enter `npm install apiconnect -g`.

5. Create a new directory for the required loopback project, and `cd` into it.

6. Install a loopback project when you enter the following.
  ```
  apic loopback
  ```
  Loopback presents a series of choices, select the default for each.

7. Prepare API Connect to use the Toolkit preview Docker image by entering `apic config:set datapower-api-gateway-experimental=true`.

8. Start API Connect Designer by entering `apic edit`.

**Step result:** `Express server listening on http://127.0.0.1:9000...`

9. In the API Connect Designer, remove the automatically generated Security Definitions.
   - a. Select the existing API, and then the **Design** tab.
   - b. Select **Security Definitions** in the left navigation menu.
   - c. Click the [](https://github.com/ibm-apiconnect/apigateway-experimental/images/delete_icon_dark.png "Delete") symbol to delete the existing definitions, and click `Ok` in each popup confirmation.
   - d. Click the **Save** icon [](https://github.com/ibm-apiconnect/apigateway-experimental/images/icon_save.png "Save").

![Security Definitions step](https://github.com/ibm-apiconnect/apigateway-experimental/images/security_definitions.png "Security Definitions step")

10. In the API Connect Designer, select DataPower Policies.
   - Click the **Assemble** tab.
   - Click the **Filter policies** icon [](https://github.com/ibm-apiconnect/apigateway-experimental/images/filter-policies.png "Filter policies") to expose the policies chooser.
   - Ensure that **DataPower Gateway policies** is selected.
   - Click the **Save** icon [](https://github.com/ibm-apiconnect/apigateway-experimental/images/icon_save.png "Save") to complete the step.

11. Click the **Start the servers** icon [](https://github.com/ibm-apiconnect/apigateway-experimental/images/api-designer-run-btn.png "Start the servers").

**Step result:** The status bar of the browser window displays "Running" next to the Gateway and Application IP addresses.

### Using the DataPower Docker Container
To find the DataPower gateway URL, use a new CLI window.
   1. Enter `docker ps`.
      DataPower is associated with the image that contains `datapower-api-gateway-v6` or `/bin/drouter`.
   2. The PORTS entry with `->9090tcp` contains the port where the DataPower gateway can be reached.
      Example: `0.0.0.0:32769->9090/tcp`
   3. Access the DataPower gateway by opening the secure IP `0.0.0.0:port` in your browser.
      Example: `https://0.0.0.0:32769`
   4. Log in to `drouter` with the default username/password (`admin`/`admin`) and use the `default` domain.


## If you are using a proxy
For **Ubuntu 16.04**:

 1. Configure Docker proxy :

 Create the file `/etc/systemd/system/docker.service.d/proxy.conf` with the following 2 lines:
  ```
  [Service]
  Environment="HTTP_PROXY=http://<user:password@><proxy_host><:proxy_port>;" "HTTPS_PROXY= http://<user:password@><proxy_host><:proxy_port>"
  ```

 2. Restart Docker by entering the following commands.
  ```
  sudo systemctl daemon-reload
  sudo systemctl restart docker
  ```

 3. Configure the apk and `npm proxy` in file `node_modules/apiconnect/node_modules/apiconnect-mgmt-lite-datapower/Dockerfile`.

 Before line `RUN apk` add `--no-cache openssl`, add the following two lines:
  ```
  ENV http_proxy http://<user:password@><proxy_host><:proxy_port>;
  ENV https_proxy http://<user:password@><proxy_host><:proxy_port>;
  ```

 Before line `RUN npm install --prod --quiet --depth 0`, add the lines:
  ```
  RUN npm config set proxy $http_proxy
  RUN npm config set https-proxy $https_proxy
  ```


![Return to Top Level](../../)
