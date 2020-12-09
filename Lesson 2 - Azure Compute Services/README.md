### Introduction

[![Introduction](https://img.youtube.com/vi/UkXt_e9-SYc/0.jpg)](https://www.youtube.com/watch?v=UkXt_e9-SYc)

### Big Picture: Compute Services

[![Big Picture - Compute Services](https://img.youtube.com/vi/JMbPWOjSCZ8/0.jpg)](https://www.youtube.com/watch?v=JMbPWOjSCZ8)

There are a lot of compute services available through Azure, each with their own use cases. You can check out a good chart for deciding when to use each in the [Microsoft documentation](https://docs.microsoft.com/en-us/azure/architecture/guide/technology-choices/compute-decision-tree?WT.mc_id=udacity_learn-wwl). Some of the available options are:

* Virtual Machines
* App Services
* Azure Batch
* Azure Functions
* Container Instances
* Service Fabric
* Azure Kubernetes Service (AKS)

**Microsoft Learn Resources**

* [Core Cloud Services - Azure compute options](https://docs.microsoft.com/learn/modules/intro-to-azure-compute/?WT.mc_id=udacity_learn-wwl)

### Subscriptions and Resource Groups

[![Subscriptions And Resource Groups](https://img.youtube.com/vi/5LEbboIWNgg/0.jpg)](https://www.youtube.com/watch?v=5LEbboIWNgg)

Azure uses a hierarchical system to keep resources organized and to manage expenses easily.

This starts at the top with your **Azure Account**. The next level down is the **Subscription** level; it's likely in your day-to-day Azure work that you may be working with more than one. For instance, there may be one subscription for development and testing, and another for production systems.

Below the subscription level is where you'll find **Resource Groups**. These help to organize resources you use, such as Virtual Machines and App Services, in order to make resource management easier. You may have a resource group for a specific project, or because resource groups are tied to a **Region**, you may have resource groups containing similar resources in multiple locations across the world. A region contains at least one data center, but could have multiple data centers that are close by and networked together through a low-latency network. There are over 60 regions available worldwide and available in 140 countries, such as East US and Japan West.

![Resource groups can encompass multiple services in a region.](https://video.udacity-data.com/topher/2020/July/5f108911_subscription-resource-group-hierarchy/subscription-resource-group-hierarchy.png)

When choosing a region, it's important to consider what you are trying to achieve. For development and testing purposes, you likely want a region close to yourself; for production purposes, you often want resources to be close to your user. Keep the following in mind:

* Service availability - Some services may not be available in a particular region.
* Performance - Latency determines network service performance; are you creating resources for yourself or your end user?
* Cost - Costs of services vary by region. If latency isn’t an issue, you might want to deploy your services in the cheapest region.


### Exercise - Create a Linux Virtual Machine

**Prerequisite**: If you're using Windows, you’ll need PowerShell or Bash to connect to the VM with ssh. Windows 10 should already have Powershell installed. If you don't have it already installed, here is a [guide](https://docs.microsoft.com/en-us/powershell/scripting/install/installing-powershell-core-on-windows?view=powershell-7&WT.mc_id=udacity_learn-wwls) on how to install it.

1. Create a Linux VM called “linux-vm-west” inside “resource-group-west”. The VM should have the following configurations:

* VM Name: "linux-vm-west"
* Region: West US or the closest region to you that's available
* Availability Options: No infrastructure redundancy required.
* Image: Ubuntu Server (any version)
* Azure Spot instance: No
* Size: Standard B1ls
* Authentication type: Password
* Username: (any username you choose)
* Password: (any password you choose)
* Inbound Port Rules: Allow both 22 and 80

2. After creating the VM, use **secure copy** to copy the `web` directory from [here](https://video.udacity-data.com/topher/2020/July/5f1875e2_create-vm-starter/create-vm-starter.zip) to the VM. 
`scp -r ./web <USERNAME>@<IPADDRESS>:/home/<USERNAME>`

3. After copying the files to the VM, **connect** to it and run the command `ls` to check the `web` directory is on the VM.

4. Next, install `python3-env` and `nginx` 

`sudo apt-get -y update && sudo apt-get -y install nginx python3-venv`

5. Next, configure nginx to listen for incoming traffic on port 80 and set port 3000 as the proxy.

* Navigate to `/etc/nginx/sites-avaiable`
* Remove the `default` file
* Replace it with a file containing:

```
server {
  listen 80;
  location / {
      proxy_pass http://localhost:3000;
      proxy_http_version 1.1;
      proxy_set_header Upgrade $http_upgrade;
      proxy_set_header Connection keep-alive;
      proxy_set_header Host $host;
      proxy_cache_bypass $http_upgrade;
  }
}
```

* After saving the file, restart nginx `sudo service nginx restart`

6. Change to the `web` directory and create and activate a virtual env
7. As a best practice, update pip in a newly created virtual env
8. Install dependencies from **requirements.txt**
9. Run the application and visit the public IP address in your browser. You should see the application running if done correctly.

#### Cleanup

Once you're done with the exercise, be sure to delete the VM and it's resources to avoid incurring unwanted charges.

**Note:** Azure free accounts only allow 750 hours of free hosting. Make sure to delete this VM after completing the exercise to avoid charges.

Supporting Materials
 [create-vm-starter.zip](https://video.udacity-data.com/topher/2020/July/5f1875e2_create-vm-starter/create-vm-starter.zip)
