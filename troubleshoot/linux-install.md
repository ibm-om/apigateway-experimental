---

copyright:
years: 2017
lastupdated: "2017-07-10"
author: "Om Goeckermann"

---
# Linux install of the Toolkit preview
Information References
https://www.npmjs.com/package/apiconnect
https://github.ibm.com/apimesh/apiconnect-mgmt-lite-datapower
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
   - a. Click the **Assemble** tab.
   - b. Click the **Create assembly** button.
   - c. Select the **Filter policies** icon (striped triangle).
   - d. Select the **DataPower Gateway Policies**.
   - e. Click **Save** to complete the step.

### Using the DataPower Docker Container

To find the URL for DataPower enter `docker ps`.

Find the image with `datapower-api-gateway-v6` or in `/bin/drouter`.

Find the Ports entry with 9090/tcp
    • Example : `0.0.0.0:32769->9090/tcp`

To access the DataPower container, open the web page https://0.0.0.0:32769 in your browser, and log in to `drouter` with the default username/password (`admin`/`admin`).

## Results
The successful build will produce output similar to the following.
 ```
 Successfully built 23d09337f161
 Successfully tagged ibm-apiconnect-toolkit/datapower-api-gateway-v6:1.0.52
 ```

## If you are using a proxy
For Ubuntu 16.04:

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
