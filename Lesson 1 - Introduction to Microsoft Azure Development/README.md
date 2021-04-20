# Lesson 1

## Course Outline

[![Course Outline](https://img.youtube.com/vi/Gg4F6wraBEY/0.jpg)](https://www.youtube.com/watch?v=Gg4F6wraBEY)

The course is divided into 3 major sections - Azure Compute Services, Storage Options in Azure, and Security, Monitoring and Logging.

![Course Outline](https://video.udacity-data.com/topher/2020/July/5f04bb0d_azure-dev-c1-course-outline/azure-dev-c1-course-outline.png)

## Introduction to Cloud Development

[![Introduction To Cloud Development](https://img.youtube.com/vi/MDR-azB162Y/0.jpg)](https://www.youtube.com/watch?v=MDR-azB162Y)

The **cloud** is a collection of servers on the internet that store and manage data, run apps, and deliver content such as email or videos. **Cloud computing** is the delivery of software and storage over the Internet (i.e. *the cloud*).

Some of the benefits of using cloud computing are:

* Cost
* Scale
* Reliability
* Security

The three major types of cloud services are **Public**, **Private**, and **Hybrid** cloud. The major differences between these are in where they are deployed, and who manages them. Microsoft OneDrive, Microsoft Azure, and Microsoft Office365 are examples of public cloud options.

Cloud Developers perform some of the following:

* Plan and design cloud based apps
* Monitor, maintain and support cloud applications
* Develop work flows and processes

### Microsoft Learn Resources

[Cloud Concepts - Principles of cloud computing](https://docs.microsoft.com/learn/modules/principles-cloud-computing/?WT.mc_id=udacity_learn-wwl)

[Foundations of cloud computing for developers](https://docs.microsoft.com/en-us/learn/modules/cmu-cloud-computing-overview/?WT.mc_id=udacity_learn-wwl)

## Why Cloud Development Is Important

[![Why Cloud Development Is Important](https://img.youtube.com/vi/6Xj7ZVtr9H8/0.jpg)](https://www.youtube.com/watch?v=6Xj7ZVtr9H8)

You've probably worked with various cloud services before, such as Microsoft OneDrive and Google Docs.

Some of the advantages of cloud computing are:

* Cost: The cloud provider handles all the upfront costs associated with buying hardware, along with on-going maintenance costs
* Scale: Most are pay-as-you-go depending on demand (elasticity), and can be expanded as needed
* Reliability: Management of backups, disaster recovery, etc. is made easier
* Security: Policies and controls are already in place to protect your data

Some of the disadvantages of cloud computing are:

* It is internet-based, so it can be prone to outages and fluctuations in speed
* Sensitive, private and core data is physically located on someone else's server
* Cloud services will be tailored and customized for your specific cloud instance, potentially making it hard to quickly change providers.

### QUIZ 

Which of the following is NOT a reason to develop for the cloud?

[] Lower up-front costs

[] Easier scalability of resources

[] Lower server maintenance costs

[x] No responsibility for security breaches

### Microsoft Learn Resources

[Economics of cloud computing](https://docs.microsoft.com/learn/cmu-cloud-computing/cmu-cloud-economics/?WT.mc_id=udacity_learn-wwl)

[Predict costs and optimize spending for Azure](https://docs.microsoft.com/learn/modules/predict-costs-and-optimize-spending/?WT.mc_id=udacity_learn-wwl)

## Business Stakeholders

[![Business Stakeholders](https://img.youtube.com/vi/uyHY8ECPx2Y/0.jpg)](https://www.youtube.com/watch?v=uyHY8ECPx2Y)

As a cloud developer, you will interact and engage with numerous stakeholders, each of whom has different priorities. Some of these are:

* Your users
* Company executives
* I.T. Department
* Cloud Service provider
* Finance Department

![The key stakeholders in cloud development](https://video.udacity-data.com/topher/2020/July/5f04bb8f_azure-dev-c1-stakeholders/azure-dev-c1-stakeholders.png)

### QUIZ

Match each of the below stakeholders to their role in the cloud development process.

* **[IT Department]** Responsible for ensuring individuals have the right access roles based on their positions, and appropriately add or remove access roles when employees join or leave the company

* **[Cloud Developer]** Responsible for ensuring applications run efficiently in the cloud, require appropriate authentication to access, and identifying appropriate resources to use

* **[Company Executives]** Understanding basics of the cloud (including cost/benefits), empowering other departments to take advantage of it, and ensuring staffing needs met in departments making key cloud decisions

* **[Cloud Service Provider]** Ensuring physical cloud infrastructure is kept secure with high uptime

* **[Finance Department]** Work with IT department to ensure critical financial documents are stored in secure environments

## History of Cloud Development

The roots of cloud computing go as far back as the 1960s.

![The timeline of cloud development](https://video.udacity-data.com/topher/2020/July/5f10b7b8_cloud-history-timeline/cloud-history-timeline.png)

1969 - JCR Licklider aimed to create a system where information could be accessed anywhere in the world called the “Intergalactic Computer Network”.

1980s - Supercomputing Centers start to form and Commercial Internet Service Providers start to emerge in the late 1980s.

1990 - The internet becomes visible to all when Tim Berners-Lee invents the World Wide Web.

1999 - Salesforce.com launches and becomes a pioneer in delivering enterprise applications over the internet, which is known as Software-as-a-Service(SaaS). This paves the way for other SaaS applications such as Microsoft 365 and Gmail.

2002 - Amazon launches its Amazon Web Services (AWS) platform. AWS is formally launched as a business unit in 2006.

2006 - Amazon launches its Elastic Compute Cloud (EC2), a commercial web service that allowed users to rent computers to run their applications. EC2 paved the way for application delivery over the internet, which allowed web-scaled businesses like Netflix and Spotify to exist.

2007 - Dropbox introduces its file hosting service, and with that cloud storage becomes a commodity.

2008 - Google launches its Google App Engine (GAE) Platform-as-a-Service (PaaS). This service allowed developers to host their web applications on Google’s managed data centers.

2010 - Microsoft launches its cloud computing platform, Azure, after announcing it back in 2008. Azure now covers Software-as-a-Service(SaaS), Platform-as-a-Service(PaaS), and Infrastructure-as-a-Service(IaaS).

2011 - IBM launches SmartCloud, a suite of enterprise-class cloud computing technologies for building private, public, and hybrid clouds.

2013 - Google launches Google Compute Engine (GCE) as an addition to its Google Compute Platform. This is an Infrastructure-as-a-Service (IaaS) component of the platform that allows a user to spin up Virtual Machines (VMs) on demand.

So what’s next? Cloud computing is on the rise in this day and age. As cloud computing continues to become more mainstream, more and more companies are looking to adopt it. Industries such as marketing, education, and healthcare are beginning to increase their use of cloud-based services and platforms.

## Microsoft Azure

[![Microsoft Azure](https://img.youtube.com/vi/Py-MVOl3YS8/0.jpg)](https://www.youtube.com/watch?v=Py-MVOl3YS8&t)

Azure is a public computing platform with tremendous value and benefits:

* Scalability: can dynamically handle changes in volume, bandwidth, storage size
* Availability: redundant on a global scale with 99.9%+ uptime (see SLA by service here)
* Security: replicated data helps protect against natural disaster, while authentication strategies help secure access to the data
* Standard delivery pipeline development services, such as:
    * Source control
    * Unit testing
    * Integration testing
    * Delivery
    * Live development tools

Azure products span multiple categories, such as Compute, Analytics, Databases, A.I. and Machine Learning.

The Azure products this course will focus on are:

1. App Services
2. Virtual Machines
3. Azure SQL Databases
4. Blob Storage
5. Azure Active Directory
6. Aspects of Azure Monitor, such as logs and alerts


### QUIZ QUESTION

Match the below benefits to their descriptions.

**[Scalability]**: Increased speed, storage, or bandwidth as needed.

**[Security]**: Authentication and data redundancy provide protection.

**[Availability]**: `99.9%+` uptime is the goal.

**[Development Environment]**: Provides access to Source control, Unit testing, Integration testing, Delivery, and Live development tools.

### Microsoft Learn Resources

[Align requirements with cloud types and service models in Azure](https://docs.microsoft.com/learn/modules/align-requirements-in-azure/?WT.mc_id=udacity_learn-wwl)

[Core Cloud Services - Azure architecture and service guarantees](https://docs.microsoft.com/learn/modules/explore-azure-infrastructure/?WT.mc_id=udacity_learn-wwl)

## The Azure Portal

[![The Azure Portal](https://img.youtube.com/vi/0qb__6Frgn0/0.jpg)](https://www.youtube.com/watch?v=0qb__6Frgn0)


### Practice - The Azure Portal

Make sure you have an Azure account and navigate to the Azure Portal.

* Navigate to the Azure free account page [here](https://azure.microsoft.com/en-us/free/).
* Click on "Start Free".
* Complete the account registration.
* Navigate to the [Azure Portal](https://portal.azure.com/).
* If there is a box named "Start with an Azure free trial", click on "Start".

### Microsoft Learn Resources

[Core Cloud Services - Manage services with the Azure portal](https://docs.microsoft.com/learn/modules/tour-azure-portal/?WT.mc_id=udacity_learn-wwl)

## IaaS, PaaS, and SaaS

[![IaaS, PaaS, And SaaS](https://img.youtube.com/vi/8X5d-pUlq5E/0.jpg)](https://www.youtube.com/watch?v=8X5d-pUlq5E)

In contrast to on-premises solutions, there are three types of services that Azure offers us:

* Infrastructure as a Service (IaaS) - removes the expense of up-front costs of hardware, software and test environments
* Platform as a Service (PaaS) - handles networking, provides middleware and development & database tools
* Software as a Service (SaaS) - provides end-users access to online cloud solutions

![Azure services organized by IaaS, PaaS and SaaS](https://video.udacity-data.com/topher/2020/July/5f10a86a_azure-service-level-comparison/azure-service-level-comparison.png)

### QUIZ QUESTION

Match the below situations to which of the cloud services types they represent.

**[IaaS]**: You need a high level of control over the cloud service, even down to the operating system level. An Azure Virtual Machine is one example of this cloud service type.

**[PaaS]**: You need to quickly deploy a web application. An App Service is one example of this cloud service type.

**[SaaS]**: You want an already pre-built office productivity suite for your employees to work with. Microsoft Office 365 is an example of this cloud service type.


## Tools & Environment

[![Tools & Environment](https://img.youtube.com/vi/aH_2wE-s2Vo/0.jpg)](https://www.youtube.com/watch?v=aH_2wE-s2Vo)

### Tools & Environment Checklist

It's time to get all the tools you need to get started!

* Sign up for an Azure free account [here](https://azure.microsoft.com/en-us/free/), if you haven't already.
* Create a Github account [here](https://github.com/join)
* Install Python 3.6 or above [here](https://www.python.org/downloads/)
* Install Azure CLI tools for VS Code [here](https://marketplace.visualstudio.com/items?itemName=ms-vscode.azurecli), or search for it within VS Code.
* Additionally, install Azure CLI for your terminal [here](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest).

### Microsoft Learn Resources

* [Create an Azure account](https://docs.microsoft.com/learn/modules/create-an-azure-account/?WT.mc_id=udacity_learn-wwl)
* [Control Azure services with the CLI](https://docs.microsoft.com/learn/modules/control-azure-services-with-cli/?WT.mc_id=udacity_learn-wwl)
* [Prepare your development environment for Azure development](https://docs.microsoft.com/learn/modules/prepare-your-dev-environment-for-azure-development/?WT.mc_id=udacity_learn-wwl)
* [Implement a code workflow in your build pipeline by using Git and GitHub](https://docs.microsoft.com/learn/modules/implement-code-workflow/?WT.mc_id=udacity_learn-wwl)


## Project: Deploy an Article CMS to Azure

[![Project - Deploy An Article CMS To Azure](https://img.youtube.com/vi/cqrOmTP1q_g/0.jpg)](https://www.youtube.com/watch?v=cqrOmTP1q_g)

It is exciting to take a look at what we will be creating in our final course project. Similar to many such systems that exist in the real world, we will be designing, building, and deploying an Article Content Management System (CMS), which will include the ability to:

* Login and authenticate
* Read posts
* Create and save a post
* Edit and save an existing post

The project looks straightforward from the user interface, but there is a lot going on under the hood of this Flask app. The Sign In page makes use of the Microsoft Authentication Library (MSAL) and Azure Active Directory to log in with a Microsoft account, while data related to article titles, authors and text bodies is stored in an Azure SQL Server. An Azure Storage Account with Blob Storage is used to store the images, and the web app itself can be deployed using either an Azure Virtual Machine or an Azure App Service. All of these resources are likely tied to a single resource group.

![An example article within the deployed CMS](https://video.udacity-data.com/topher/2020/March/5e6f8ed6_article-cms/article-cms.png)

## Glossary

Key Term                            |	Definition
------------------------------------| -----------------------------------------
The Cloud                           | A collection of servers on the internet that store and manage data, run apps, and deliver content such as email or videos.
Cloud Computing                     | The delivery of software and storage over the Internet (i.e. the cloud).
Public Cloud                        | Cloud computing resources shared amongst multiple customers, with applications and data still separate.
Private Cloud                       | Cloud computing resources that are dedicated to only one entity. This is most similar to how on-premises resources operate, but with the resources still hosted off-site by a third party.
Hybrid Cloud                        | Utilizing a mix of public and private cloud resources.
Cloud Developer	                    | Developers who build cloud applications or utilize other cloud resources in their applications. They are responsible for ensuring applications run efficiently in the cloud, requiring appropriate authentication to access, and identifying appropriate resources to use.
Microsoft Azure	                    | A public computing platform provided by Microsoft, with many products spanning many categories, such as Compute, Analytics, Databases, A.I. and Machine Learning.
Azure Portal                        | The browser-based and GUI version of working with Azure resources.
Elasticity                          | The ability to scale up or down resources to match demand.
On-Premises	                        | The non-cloud option where companies host all their necessary compute, storage and other resources on-site.
Infrastructure as a Service (Iaas)  | Removes the expense of up-front costs of hardware, software and test environments, as the cloud provider is instead responsible for providing physical hardware.
Platform as a Service (Paas)        | Handles networking, provides middleware and development & database tools, in addition to the physical hardware provided at the IaaS level.
Software as a Service (Saas)        | Provides end-users access to online cloud solutions, without the need to build or support the underlying applications themselves.