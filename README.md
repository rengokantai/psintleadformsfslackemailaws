# psintleadformsfslackemailaws
## 4. Sending Messages to Slack
### 4 Setup Your Slack Channel and Webhook
create a private channel, add an app or custom integration->Incoming WebHooks

### 5 Test and Deploy Your Integration
create resource,create method=post, test:
```
{"text":"ke"}
```

## 5. Posting Leads in Salesforce


## 6. Sending Emails with SES
```
import boto3
        
def lambda_handler(event, context):
    if not ('email' in event):
        return {"code": 1, "message": "Must provide an email"}
    
    toEmail = event['email']
    fromEmail = "<USE VERIFIED EMAIL ADDRESS>"
    replyTo = event['email']
    name = event['first_name']
    subject = "Thank you - " + name
    message = "Here is some valuable marketing information!"

    client = boto3.client('ses')
    response = client.send_email(
		Source=fromEmail,
		Destination={
			'ToAddresses': [
				toEmail,
			],
		},
		Message={
			'Subject': {
				'Data': subject,
				'Charset': 'utf8'
			},
			'Body': {
				'Text': {
					'Data': message,
					'Charset': 'utf8'
				}
			}
		},
		ReplyToAddresses=[
			replyTo
		]
	)
		
    print response['MessageId']
    return {'code': 200, 'message': 'Success'}
```
## 7. Coding a Lambda Workflow Coordinator
### 4 JavaScript Code Review
### 7 Command Line Deployments
```
#! /bin/bash
rm index.zip
zip -r index.zip .
echo "update"
aws lambda update-function-code --function-name coordnatework --zip-file fileb://index.zip
```

