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

* [Deep Dive: App Service Best Practices](https://docs.microsoft.com/en-us/azure/security/fundamentals/paas-applications-using-app-services)
* [Deep Dive: Azure SQL Database Best Practices](https://docs.microsoft.com/en-us/azure/security/fundamentals/paas-applications-using-sql)
* [Deep Dive: Azure Storage](https://docs.microsoft.com/en-us/azure/security/fundamentals/paas-applications-using-storage)

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

## OAuth2 with MSAL Part 1

[![OAuth2 With MSAL](https://img.youtube.com/vi/DKbR5ACrXGw/0.jpg)](https://www.youtube.com/watch?v=DKbR5ACrXGw)

**Authentication** is the process of checking if the user is who they say they are, and **authorization** is the process of checking if the user is allowed to access data and what they can do with the data.

![Authentication vs Authorization](https://video.udacity-data.com/topher/2020/July/5f10b5e8_authentication-vs-authorization/authentication-vs-authorization.png)

OAuth 2.0 is the industry-standard protocol for authorization. Instead of creating apps that each maintain their username and password information, apps can delegate that responsibility to a centralized identity provider.

Azure AD is the centralized identity provider in the cloud that we’ll use to implement OAuth 2.0, or more specifically "Sign in with Microsoft", in our case. The Microsoft Authentication Library (MSAL) is a Python library we’ll use to implement “Sign in with Microsoft” functionality in an app. You may have also heard of or used Active Directory Authentication Library (ADAL) before; this is an older library that does not support personal Microsoft accounts.

![The “Sign in with Microsoft” button uses MSAL under the hood in Python.](https://video.udacity-data.com/topher/2020/July/5f10b643_sign-in-with-ms/sign-in-with-ms.svg)

### The MSAL Process

[![MSAL Process Part 1](https://img.youtube.com/vi/oVsNS-xIXSQ/0.jpg)](https://www.youtube.com/watch?v=oVsNS-xIXSQ)

In our simplified workflow, the authorization process with MSAL is as follows:

* First, when the user clicks the “Sign in with Microsoft” button in your app, a function in your app will be activated, which will cause a browser pop-up. The user signing in will request an authorization code, from the `/oauth/v2.0/authorize` endpoint.
* The OAuth2 provider, Microsoft in this case, will return an authorization code and will redirect the user based on a URL you have provided within your application’s Python code.
* From here, your app will then need to request an access token. To do so, you’ll need the authorization code you received before, along with information like client ID and client secret, in the case of Azure Active Directory. It’s also likely you will be requesting a certain scope, such as `USER.READ`, which would allow you to read the user’s profile information (but not make changes to it). * This will hit the `/oauth/v2.0/token` endpoint.
This will then return the access token for that user.
* At this point, the access token itself is then used to actually hit some secure endpoint.
* The endpoint must actually validate the token your app sent it, which is outside of your hands. It then will return the requested secure data, if the token is validated.

You'd also need to provide the ability for users to logout.

You can also find the complete workflow in [Microsoft's documentation](https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-oauth2-auth-code-flow).

![A simplified workflow for OAuth 2.0 with MSAL](https://video.udacity-data.com/topher/2020/July/5f10b619_msal-oauth-process/msal-oauth-process.png)

## OAuth2 with MSAL Part 2

### MSAL in Code

There are a few key parts to implement in your code when working with MSAL. Note that the library is just `msal` if you install it with `pip install`.


[![MSAL Process Part 2](https://img.youtube.com/vi/7OS920xtw1A/0.jpg)](https://www.youtube.com/watch?v=7OS920xtw1A)

#### Getting the Authorization Code

You'll first need to create a `ConfidentialClientApplication`:

* First create a `ConfidentialClientApplication` object. This class requires a Client ID and Client Secret from Azure AD.
* It also requires an “authority” based on single or multi-tenant access.
    * For example, https://login.microsoftonline.com/common is for multi-tenant access whereas single tenant access would replace /common with a tenant id
* We can also pass in an optional argument for a cached session to avoid re-requesting information.

Once the client is created, you'll use the `get_authorization_request_url` function of the client object. This requires:

* A scope, such as `USER.READ`
* State (UUID in our case, identifying the session)
* Redirect URI

Note that you can find more on the MSAL library code in the link further down the page as well.

#### Getting the Access Token

[![MSAL Process Part 3](https://img.youtube.com/vi/ctTVH1I2Z2A/0.jpg)](https://www.youtube.com/watch?v=ctTVH1I2Z2A)

After re-creating the `ConfidentialClientApplication` object using the cache value, you then use the `acquire_token_by_authorization_code` method. This method requires:

* An authorization code
* A scope

This method also takes other parameters, so this could be a good spot for adding in a `redirect_uri` to push a user to a particular endpoint.

#### Logging Out

It's also important to make sure your users can log out. This is actually a bit separate from the MSAL library itself, and is more concerned with a particular endpoint:

```python
return redirect(Config.AUTHORITY + '/oauth2/v2.0/logout' +
    '?post_logout_redirect_uri=' +
    url_for('login', _external=True))
```

I briefly mentioned the `/oauth2/v2.0/logout` endpoint earlier, and that’s what you can redirect to after the user clicks a sign out button. It will start with the authority they signed in with, such as `https://login.microsoftonline.com/common` for a multi-tenant app, the OAuth logout endpoint, as well as a post-logout redirect URI.

Here, this assumes the app has some Flask endpoint for “login”, that is external to the original redirect URI (separate from Microsoft). You will also want to enter your redirect URI back in Azure AD, like you did with the redirect URIs for logging in.

### Additional Resources - MSAL

* [Python Documentation for Microsoft Authentication Library](https://msal-python.readthedocs.io/en/latest/)
* [Microsoft Graph permissions levels](https://docs.microsoft.com/en-us/graph/permissions-reference) - such as `User.Read` that gives an app permission to read user profile data

### QUESTION 1 OF 2

Match the below security topics, resources and libraries to their related definition.

DEFINITION | AREA OF AUTHENTICATION/AUTHORIZATION
-----------|-------------------------------------
Azure option for providing single sign-on and multi-factor authentication capabilities. | `Azure Active Directory`
A form of authentication that, instead of giving usernames and passwords to an app, instead handles tokens allowing apps to access certain portions of the user's account. | `OAuth2`
The library developers can work with to add functionality around token grants for secure API access. | `MSAL`
Whether a user is who they say they are | `Authentication`
Whether a user is allowed to access something | `Authorization`

### QUESTION 2 OF 2

You've built an app that utilizes the `msal` library for authentication purposes. The app and its related login/logout flow work fine when running on localhost, but when you deploy the app, the app loads but authentication doesn't work appropriately. What step might you have skipped with the live application?

[x] The live app's redirect URI needs to be added in Azure AD

[ ] The app needs to be registered in Azure AD

[ ] You have the wrong account types allowed in Azure AD

[ ] None of the above

### Microsoft Learn Resources - Authentication

While KeyVault API, Managed Identities, Shared Access Signatures, and Role-Based Access Controls (RBAC) are outside the scope of this course, we encourage you to check them out below, especially if you plan to take Microsoft's [AZ-204](https://docs.microsoft.com/en-us/learn/certifications/exams/az-204) exam on Developing Solutions for Microsoft Azure.

* [Secure app configuration data by using the App Configuration and KeyVault API](https://docs.microsoft.com/en-us/learn/modules/configure-and-manage-azure-key-vault/)
* [Manage keys, secrets, and certificates by using the KeyVault API (same content as above)](https://docs.microsoft.com/en-us/learn/modules/configure-and-manage-azure-key-vault/)
* [Implement Managed Identities for Azure resources](https://docs.microsoft.com/en-us/learn/modules/authenticate-apps-with-managed-identities/)
* [Create and implement shared access signatures](https://docs.microsoft.com/en-us/learn/modules/control-access-to-azure-storage-with-sas/)
* [Control access to resources by using role-based access controls (RBAC)](https://docs.microsoft.com/en-us/learn/modules/secure-azure-resources-with-rbac/)

## Exercise: OAuth2 with MSAL

This exercise will help you get familiar with integrating the Microsoft Authentication Library, or `msal`, into an application. In the previous exercise, you registered an app with Azure Active Directory, and you'll use some of the information from there so that authentication can occur.

First, download the application code [here](https://video.udacity-data.com/topher/2020/July/5f075c1e_oauth-msal-starter/oauth-msal-starter.zip).

**Note:** This app will be served on `https` only as Azure AD will block insecure connections for redirect URIs on deployed applications. As such, when testing on `localhost`, make sure to add `https` at the start instead of `http`, e.g. `https://localhost:5555`.

1. You can launch the app, if desired, to start, but you'll notice that it doesn't yet allow you to log in with your Microsoft account. To start, open up `config.py`, and enter in both the client secret and application client ID you previously copied down from Azure AD. If your app is no longer registered, go back through the steps in the previous exercise to obtain new values.
2. You'll also notice a variable for `REDIRECT_PATH`. This should start with a `/`, and then can be whatever else you want it to be (although you should stay away from `/home`, `/login` or `/logout`, since those are used elsewhere in the app). Once you have this set, go back to Azure AD and enter this as the redirect URI for your app, as well as adding a logout URI.
3. Now, you're ready to get started with `msal`. The app code contained in views.py currently implements a bit of basic log in and logout with the `Flask-Login` library, but you need to implement the TODOs throughout for the "Sign in with Microsoft" button on the app to work appropriately. The suggested order is as follow:

* Implement `_build_msal_app` to create a confidential client application
* Implement `_build_auth_url` to get an authorization request URL
* Acquire a token from an msal app within the `authorized` function
* Add the appropriate logout URL to the `logout` function

    Together, the above four steps should allow you to have a functional "Sign in with Microsoft" button with the Microsoft Authentication Library, as well as to log back out of the related Microsoft account.

4. Test your app out in localhost (making sure to use `https`), or feel free to deploy the app as well.

Supporting Materials
 [oauth-msal-starter.zip](https://video.udacity-data.com/topher/2020/July/5f075c1e_oauth-msal-starter/oauth-msal-starter.zip)

## Solution: OAuth2 with MSAL

[![Solution - OAuth2 With MSAL Part 1](https://img.youtube.com/vi/CFRywEmy-2Q/0.jpg)](https://www.youtube.com/watch?v=CFRywEmy-2Q)

This was my approach to the exercise:

#### Add necessary variables in `config.py`

1. Fill out `CLIENT_SECRET` and `CLIENT_ID` by getting the relevant values from the registered app in Azure Active Directory (see previous exercise).
2. Add a `REDIRECT_PATH` - I used `"/getAToken"`.
3. Note that if we were using a single tenant app, `AUTHORITY` would switch from `https://login.microsoftonline.com/common` to ending instead with the tenant name (in place of `common`).

#### Add the redirect and logout URIs in Azure AD

1. Within your registered app, under "Manage", click on "Authentication", then "+Add a platform".
2. Select "Web" under "Web applications" in the new window.
3. Enter `https://localhost:5555/getAToken` in the redirect URI (replace `/getAToken` with your own `REDIRECT_PATH`).
4. Enter `https://localhost:5555/login` in the logout URI - we want the user to be redirected back to the login page of this app when they logout. Other apps could potentially just redirect back to a homepage (our homepage is hidden behind the login process).
5. Click Configure.

### Adding MSAL functionality

[![Solution - OAuth2 With MSAL Part 2](https://img.youtube.com/vi/7VLkAvYBQ7E/0.jpg)](https://www.youtube.com/watch?v=7VLkAvYBQ7E)

**Implement "Sign in with Microsoft" with MSAL**

1. In `_build_msal_app`, you'll want to use a `ConfidentialClientApplication`([documentation](https://msal-python.readthedocs.io/en/latest/#confidentialclientapplication)):

```python
return msal.ConfidentialClientApplication(
    Config.CLIENT_ID, authority=authority or Config.AUTHORITY,
    client_credential=Config.CLIENT_SECRET, token_cache=cache)
```

2. In `_build_auth_url`, you can use the previous msal app to get an authorization request url (see documentation [here](https://msal-python.readthedocs.io/en/latest/#msal.ClientApplication.get_authorization_request_url)):

```python
return _build_msal_app(authority=authority).get_authorization_request_url(
    scopes or [],
    state=state or str(uuid.uuid4()),
    redirect_uri=url_for('authorized', _external=True, _scheme='https'))
```

3. If we go back to our `authorized` function, we'll see a place where we can use our `_build_msal_app` function again, this time to acquire a token ([documentation](https://msal-python.readthedocs.io/en/latest/#msal.ClientApplication.acquire_token_by_authorization_code)):

```python
result = _build_msal_app(cache=cache).acquire_token_by_authorization_code(
    request.args['code'],
    scopes=Config.SCOPE,
    redirect_uri=url_for('authorized', _external=True, _scheme='https'))
```

4. At this point, logging a user in with Microsoft should work just fine, but you should also make sure they are able to log out. So, along with making sure you have the correct logout URI in Azure AD, you also need to return the correct redirect in `logout`:

```python
return redirect(
    Config.AUTHORITY + '/oauth2/v2.0/logout' +
    '?post_logout_redirect_uri=' + url_for('login', _external=True))
```

### Using HTTPS with Your App

You may have noticed the use of `_scheme='https'` and `_external=True` in the `url_for()` functions used in this exercise.

Setting the `_scheme` to "https" allows it to be served to the browser, as you may guess, through "https". Now, we don't have a fully secure app, as you may note when you try to open it in your browser; however, in this basic app, it's not super concerning just yet. However, Azure Active Directory will not allow you to use a non-HTTPS website for a live app's redirect URI (localhost can still use HTTP).

*In order for this* `_scheme` *setting to work*, `_external` must also be set to True, which just means an absolute URL will be created, as opposed to a relative URL such as which works with localhost.

### Handle MSAL Exceptions and Errors

This [article](https://docs.microsoft.com/en-us/azure/active-directory/develop/msal-handling-exceptions?tabs=python) gives an overview of the different types of errors and recommendations for handling common sign-in errors.

## Monitoring and Logging in Azure

[![Monitoring And Logging In Azure](https://img.youtube.com/vi/lxTPv7Nte8I/0.jpg)](https://www.youtube.com/watch?v=lxTPv7Nte8I)

**Note:** I should be using console logs when setting up my alert, not app logs.

#### Benefits of Logging

Implementing logging in your applications can help with:

* Troubleshooting problems or preventing potential new ones
* Improving application performance or maintainability
* Automating operations that would otherwise require manual intervention

#### Monitoring and Logging in Azure

Azure gives developers the ability to:

* Monitor metrics, such as performance and service quotas
* Use App-based logging
* Send logs to storage
* Create alerts

There are other monitoring and logging options, such as Application Insights and Log Analytics using the Kusto query language, that are outside of the scope of this course. We’ll focus on the built-in monitoring and logging offered to help debug an App Service App.

![An example log within the Azure Portal](https://video.udacity-data.com/topher/2020/July/5f10b55d_log-solution/log-solution.png)

### Logging Considerations in a Flask App

When building a Flask application, `print` statements won’t show up like they usually would in a regular Python application. You’ll need to use the built-in logger Flask has to log events. You’re able to set the minimum severity level of the events you want to capture; for example, you could set the logger to only capture events at a warning level or above.

Check out the documentation in the resources below if you need some more background on how logging works for Flask applications.

### Additional Resources - Flask and Logging

* [Flask Documentation](https://flask.palletsprojects.com/en/1.1.x/)
* [Flask Logging Documentation](https://flask.palletsprojects.com/en/1.1.x/logging/)
* [Standard Python Logging Library](https://docs.python.org/3/library/logging.html) (Flask logging is a logger object from this library)


### QUESTION 1 OF 2

Match the below scenarios with their related monitoring or logging option that best fits them.


SCENARIO | MONITORING/LOGGING OPTION
---------|--------------------------
You want to see the level of requests made to your app over time.| Monitoring Metrics
You notice a recent increase of requests made to the login page of your app, but the rest of the app has steady activity. You want to keep track of whether these visits are failing to log in. | Log Analytics
You want to receive an email when the number of requests passes a certain threshold over a 15 minute period. | Alerts

### QUESTION 2 OF 2

Which of the below would be appropriately logged in a Flask `app` with the `log` level set to `error`?

[x] `app.log.critical("Critical!")`

[] `print("Something happened.")`

[] `app.log.warning("Warning!")`

[] None of the above

### Microsoft Learn Resources

* [Analyze your Azure infrastructure by using Azure Monitor logs](https://docs.microsoft.com/learn/modules/analyze-infrastructure-with-azure-monitor-logs/?WT.mc_id=udacity_learn-wwl)
* [Monitor apps in Azure App Service](https://docs.microsoft.com/azure/app-service/web-sites-monitor?WT.mc_id=udacity_learn-wwl)
* [Implement code that handles transient faults](https://docs.microsoft.com/azure/architecture/best-practices/transient-faults?WT.mc_id=udacity_learn-wwl)




