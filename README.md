# Amazon-DynamoDB-pricing-and-security

A quick breakdown of Amazon DynamoDB pricing and security concepts.

## Overview

I thought that since the DynamoDB users are only increasing as time goes by I would create this repository to help newer users breakdown pricing and security concepts into more basic and staright-forward terms. This quick breakdown will be divided into two parts, starting with cost optimization and slowly getting into security concepts. By the end of this you should be able to quickly assess your needs and limits as it pertains to your DynamoDB database.

# Amazon DynamoDB pricing

DynamoDb charges for reading, writing, and storing data in your DynamoDB tables, along with any optional features you choose to enable so your utilization is a big factor that will determine price of the services that you use. DynamoDB has two capacity modes, which come with specific billing options for processing reads and writes on your tables: on-demand capicity mode: With on-demand capacity mode, you pay per request for the data reads and writes your application performs on your tables. You do not need to specify how much read and write throughput you expect your application to perform, as DynamoDB instantly accommodates your workloads as they ramp up or down and provisioned capacity mode: With provisioned capacity mode, you specify the number of reads and writes per second that you expect your application to require. You can use auto scaling to automatically adjust your table’s capacity based on the specified utilization rate to ensure application performance while reducing costs. I will include the roundabout estimate cost for each DynamoDB service, to get a more comfortable feel of service prices.


# DynamoDB detailed feature pricing (On-demand capacity)

Even though DynamoDB is one service there are a multitude of things that can determine your price output. AWS calls it DynamoDB deatiled featured pricing where pricing split up into diffrent types of DynamoDB use cases read and write requests, Data storage, backup and restore, global tables, change data capture for Amazon Kinesis Data Streams, change data capture for AWS Glue, data export to Amazon S3, data import from Amazon S3, DynamoDB Accelerator (DAX), DynamoDB streams, and data transfers. I know it's alot but were going to seperate it and break it all down (remember that some of theses pricings can be difrrent depending on the region you live in, for this specific breakdown I'm going to be using my region which is US East (Ohio)).

## Read and write requests 

When you select on-demand capacity mode for your DynamoDB table, you pay only for the reads and writes your application performs. You can make API calls as needed without managing throughput capacity on the table. DynamoDB handles the management of hardware resources to accommodate your workload with consistent, low-latency performance. DynamoDB charges one write request unit for each write (up to 1 KB) and two write request units for transactional writes. For reads, DynamoDB charges one read request unit for each strongly consistent read (up to 4 KB), two read request units for each transactional read, and one-half read request unit for each eventually consistent read. The prices for read and write requests depend on your table class. 

#### DynamoDB Standard table class:

On-Demand Throughput Type	Price

Write Request Units (WRU) -	$1.25 per million write request units and
Read Request Units (RRU) - $0.25 per million read request units


#### DynamoDB Standard-Infrequent Access (DynamoDB Standard-IA) table class:


On-Demand Throughput Type	Price

Write Request Units (WRU)	- $1.56 per million write request units and
Read Request Units (RRU)	- $0.31 per million read request units

## Data storage

You do not need to provision storage: DynamoDB monitors the size of your tables continuously to determine your storage charges. DynamoDB measures the size of your billable data by adding the raw byte size of your data plus a per-item storage overhead that depends on the features you have enabled. The price for data storage depends on your table class. 

#### DynamoDB Standard table class:

First 25 GB stored per month is free using the DynamoDB Standard table class and $0.25 per GB-month thereafter

#### DynamoDB Standard-Infrequent Access (DynamoDB Standard-IA) table class:

$0.10 per GB-month

## Backup and Restore 

DynamoDB offers two methods to back up your table data. Continuous backups with point-in-time recovery (PITR) provide an ongoing backup of your table for the preceding 35 days. You can restore your table to the state of any specified second in the preceding five weeks. On-demand backups create snapshots of your table to archive for extended periods to help you meet corporate and governmental regulatory requirements.

#### Continuous backups (PITR):

DynamoDB charges for PITR based on the size of each DynamoDB table (table data and local secondary indexes) on which it is enabled. DynamoDB monitors the size of your PITR-enabled tables continuously throughout the month to determine your backup charges and continues to bill you until you disable PITR on each table.

$0.20 per GB-month.

#### On-demand backup:

