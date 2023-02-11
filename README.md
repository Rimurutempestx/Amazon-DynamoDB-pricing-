# Amazon-DynamoDB-pricing-and-security

A quick breakdown of Amazon DynamoDB pricing and security concepts.

## Overview

I thought that since the DynamoDB users are only increasing as time goes by I would create this repository to help newer users breakdown pricing and security concepts into more basic and staright-forward terms. This quick breakdown will be divided into two parts, starting with cost optimization and slowly getting into security concepts. By the end of this you should be able to quickly assess your needs and limits as it pertains to your DynamoDB database.

# Amazon DynamoDB pricing

DynamoDb charges for reading, writing, and storing data in your DynamoDB tables, along with any optional features you choose to enable so your utilization is a big factor that will determine price of the services that you use. DynamoDB has two capacity modes, which come with specific billing options for processing reads and writes on your tables: on-demand capicity mode and provisioned capacity mode. I will include the roundabout estimate cost for each dynamodb service, to get a more comfortable feel of service prices.

## On-demand capacity

With on-demand capacity mode, you pay per request for the data reads and writes your application performs on your tables. You do not need to specify how much read and write throughput you expect your application to perform, as DynamoDB instantly accommodates your workloads as they ramp up or down.



