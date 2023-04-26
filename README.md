# cd-demo

This repo demonstrates how to implement GitHub actions workflows to build and deploy PRs, as well as a blue green deployments to staging and production environments.  

This repo uses a cloudformation template to deploy a stack to AWS. The stack contains an auto-scaling-group of ec2 instances, a load balancer, and other related resources.  

There are several workflows in this repo:  
 - PR - build and deploy
 - PR - delete stack
 - Blue Green Deploy Pipeline

## PR - build and deploy
This workflow is triggered when a PR is created or updated. The workflow does the following:  
 - Build and run unit tests
 - Build AMI using Packer
 - Deploy a test stack in AWS

## PR - delete stack
This workflow is triggered when a PR is closed. The workflow deletes the test stack created by `PR - build and deploy`.  

## Blue Green Deploy Pipeline
This workflow is triggered on push to main. The workflow can also be triggered manually. The workflow does the following:  
 - Build and run unit tests (skipped if AMI is provided)
 - Build AMI using Packer (skipped if AMI is provided)
 - Deploy stack to staging and production environments in AWS
