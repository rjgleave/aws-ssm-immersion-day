AWS Systems Manager Immersion Day 
==================================================

This repo contains collateral content to support an immersion day around AWS Systems Manager   


What's Here
-----------

This repo includes:

1. README.md - this file
2. FOLDER: dynamo - this contains code to help build the tag group table in dynamoDB.  It includes:
    *   createTagGroupTable.py - a program to create the base dynamo table
    *   DataEntryTemplate.xlsx - an Excel template with sample data for the dynamo table
    *   sample-data.csv - a CSV extract of the excel file above
    *   sample-data.json - a JSON equivalent to the CSV file above
    *   loadTagGroupTable.py - a program to load the dynamodb table with sample data
3. FOLDER: policy - contains a json file for defining a custom policy:  custom-tag-group-policy.json
4. FOLDER: tag-builder-direct  - It includes:
    *   tagbuilder.py - the main lambda program to update resources with tags.  
5. FOLDER: tag-builder-lambda - It includes:
    *   tagbuilder-paginate.py - same as lambda program above, except can be called from command line.
6. FOLDER: api-throttler - contains the lambda which is triggered by SQS.  This performs the call to the AWS ResourceGroupsAPI to update tags if you are operating in de-coupled mode (see the SQS-ENABLED environment variable below)

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