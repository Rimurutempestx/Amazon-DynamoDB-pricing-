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




