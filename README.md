# Slack Summarization Bot

This is a Slack bot that summarizes messages in a thread using the OpenAI GPT-3 API. The bot is implemented as an AWS Lambda function that is triggered by an API Gateway endpoint whenever a user sends a message in a thread with the `/sumit` command. The bot summarizes all the messages in the thread and sends the summary as a private message to the user who invoked the command.

## Prerequisites

To deploy this bot, you'll need:

- An AWS account with sufficient permissions to create Lambda functions, API Gateway endpoints, CloudWatch events, S3 buckets, and Lambda function permissions.
- A Slack account with permission to create slash commands and use the Slack API.
- An OpenAI key

## Deployment

To deploy the bot, follow these steps:

1. Clone this repository and navigate to the "infrastructure" directory.

2. Set the following environment variables:

   ```
   export TF_VAR_slack_api_token=<your  Slack  API  token>

   export TF_VAR_openai_api_key=<your  OpenAI  API  key>
   ```

   Replace <your  Slack  API  token> and <your  OpenAI  API  key> with your own Slack API token and OpenAI API key, respectively.

3. Deploy using Terraform

   ```
   terraform init
   terraform plan
   terraform apply
   ```

   Once the Terraform apply is successful, the output of the command will include the API Gateway endpoint URL that you can use to trigger the Lambda function with a POST request.

4. Configure the Slack slash command to send a POST request to the API Gateway endpoint URL whenever the /sumit command is used. You can follow Slack's documentation on how to set up a slash command [here](https://api.slack.com/interactivity/slash-commands).
   Once the slash command is set up, you can test the Lambda function by sending a message in a thread with the /sumit command. The Lambda function will summarize all the messages in the thread and send the summary as a private message to the user who invoked the command.

## Cleanup

To remove all the resources created by this bot, run the following command:

```
terraform destroy
```

This will delete the Lambda function, API Gateway endpoint, CloudWatch events, S3 bucket, and Lambda function permissions created by this bot. Note that this will also delete all data stored in the S3 bucket used to store the Lambda function deployment package.
