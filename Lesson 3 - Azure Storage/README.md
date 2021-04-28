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

[![Adding Data To The Database](https://img.youtube.com/vi/nOqbJ/0.jpg)](https://www.youtube.com/watch?v=nOqbJ)

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

## Connecting Your App to Storage

To connect an app to the storage we've set up, we need a few things from each storage service.

From the SQL server and database:

SQL Server server name (the name of the sql server with .database.windows.net appended to it)
Admin username
Admin password
SQL Database name
From blob storage:

Storage account name
A storage account access key
Container name
In our case, we're keeping the management of these values a bit simpler with a config.py file that will be imported into the primary app file.

Azure Storage Blob Library for Python

In order to interact with our Azure blob storage from within the Python web app, we'll need the Azure Storage Blob Library. Note that you can install this with pip install azure-storage-blob, and you'll need to make sure to include the library in your requirements.txt file in your own apps.

We will largely focus on the BlobServiceClient class. This class has three methods we’ll use:

get_blob_client - creates a blob client using the filename as the name for the blob
upload_blob - upload the file to the blob container
delete_blob - delete a blob from a blob container
Uploading a blob
Here is the code I included for uploading a blob.

from azure.storage.blob import BlobServiceClient

blob_container = app.config['BLOB_CONTAINER']
storage_url = "https://{}.blob.core.windows.net/".format(app.config['BLOB_ACCOUNT'])
blob_service = BlobServiceClient(account_url=storage_url, credential=app.config['BLOB_STORAGE_KEY'])

blob_client = blob_service.get_blob_client(container=blob_container, blob=filename)
blob_client.upload_blob(file)
Note that I am getting the BLOB_CONTAINER name from the configuration file, which was attached to the Flask app separately. I do a similar procedure for getting the BLOB_ACCOUNT AND BLOB_STORAGE_KEY where needed. I then use the aforementioned get_blob_client and upload_blob functions to upload a file.

You might notice that there is a filename and file used here - these are not the same things! The filename is just the name of the file, e.g. test_image.png, while the file is the actual file object. So, the blob client is first called to create a blob with the given filename, and then the file is uploaded into that filename blob.

Deleting a blob
Assuming you've already defined the blob_service from before, you just need to get a new blob client with get_blob_client for the related container and filename, then delete_blob.

blob_client = blob_service.get_blob_client(container=blob_container, blob=filename)
blob_client.delete_blob()
It's important to note here you don't need a file to feed to delete_blob - by specifying the filename when you get_blob_client, it already knows what blob you are referring to.

