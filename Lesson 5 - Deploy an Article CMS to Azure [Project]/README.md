# Project: Deploy An Article CMS to Azure

## Project Overview

In this project, you'll be given a simple Content Management System (CMS) for articles, where a user can log in, view published articles, and publish new articles. An article consists of a title, author, and body of text (to be stored in an Azure SQL Server) along with an image (to be stored in Azure Blob Storage).

The CMS includes the following components:

* A webapp using Python with the Flask framework.
* A SQL database that contains a user table and an article table for the webapp to query.
* A Blob Storage container where images are stored.

It will be up to you to create and manage the resources necessary to fully deploy both the necessary storage and compute resources for the app to Azure. As part of the project, you'll also need to analyze which resource best fits for app deployment between a VM or App Service. Lastly, you'll add in an authentication option to Sign in with Microsoft, as well as logging for successful and unsuccessful logins.

### App Example

Below is a screenshot from the Python Web Application, viewing an article that was created successfully.

![An article from the deployed CMS app](https://video.udacity-data.com/topher/2020/March/5e6f8ed6_article-cms/article-cms.png)

## Project Instructions

In this project, you will create resources in Azure. **Once you create these resources they will result in charges in your Azure account if they are not stopped or deleted**. Make sure you stop or delete resources immediately after completing the project or while you are not actively working on it.

First, take a look at the [project rubric](https://review.udacity.com/#!/rubrics/2850/view), which will be used to grade your submission. Then, get the starter code from this [repository](https://github.com/udacity/nd081-c1-provisioning-microsoft-azure-vms-project-starter).

You are expected to do the following to complete this project:

1. Create a Resource Group in Azure.
2. Create an SQL Database in Azure that contains a user table, an article table, and data in each table (populated with the scripts provided in the SQL Scripts folder).
* Provide a screenshot of the populated tables as detailed further below.
3. Create a Storage Container in Azure for `images` to be stored in a container.
* Provide a screenshot of the storage endpoint URL as detailed further below.
4. Add functionality to the Sign In With Microsoft button.
* This will require completing TODOs in `views.py` with the `msal` library, along with appropriate registration in Azure Active Directory.
5. Choose to use either a VM or App Service to deploy the FlaskWebProject to Azure. Complete the analysis template in `WRITEUP.md` (or include in the README) to compare the two options, as well as detail your reasoning behind choosing one or the other. Once you have made your choice, go through with deployment.
6. Add logging for whether users successfully or unsuccessfully logged in.
* This will require completing TODOs in `__init__.py`, as well as adding logging where desired in `views.py`.
7. To prove that the application in on Azure and working, go to the URL of your deployed app, log in using the credentials in this README, click the Create button, and create an article with the following data:
* Title: "Hello World!"
* Author: "Jane Doe"
* Body: "My name is Jane Doe and this is my first article!"
* Upload an image of your choice. Must be either a .png or .jpg. After saving, click back on the article you created and provide a screenshot proving that it was created successfully. Please also make sure the URL is present in the screenshot.
8. Log into the Azure Portal, go to your Resource Group, and provide a screenshot including all of the resources that were created to complete this project. (see sample screenshot in "example_images" folder)
9. Take a screenshot of the Redirect URIs entered for your registered app, related to the MS Login button.
10. Take a screenshot of your logs (can be from the Log stream in Azure) showing logging from an attempt to sign in with an invalid login, as well as a valid login.

![An example screenshot of all resources deployed.](https://video.udacity-data.com/topher/2020/May/5ed0057a_sample-azure-portal-resource-group/sample-azure-portal-resource-group.png)

## Submission

Your submission must include the following, as according to the [project rubric](https://review.udacity.com/#!/rubrics/2850/view):

1. A screenshot of an article created in the Article CMS on Azure. The screenshot must also include the URL. The article should have the following fields set:
Title: "Hello World!"
Author: "Jane Doe"
Body: "My name is Jane Doe and this is my first article!"
An image of your choice. It must be either a .png or .jpg.
2. A screenshot of the resource group from the Azure Portal including all of the resources that were created to complete this project. (see sample screenshot above).
3. A screenshot showing the created tables and one query of data from the initial scripts in the SQL database (see example in the project repository).
4. A screenshot showing an example of blob endpoints for where images are sent for storage (see example in project repository).
5. A screenshot of the redirect URIs related to Microsoft authentication (see example in the project repository).
6. A screenshot showing one potential form of logging with an "Invalid login attempt" and "admin logged in successfully", taken from the app's Log stream or other logs you create and store (see example in project repository). You can customize your log messages as you see fit for these situations.
7. Your application code—most importantly `__init__.py` and `views.py` since they will contain your updates for Auth and Logging.
8. Your `WRITEUP.md` file analyzing and explaining your choice between a VM or App Service.
9. OPTIONAL: A URL to your Python App Service.

#### Cleaning Up

##### IMPORTANT:

Please make sure to cleanup your resource group in Azure after receiving your grade for this course to avoid being billed for any running services when your free account with Azure expires.

## PROJECT SPECIFICATION

### Resource Group

CRITERIA | MEETS SPECIFICATIONS
---------|---------------------
All relevant resources are contained in a single resource group.| The resource group must include a Storage Account, SQL Server, SQL Database, as well as any relevant services for deploying the web app.
Provide a screenshot of the resource group in Azure, containing your running resources.

### Storage

CRITERIA | MEETS SPECIFICATIONS
---------|---------------------
Create and add article data to a SQL Server in Azure. | A SQL Server is created in Azure and is capable of storing the necessary article data (title, author, body).
Provide a screenshot from your SQL database within Azure, showing that both the posts and users tables have been created. Alternatively, if the site is still live, provide the URL for the site.
Create and upload images to a Storage Account. | A Storage Account is created in Azure and is capable of storing the necessary image data for an article.
Provide a screenshot from your Storage Account within Azure, with the blob storage endpoint URL visible (can be seen in “Settings”->”Properties”). Alternatively, if the site is still live, provide the URL for the CMS site to show images are able to be stored and viewed.

### Resource Justification

CRITERIA | MEETS SPECIFICATIONS
---------|---------------------
Analyze, choose, and justify the appropriate resource option for deploying the app. | In the provided `writeup.md` file, for both a VM or App Service solution for the CMS app:

* Analyze costs, scalability, availability, and workflow
* Choose the appropriate solution (VM or App Service) for deploying the app
* Justify your choice

This does not need to be substantially long, but should include information on all four analysis points for each option, your choice, and at least 2-3 sentences on why you choose that option.

Assess app changes that would change your decision. | In the provided `writeup.md` file, detail how the app and any other needs would have to change for you to change your decision in the last section.

This should be at least 2-3 sentences, but feel free to add as much detail as you feel necessary.

### Deployment

CRITERIA | MEETS SPECIFICATIONS
---------|---------------------
The Python web app is deployed to Azure. | The Python web app has been deployed to Azure using the chosen resource in the previous section.
As evidence, provide a screenshot of the Python application running from a browser (this can be part of the screenshot in the next section). The screenshot should include the URL and the black header that states “Article CMS”. Alternatively, you can provide a link to the deployed app, if it is still live.
The Python web app is able to connect to storage. | The Python web app is able to connect to the related storage solutions.
As evidence, provide a screenshot of the Python application running from a browser. The screenshot should include the URL and at least one article containing title, author, body, and an image. Alternatively, you can provide a link to the deployed app, if it is still live.

### Security & Monitoring

CRITERIA | MEETS SPECIFICATIONS
---------|---------------------
Add a functioning “Sign in with Microsoft” option to the app. | The Python web app has an additional, operational option to sign in with Microsoft.
As evidence, provide a screenshot of the redirect URIs configured within the App Registration page in Azure. Alternatively, you can provide a link to the deployed app, if it is still live.
Additionally, your code in views.py should appropriately implement the Microsoft sign-in button using the msal library.
Access attempts to the app are logged. | Both successful and unsuccessful attempts to access the web app are logged.
As evidence, provide a screenshot or download the logs from Azure containing at least one successful and one unsuccessful access attempt, and include in your submission files. If otherwise submitting a URL, please include a link to screenshot/logs in the “Submission Details” box on the project submission page.

### Suggestions to Make Your Project Stand Out!

1. Modify both the Python Application and SQL Database to include a Subtitle field. The field should be displayed below the Title field in the screenshot, and deployed with the app.
2. The current application does not allow for the deletion of a created article, or complete removal of an image after one is added (it can only be replaced). Add this functionality to the application.
3. The current application just uses the admin account if the user signs in with Microsoft. Adjust the app to better track which user is logged in.