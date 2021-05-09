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
Your company currently stores access keys and client secrets on a single server on-premises. | Key Vault API
Your company wants to add a single sign on option to its applications.| Azure Active Directory
You are working with an external contractor who needs access to certain resources in your Azure storage accounts. |  Shared Access Signatures
With recent distributed denial of service (DDoS)attacks in the news, your CEO wants to implement additional measures to both identify and mitigate potential attacks. | Azure Monitor

### QUIZ QUESTION

Your company is developing a new app on Azure, and developers under the project are under a strict NDA to not discuss project details with others inside the company. Within the app itself, it should be able to authenticate users with their Microsoft logins, as well as log attempts to access the deployed app by non-authorized accounts. Which of the following security options might be used here?

[x] Azure RBAC

[x] Azure Active Directory

[x] Azure Monitor

[ ] Azure SQL Database

### Microsoft Learn Resources

[Learning Path: Manage security operations in Azure](https://docs.microsoft.com/learn/paths/manage-security-operations/?WT.mc_id=udacity_learn-wwl)


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

#### QUIZ QUESTION

Which of the following are security best practices related to Virtual Machines?

[x] Enable encryption on VMs.

[x] Identify and remediate exposed VMs that allow access from “any” source IP address.

[ ] Avoid operating system updates to keep the OS stable.

[x] Install the latest security updates.

[x] Control VM access.

#### QUIZ QUESTION

Which of the following are security best practices related to App Services?
 
[ ] Keep the operating system up to date.

[x] Authenticate through Azure Active Directory.

[x] Don’t put credentials and other secrets in source code or GitHub.

[ ] Restrict access based on the desire to know and most privilege security principles.

[x] Perform security penetration testing.

#### QUIZ QUESTION

Which of the below describe a difference in best practices between Virtual Machines and App Services?

[ ] Virtual Machines require less attention to the underlying operating system itself.

[ ] Azure Active Directory only applies to App Service solutions.

[ ] Role-based access controls (RBAC) can only be applied to VMs.

[x] App Services do not have best practices around hard disks.

[ ] There are no differences in best practices between Virtual Machines and App Services.


#### QUIZ QUESTION

You are moved onto a project at work, and given your Azure experience, are asked to identify any security issues. One virtual machine that supports the project was deployed October 30th, 2017. What best practice may have been violated?

[ ] Control VM access.

[ ] Install an anti-malware solution to protect against malware.

[ ] Ensure at deployment that images you built include the most recent round of Windows updates.

[x] Periodically redeploy your VMs to force a fresh version of the OS.

[ ] Deploy and test a backup solution.

#### QUIZ QUESTION

Your app service is running version 0.12.1 of a Python library, while the latest version is 2.1.3. An external party is able to access certain data due to a vulnerability fixed in version 1.5.6. What best practice may have been violated?

[ ] Protect your keys.

[x] Monitor the security state of your App Service environments.

[ ] Use strong authentication and authorization platforms.

[ ] Secure your keys and credentials to secure your PaaS deployment.

[ ] Periodically redeploy your App Service to force a fresh version of the OS.


## Azure Active Directory

 [![Azure Active Directory](https://img.youtube.com/vi/7jZxyvMsVtI/0.jpg)](https://www.youtube.com/watch?v=7jZxyvMsVtI)

 Azure Active Directory is Microsoft’s solution for single sign-on (SSO) and multi-factor authentication (MFA). We'll be using it in combination with the Microsoft Authentication Library (MSAL) to use "Sign in with Microsoft" buttons in an app, although it can be used more broadly for identity management purposes within an organization. The "tenant" in Azure AD is usually equivalent to an organization.

As you get started with Azure AD, there may be a limit to your access if you are using an enterprise account - for instance, while building this course, I was actually locked out of the main Azure AD tenant for Udacity (for security reasons), and had to use a separate one for building course materials.

Using Azure Active Directory in the Portal
As usual, you can start things off in the Azure Portal by just searching for "Active Directory". From there, you should already be in a tenant by default, although you can create a new one, if needed, to keep things separate from your main tenant. Again, if you are on an enterprise account that limits your access here, you may need to use another (personal) account.

To register an app in Azure AD (which does not actually need a deployed app for these steps):

* Click on app registrations on the left panel.
* Enter a user-facing display name.
* I allowed the widest set of accounts to access it (Accounts in any organizational directory and personal Microsoft accounts).
    * When you build your own apps, you may want to be more restrictive, but in this case, it will make it easier for you to allow other users to authenticate with your app. An internal application, for instance, might be limited to a single tenant.
* You can ignore the redirect URI here for now, and revisit that when we get to implementing OAuth 2.0. However, if you already know this for your app, you can enter one here now, and any others necessary later on.
* Once the Application has been registered, you need to copy the Application (client) ID, as it’ll be used later in another exercise.
* Next, under manage on the left here, click on certificates and secrets
* Click on "+ New client secret", then enter a description (you can decide on your own desired expiration time, I chose one year). Copy down the string under "Value", and make sure you store it somewhere safe - **you won't be able to see it again**, and would otherwise have to create a new client secret once again. We’ll use this value and the application client ID when implementing OAuth 2.0.
You'll practice this yourself in the upcoming exercise.

### QUIZ QUESTION

You created a web app and have deployed it as a live website, with a requirement to sign in with a Microsoft account to access it. When you signed on with your own account, the app seems to appropriately log you in, but your friend, who can access the sign in page, said they could not. What might have happened? (You can answer this without seeing the next section on OAuth2!)

[x] The supported account type in Azure Active Directory may limit their access

[ ] You only have the app running on localhost

[ ] You have to add your friend as a valid user in an Azure Active Directory database

[ ] You need a new friend


### Microsoft Learn Resources

[Secure Azure Active Directory users with Multi-Factor Authentication](https://docs.microsoft.com/learn/modules/secure-aad-users-with-mfa/?WT.mc_id=udacity_learn-wwl)
[Enable secure access to apps for external users with Azure AD B2C](https://docs.microsoft.com/learn/modules/enable-external-access-with-b2c/?WT.mc_id=udacity_learn-wwl)
[Monitor and report on security events in Azure AD](https://docs.microsoft.com/learn/modules/monitor-report-aad-security-events/?WT.mc_id=udacity_learn-wwl)

## Exercise: Azure Active Directory

This exercise will get you familiar with registering an app in Azure Active Directory, which will set you up for the next exercise to use Microsoft Authentication.

1. Navigate to Azure Active Directory in the Azure portal.
If you are using a corporate Microsoft account, you might be restricted from access, in which case you would need to use a personal account for this stage of the exercise.
2. You should already have a default tenant to use, but if not, create a new tenant and fill in the required information.
3. Create a new app registration, and set it to allow both any organizations and personal accounts.
4. You can ignore the Redirect URI for now, as that will be added as part of the next exercise.
5. Copy down the "Application (client) ID", which will be used in the next exercise.
6. Create and copy down a client secret key, which will be used in the next exercise.

## Solution: Azure Active Directory

This is the same process as before, so we'll skip the video this time through.

**To register your app and get the necessary app information for the next exercise:**

1. Navigate to Azure Active Directory in the Azure portal.
    * If you are using a corporate Microsoft account, you might be restricted from access, in which case you would need to use a personal account for this stage of the exercise.
2. You should already have a default tenant to use, but if not, create a new tenant and fill in the required information.
3. Navigate to the "App registrations" page, and enter a name for the app, while allowing the widest set of accounts to access it.
    * Remember, you'll likely want to be more restrictive when creating your own apps.
4. You can ignore the Redirect URI for now, as that will be added as part of the next exercise.
5. After you click "Register", copy down the "Application (client) ID", as you'll need that for the next exercise.
6. Additionally, under "Manage", click "Certificates & secrets", then "+ New client secret", then enter a description (you can decide on your own desired expiration time). Copy down string under "Value", and make sure you store it somewhere safe.


## OAuth2 with MSAL Part 2

### MSAL in Code

There are a few key parts to implement in your code when working with MSAL. Note that the library is just `msal` if you install it with `pip install`.


[![MSAL Process Part 2](https://img.youtube.com/vi/7OS920xtw1A/0.jpg)](https://www.youtube.com/watch?v=7OS920xtw1A)