---

copyright:
years: 2017
lastupdated: "2017-07-10"
author: "Om Goeckermann"
comment: "US Government Users Restricted Rights - Use, duplication, or
disclosure restricted by GSA ADP Schedule Contract with IBM Corp."
---
## Troubleshooting API Connect Toolkit technology-preview with the DataPower Gateway
The API Connect Toolkit technology-preview allows you to develop APIs on a local machine and test them locally with a DataPower Gateway in the form of a Docker container. Docker-compose assembles and starts DataPower and a minimal API Connect Management Server on the same machine the developer is using. You do not need remote access to DataPower or API Connect Management Server when using the Toolkit.

Troubleshooting usually consists of resolving Docker and Docker Compose installation issues. It is not advised to use installation managers such as Homebrew when you install npm for use with the Toolkit.

 ## Prerequisites:
 **Node**, **npm**, **Docker**, and **Docker Compose** must be installed and operating correctly on your computer to use the Toolkit technology-preview.

**Install Node and NPM**
See: https://github.com/ibm-apiconnect/getting-started/blob/master/toolkit/0-Prereq/README.md)

**OS specific install instructions:**
 | Operating System  | Reference              |
 | _________________ | ______________________ |
 | MacOS             | ![macos-install.md](macos-install.md) |
 | Linux             | ![linux-install.md](linux-install.md) |
 | Windows 10        | ![win10-install.md](win10-install.md) |
 | Windows 7         | ![win7-install.md](win7-install.md)   |

**Configuration Note:**
Ensure that you configure Docker to allocate at least 4.0 GB of memory and 2 CPU to the images.

## Troubleshooting:
see ![Troubleshooting](../troubleshooting.md)
