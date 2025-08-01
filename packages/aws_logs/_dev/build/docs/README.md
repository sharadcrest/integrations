# Custom AWS Log Integration

The custom AWS input integration offers users two ways to collect logs from AWS: from an [S3 bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/ServerLogs.html) (with or without SQS notification) and from [CloudWatch](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/WhatIsCloudWatchLogs.html).
Custom ingest pipelines may be added by adding the name to the pipeline configuration option, creating custom ingest pipelines can be done either through the API or the [Ingest Node Pipeline UI](/app/management/ingest/ingest_pipelines/).

## Collecting logs from S3 bucket

When collecting logs from S3 bucket is enabled, users can retrieve logs from S3
objects that are pointed to by S3 notification events read from an SQS queue or
directly polling list of S3 objects in an S3 bucket. 

The use of SQS notification is preferred: polling list of S3 objects is 
expensive in terms of performance and costs and should be preferably used only 
when no SQS notification can be attached to the S3 buckets. This input 
integration also supports S3 notification from SNS to SQS.

You can enable SQS notification method by setting `queue_url` and `number_of_workers` configuration values.
You can enable S3 bucket list polling method by setting `bucket_arn`, `access_point_arn`
or `non_aws_bucket_name` configuration values and `number_of_workers` value.

`queue_url`, `bucket_arn`, `access_point_arn` and `non_aws_bucket_name` cannot be set 
at the same time and at least one of these value must be set.

NOTE: To access SQS and S3, these [specific AWS permissions](https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-input-aws-s3.html#_aws_permissions_2) are required.

## Collecting logs from CloudWatch

When collecting logs from CloudWatch is enabled, users can retrieve logs from 
all log streams in a specific log group. `filterLogEvents` AWS API is used to 
list log events from the specified log group. Amazon CloudWatch Logs can be used
to store log files from Amazon Elastic Compute Cloud(EC2), AWS CloudTrail, 
Route53, and other sources.

NOTE: To access aws-cloudwatch, these [specific AWS permissions](https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-input-aws-cloudwatch.html#_aws_permissions) are required.
