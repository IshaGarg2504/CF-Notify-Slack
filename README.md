# CF-Notify-Slack

**Agenda** :
To automate and derive a better solution for retrieving the CloudFormation stacks status on Business Communication Tool (Slack)

**Prerequisites** :
1. Slack incoming webhook
2. AWS SNS Topic

**How ?** 

While deploying stack using template "CF_template.yml" use AWS SNS topic arn :

**aws cloudformation create-stack --stack-name Redis-service --template-body file://CF_template.yml --parameters ParameterKey=Service,ParameterValue=Redis  ParameterKey=Cpu,ParameterValue=<> ParameterKey=MemoryTask,ParameterValue=<> ParameterKey=DesiredCount,ParameterValue=<> ParameterKey=MinCapacity,ParameterValue=<> ParameterKey=Memory,ParameterValue=<> ParameterKey=MemoryReservation,ParameterValue=<> ParameterKey=Image,ParameterValue=_Docker Image URL_ ParameterKey=Port,ParameterValue=_PORT_ --notification-arns _Topic ARN_**

Above commands send message to AWS Lambda (which is created with a trigger event of AWS SNS) and the python function **lambda.py** which is reponsible to post CF updates on slack will get trigger.
Lambda function needs Slack WEBHOOK url and Slack channel to post message

Below is the Screenshot of how slack message appear:

./slack_message.jpg