DynamoDB charges for on-demand backups based on the storage size of the table (table data and local secondary indexes). The size of each backup is determined at the time of each backup request. The total backup storage size billed each month is the sum of all backups of DynamoDB tables. DynamoDB monitors the size of on-demand backups continuously throughout the month to determine your backup charges. 

Warm Backup Storage $0.10 per GB-month and
Cold Backup Storage $0.03 per GB-month

#### Restoring a table

Restoring a table from on-demand backups or PITR is charged based on the total size of data restored (table data, local secondary indexes, and global secondary indexes) for each request.

Warm Backup Storage $0.15 per GB and 
Cold backup Storage $0.20 per GB

## Global Tables

When you select on-demand capacity mode for your DynamoDB global tables, you pay only for the resources your application uses on each replica table. Write requests for global tables are measured in replicated write request units instead of standard write request units. The number of write request units consumed for replication depends on the version of global tables you are using. The pricing depends on your table class. If you add a table replica to create or extend a global table in new Regions, DynamoDB charges for a table restore in the added Regions per gigabytes of data restored. Cross-Region replication and adding replicas to tables that contain data also incur charges for data transfer out. 

#### DynamoDB Standard table class

Global Tables Resource Type: Replicated write request unit, Price:	$1.875 per million replicated write request units

#### DynamoDB Standard-Infrequent Access (DynamoDB Standard-IA) table class

Global Tables Resource Type: Replicated write request unit, Price:	$2.344 per million replicated write request units

## Change data capture for Amazon Kinesis Data Streams

DynamoDB charges for change data capture for Amazon Kinesis Data Streams in change data capture units. DynamoDB charges one change data capture unit for each write (up to 1 KB). You pay only for the writes your application performs without having to manage throughput capacity on the table. Kinesis Data Streams charges still apply when you replicate DynamoDB changes to a Kinesis data stream.

Change data capture for Amazon Kinesis Data Streams: Price: $0.10 per million change data capture units

## Change Data Capture for AWS Glue

DynamoDB charges for change data capture for AWS Glue in change data capture units. DynamoDB charges one change data capture unit for each write (up to 1 KB). You pay only for the writes your application performs without having to manage throughput capacity on your table. AWS Glue charges still apply when you replicate DynamoDB changes to an AWS Glue target database. 

Change data capture for AWS Glue: Price: $0.10 per million change data capture units.

## Data export to Amazon S3

Use this feature to export data from your DynamoDB continuous backups (point-in-time recovery) to Amazon Simple Storage Service (Amazon S3). The supported output data formats are DynamoDB JSON and Amazon Ion. You can analyze the exported data by using AWS services such as Amazon Athena, Amazon SageMaker, and AWS Lake Formation. DynamoDB charges for data you export based on the size of each DynamoDB table (table data and local secondary indexes) at the specified point in time when the backup was created.

Data Export to Amazon S3 Price: $0.10 per GB

## Data Import to Amazon S3

Amazon DynamoDB data import provides a simple and efficient way to move data between Amazon S3 and DynamoDB tables without writing any code. You can copy tables between AWS regions and accounts to help migrate data and build new applications, facilitate data sharing and collaboration between teams, and help simplify disaster recovery and business continuity planning. Data import pricing is based on the uncompressed file size in Amazon S3. Amazon S3 charges also apply for storing your source data and for GET requests made against your Amazon S3 bucket.

Data import from Amazon S3 Price: $0.15 per GB

## DynamoDB Accelerator (DAX)

DynamoDB charges for DAX capacity by the hour and your DAX instances run with no long-term commitments. Pricing is per node-hour consumed and is dependent on the instance type you select. Each partial node-hour consumed is billed as a full hour. Pricing applies to all individual nodes in the DAX cluster. For example, if you have a three-node DAX cluster, you are billed for each of the separate nodes (three nodes in total) on an hourly basis. There is no charge for data transfer between Amazon Elastic Compute Cloud (Amazon EC2) and DAX within the same Availability Zone. Standard Amazon EC2 data transfer charges apply when transferring data between an Amazon EC2 instance and a DAX node in different Availability Zones of the same AWS Region. However, you are charged only for the data transfer into or out of the Amazon EC2 instance. There is no DAX data transfer charge for traffic into or out of the DAX node itself.

Prices: vary based on Dax Node Type, vCPU,and Memory(GIB)




