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

