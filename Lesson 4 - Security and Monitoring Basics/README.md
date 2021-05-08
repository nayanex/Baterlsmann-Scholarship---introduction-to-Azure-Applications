# Lesson4 - Security and Monitoring Basics

## Introduction

[![Introduction](https://img.youtube.com/vi/D0U8Hnk086w/0.jpg)](https://www.youtube.com/watch?v=D0U8Hnk086w)

In this lesson, you'll:

* Differentiate the security responsibilities between cloud developers and the cloud provider
* Discover the various security options available in Azure
* Get hands-on with Azure Active Directory, OAuth 2.0, and the Microsoft Authentication Library (MSAL)
* Add monitoring and logging into your Azure applications, including storing logs and activating alerts

Once again, this could be a course of its own, so we'll also provide a lot of additional materials for other areas to investigate outside of the scope of this lesson.

![The Course and Lesson Outline](https://video.udacity-data.com/topher/2020/July/5f10a70f_course-outline-security-monitor/course-outline-security-monitor.png)

## Security Responsibilities

[![Security Responsibilities](https://img.youtube.com/vi/BF_x0aKdmNw/0.jpg)](https://www.youtube.com/watch?v=BF_x0aKdmNw)

Just like we saw early on in the course with technology stack differences between on-premises, IaaS, PaaS and SaaS, security responsibilities also differ among these service types. For the cloud developer, on-premises still puts all security responsibilities onto them. With IaaS, the security of physical hardware shifts to the cloud provider. With PaaS, the operating system security shifts to be the responsibility of the cloud provider, while network, application and identity security are a shared responsibility. With SaaS, the network and application shift responsibility to the cloud provider, but identity stays as a shared responsibility.

It's important to note here that some security responsibilities *always* stay with the cloud developer:

* Account and access management (E.g. do you give the appropriate people the right access, and revoke access when appropriate?)
* Client endpoints (E.g. do you secure the appropriate endpoints to confidential information?)
* Data Governance and Rights Management (E.g. do you prevent employees from emailing confidential documents to third parties?)

![Developer vs. Provider Responsibilities in Azure](https://video.udacity-data.com/topher/2020/July/5f10b4be_azure-security-responsibilities/azure-security-responsibilities.png)

### QUIZ QUESTION

When comparing an application that used to be deployed with on-premise resources, to one now deployed on an App Service, which of the following would you no longer be responsible for, from a security standpoint?


[x] Physical hardware running the app

[x] Operating system security

[ ] Application Security

[ ] Client endpoints

### Microsoft Learn Resources

* [Cloud security](https://docs.microsoft.com/learn/modules/cmu-cloud-security/?WT.mc_id=udacity_learn-wwl)
* [Security, responsibility, and trust in Azure](https://docs.microsoft.com/learn/modules/intro-to-security-in-azure/?WT.mc_id=udacity_learn-wwl)
* [Use a framework to identify threats and find ways to reduce or eliminate risk](https://docs.microsoft.com/learn/modules/tm-use-a-framework-to-identify-threats-and-find-ways-to-reduce-or-eliminate-risk/?WT.mc_id=udacity_learn-wwl)
* [Prioritize your issues and apply security controls](https://docs.microsoft.com/learn/modules/tm-prioritize-your-issues-and-apply-security-controls/?WT.mc_id=udacity_learn-wwl)

## Security Options in Azure

[![Security Options In Azure](https://img.youtube.com/vi/2yjmc8D7a9c/0.jpg)](https://www.youtube.com/watch?v=2yjmc8D7a9c)

There are a ton of services and topics to consider in Azure, each with their own respective use cases. 

* **Azure Active Directory:** Provides single sign-on (SSO) and multi-factor authentication (MFA) capabilities, such as Sign in with Microsoft
* **App Configuration:** Stores application settings in one secure location
* Key Vault API: Stores application keys and secrets in one secure location
* **Managed Identities:** A part of Azure Active Directory; This helps streamline providing an app or app user access to other Azure resources
* **Shared Access Signatures:** Give external parties certain limited access (determined by you) to different Azure resources
* **Role-Based Access Controls (RBAC):** Help internally manage who has access to what resources, and what they can do to said resources
* **Azure Monitor:** Provides a wide range of monitoring services such as log analytics, metrics, alerts, and much more
* **Application Insights:** Part of Azure Monitor; This helps monitor performance and other key metrics

### QUIZ QUESTION

Given the below security situations, which of the Azure security resource would make the most sense to utilize for alleviating security concerns?

SITUATION                                        | SECURITY RESOURCE
-------------------------------------------------|----------------------------------------------------
Your company currently stores access keys and    |  Key Vault API
client secrets on a single server on-premises.   |
Your company wants to add a single sign on option|
to its applications.                             |  Azure Active Directory
You are working with an external contractor who  |
needs access to certain resources in your Azure  |
storage accounts.                                |  Shared Access Signatures
With recent distributed denial of service (DDoS) |
attacks in the news, your CEO wants to implement |  Azure Monitor
additional measures to both identify and mitigate| 
potential attacks.                               |

## Case Study: Security Best Practices

While we'll focus largely on Azure Active Directory and the Microsoft Authentication library in upcoming sections, it's important to also look at the broader contexts of best practices in security for the different deployment types we had earlier in the course - IaaS (with Virtual Machines) and PaaS (with App Services).

Microsoft has put together some great documentation for best practices for both of these, so first spend a few minutes reading each post (or at a minimum, skimming them).

* (IaaS Security Best Practices)[https://docs.microsoft.com/en-us/azure/security/fundamentals/iaas]
* (PaaS Security Best Practices)[https://docs.microsoft.com/en-us/azure/security/fundamentals/paas-deployments]

You'll use the knowledge from each of these to answer the below quizzes.

### Deep Dive - PaaS

If you want, you can also dive a little deeper on the PaaS side of things with more specific articles around App Services, Azure SQL Database and Azure Storage with the below links, but they aren't required to answer the quiz questions.

* (Deep Dive: App Service Best Practices)[https://docs.microsoft.com/en-us/azure/security/fundamentals/paas-applications-using-app-services]
* (Deep Dive: Azure SQL Database Best Practices)[https://docs.microsoft.com/en-us/azure/security/fundamentals/paas-applications-using-sql]
* (Deep Dive: Azure Storage)[https://docs.microsoft.com/en-us/azure/security/fundamentals/paas-applications-using-storage]


## Azure Active Directory

 [![Creating An App Service Part 1](https://img.youtube.com/vi/7jZxyvMsVtI/0.jpg)](https://www.youtube.com/watch?v=7jZxyvMsVtI)

 Azure Active Directory is Microsoft’s solution for single sign-on (SSO) and multi-factor authentication (MFA). We'll be using it in combination with the Microsoft Authentication Library (MSAL) to use "Sign in with Microsoft" buttons in an app, although it can be used more broadly for identity management purposes within an organization. The "tenant" in Azure AD is usually equivalent to an organization.

As you get started with Azure AD, there may be a limit to your access if you are using an enterprise account - for instance, while building this course, I was actually locked out of the main Azure AD tenant for Udacity (for security reasons), and had to use a separate one for building course materials.

Using Azure Active Directory in the Portal
As usual, you can start things off in the Azure Portal by just searching for "Active Directory". From there, you should already be in a tenant by default, although you can create a new one, if needed, to keep things separate from your main tenant. Again, if you are on an enterprise account that limits your access here, you may need to use another (personal) account.

To register an app in Azure AD (which does not actually need a deployed app for these steps):

Click on app registrations on the left panel.
Enter a user-facing display name.
I allowed the widest set of accounts to access it (Accounts in any organizational directory and personal Microsoft accounts).
When you build your own apps, you may want to be more restrictive, but in this case, it will make it easier for you to allow other users to authenticate with your app. An internal application, for instance, might be limited to a single tenant.
You can ignore the redirect URI here for now, and revisit that when we get to implementing OAuth 2.0. However, if you already know this for your app, you can enter one here now, and any others necessary later on.
Once the Application has been registered, you need to copy the Application (client) ID, as it’ll be used later in another exercise.
Next, under manage on the left here, click on certificates and secrets
Click on "+ New client secret", then enter a description (you can decide on your own desired expiration time, I chose one year). Copy down the string under "Value", and make sure you store it somewhere safe - you won't be able to see it again, and would otherwise have to create a new client secret once again. We’ll use this value and the application client ID when implementing OAuth 2.0.
You'll practice this yourself in the upcoming exercise.

QUIZ QUESTION
You created a web app and have deployed it as a live website, with a requirement to sign in with a Microsoft account to access it. When you signed on with your own account, the app seems to appropriately log you in, but your friend, who can access the sign in page, said they could not. What might have happened? (You can answer this without seeing the next section on OAuth2!)









Microsoft Learn Resources
Secure Azure Active Directory users with Multi-Factor Authentication
Enable secure access to apps for external users with Azure AD B2C
Monitor and report on security events in Azure AD


## OAuth2 with MSAL Part 2

### MSAL in Code

There are a few key parts to implement in your code when working with MSAL. Note that the library is just `msal` if you install it with `pip install`.


[![MSAL Process Part 2](https://img.youtube.com/vi/7OS920xtw1A/0.jpg)](https://www.youtube.com/watch?v=7OS920xtw1A)