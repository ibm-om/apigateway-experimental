# Getting Started with the DataPower API Gateway (Experimental)

**Authors** 
* [Ozair Sheikh](https://github.com/ozairs)
* [Tony Ffrench](https://github.com/tonyffrench)

**Duration:** 10 minutes

**Prerequisites**
* [API Connect Developer Toolkit](https://developer.ibm.com/apiconnect/getting-started/)  
	* Follow the instructions to install on your laptop.
	* Highly recommended to uninstall previous versions of the API Connect Developer toolkit (`npm uninstall apiconnect -g`)
* [Docker](https://store.docker.com/search?type=edition&offering=community) installed on your workstation.
	* The tutorial assumes you have a basic understanding of docker and its commands
	* Ensure the Docker engine is allocated atleast 4GB of memory
		1. Go to **Preferences** and click on **Advanced**
		2. Move the slider  to  Allocate 4GB of memory
* [curl](https://curl.haxx.se/) or another API testing tool
		
		
In this tutorial, you will learn how to create an API definition using the API Connect Developer toolkit with the new API Gateway on DataPower. This API definition will expose an existing REST service as an API. It will be tested using curl.

**Instructions:** 

1. Before we create an API definition, lets test the backend service that will be used in the tutorial. Go ahead and try it out on a Web browser: [https://myweatherprovider.mybluemix.net/current?zipcode=10504](https://myweatherprovider.mybluemix.net/current?zipcode=10504).  
	```
	{
		"zip":10504,
		"temperature":75,
		"humidity":64,
		"city":"Armonk, North Castle",
		"state":"New York",
		"message":"Sample Randomly Generated"
	}
	```
	Now we know the backend service is up, let's create an API definition to expose it as an API!

2. Using the command prompt, create a directory on your workstation.
	```
	mkdir apigateway
	cd apigateway
	```

3. Configure the API Connect Developer Toolkit to use the new experimental API Gateway. This command tells the toolkit to use the experimental DataPower Gateway instead of the default one already available today.
	
	`apic config:set datapower-api-gateway-experimental=true`	

4. Open the API designer and signin with your IBM Id. Follow the prompts to create a new IBMid if you don't have one already.

	`apic edit &`

5. Create an API definition. Click **Add+ -> New API** and enter the following information
	* Title: weather-service
	* Name: weather-service
	* Base Path: /api

6. Click **Create API** button. It will take you to the API designer page where you can configure additional information about your API.

7. In the left nav bar, click **Paths**. Click the + button and configure a new path called `current`.

8. Click the **Assemble** tab at the top. Select the toggle for **DataPower Gateway policies**. The policies will update to reflect policies available on the DataPower API Gateway.

9.  You should see a policy called **Invoke** in the editor. Click on the policy and modify the URL to **https://myweatherprovider.mybluemix.net/current?zipcode=90210**. Click the Save icon (at the top right-hander corner) once complete.

10. Start the Gateway by clicking the **Play** button at the bottom. Wait till the gateway is fully started - it may take a minute or so. The first time you start Gateway, it will install the pre-requisite components - two docker containers. 

	**Note**: 

	* You can manually start / stop the API gateway with the commands `apic services:start` and `apic services:stop`. These command must be executed in the directory where you opened the API Connect developer toolkit `apic edit`.

11. Switch back to the command prompt and enter the command `docker ps` to examine the API Gateway docker containers.

  ```
CONTAINER ID        IMAGE                                                      COMMAND                  CREATED             STATUS              PORTS                                                                                             NAMES
093b72c62dc0        ibm-apiconnect-toolkit/datapower-api-gateway-v6:1.0.10     "/bin/drouter"           21 seconds ago      Up 20 seconds       0.0.0.0:32838->80/tcp, 0.0.0.0:32837->5554/tcp, 0.0.0.0:32836->9090/tcp, 0.0.0.0:4001->9443/tcp   apigateway_datapower-api-gateway_1
69e413b928a6        ibm-apiconnect-toolkit/datapower-gateway-director:1.0.10   "node lib/gateway-..."   22 seconds ago      Up 21 seconds       0.0.0.0:32835->2443/tcp                                                                           apigateway_datapower-gateway-director_1
  ```
   The `ibm-apiconnect-toolkit/datapower-api-gateway` container is the DataPower Gateway that executes the policies. The Web GUI can be viewed using the mapped 9090 port with credentials `admin/admin`. The `ibm-apiconnect-toolkit/datapower-gateway-director` simulates the API manager capabilities.

12. APIs are protected using an API key. A default API key is provided for quick testing. Run the following `curl` command to test the API definition:

	```
	curl https://127.0.0.1:4001/api/current -H "X-IBM-Client-Id: default" -k

	{"zip":10504,"temperature":95,"humidity":57,"city":"Armonk, North Castle","state":"New York","message":"Sample Randomly Generated"}
	```
Congratulations! You have successfully created an API definition using the new DataPower API Gateway.

**So what is different?**

First, you will notice there are a few less policies than the currently supported release. This is temporary. We will be adding policies throughout the tech preview phase.

You can use datapower to test your APIs on your laptop (yeah, thats pretty cool)
What you cannot see is the speed and performance... that will come with time! For now, enjoy!