## Creating an AWS EventBridge Rule for High-Severity GuardDuty Findings

AWS GuardDuty is a threat detection service that provides detailed findings about potential security issues within your AWS environment. By creating an EventBridge rule to forward high-severity findings to an SNS topic, you can enhance your security response strategy. This guide will walk you through setting up this rule.

### Step 1: Sign in to AWS Management Console
- **Access the Console**: Open your web browser and navigate to the [AWS Management Console](https://aws.amazon.com/console/).
- **Log in** with your AWS account credentials.

### Step 2: Navigate to the EventBridge Console
- Open the **Services** menu and select **EventBridge** under the Application Integration section.

### Step 3: Create a New Rule
- In the EventBridge console, click on **Rules** in the left-hand navigation pane.
- Click **Create rule**.

### Step 4: Configure the Rule
- **Name your rule**: Enter a descriptive name, such as `HighSeverityGuardDutyFindings`.
- **Description** (optional): Provide a brief description of what the rule does.

### Step 5: Define the Event Pattern
- Under **Define pattern**, choose **Event pattern**.
- Select **Custom pattern** and enter the following pattern to filter for high-severity GuardDuty findings:
  
```json
{
  "source": [
    "aws.guardduty"
  ],
  "detail-type": [
    "GuardDuty Finding"
  ],
  "detail": {
    "severity": [
      {
        "numeric": [
          ">=",
          7
        ]
      }
    ]
  }
}
```json

This pattern specifies that the rule should trigger for GuardDuty findings where the severity level is 7 or higher.

### Step 6: Select the Event Bus
- Make sure the **Event bus** is set to **default**.

### Step 7: Set the Target
- Under **Select target**, choose **SNS topic** from the dropdown.
- **Select your SNS topic**: Choose the SNS topic to which you want to send the alerts. If you do not have an SNS topic created for this purpose, you need to create one:
- Go to the **SNS** dashboard.
- Click on **Topics** and then **Create topic**.
- Enter a name for the topic and create it.
- Come back to this setup and select the newly created topic.

### Step 8: Configure Additional Settings (optional)
- You may choose to transform the data sent to the SNS topic or configure retry policies and dead-letter queues to handle failed deliveries.

### Step 9: Create the Rule
- Review all settings to ensure they are correct.
- Click **Create** to finalize the rule.
