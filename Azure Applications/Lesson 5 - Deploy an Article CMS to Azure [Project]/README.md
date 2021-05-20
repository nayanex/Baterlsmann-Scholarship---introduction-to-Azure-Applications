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
