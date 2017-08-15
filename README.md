# Api Gateway - Experimental Information and Feedback Repo

## Overview

Welcome to the DataPower API Gateway Github repo.  The purpose of this repo is to **gather feedback** from the new DataPower API Gateway available on Docker.  
To utilze the Gateway, you must use the newest version of the [APIC API Toolkit.](http://link)  

### What is new? 

![Image of Datapower Reboot](/images/DataPower_reboot_small.jpeg)

1. **WISIWIG:** What You See Is What You Get. With the new DataPower API Gateway, there is a one to one relationship between what you drag and drop in the assembly tool and what happens in the gateway.  As you can assume, this greatly increases performance and decreases time debugging, as the developer now knows exactly what should happen on the Gateway.

2. **Enhansed serviceability and performance:** When we first introduced DataPower, we wanted to have a very flexible gateway.  Over the past decade, we have now understand the market, and in particular the needs API providors and consumers, and we have optimized the gateway for the API usecase.  Instead of having APIC and Policies built on top of the Gateway, it is now baked into the gateway. 

3. **Unleash the Power of the Gateway with project level Gateway Configurations:**  The DataPower gateway has so much power, yet, in the past, only a tiny fraction of it has been provided in APIC natively.  Any capability of DataPower will be fairgame in APIC in the future.  For example, if you want to "turn on websockets", you will be able to do that, through API Connect, in the UI, without having to manually configure the gateway.  The full power of DataPower will be available.  

**What does this all mean?** 
You will have a faster, more agile, Gateway, with more capabiltiies. 

![Image of Datapower Reboot](/images/API_gateway_stats.png)

### Give us Feedback!
1. Open new issues with questions, commments, or bugs.
2. We will get back to you ASAP
3. Let us know what you think!  


### How To Try it.

1. You must have the latest version of the API Tool kit: [Link to Toolkit Getting Started](http://link)
2. Get Docker running in your local environment
3. In the command line: Pull down the Experimental API Gateway `text`
4. Turn on "experimental mode" in APIC Toolkit `apic config:set datapower-api-gateway-experimental=true`
5. Follow the rest of the API Tool Kit getting started [text](http://link)

Check out our [Blog](http://link) and a [getting started video](https://link)

![Image of Datapower Reboot](/images/API_Gateway_assembly_tab.png)


### So what is different?
1. First, you will notice there are a few less policies than you may be used to.  This is temporary. We will be adding policies throughout the **tech preview** phase.
2. You can use datapower to test your APIs on your laptop (yeah, thats pretty cool)
3. What you cannot see is the speed and performance... that will come with time!  For now, enjoy!
