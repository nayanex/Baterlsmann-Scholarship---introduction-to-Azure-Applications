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