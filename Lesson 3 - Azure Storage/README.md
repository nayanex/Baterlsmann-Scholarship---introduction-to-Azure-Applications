## Introduction

[![Introduction](https://img.youtube.com/vi/rc_GZ9vPE2U/0.jpg)](https://www.youtube.com/watch?v=rc_GZ9vPE2U)

In this lesson, you will:

* Take a look at all the different storage options available in Azure and their benefits
* Take a deep dive on Azure SQL Databases and Blob Storage, including creating the related resources and uploading data
* Connect those storage services to your app


![The Course and Lesson Outline](https://video.udacity-data.com/topher/2020/July/5f10a6f7_course-outline-storage/course-outline-storage.png)

## Big Picture: Storage

[![Big Picture - Storage](https://img.youtube.com/vi/swQo_XH9Ngg/0.jpg)](https://www.youtube.com/watch?v=swQo_XH9Ngg)

Some of the benefits of using Azure for storage are:

* Automated backup and recovery
* An option to replicate data at multiple data centers worldwide to help prevent outages from unplanned events, such as hardware failure.
* Data analytics support
* Data encryption for added security
* Support for the storage of multiple data types. Azure is designed to hold 3 main types data—relational data, non-relational data or NoSQL data, and unstructured data such as images.
* Scale up or scale out when demand is high and scale back when demand is low.
* Eliminate the expense of having to purchase, install, configure, and maintain on premises hardware.

### Azure Storage Options

Among others, some of the Azure Storage options are:

* Azure SQL Server and SQL Database
* Azure Blob Storage
* Azure CosmosDB
* Disk Storage
* Azure Data Lake Storage
* HPC Cache

### Microsoft Learn Resources

* [Core Cloud Services - Azure data storage options](https://docs.microsoft.com/learn/modules/intro-to-data-in-azure/?WT.mc_id=udacity_learn-wwl)
* [Choose a data storage approach in Azure](https://docs.microsoft.com/learn/modules/choose-storage-approach-in-azure/?WT.mc_id=udacity_learn-wwl)
* [Learning Path: Store data in Azure](https://docs.microsoft.com/learn/paths/store-data-in-azure/?WT.mc_id=udacity_learn-wwl)
* [Learning Path: Architect a data platform in Azure](https://docs.microsoft.com/learn/paths/architect-data-platform/?WT.mc_id=udacity_learn-wwl)

## Azure SQL Databases

[![Azure SQL Databases](https://img.youtube.com/vi/eZHNDuYasj8/0.jpg)](https://www.youtube.com/watch?v=eZHNDuYasj8)

* Azure SQL databases are used for structured, relational data.
* In Azure, you also need to first create a related SQL server to hold the database, although you can create multiple SQL databases under a single SQL server.
* Azure SQL databases do not have a free tier option like we saw with App Services earlier; however, when you sign up for a new free Azure account, you get 12 months of up to 250GB of Azure SQL database storage. The lowest tier is currently ~$5 / month otherwise for a small amount of storage.

### Creating an Azure SQL Database in the Portal

To create an Azure SQL Database in the Azure Portal:

1. Find the "SQL databases" service in Azure.
2. Click "Create SQL Database".
3. Select the appropriate subscription and resource group (likely “resource-group-west”).
4. Enter a database name.
5. If you already have a SQL server, you can use it; however, you likely need to click "Create New".

* If creating a new SQL server, enter a server name, and then admin and password - make sure you can remember these, or you will not be able to access the server when necessary. The admin name cannot just be "admin".
* Set the location to match the resource group.

6. Keep SQL elastic pool on the default of "No".
7. Under Compute+Storage, click on "Configure Database". While General Purpose won't end up charging you anything for the short time the server is live for these exercises, you might as well press "Looking for basic, standard, premium?", and change it to "Basic".
8. Press the "Next: Networking" button, then select "Public Endpoint", and set both of the Firewall rules that appear to "Yes". This will allow us to more easily access the SQL database later on within our app.
9. Click "Review + Create" and then "Create" to create the database, then wait for it to deploy.

### QUIZ QUESTION

Azure SQL Databases can be left up on the basic tier for no cost forever.

[x] False

[ ] True

### Microsoft Learn Resources

[Work with relational data in Azure](https://docs.microsoft.com/learn/paths/work-with-relational-data-in-azure/?WT.mc_id=udacity_learn-wwl)

[Provision an Azure SQL database to store application data](https://docs.microsoft.com/learn/modules/provision-azure-sql-db/?WT.mc_id=udacity_learn-wwl)

[Create an Azure Database for PostgreSQL server](https://docs.microsoft.com/learn/modules/create-azure-db-for-postgresql-server/?WT.mc_id=udacity_learn-wwl)

## Adding Data to the Database

[![Adding Data To The Database](https://img.youtube.com/vi/nOqbJ-HTicQ/0.jpg)](https://www.youtube.com/watch?v=nOqbJ-HTicQ)

To add data to the SQL Database, I performed the following:

1. Once the SQL database is deployed, click on its name to access it (you may need to go back to the main "SQL databases" page in Azure).
2. Click on the "Query editor" in the left side menu, and then log in with my SQL Server credentials.
3. I pasted the query from my `posts-table-init.sql` script into the query window, and hit "Run"; you should see `Query succeeded: Affected rows: 3`.
4. On the left side of the query window, I clicked on the "Tables" folder, and double-checked that the `dbo.POSTS` table was successfully created with the correct fields.
5. I ran a new query with `SELECT * FROM posts`, to see the three posts listed.

### QUIZ QUESTION

Which of the following would be appropriate data to store in a SQL database?

[x] Information about books like author, title, year published, and summary

[ ] Unstructured event data

[ ] Images or code repositories

[x] Sales invoices, such as id, price, and item quantities

## Exercise: Azure SQL Databases

In this exercise, you will create an Azure SQL Database and add data to it. 

1. Deploy a SQL Database in Azure called “database-west” to the “resource-group-west” resource group (or whichever resource group you have been using in earlier exercises).
2. Within the Azure portal, add the data from the script in the `sql_scripts` directory [here](https://video.udacity-data.com/topher/2020/July/5f075d26_sql-scripts/sql-scripts.zip) to the database. You should be able to run a `SELECT` query afterward on the `animals` table to see the example animals populated in your database.

**Note:** Azure free accounts only allow 250GB of free storage using SQL Databases. Once you get to the end of this lesson, you will want to delete the SQL Database and SQL Server to avoid incurring any charges.

## Solution: Azure SQL Databases

[![Solution - Azure SQL Databases Part 1](https://img.youtube.com/vi/xyfZkpSg2bs/0.jpg)](https://www.youtube.com/watch?v=xyfZkpSg2bs)

### Create SQL Server

```bash
az sql server create \
--admin-user udacityadmin \
--admin-password p@ssword1234 \
--name hello-world-server \
--resource-group resource-group-west \
--location westus2 \
--enable-public-network true \
--verbose
```

### Create Firewall rule

Next, we have to create two firewall rules. These are the same two rules we checked as yes when we used the portal.

The first one is to allow Azure services and resources to access the server we just created.

```bash
az sql server firewall-rule create \
-g resource-group-west \
-s hello-world-server \
-n azureaccess \
--start-ip-address 0.0.0.0 \
--end-ip-address 0.0.0.0 \
--verbose
```

This second rule is to set your computer's public Ip address to the server's firewall. You'll need to find your computer's public ip address for this part.

I'm using macOS, so I used the command `curl ifconfig.me`; you can use `ipconfig` in the command prompt if you are on Windows.

#### Create clientIp firewall rule

```bash
az sql server firewall-rule create \
-g resource-group-west \
-s hello-world-server \
-n clientip \
--start-ip-address <PUBLIC-IP-ADDRESS> \
--end-ip-address <PUBLIC_IP_ADDRESS> \
--verbose
```

### Create SQL Database

Finally, to create the database itself, I used the below command.

```bash
az sql db create \
--name hello-world-db \
--resource-group resource-group-west \
--server hello-world-server \
--tier Basic \
--verbose
```

### Adding Data

We'll again add data to the database through the portal, as that's the most straightforward method for now (until we connect to an app).

[![Solution - Azure SQL Databases Part 2](https://img.youtube.com/vi/C6nP7JAozDM/0.jpg)](https://www.youtube.com/watch?v=C6nP7JAozDM)

### Cleanup

You can find the CLI commands for cleaning up the SQL resources below.

#### Delete DB

```
az sql db delete \
--name hello-world-db \
--resource-group resource-group-west \
--server hello-world-server \
--verbose
```

#### Delete SQL Server

```
az sql server delete \
--name hello-world-server \
--resource-group resource-group-west \
--verbose
```

## Blob Storage

[![Blob Storage Part 1](https://img.youtube.com/vi/rvqm0KK6NtY/0.jpg)](https://www.youtube.com/watch?v=rvqm0KK6NtY)

Before discussing Blob Storage Accounts, you may need to know what a **Blob** is in the first place.

A **Binary Large Object** or Blob is a data type that can store unstructured (binary) data and is used to store things like images or videos in a database. Blobs are not the go-to choice when it comes to structured data that is queried frequently, such as user profile information. They have higher latency than memory and local disk and don't have the indexing features that make databases efficient at running queries. Blobs are commonly used in combination with databases to store non-queryable data, such as a profile picture for a user's profile. Each user record in the database would include the URL of the blob containing the user's photo.

### Azure Storage Accounts

An Azure storage account can store data objects you create, such as blobs and files. This storage account provides a unique namespace in Azure for your data, and every item that you store has an address that includes your unique account name. It’s worth noting the name of the storage account can contain only lowercase letters and numbers.

In this course, you'll mostly utilize *General-purpose v2* storage accounts, which provide support and the latest features for Azure Storage services such as blobs, Data Lake Gen2, Files, Disks, Queues, and Tables. This type of storage account is recommended for most scenarios when using Azure Storage services.

Storage accounts can contain multiple blob containers within them, such as "images" and "movies" containers, to organize different data files. From there, each container can have many blobs inside of them (the files themselves).

![The Blob Storage Hierarchy - "Udacity" is the storage account, with "Pictures" and "Videos" as containers, each with more than one blob inside.](https://video.udacity-data.com/topher/2020/July/5f10b31c_blob-storage-hierarchy/blob-storage-hierarchy.png)

### Blob Storage Lifecycle

We discussed blob storage tiers—hot, cold, and archive. These are set based on how frequently data will be accessed, with hot accessed the most frequently, with relatedly lower latency for requests, but higher costs.

Blob storage offers a rule-based policy you can use to transition your data between these tiers to optimize performance and cost. This is shown again in the below graphic - while your blobs may start in a Hot container, they could be moved to a Cool container if they have not been modified in the past 30 days. From there, if they have not been modified in 90 days, they could be transitioned to Archive storage; you could then perhaps delete them after a year of non-usage.

![The blob storage lifecycle.](https://video.udacity-data.com/topher/2020/July/5f10b341_blob-storage-lifecycle/blob-storage-lifecycle.png)

### QUIZ QUESTION

True or False: Blob Storage and SQL Databases can be used interchangeably.

[x] False

[ ] True


### Creating Blob Storage in the Portal

[![Blob Storage Part 2](https://img.youtube.com/vi/9-ZCMnrULsk/0.jpg)](https://www.youtube.com/watch?v=9-ZCMnrULsk)

To create a blob storage account on Azure Portal, I did the following:

#### Create a Storage Account in Azure:

1. Click Create a resource
2. Search for storage account
3. Select the appropriate subscription and resource group (likely “resource-group-west”).
4. Enter a storage account name, note—it can only be lowercase letters and numbers. “helloworld1234”
5. Set the location to West US 2 to match the resource group.
6. Leave "Performance" as Standard, while making sure "Account kind" is StorageV2. This could also be BlobStorage, but StorageV2 is preferred.
7. We’ll leave replication on the default setting
8. Set "Access tier" to Cool - in a live production app, you may need this to be Hot, but in our case, Cool will work just fine.
9. Click "Next: Networking" to confirm that the storage account is using a Public endpoint (all networks)
10. Click "Next: Data Protection", "Next: Advanced", then set "Blob public access" to "Enabled".
11. Click "Review + Create" and then "Create" to create the database, then wait for it to deploy.

#### To add a Blob Container called `images`:

1. Once the Storage account is deployed, click on its name to access it (you may need to go back to the main "Storage accounts" page in Azure).
2. Click on the "Containers" button in the storage account's "Overview" page.
3. Click "+ Container", then add the name of `images`.
4. Set "Public access level" to Container, and click "Create".

**NOTE:** I had to refresh my page a few times before I could access the container.

#### Adding Images to the Container

To add an image to the Blob Container:

1. Click on the container named `images`.
2. Click "Upload", and add an image of your choosing.
3. Once the image appears within the container view, click on it, and copy the "URL" property.
4. Paste the URL into your browser to see if the image appropriately loads.


### QUIZ QUESTION

You are trying to pull in some images from blob storage into your app, but have been unsuccessful. Which of the following changes might resolve this?


[x] Give the blob storage container a public endpoint.

[x] Add the access key for the blob storage account into the call.

[ ] Register the app with the blob storage container.

[ ] None of the above.

### Microsoft Learn Resources

[Create an Azure Storage account](https://docs.microsoft.com/learn/modules/create-azure-storage-account/?WT.mc_id=udacity_learn-wwl)

[Secure your Azure Storage account](https://docs.microsoft.com/learn/modules/secure-azure-storage-account/?WT.mc_id=udacity_learn-wwl)

[Organize Azure storage blobs with properties and metadata](https://docs.microsoft.com/learn/modules/organize-blobs-properties-metadata/?WT.mc_id=udacity_learn-wwl)

[Implement data archiving and retention](https://docs.microsoft.com/azure/storage/blobs/storage-blob-storage-tiers?tabs=azure-portal&WT.mc_id=udacity_learn-wwl)

[Implement hot, cool, and archive storage](https://docs.microsoft.com/azure/storage/blobs/storage-blob-storage-tiers?tabs=azure-portal&WT.mc_id=udacity_learn-wwl) (same content as above)

[Move items in Blob storage between storage accounts or containers](https://docs.microsoft.com/learn/modules/copy-blobs-from-command-line-and-code/?WT.mc_id=udacity_learn-wwl)

[Blob Storage lifecycle](https://docs.microsoft.com/azure/storage/blobs/storage-lifecycle-management-concepts?tabs=azure-portal&WT.mc_id=udacity_learn-wwl)

## Exercise: Blob Storage

In this exercise, you will create a Storage Account with a Blob Container capable of storing images. 

1. Deploy a Storage Account in Azure to the “resource-group-west” resource group (or whichever resource group you have been using in earlier exercises).
2. Add a Blob Container to the Storage Account named `images`.
3. Upload an image into the container.

**Note:** Azure free accounts only allow 5GB of free blob storage. Once you get to the end of this lesson, you will want to delete the Storage Account to avoid incurring any charges.

## Solution: Blob Storage

[![Solution - Blob Storage](https://img.youtube.com/vi/0fpwGAA0BFw/0.jpg)](https://www.youtube.com/watch?v=0fpwGAA0BFw)

In this solution video, I showed you an alternative way to create an Azure Storage Account and a Storage Container using Azure CLI.

First we create our storage account. We use the following command:

```
az storage account create \
 --name helloworld12345 \
 --resource-group resource-group-west \
 --location westus2
```

The storage will default to general purpose V2 and the access tier cannot be set, so it will default to hot.

Then we create our container.

```
az storage container create \
 --account-name helloworld12345 \
 --name images \
 --auth-mode login \
 --public-access container
```

You can go to the portal to check that the storage account and container have been created. You can then upload an image through the portal.

Lastly, we set up a new lifecycle management rule for an alert, which can be found under "Blob Service" within your Storage Account, under "Lifecycle Management".

## Connecting Your App to Storage

[![Connecting Your App To Storage Part 1](https://img.youtube.com/vi/4n_L0OlldXc/0.jpg)](https://www.youtube.com/watch?v=4n_L0OlldXc)

To connect an app to the storage we've set up, we need a few things from each storage service.

From the SQL server and database:

1. SQL Server server name (the name of the sql server with .database.windows.net appended to it)
2. Admin username
3. Admin password
4. SQL Database name

From blob storage:

1. Storage account name
2. A storage account access key
3. Container name

In our case, we're keeping the management of these values a bit simpler with a config.py file that will be imported into the primary app file.

### Azure Storage Blob Library for Python

[![Connecting Your App To Storage Part 2](https://img.youtube.com/vi/Fra5C7MdRGc/0.jpg)](https://www.youtube.com/watch?v=Fra5C7MdRGc)

In order to interact with our Azure blob storage from within the Python web app, we'll need the [Azure Storage Blob Library](https://pypi.org/project/azure-storage-blob/). Note that you can install this with `pip install` azure-storage-blob`, and you'll need to make sure to include the library in your `requirements.txt` file in your own apps.

We will largely focus on the `BlobServiceClient` class. This class has three methods we’ll use:

* `get_blob_client` - creates a blob client using the filename as the name for the blob
* `upload_blob` - upload the file to the blob container
* `delete_blob` - delete a blob from a blob container

#### Uploading a blob

Here is the code I included for uploading a blob.

```python
from azure.storage.blob import BlobServiceClient

blob_container = app.config['BLOB_CONTAINER']
storage_url = "https://{}.blob.core.windows.net/".format(app.config['BLOB_ACCOUNT'])
blob_service = BlobServiceClient(account_url=storage_url, credential=app.config['BLOB_STORAGE_KEY'])

blob_client = blob_service.get_blob_client(container=blob_container, blob=filename)
blob_client.upload_blob(file)
```

Note that I am getting the `BLOB_CONTAINER` name from the configuration file, which was attached to the Flask app separately. I do a similar procedure for getting the `BLOB_ACCOUNT` AND `BLOB_STORAGE_KEY` where needed. I then use the aforementioned `get_blob_client` and `upload_blob` functions to upload a file.

You might notice that there is a `filename` and `file` used here - these are not the same things! The `filename` is just the name of the file, e.g. `test_image.png`, while the `file` is the actual file object. So, the blob client is first called to create a blob with the given `filename`, and then the `file` is uploaded into that `filename` blob.

#### Deleting a blob

Assuming you've already defined the `blob_service` from before, you just need to get a new blob client with `get_blob_client` for the related container and `filename`, then `delete_blob`.

```
blob_client = blob_service.get_blob_client(container=blob_container, blob=filename)
blob_client.delete_blob()
```

It's important to note here you don't need a file to feed to `delete_blob` - by specifying the `filename` when you `get_blob_client`, it already knows what blob you are referring to.

### QUIZ QUESTION

Match the below endpoints to which resource they are related to. Only one goes with each!

ENDPOINT                | ASSOCIATED RESOURCE
------------------------|---------------------

`.database.windows.net` | SQL Server


`.azurewebsites.net`    | App Service


`.blob.core.windows.net`| Storage Account


### QUIZ QUESTION

You create a book app showing book names, authors and front covers. You successfully connect your app to storage, and can see information queried from a SQL database within the app. When you add images to the app through your blob storage account, you don't see any errors, but they show up as broken images within the app afterward. They do appear in the container in the portal. What went wrong?

[ ] The app is failing to connect to the SQL database

[x] The app may not have any way to associate the book cover image to related query data

[ ] The app is failing to connect to blob storage

[ ] You need to deploy the app with `az webapp up`

### Microsoft Learn Resources

* [Connect an app to Azure Storage](https://docs.microsoft.com/learn/modules/connect-an-app-to-azure-storage/?WT.mc_id=udacity_learn-wwl)

* [Store application data with Azure Blob storage](https://docs.microsoft.com/learn/modules/store-app-data-with-azure-blob-storage/?WT.mc_id=udacity_learn-wwl)


## Solution: Connecting Your App to Storage

[![Solution - Connecting Your App To Storage](https://img.youtube.com/vi/7Wev-BXDovs/0.jpg)](https://www.youtube.com/watch?v=7Wev-BXDovs)


### To connect with the SQL Database:

1. Within `config.py`, fill out the:

* `SQL_SERVER` with the URL of your SQL Server, e.g. `{YOUR-SQL_SERVER}.database.windows.net`
* `SQL_DATABASE` with the name of your SQL Database
* `SQL_USER_NAME` with the username for your SQL Server
* `SQL_PASSWORD` with the password for your SQL Server


### To connect to the Blob Storage Container:

1. Within `config.py`, fill out the:

* `BLOB_ACCOUNT` with the name of your storage account (above the container level)
* `BLOB_STORAGE_KEY` with the primary access key for your storage account. From the Azure portal, navigate to the storage account, and then under "Setting", click on "Access keys". Copy and paste the "Key" under "key1", including the double equal signs ("==") at the end.
* `BLOB_CONTAINER` with the name of your blob container, likely `images`

2. Within `models.py`, you'll need to use the `BlobServiceClient` called `blob_service` to get a Blob Client using the container name and related filename, and then either upload or delete the blob as follows:

```python
try:
     blob_client = blob_service.get_blob_client(container=blob_container, blob=filename)
     blob_client.upload_blob(file)
     if self.image_path: # Get rid of old image, since it's replaced
         blob_client = blob_service.get_blob_client(container=blob_container, blob=self.image_path)
         blob_client.delete_blob()
```

### Why to Use a Random Filename

You might be wondering why a random filename was chosen for our blob upload. Well, let's say you've created an app, and uploaded a `tiger.png` file to it. You give access to some of your friends to add more animals to it, and as a joke, they upload a picture of an elephant under the name `tiger.png` as well. Your original tiger image would be deleted and replaced.

Even outside of a friendly joke, it's quite likely as your app scales up to thousands (and hopefully millions!) of users, they will be uploading files with the same names as others, if you don't randomize them. With unique, random filenames, you won't have to worry about this issue.