![Untitled design-3.pdf](https://github.com/Rimurutempestx/Amazon-DynamoDB-pricing-and-security/files/10717688/Untitled.design-3.pdf)






DAX T3 instances run in unlimited mode, which means that you will be charged if your average CPU utilization over a rolling 24-hour period exceeds the baseline of the instance. CPU credits are charged at $0.096 per vCPU-hour. The CPU credit pricing is the same for all T3 instance sizes across all AWS Regions.

## DynamoDB Streams

DynamoDB charges for reading data from DynamoDB Streams in read request units. Each GetRecords API call is billed as a streams read request unit and returns up to 1 MB of data from DynamoDB Streams. Streams read request units are unique from read requests on your DynamoDB table. You are not charged for GetRecords API calls invoked by AWS Lambda as part of DynamoDB triggers. You also are not charged for GetRecords API calls invoked by DynamoDB global tables.

Every month, the first 2,500,000 DynamoDB Streams read request units are free
Price after the first 2,500,000: $0.02 per 100,000 DynamoDB Streams read request units thereafter.

## Data transfer

Data transfer in and out refers to transfer into and out of DynamoDB. DynamoDB does not charge for inbound data transfer, and it does not charge for data transferred between DynamoDB and other AWS services within the same AWS Region (in other words, $0.00 per GB). Data transferred across AWS Regions (such as between DynamoDB in the US East [N. Virginia] Region and Amazon EC2 in the EU [Ireland] Region) is charged on both sides of the transfer. As part of the AWS Free Tier, AWS customers receive 100 GB of free data transfer out to the internet free each month, aggregated across all AWS Services and Regions (except China and GovCloud). For more information, see the AWS Free Tier. To transfer data exceeding 500 TB per month, contact AWS.


![Data Transfer.pdf](https://github.com/Rimurutempestx/Amazon-DynamoDB-pricing-and-security/files/10718369/Data.Transfer.pdf)

# DynamoDB detailed feature pricing (provisioned capacity)

With provisioned capacity mode, you specify the number of data reads and writes per second that you require for your application. You can use auto scaling to automatically adjust your table’s capacity based on the specified utilization rate to ensure application performance while reducing costs. This pricing page details how DynamoDB charges for the core and optional features of DynamoDB.

## Read and write requests

When you select provisioned capacity mode, you specify the read and write capacity that you expect your application to require. You can use auto scaling to automatically adjust your table’s capacity based on the specified utilization rate to ensure application performance while reducing costs. DynamoDB charges one WCU for each write per second (up to 1 KB) and two WCUs for each transactional write per second. For reads, DynamoDB charges one RCU for each strongly consistent read per second, two RCUs for each transactional read per second, and one-half of an RCU for each eventually consistent read per second (up to 4 KB). You will be charged for the throughput capacity (reads and writes) you provision in your Amazon DynamoDB table, even if you do not fully utilize the provisioned capacity. The price for provisioned capacity depends on your table class. The actual reads and writes performance of your DynamoDB tables may vary and may be less than the throughput capacity that you provision.

![DynamoDB standard class.pdf](https://github.com/Rimurutempestx/Amazon-DynamoDB-pricing-and-security/files/10727038/DynamoDB.standard.class.pdf)

## Reserved cpacity

DynamoDB reserved capacity can help you save on your provisioned capacity costs by making an upfront commitment on your base level of provisioned capacity. With reserved capacity, you pay a one-time upfront fee and commit to a minimum provisioned usage level over a period of time. Reserved capacity is billed at a discounted hourly rate. Any capacity that you provision in excess of your reserved capacity is billed at undiscounted provisioned capacity rates. Reserved capacity is available for single-region, provisioned read and write capacity units (RCU and WCU) on DynamoDB tables that use the DynamoDB Standard table class. Reserved capacity is not available for tables that use the DynamoDB Standard-IA table class, or on-demand capacity.

You may purchase DynamoDB reserved capacity by submitting a request through the AWS Management Console. Reserved capacity is purchased in blocks of 100 WCUs or 100 RCUs. You cannot purchase reserved capacity for replicated WCUs (rWCUs). When you purchase reserved capacity, you must designate an AWS Region, quantity, and term. You will be charged (1) a one-time upfront fee, and (2) an hourly fee for each hour during the term based on the amount of DynamoDB reserved capacity you purchase. DynamoDB reserved capacity is also subject to all storage, data transfer, and other fees applicable under the AWS Customer Agreement or other agreement with us governing your use of our services.

![Untitled design-4.pdf](https://github.com/Rimurutempestx/Amazon-DynamoDB-pricing-and-security/files/10727056/Untitled.design-4.pdf)

## Data storage 

You do not need to provision storage: DynamoDB monitors the size of your tables continuously to determine your storage charges. DynamoDB measures the size of your billable data by adding the raw byte size of your data plus a per-item storage overhead that depends on the features you have enabled.

#### DynamoDB standard class
- First 25 GB stored per month is free using the DynamoDB Standard table class
- $0.25 per GB-month thereafter

#### DynamoDB Standard-Infrequent Access (DynamoDB Standard-IA) table class
- $0.10 per GB-month

## Backup and restore

DynamoDB offers two methods to back up your table data. Continuous backups with point-in-time recovery (PITR) provide an ongoing backup of your table for the preceding 35 days. You can restore your table to the state of any specified second in the preceding five weeks. On-demand backups create snapshots of your table to archive for extended periods to help you meet corporate and governmental regulatory requirements.

#### Continuous backups (PITR)

DynamoDB charges for PITR based on the size of each DynamoDB table (table data and local secondary indexes) on which it is enabled. DynamoDB monitors the size of your PITR-enabled tables continuously throughout the month to determine your backup charges and continues to bill you until you disable PITR on each table.

- $0.20 per GB-month

#### On-demand backup

DynamoDB charges for on-demand backups based on the storage size of the table (table data and local secondary indexes). The size of each backup is determined at the time of each backup request. The total backup storage size billed each month is the sum of all backups of DynamoDB tables. DynamoDB monitors the size of on-demand backups continuously throughout the month to determine your backup charges. You can use DynamoDB or AWS Backup to create and manage on-demand backups. With AWS Backup you can centralize and automate data protection across AWS services. AWS Backup also offers advanced features such cross-account and cross-Region on-demand backup copying, low-cost storage tier, backup tagging, and backup encryption that is independent from its source data to help meet your business continuity requirements and optimize backup costs. Additional charges apply for cross-Region data transfer.

- Warm Backup Storage:	$0.10 per GB-month
- Cold Backup Storage:	$0.03 per GB-month

(Cold backup storage is supported for on-demand backups that are managed by AWS Backup only. You can opt-in to use AWS Backup from the AWS Management Console. Backups that are transitioned to Cold Storage have a minimum 90 days of storage, and backups deleted before 90 days incur a pro-rated charge equal to the storage charge for the remaining days.)

#### Restoring a table

Restoring a table from on-demand backups or PITR is charged based on the total size of data restored (table data, local secondary indexes, and global secondary indexes) for each request.

- Warm Backup Storage:	$0.15 per GB
- Cold Backup Storage:	$0.20 per GB

(Restoring from cold backup storage is supported for on-demand backups that are managed by AWS Backup only. You can opt-in to use AWS Backup from the AWS Management Console. Cold backup storage is not applicable for continuous backups with point-in-time recovery (PITR).)

## Global tables

DynamoDB charges for global tables usage based on the resources used on each replica table. Write requests for global tables are measured in replicated WCUs instead of standard WCUs. The number of replicated WCUs consumed for replication depends on the version of global tables you are using. For more information, see Best Practices and Requirements for Managing Global Tables. The pricing depends on your table class. Read requests and data storage are billed consistently with tables that are not global tables. If you add a table replica to create or extend a global table in new Regions, DynamoDB charges for a table restore in the added Regions per gigabyte of data restored. Cross-Region replication and adding replicas to tables that contain data also incur charges for data transfer out. 

![Untitled design-5.pdf](https://github.com/Rimurutempestx/Amazon-DynamoDB-pricing-and-security/files/10727656/Untitled.design-5.pdf)

DynamoDB charges for change data capture for Amazon Kinesis Data Streams in change data capture units. DynamoDB charges one change data capture unit for each write (up to 1 KB). You pay only for the writes your application performs without having to manage throughput capacity on the table. Kinesis Data Streams charges still apply when you replicate DynamoDB changes to a Kinesis data stream.

Change data capture for Amazon Kinesis Data Streams:	$0.10 per million change data capture units

## Change data capture for AWS Glue

DynamoDB charges for change data capture for AWS Glue in change data capture units. DynamoDB charges one change data capture unit for each write (up to 1 KB). You pay only for the writes your application performs without having to manage throughput capacity on your table. AWS Glue charges still apply when you replicate DynamoDB changes to an AWS Glue target database. 

Change data capture for AWS Glue:	$0.10 per million change data capture units

## Data export to Amazon S3

Use this feature to export data from your DynamoDB continuous backups (point-in-time recovery) to Amazon Simple Storage Service (Amazon S3). The supported output data formats are DynamoDB JSON and Amazon Ion. You can analyze the exported data by using AWS services such as Amazon Athena, Amazon SageMaker, and AWS Lake Formation. DynamoDB charges for data you export based on the size of each DynamoDB table (table data and local secondary indexes) at the specified point in time when the backup was created. Additional charges apply for storing exported data in Amazon S3 and for PUT requests made against your Amazon S3 bucket. 

Data Export to Amazon S3:	$0.10 per GB

## Data import from Amazon S3

Amazon DynamoDB data import provides a simple and efficient way to move data between Amazon S3 and DynamoDB tables without writing any code. You can copy tables between AWS regions and accounts to help migrate data and build new applications, facilitate data sharing and collaboration between teams, and help simplify disaster recovery and business continuity planning. Data import pricing is based on the uncompressed file size in Amazon S3. The supported input data formats are CSV, DynamoDB JSON, and Amazon Ion. Amazon S3 charges also apply for storing your source data and for GET requests made against your Amazon S3 bucket. 

Data import from S3: $0.15 per GB

## DynamoDB Accelerator (DAX)

DynamoDB charges for DAX capacity by the hour and your DAX instances run with no long-term commitments. Pricing is per node-hour consumed and is dependent on the instance type you select. Each partial node-hour consumed is billed as a full hour. Pricing applies to all individual nodes in the DAX cluster. For example, if you have a three-node DAX cluster, you are billed for each of the separate nodes (three nodes in total) on an hourly basis. There is no charge for data transfer between Amazon Elastic Compute Cloud (Amazon EC2) and DAX within the same Availability Zone. Standard Amazon EC2 data transfer charges apply when transferring data between an Amazon EC2 instance and a DAX node in different Availability Zones of the same AWS Region. However, you are charged only for the data transfer into or out of the Amazon EC2 instance. There is no DAX data transfer charge for traffic into or out of the DAX node itself.

![Dax Node TypevCPUMemory (GiB)Pricingdax.t3.small22$0.04 Per Hourdax.t3.medium24$0.08 Per Hourdax.t2.small12$0.04 Per Hourdax.t2.medium24$0.08 Per Hourdax.r5.large216$0.255 Per Hourdax.r5.xlarge432$0.509 Per Hourdax.r.pdf](https://github.com/Rimurutempestx/Amazon-DynamoDB-pricing-and-security/files/10737056/Dax.Node.TypevCPUMemory.GiB.Pricingdax.t3.small22.0.04.Per.Hourdax.t3.medium24.0.08.Per.Hourdax.t2.small12.0.04.Per.Hourdax.t2.medium24.0.08.Per.Hourdax.r5.large216.0.255.Per.Hourdax.r5.xlarge432.0.509.Per.Hourdax.r.pdf)

## DynamoDB Streams

DynamoDB charges for reading data from DynamoDB Streams in read request units. Each GetRecords API call is billed as a streams read request unit and returns up to 1 MB of data from DynamoDB Streams. Streams read request units are unique from read requests on your DynamoDB table. You are not charged for GetRecords API calls invoked by AWS Lambda as part of DynamoDB triggers. You also are not charged for GetRecords API calls invoked by DynamoDB global tables.

- Every month, the first 2,500,000 DynamoDB Streams read request units are free
- $0.02 per 100,000 DynamoDB Streams read request units thereafter

## Data transfer

Data transfer in and out refers to transfer into and out of DynamoDB. DynamoDB does not charge for inbound data transfer, and it does not charge for data transferred between DynamoDB and other AWS services within the same AWS Region (in other words, $0.00 per GB). Data transferred across AWS Regions (such as between DynamoDB in the US East [N. Virginia] Region and Amazon EC2 in the EU [Ireland] Region) is charged on both sides of the transfer. As part of the AWS Free Tier, you receive 1 GB of free data transfer out each month.

![Untitled design-6.pdf](https://github.com/Rimurutempestx/Amazon-DynamoDB-pricing-and-security/files/10737730/Untitled.design-6.pdf)
aggregated across all AWS services except in the AWS GovCloud (US) Region.
























