## Introduction

[![Introduction](https://img.youtube.com/vi/UkXt_e9-SYc/0.jpg)](https://www.youtube.com/watch?v=UkXt_e9-SYc)

![The Course and Lesson Outline.](https://video.udacity-data.com/topher/2020/July/5f10a6cb_course-outline-compute/course-outline-compute.png)

## Big Picture: Compute Services

[![Big Picture - Compute Services](https://img.youtube.com/vi/JMbPWOjSCZ8/0.jpg)](https://www.youtube.com/watch?v=JMbPWOjSCZ8)

There are a lot of compute services available through Azure, each with their own use cases. You can check out a good chart for deciding when to use each in the [Microsoft documentation](https://docs.microsoft.com/en-us/azure/architecture/guide/technology-choices/compute-decision-tree?WT.mc_id=udacity_learn-wwl). Some of the available options are:

* Virtual Machines
* App Services
* Azure Batch
* Azure Functions
* Container Instances
* Service Fabric
* Azure Kubernetes Service (AKS)

### QUIZ QUESTION

Which of the following are Azure compute services?

[x] Virtual Machines
[] Key Vault
[x] App Service
[] SQL Database
[x] Azure Functions

**Microsoft Learn Resources**

* [Core Cloud Services - Azure compute options](https://docs.microsoft.com/learn/modules/intro-to-azure-compute/?WT.mc_id=udacity_learn-wwl)

## Subscriptions and Resource Groups

[![Subscriptions And Resource Groups](https://img.youtube.com/vi/5LEbboIWNgg/0.jpg)](https://www.youtube.com/watch?v=5LEbboIWNgg)

Azure uses a hierarchical system to keep resources organized and to manage expenses easily.

This starts at the top with your **Azure Account**. The next level down is the **Subscription** level; it's likely in your day-to-day Azure work that you may be working with more than one. For instance, there may be one subscription for development and testing, and another for production systems.

Below the subscription level is where you'll find **Resource Groups**. These help to organize resources you use, such as Virtual Machines and App Services, in order to make resource management easier. You may have a resource group for a specific project, or because resource groups are tied to a **Region**, you may have resource groups containing similar resources in multiple locations across the world. A region contains at least one data center, but could have multiple data centers that are close by and networked together through a low-latency network. There are over 60 regions available worldwide and available in 140 countries, such as East US and Japan West.

![Resource groups can encompass multiple services in a region.](https://video.udacity-data.com/topher/2020/July/5f108911_subscription-resource-group-hierarchy/subscription-resource-group-hierarchy.png)

When choosing a region, it's important to consider what you are trying to achieve. For development and testing purposes, you likely want a region close to yourself; for production purposes, you often want resources to be close to your user. Keep the following in mind:

* Service availability - Some services may not be available in a particular region.
* Performance - Latency determines network service performance; are you creating resources for yourself or your end user?
* Cost - Costs of services vary by region. If latency isn’t an issue, you might want to deploy your services in the cheapest region.

### Creating a Resource Group in the Azure Portal

[![Walkthrough - Resource Group](https://img.youtube.com/vi/_9nHPP0gixc/0.jpg)](https://www.youtube.com/watch?v=_9nHPP0gixc)

To set up a resource group in the Azure Portal:

* Go to the [Azure Portal homepage](https://portal.azure.com/#home)
* Click "Create a Resource Group"
* Search for "Resource group" and click "Create"
* You'll need to select the subscription for the resource group, name it, and select a region
* Make sure once you select "Review and create" to actually review the information! While it doesn't take too much time to go back and create a new resource group, you'll want to check for any typos in the name or if the wrong region was selected. When we work out of Azure CLI later, this becomes even more important, as you could cause other scripts to fail if things are named incorrectly or are in an inappropriate region.
* Click "Create" once you are done reviewing.

### QUIZ

Why is choosing the appropriate region (or deploying to multiple regions) for your resources important?

[x] Some services may only be available in certain regions.

[x] Some pricing tiers are only available in certain regions.

[x] Users located closer to the resources will experience less latency.

[] You should always choose the options closest to you.

### QUIZ

Match each of the below terms to their respective definitions.

* **[Subscription]:** Billing and policies for resources are grouped at this level.
* **[Region]:** Where resources are located in the world.
* **[Resource Group]:** Oftentimes, used to group together resources related to a single application to help with management.

### Microsoft Learn Resources

* [Manage resources in Azure](https://docs.microsoft.com/learn/paths/manage-resources-in-azure/?WT.mc_id=udacity_learn-wwl)
* [Move Azure resources to another resource group](https://docs.microsoft.com/learn/modules/move-azure-resources-another-resource-group/?WT.mc_id=udacity_learn-wwl)
* [Control and organize Azure resources with Azure Resource Manager](https://docs.microsoft.com/learn/modules/control-and-organize-with-azure-resource-manager/?WT.mc_id=udacity_learn-wwl)
* [Create ARM templates](https://docs.microsoft.com/learn/modules/build-azure-vm-templates/?WT.mc_id=udacity_learn-wwl)

## Exercise: Create a Resource Group

* Create a Resource Group named **resource-group-west** in [Azure](https://www.portal.azure.com/) in the **West US** region.

Resource Groups are fully covered in the Azure free account.

[![Solution - Subscriptions And Resource Groups](https://img.youtube.com/vi/rmWRvxY0Hh8/0.jpg)](https://www.youtube.com/watch?v=rmWRvxY0Hh8)

### Steps to Create a Resource Group using the Azure CLI:

1. Log in using `az login`.
2. We'll use the Azure CLI command `az group create` and pass in two flags:
* resource group `--name`
* `--location` which is the same as the "region" field on the Azure portal.
3. If you want to see a list of all locations, you can run `az account list-locations -o table` to output the list in table format.
4. I want to create my resource group in the West US 2 region:

`az group create --name resource-group-west --location westus2`

The resource group will be created and a JSON response will be returned with the status.

### Azure CLI Documentation

You can reference the [Azure CLI documentation](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest&WT.mc_id=udacity_learn-wwl) for further information on other commands.

## Virtual Machines vs. App Services

[![Virtal Machines Vs. App Services](https://img.youtube.com/vi/zvSHartWx9g/0.jpg)](https://www.youtube.com/watch?v=zvSHartWx9g)

### Virtual Machines

**Azure Virtual Machines** (VMs) provide infrastructure as a service (IaaS) by allowing you to create and use virtual machines in the cloud.

Some of the benefits of VMs are:

* VMs allow you full access and control of the VM.
* Lower up-front cost compared to purchasing and maintaining hardware.
* Support of both Linux and Windows VMs.
* Multiple types to choose from, such as compute or memory-optimized VMs, along with varying amounts of CPU, RAM and storage.
* VMs allow for the installation of custom images and are an excellent choice for migrating from an on-premises server to the cloud.
* Multiple VMs can be grouped to provide high availability, scalability, and redundancy. There are two options when it comes to scaling—Virtual Machine Scale Sets and Load Balancers. These will be covered in a different course.

Some of the limitations of VMs are:

*  They are more expensive
*  They can be more time consuming for the developer than other compute options

### App Service

**Azure App Service** is an HTTP-based service for hosting web applications, REST APIs, and mobile back ends. It is a Platform as a Service (PaaS) that allows a developer to focus on the application while Azure takes care of the infrastructure.

Some of the benefits of using an App Service are:

* Support of multiple languages, such as .NET, .NET Core, Java, Ruby, Node.js, PHP, or Python
* High availability, auto-scaling and support of both Linux and Windows environments.
* Continuous deployment model using GitHub, Azure DevOps, or any Git repo.
* Vertical or Horizontal scaling. Vertical scaling increases or decreases resources allocated to our App Service, such as the amount of vCPUs or RAM, by changing the App Service pricing tier. Horizontal scaling increases or decreases the number of Virtual Machine instances our App Service is running.
* You can set the amount of hardware allocated to host your application, and cost varies based on the plan you choose. There are three different tiers - Dev/Test, Production, and Isolated. We’ll be using the free option within Dev/Test for the exercises in this course.

Some of the limitations of an App Service are:

* You have limited access to the host server, so you are unable to control the underlying OS or install software on the server.
* You’re always paying for the service plan, even if your services or application isn’t running.
* There are hardware limitations, such as a maximum of 14GB of memory and 4 vCPU cores per instance
* While they support multiple languages, as noted in the benefits above, they are limited to just using those languages (as of when this course was built).

### Use Cases

Each of these has their own use cases, although sometimes there is still some ambiguity on when to use each. Virtual Machines are usually better when you need control of the underlying operating system or are using custom software to support your needs; an app service is typically better for lightweight applications and services, especially when you don't have the need for high performance compute services. Additionally, you'll need to take into consideration the hardware limitations of App Services, as noted above.

### QUIZ

Match the below features to which compute service they relate.

* **[Virtual Machine]:** IaaS option giving the developer complete control over deployment and the technology stack of the operating system. Provides tiers getting into substantially more memory and CPU cores.
* **[App Service]:** PaaS option allowing the developer to focus on app development while receiving less control over the deployment pipeline. Tiers provide less memory and CPU cores.
* **[Neither]:** Able to deploy containerized apps onto Kubernetes clusters.

## Exercise: Virtual Machines vs. App Services

For each of the three scenarios below, analyze and determine whether a virtual machine or an app service would be best served for the situation. It's important to note that this involves some level of ambiguity - you should feel free to expand beyond the given scenario and consider any other areas that might be important in making your decision.

### Scenario 1

> *Your company wants to deploy a series of lightweight APIs as part of their plan to shift to using microservices in the future. The company is very cost-conscious due to the current economic environment, and wants to focus on using the correct services right now, and is less concerned about scaling concerns due to stagnant growth.*

Some key points that stood out to me were:

* Deploying a series of lightweight APIs
* Less concern about scaling up processing power
* Cost-consciousness

I would choose an **App Service** in this situation. Lightweight APIs tend to be well-suited to App Services over VMs, and won't approach the size limit for App Services very easily. Additionally, App Services cost less than VMs do. Lastly, since the ability to scale quickly is less of a concern, we don't need to factor that into the analysis.

As the company shifts into microservices, Azure Functions would also be a good compute option for them to consider, but that won’t be covered until a later course.

### Scenario 2

> *Your company has recently signed a sizable government contract in which you will deploy various apps for the related government departments to use. The contract was a big win for the company, as it vastly increases the number of users of your apps. Additionally, the contract does contain provisions that require dedicated servers for security reasons to host any of the government department's services and information. Relatedly, some of the different departments' applications are required to be maintained on different servers.*

A couple of key points that stood out to me were:

* A vast increase in the number of users
* The need for dedicated servers for security reasons

This situation is likely best for **Virtual Machines**. Handling the vast increase in the number of users, with separate, dedicated servers, is going to be better achieved this way.

### Scenario 3

> *You have been assigned to determine the cloud needs for a new product your company will soon be launching. In the past couple of years, your company has been on a roller coaster ride - some product launches meet massive success, while others flounder pretty quickly out of the gates. As such, the product manager is a bit wary of immediately creating a bunch of resources without knowing for sure what the real demand for this new product will be. The application currently utilizes ~5 GB on 2 CPUs during your stress testing, but is definitely a minimum viable product, and could grow vastly in size and compute resources if successful.*

This is a bit of a tough one - it's important to remember that in real-life situations, there may not always be a clear dividing line on exactly which service is best.

Some key points that stood out to me were:

* *he confidence level of this application being a massive success seems low (do we want to assume we'll need a lot of scaling?)
* The application currently utilizes ~5 GB on 2 CPUs during stress testing
* The potential the app will grow in resource needs

The answer here depends greatly on which of the above points you highlight. *In the current situation*, an App Service likely works fine - it can scale vertically to meet different demand levels, and the compute resources needed are well within App Service limits. However, there's some consideration that Virtual Machines may be necessary in the near future if many more features are added, or demand changes in a way that requires vertical scaling. In fact, I'd argue that the problem so far is a bit ill-defined - I'd want to know what level of control we need over the underlying OS, security requirements we have, etc.

[![Solution - Virtual Machines Vs. App Services](https://img.youtube.com/vi/B2LuN50DtAs/0.jpg)](https://www.youtube.com/watch?v=B2LuN50DtAs)

## Creating a Virtual Machine

[![Creating A Virtual Machine Part 1](https://img.youtube.com/vi/ngD-D9XBPw4/0.jpg)](https://www.youtube.com/watch?v=ngD-D9XBPw4)

The steps I took to create a Linux Virtual Machine on Azure were:

1. On the homepage, click "Create a resource"
2. Click on "Compute" in the left menu
3. Click on "Virtual Machine"
4. Create a Linux VM with the following details:

* Subscription: This will vary for you. Should default to your subscription.
* Resource Group: "hello-world-rg"
* VM Name: "linux-vm-west"
* Region: West US 2 or a region closest to you that's available
* Availability Options: Default option of "No infrastructure redundancy required" is fine here.
* Image: Ubuntu Server (any version) but I'm going to use the latest version 18.04 LTS
* Azure Spot instance: No
* Size: Click on "Select Size" and select "Standard B1ls"
* Authentication type: Password
* Username: (any username you choose) something other than the default "AzureUser" 
* Password: (any password you choose)
* Inbound Port Rules: "Allow Select Ports" and make sure from the drop-down menu, 22 and 80 are selected.

[![Creating A Virtual Machine Part 2](https://img.youtube.com/vi/Ty_ZR_E6Ukg/0.jpg)](https://www.youtube.com/watch?v=Ty_ZR_E6Ukg)

To connect to the created VM, I did the following (note that Windows users should use PowerShell or Bash):

1. We'll need our admin username we set when creating the VM.
2. We'll need the public IP address of our VM. You can use the following command to grab the IPs addresses for a particular VM from the CLI `az vm list-ip-addresses -g <RESOURCE-GROUP> -n <VIRTUAL-MACHINE-NAME>` or use Azure portal.
3. Next, we're going to copy a basic Flask app from my local machine to the VM. We'll be using the secure copy utility `scp -r <SOURCE-DIR> [ADMIN-NAME]@[PUBLIC-IP]:<TARGET-DIR>`. In this example, I used `scp -r ./web <username>@IPADDRESS:/home/<username>`. 

**NOTE:** The first time you try connecting to the VM, you'll see a similar message to the one below and should answer 'yes' to permanently add the IP address to the list of known hosts.

> *The authenticity of host '52.191.135.139 (52.191.135.139)' can't be established.*
> *ECDSA key fingerprint is SHA256:7bBVTsYNImhXxAn+xscCHm/OkcodHZS615VSKO3GP8c.*
> *Are you sure you want to continue connecting (yes/no)?*

4. Once the files have been copied to the VM, we can connect to the VM using
`ssh [ADMIN-NAME]@[PUBLIC-IP]`

5. We can use `ls` to see the web directory we just uploaded
6. Python 3 is already installed on the VM. We'll install Python Virtual Environment and NGNIX to use as a reverse proxy 
`sudo apt-get -y update && sudo apt-get -y install nginx python3-venv`
7. Before we run the app, we have to configure Nginx to redirect all incoming connections on port 80 to our app that is running on localhost port 3000

* By default, Nginx has a default page that is displayed. If you visit the public IP address in your browser, you should see this page rendered.
* We'll navigate to the **/etc/nginx/sites-available** directory
`cd /etc/nginx/sites-available`
* We’ll first unlink the default site using 
`sudo unlink /etc/nginx/sites-enabled/default`
* Then we’ll create a new file **reverse-proxy.conf** in the **/etc/nginx/sites-available**
`sudo vim reverse-proxy.conf`
* We're going to add the following code to this file:

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

Now we’ll activate the directories by creating a sym link to the **/sites-enabled** directory 

`sudo ln -s /etc/nginx/sites-available/reverse-proxy.conf /etc/nginx/sites-enabled/reverse-proxy.conf`

* We have to restart nginx so the changes take effect. `sudo service nginx restart`

8. cd to `web`
9. Create venv `python3 -m venv venv`
10. Activate the env `source venv/bin/activate`
11. Upgrade pip in our virtual environment and then Install dependencies 
`pip install --upgrade pip``
`pip install -r requirements.txt`
12. We'll run our app `python application.py`
13. In a web browser, we can visit the public IP address of the VM and you should see the application
14. Type "exit" to disconnect from the VM

**Note:** Azure free account only allows 750 hours of free hosting. Make sure to delete this VM after creation for any exercises to avoid charges.

### Cleanup
If we no longer need a resource, we can delete them through the portal.

1. From the homepage, click on "Resource Group"
2. Click on the resource group you want to manage
3. You have two options—"Delete resource group" or if you want to keep the resource group, you can click on the individual or collection of resources you want to delete and click on "Delete"

### QUIZ

Put the steps of deploying an app to a Virtual Machine in Azure in the appropriate order.

1. Create or utilize a resource group
2. Create the Virtual Machine
3. Connect to the VM
4. Install any dependencies.
5. Run the application.

### QUIZ

You've gone through all the steps for creating a Virtual Machine and deploying an app to it, and everything appears to be working from within the VM itself. However, when you navigate to the public IP address, it gives a connection error. Which of the following is a likely cause of the issue?

[] You need to turn off the VM's firewall
[] You forgot to add a required library in the app's virtual environment
[] The VM has a bug and needs to be restarted
[x] You need to make sure the VM is listening to port 80.

### Microsoft Learn Resources

* [Introduction to Azure virtual machines](https://docs.microsoft.com/learn/modules/intro-to-azure-virtual-machines/?WT.mc_id=udacity_learn-wwl)
* [Create a Linux virtual machine in Azure](https://docs.microsoft.com/learn/modules/create-linux-virtual-machine-in-azure/?WT.mc_id=udacity_learn-wwl)
* [Deploy a website with Azure virtual machines](https://docs.microsoft.com/learn/paths/deploy-a-website-with-azure-virtual-machines/?WT.mc_id=udacity_learn-wwl)

## Exercise - Create a Linux Virtual Machine

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

### Cleanup

Once you're done with the exercise, be sure to delete the VM and it's resources to avoid incurring unwanted charges.

**Note:** Azure free accounts only allow 750 hours of free hosting. Make sure to delete this VM after completing the exercise to avoid charges.

#### Supporting Materials

[create-vm-starter.zip](https://video.udacity-data.com/topher/2020/July/5f1875e2_create-vm-starter/create-vm-starter.zip)


### Solution: Creating a Virtual Machine

[![Solution - Creating A Virtual Machine Part 1](https://img.youtube.com/vi/a5gKkVARnXU/0.jpg)](https://www.youtube.com/watch?v=a5gKkVARnXU)

This is an alternative way to create a Linux VM using Azure CLI. Use whichever method you feel more comfortable with moving forward. Connecting to the VM is done the same way in both instances.

1. First, we'll login using `az login`
2. Next, we'll create our VM using `az vm create`. If we don't pass a location, it defaults to the location of the resource group. This would be fine in most cases, but it's worth noting that sometimes a VM size might not be available in the same region as your resource group, so you'd have to pass in a location for a different region.

```
az vm create \
   --resource-group "resource-group-west" \
   --name "linux-vm-west" \
   --location "westus2" \
   --image "UbuntuLTS" \
   --size "Standard_B1ls" \
   --admin-username "udacityadmin" \
   --generate-ssh-keys \
   --verbose
```

3. Upon success, you will have a JSON response.
4. Next we will open port 80 to allow outside traffic to our VM

```bash
az vm open-port \
    --port "80" \
    --resource-group "resource-group-west" \
    --name "linux-vm-west"
```

5. Upon success, you will receive a JSON response.

### Connecting to the VM

1. We'll need the admin username we set when creating the VM
2. We'll need the public IP address of our VM. You can use the following command to grab the IP address for a particular VM from the CLI. 
`az vm list-ip-addresses -g resource-group-west -n linux-vm-west`
3. Next we're going to copy a basic Flask app from my local machine to the VM. We'll be using the [secure copy utility](http://www.hypexr.org/linux_scp_help.php).
`scp -r ./web <username>@IPADDRESS:/home/<username>`
4. Now we can connect to the VM with `ssh [username]@[IP Address]` 
**Note:** Since we generated SSH keys, you won't be prompted for a password.
5. Run `ls` to see the web directory we just uploaded
6. Python 3 is already installed on the VM. We'll install Python Virtual Environment and NGNIX to use as a reverse proxy 
`sudo apt-get -y update && sudo apt-get -y install nginx python3-venv`
7. Before we run the app, we have to configure Nginx to redirect all incoming connections on port 80 to our app that is running on localhost port 3000

* By default, Nginx has a default page that is displayed. If you visit the public IP address in your browser, you should see this page rendered.
* We'll navigate to the **/etc/nginx/sites-available** directory
`cd /etc/nginx/sites-available`
* We’ll first unlink the default site using 
`sudo unlink /etc/nginx/sites-enabled/default`
* Then we’ll create a new file **reverse-proxy.conf** in **/etc/nginx/sites-available**
`sudo vim reverse-proxy.conf`
* We're going to add the following code to this file:
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

8. Now we’ll activate the directories by creating a sym link to the **/sites-enabled** directory `sudo ln -s /etc/nginx/sites-available/reverse-proxy.conf /etc/nginx/sites-enabled/reverse-proxy.conf`
* We have to restart nginx so the changes take effect. 
`sudo service nginx restart`

### Deploying the App to the VM

This section is the same as the earlier walkthrough.

To deploy the app on the virtual machine, I did the following:

1. CD to `web`
2. Create `venv python3 -m venv venv`
3. Activate the env `source venv/bin/activate`
4. Upgrade pip in our virtual environment and then Install dependencies
`pip install --upgrade pip pip install -r requirements.txt`
5. We'll run our app `python application.py`
6. In a web browser, we can visit the public Ip address
7. Type "exit" to disconnect from the VM

### Cleanup

If we no longer need a resource, we can delete them through the portal. The quickest way to do this from the CLI is to delete the resource group. This will delete all resources in that group

`az group delete -n resource-group-west`

## Creating an App Service

 [![Creating An App Service Part 1](https://img.youtube.com/vi/C4B4Ebchf0U/0.jpg)](https://www.youtube.com/watch?v=C4B4Ebchf0U)

 I took the following steps to create an App Service Web App using the Azure Portal

1. On the homepage, click "Create a resource"
2. Search for "Web App"
3. Click "Create"
4. Select your subscription
5. Select your resource group "resource-group-west"
6. Enter a name for your web app—This needs to be a unique name and is unique to Azure as a whole and not just your Azure account. I used "hello-world1234" as my unique name.
7. For Publish, select "Code"
8. For the "Runtime Stack", select "Python 3.7" or greater.
9. For the "Operating System" select "Linux"
10. Select a region for your app service
11. Create a new App Service Plan. You can keep the default name Azure gives you or you can create your own name.
12. For SKU and size, select "F1" (Free).
13. Click "Review + Create"
14. Click "Create"

Then, I clicked on the URL to see the app service, which confirmed the app service was up and running. Now we need to deploy our code.

**Note:** Azure free account only allows 1 Linux App Service of size F1. You will need to delete the App Service Web App along with the App Service Plan after each exercise since we will create other Linux App Services throughout this course.

[![Creating An App Service Part 2](https://img.youtube.com/vi/bpME7sOhPNg/0.jpg)](https://www.youtube.com/watch?v=bpME7sOhPNg)

To deploy an App Service from a GitHub repository, I did the following:

1. Go to Deployment Center
2. Choose GitHub
3. Choose org and repo
4. Go through the prompts; deployment takes a few minutes
5. Go to URL of web app and should see the app deployed

### Cleanup
If we no longer need a resource, we can delete them through the portal.

1. From the homepage, click on "Resource Group".
2. Click on the resource group you want to manage.
3. You have two options—"Delete resource group" or if you want to keep the resource group, you can click on the individual or collection of resources you want to delete and click on "Delete".

### QUIZ

Put the steps of deploying an app to an App Service in Azure in the appropriate order.

1. Create or utilize a resource group
2. create the App Service
3. Deploy code to the app service

### Microsoft Learn Resources

* [Host a web application with Azure App service](https://docs.microsoft.com/learn/modules/host-a-web-app-with-azure-app-service/?WT.mc_id=udacity_learn-wwl)
* [Manage an App Service plan in Azure](https://docs.microsoft.com/azure/app-service/app-service-plan-manage?WT.mc_id=udacity_learn-wwl)
* [Deploy a website to Azure with Azure App Service](https://docs.microsoft.com/learn/paths/deploy-a-website-with-azure-app-service/?WT.mc_id=udacity_learn-wwl)

## Exercise: Create and Deploy an App Service Web App

**Prerequisites:**

* A GitHub Account. If you don’t have one, create one [here](https://github.com/).


### Create an App Service Web App

Create an App Service Web App with the following configuration:

* Resource-Group: resource-group-west
* Web App Name: unique name
* Publish: Code
* Runtime stack: Python 3.7
* Operating System: Linux
* Region: West US or the closest region to you
* App Service Plan: Default name or Create new with a name of your choice
* SKU and size: F1 (Free)

**Note:** Azure free account only allows one Linux App Service of size F1. 

### Deploy the App Service Web App

It’s finally time to deploy some code to Azure! Download the web app code provided [here](https://video.udacity-data.com/topher/2020/July/5f18767d_create-app-service-starter/create-app-service-starter.zip).

1. Create a new repo and push the web app code to the repo
2. On Azure portal in the Deployment Center, deploy the web app from GitHub
3. Navigate to the deployed URL

## Solution: Creating an App Service

[![Solution - Creating An App Service](https://img.youtube.com/vi/GOieycrud0Q/0.jpg)](https://www.youtube.com/watch?v=GOieycrud0Q)


### Steps to Create and Deploy an App Service Web App from a Directory using Azure CLI:

1. Sign in to Azure az login
2. cd to `web` directory
3. Run the following command:

```bash
az webapp up \
 --resource-group resource-group-west \
 --name hello-world1234 \
 --sku F1 \
 --verbose
 ```

4. If you visit the URL, you should see your site deployed.
5. If you want to update your app, make changes to your code and then run (Note: this may not update new requirements you may have added):

```bash
az webapp up \
 --name hello-world1234 \
 --verbose
```

Alternatively, you can create the initial web app from the Portal.

### Cleanup

If we no longer need a resource, we can delete them through the portal. The quickest way to do this from the CLI is to delete the resource group. This will delete all resources in that group

`az group delete -n resource-group-west`

Alternatively, if you want to just delete the App Service and App Service plan individually, you can do so with the following commands:

### Delete an App Service

```
az webapp delete \
    --name hello-world1234 \
    --resource-group resource-group-west
```

### Delete an App Service plan

```
az appservice plan delete \
    --name [App Service Plan Name] \
    --resource-group resource-group-west
```

### QUIZ QUESTION

You've built a web app, and deployed it with `az webapp up`, but seem to be getting an `ImportError` when actually trying to access the application. What change do you need to make to the app for it to work?

[] Run <code>pip install</code> from the directory containing the app and re-deploy

[] Add <code>--validation False</code> to the end of <code>az webapp up</code>

[] Remove the library and associated code from your app, as Azure doesn't support it

[x] Add the related library to <code>requirements.txt</code> and update the deployed app

## Glossary

Key Term                       |	Definition
-------------------------------|------------------------------------------
Subscription	               | Multiple of these can exist within a single Azure account; often used for billing and other management purposes.
Resource Group	               | Help to organize resources you use, such as Virtual Machines, App Services or storage, in order to make resource management easier. Groups are often set up for different projects or regions.
Region	                       | Locations of Azure data centers around the world. The closer the region of app resources is to the end user, the lower the latency experienced.
ARM Templates	               | Created within Azure Resource Manager to more easily spin up a set of given resources multiple times.
Virtual Machines               | An Azure IaaS option giving you full access to the underlying operating system of a compute resource. These can be either Windows or Linux machines, with great availability, scalability and redundancy. These require more on-going maintenance and up-keep by cloud developers.
App Service	                   | An Azure PaaS option allowing developers to focus more on their apps than the underlying infrastructure. It is an HTTP-based service for hosting web applications, REST APIs, and mobile back ends. It supports multiple languages and continuous deployment. While they are good for scaling, there is also a limit of up to 14 GB or 4 CPU cores on the highest tier.
App Service Plan               | Contains certain settings of an App Service, such as region, number of VM instances (App Services still run on VMs, but the developer does not have control of the underlying VM, and the app may share the VM with other apps), size of those instances, and pricing tier.
Azure Batch	                   | Used for running large-scale and high-performance compute applications beyond the capabilities of an App Service.
Azure Functions	               | A serverless, event-driven, compute-on-demand platform (covered in a later course).
Container Instances	           | A platform for deploying serverless docker containers (covered in a later course), without the container orchestration provided by AKS (see below).
Service Fabric	               | Microsoft's own distributed systems platform, similar to Kubernetes.
Azure Kubernetes Service (AKS) |	Microsoft's own platform for hosting and managing Kubernetes, including deploying docker containers into clusters (covered in a later course).
