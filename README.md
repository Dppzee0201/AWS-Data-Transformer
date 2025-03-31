# AWS-Data-Transformer
This project converts CSV files into JSON format using AWS services. The pipeline is built using AWS Glue, Lambda, CloudWatch, and S3 for automation and monitoring.

<img src="https://github.com/user-attachments/assets/aaef1b48-e03b-45e2-879a-936671e640d2" alt="Architecture Diagram" width="300"/>

## AWS Services Used

- **AWS S3**: Stores the input CSV files and output JSON files.
- **AWS Glue**: Processes the CSV file and converts it into JSON.
- **AWS Lambda**: Triggers the conversion process upon file upload.
- **AWS CloudWatch**: Logs and monitors the process execution.

## Architecture

1. **Upload CSV**: A CSV file is uploaded to an S3 bucket.
2. **Lambda Trigger**: A Lambda function gets triggered upon file upload.
3. **AWS Glue Processing**: Glue extracts, transforms, and loads (ETL) the CSV data into JSON format.
4. **Store JSON**: The transformed JSON file is stored in another S3 bucket.
5. **Logging & Monitoring**: CloudWatch captures logs and metrics for debugging and monitoring.

## Prerequisites

- An AWS account with permissions to use S3, Glue, Lambda, and CloudWatch.
- CSV files for testing.
- Basic knowledge of AWS services.

## Setup & Deployment

### Step 1: Create S3 Buckets

- Create an S3 bucket to store CSV files (`csv-input-bucket`).
- Create another S3 bucket for storing JSON output (`json-output-bucket`).

### Step 2: Configure AWS Glue

- Create a Glue Crawler to read the CSV data from the input bucket.
- Create an ETL Job to convert the CSV to JSON and write it to the output bucket.

### Step 3: Deploy AWS Lambda Function

- Create a Lambda function to trigger Glue upon CSV upload.
- Use an S3 event trigger to invoke the Lambda function.

### Step 4: Configure CloudWatch

- Set up CloudWatch logs to capture logs from Glue and Lambda.
- Configure alarms for failure scenarios.

## Lambda Code (Python)

```import json
import boto3

glueClient = boto3.client('glue')
def lambda_handler(event, context):
glueClient.start_job_run(JobName="csvtojson")

return "Job started"
```

## Running the Project

1. Upload a CSV file to the `csv-input-bucket`.
2. The Lambda function triggers the Glue job.
3. Glue processes the file and stores the JSON in `json-output-bucket`.
4. Monitor logs in CloudWatch for execution status.

## Conclusion

This project automates CSV to JSON conversion using AWS services, ensuring a scalable and serverless architecture for data transformation.

