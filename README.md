[![Link to aws-billing-to-slack in hipages Developer Portal, Component: aws-billing-to-slack](https://backyard.k8s.hipages.com.au/api/badges/entity/default/Component/aws-billing-to-slack/badge/pingback "Link to aws-billing-to-slack in hipages Developer Portal")](https://backyard.k8s.hipages.com.au/catalog/default/Component/aws-billing-to-slack)
[![Entity owner badge, owner: platform](https://backyard.k8s.hipages.com.au/api/badges/entity/default/Component/aws-billing-to-slack/badge/owner "Entity owner badge")](https://backyard.k8s.hipages.com.au/catalog/default/Component/aws-billing-to-slack)
# AWS Billing to Slack

![image](https://user-images.githubusercontent.com/261584/66362145-3903a200-e947-11e9-91bd-6e40e5919ac4.png)

Sends daily breakdowns of AWS costs to a Slack channel.

# Install

1. Install [`serverless`](https://serverless.com/), which I use to configure the AWS Lambda function that runs daily.

    ```
    npm install -g serverless
    npm install
    ```

1. Create an [incoming webhook](https://www.slack.com/apps/new/A0F7XDUAZ) that will post to the channel of your choice on your Slack workspace. Grab the URL for use in the next step.

1. Deploy the system into your AWS account, replacing the webhook URL below with the one you generated above.

    ```
    serverless deploy --slack_url="https://hooks.slack.com/services/xxx/yyy/zzzz"
    ```

    You can also run it once to verify that it works:

    ```
    serverless invoke --function report_cost --slack_url="https://hooks.slack.com/services/xxx/yyy/zzzz"
    ```

## Support for AWS Credits

If you have AWS credits on your account and want to see them taken into account on this report, head to [your billing dashboard](https://console.aws.amazon.com/billing/home?#/credits) and note down the "Expiration Date", "Amount Remaining", and the "as of" date towards the bottom of the page. Add all three of these items to the command line when executing the `deploy` or `invoke`:

    ```
    serverless deploy \
        --slack_url="https://hooks.slack.com/services/xxx/yyy/zzzz" \
        --credits_expire_date="mm/dd/yyyy" \
        --credits_remaining_date="mm/dd/yyyy" \
        --credits_remaining="xxx.xx"
    ```
