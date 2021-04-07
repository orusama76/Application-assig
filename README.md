# Assesment assignment for SENTIA



## DISCLAIMER

This "result" was published solely for me not to sent an empty email of an empty repo. I wasn't aware that that was a senior cloud engineer position. Unfortunately I' am but a junior-mid network engineer that has very basic coding experience, mostly in python, and non existent cloud or IAC or even architectural design experience. 
Nevertheless I hope you enjoy my 4 day effort to learn azure cloud engineering and coding!!! ;) :D

## Introduction

**This is a very rough solution to the [Sentia Recruitment Assignment](https://github.com/sentialabs/public-cloud-recruitment/blob/master/ASSIGNEMENT.md)>**

"You have participated in a meeting with a client to assess their strategy to migrate to the public cloud. They are currently hosting a customer facing web application on their on premise emnvironment based on a NodeJS application behind an NGINX reverse proxy. They are ustilizing a MongoDB cluster for storing data as well as an FTP server for document storage. They also maintain a cron server, mostly Bash and Python scripts, relevant to a small amount of jobs that need to be executed a few times per day (no more than once per hour). All the above services are hosted on several virtual machines.

Finally, the customer currently has 3 environements, namely Test, Acceptance and Production.

The customer is interested in migrating the complete envitonment to the Public Cloud. They are not in a rush, and they have given an indication that they want to go live on the Public Cloud 12 months after they have agreed on the vendor to support them in this journey. They want to make sure that they have enough time to adjust the application to any technology related changes originating from an infrastructure perspective.

There is a hard requirement for exporting all application and infrastructure logs to an ElasticSearch Cluster. The customer needs to have access to the Kibana dashboard within their headquarters but the cluster/dashboard should not be publically accessible.

You have undertaken the task to design the future state of this environment in the public cloud. The solution needs to:

    be scalable and flexible.
    utilize managed services as much as possible.

Cost optimization should be applied when necessarty, even if a few application related modifications are necessary. Environment isolation is important, but some shared services would be acceptable if they result in major cost reduction."


## Methodology

### NodeJS

Initialy we will create an on demand SFTP Azure Container Instance (ACI). It creates a sStorage Account and a FIle Share via azure CLI. The file share is then mounted into the main Linux ACI to provide persistent storage ater the container is terminated. Later we will deploy a simulation infrastructure for on-premises two-tier Nodejs application and MongoDb on a single Ububtu server virtual machine.
Once deployment finishes, you can connect to deployed VM and verify the Mongo database as well as Nodejs application and test application by launching the same in browser. Finaly we run a reverse proxy NGINX in front of the Docker containers for more access control.

<img src="images/mongodb-sftp-nodejs.jpg"/>

### Cron Server

For this instance we will use Azure Schedule Automation and we will create a Python runbook that we will associate with the Schedule. For the bash script we will
create and store it in a storage account or Github.Then we will write a RunBook which executes the bash script on Linux VM using Custom Script extension. Finaly we will associate the playbook with the Schedule.

<img src="images/Untitled Diagram(2).jpg"/>


### ElastiSearch and Kibana

Azure tracks all the events in our Azure Account/Subscription and publishes it to Azure Activity Log service. We will take those logs and stream them to Elastic Search service and then use Kibana to visualize the logs. Ufortunately I couldnt find our  how to make the VN private.

<img src="images/elastic-kibana sta.jpg"/>

## In the Repository you will find JSON files for the NODEjs-MongoDB and Ftp Server. 
