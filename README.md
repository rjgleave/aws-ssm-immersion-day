AWS Systems Manager Immersion Day 
==================================================

This repo contains collateral content to support an immersion day around AWS Systems Manager   


What's Here
-----------

This repo includes:

1. README.md - this file
2. FOLDER: setup-lab - this contains code to setup the lab environment.  It includes:
    *   create-ssm-roles.yaml - a cloudformation template to create the necessary roles to perform the lab exercises
    *   create-server-fleet.yaml - a cloudformation template which will create a fleet of 4 sample EC2 instances, representing multiple operating systems.   It includes pre-built tags to eliminate busy work that is not relevant to learning about SSM.
    *   s3-bucket-permissions.json - a policy document to allow S3 to act as inventory repository
3. FOLDER: run-command - contains various CLI examples for invoking remote commands from the command line


Setup Instructions
------------------

1. Enter sample data into the spreadsheet: DataEntryTemplate.xlsx (note: column B below auto-computes)
![Data Entry Template](https://github.com/rjgleave/aws-tag-groups/blob/master/assets/tag-group-data-entry-template.png)
2. Export your data from the spreadsheet into a CSV file named: sample-data.csv
3. Convert the CSV file to JSON format.  The output file should be named: sample-data.json. You can do this with any online site such as:  http://www.convertcsv.com/csv-to-json.htm
4. Run the program to create the dynamodb table: createTagGroupTable.py
5. Run the program to load the data into the new table:  loadTagGroupTable.py
6. Verify that the tagGroup table has been created in dynamoDB
7. Create new custom policies, using the examples in the policy FOLDER: custom-tag-group-policy.json and custom-sqs-resource-api-policy.json
8. Create a service role for your main lambda (tagbuilder.py).   It should include the following policies:
    * CloudwatchActionsEc2Access
    * AWSResourceGroupsReadOnlyAccess
    * AmazonDynamoDBReadOnlyAccess
    * AmazonDynamoDBFullAccesswithDataPipeline
    * AWSLambdaBasicExecutionRole
    * ResourceGroupsandTagEditorFullAccess
    * custom-tag-group-policy (step #7 above)



__Additional Resources__

Blog: The New Resource Groups Tagging API Makes It Easier to Programmatically Manage Tags on Resources Across AWS Services:
https://aws.amazon.com/about-aws/whats-new/2017/03/the-new-resource-groups-tagging-api-makes-it-easier-to-programmatically-manage-tags-on-resources-across-aws-services/

Blog: AWS Lambda Adds Amazon Simple Queue Service to Supported Event Sources.   
https://aws.amazon.com/blogs/aws/aws-lambda-adds-amazon-simple-queue-service-to-supported-event-sources/