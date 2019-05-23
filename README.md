# CF-Notify-Slack

**Agenda** :
To automate and derive a better solution for retrieving the CloudFormation stacks status on Business Communication Tool (Slack)

**Prerequisites** :
1. Slack incoming webhook
2. AWS SNS Topic

**How ?** 

While deploying stack using template "CF_template.yml" use AWS SNS topic arn :

**aws cloudformation create-stack --stack-name Redis-service --template-body file://CF_template.yml --parameters ParameterKey=Service,ParameterValue=Redis  ParameterKey=Cpu,ParameterValue=512 ParameterKey=MemoryTask,ParameterValue=256 ParameterKey=DesiredCount,ParameterValue=1 ParameterKey=MinCapacity,ParameterValue=1 ParameterKey=Memory,ParameterValue=128 ParameterKey=MemoryReservation,ParameterValue=128 ParameterKey=Image,ParameterValue=023077479177.dkr.ecr.us-east-1.amazonaws.com/ishavodapoc:rediscustom ParameterKey=Port,ParameterValue=6379 --notification-arns arn:aws:sns:us-east-1:023077479177:CFSlackNotify**

Above commands send message to AWS Lambda (which is created with a trigger event of AWS SNS) and the python function **lambda.py** which is reponsible to post CF updates on slack will get trigger.
Lambda function needs Slack WEBHOOK url and Slack channel to post message

Below is the Screenshot of slack message:



