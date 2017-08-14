---

copyright:
years: 2017
lastupdated: "2017-07-27"
author: "Om Goeckermann"
comment: "US Government Users Restricted Rights - Use, duplication, or
disclosure restricted by GSA ADP Schedule Contract with IBM Corp."
---

## Troubleshooting:

### Guides for specific operating systems

| Operating System | Reference             |
| ________________ | _____________________ |
| MacOS            | ![/troubleshoot/macos-install.md](macos-install.md) |
| Linux            | ![/troubleshoot/linux-install.md](linux-install.md) |
| Windows 10       | ![/troubleshoot/win10-install.md](win10-install.md) |
| Windows 7        | ![/troubleshoot/win7-install.md](win7-install.md) |

### Stages of installation
The API Connect Toolkit technology-preview automates a substantial portion of the gateway installation process. In general, the stages are as follows.
     Platform detection
     System Validation
     Downloading and building the gateway
     Starting gateway process

- Platform detection is self evident.
- System validation examines for the existence of prerequisite conditions. The output indicates which conditions need to be met.
- Downloading and building the gateway involves data transfer of less than 500Mb.
- Starting gateway process can respond with alerts that indicate how the process ended. A good first step to resolving the issue is to ensure that the prerequisites are met and functioning before installing the Toolkit preview.


### Docker related issues
**Messages when the Gateway does not initialize:**
1. Docker not found
2. Docker daemon not running
3. Docker not accessible
4. Bad version
5. Insufficient CPU resources
6. Insufficient memory resources

These alerts are resolved by following the installation directions and documentation at http://docker.com to ensure that the prerequisite steps are completed.

### NPM related issues
 - The **npm** setting `--engine-strict` or `npm config set engine-strict true` prevents a complete installation.

- Expect one, or a few, failure notices to display during `npm install -g apiconnect`, the installation process is not typically affected.


### All platforms
API Connect Toolkit preview expects to find a loopback directory inside the project directory where API Connect is running from. Ensure that the following steps were accomplished.
      - 1. Create a directory within your project directory.
      - 2. Step into, or `cd` into this new directory.
      - 3. Run `apic loopback`.
      - 4. Accept the default selection to each loopback install prompt.
