## Creating an AWS EC2 CloudWatch Alarm for StatusCheckFailed_System with Instance Recovery Action

AWS EC2 instances can experience interruptions due to system failures that affect their underlying hardware. Monitoring the system status checks and setting up automatic recovery actions can help maintain high availability. Follow these steps to create a CloudWatch alarm for the `StatusCheckFailed_System` metric with an instance recovery action.

### Step 1: Sign in to AWS Management Console
- **Access the Console**: Open your web browser and navigate to the [AWS Management Console](https://aws.amazon.com/console/).
- **Log in** with your AWS account credentials.

### Step 2: Navigate to the CloudWatch Console
- Open the **Services** menu and select **CloudWatch** under the Management & Governance section.

### Step 3: Create a New Alarm
- In the CloudWatch console, click on **Alarms** in the left-hand navigation pane.
- Click **Create alarm**.

### Step 4: Select the Metric
- Click on **Select metric**.
- Choose **EC2** under the AWS namespaces.
- Select **Per-Instance Metrics**.
- Find and select the `StatusCheckFailed_System` metric associated with the specific instance you want to monitor.
- Click on **Select metric**.

### Step 5: Configure the Alarm
- **Specify Metric and Conditions**:
  - Set the statistic to **Sum**.
  - Choose **1 minute** for the period.
  - Set the condition to **Greater/Equal** and the threshold value to **1**. This configuration triggers the alarm if the system check fails for one minute.
- **Alarm Name**: Enter a meaningful name for the alarm, such as `SystemCheckFail-Recovery-InstanceID`.
- **Alarm Description**: Optionally, provide a description that details the alarm's purpose, such as "Triggers instance recovery if system checks fail."

### Step 6: Configure Actions
- Under **Actions**, select **In alarm**.
- Click on **Add action**.
- Choose **EC2 action** and then **Recover this instance** from the dropdown menu.
- **Specify the instance**: Ensure the correct instance ID is displayed.
- After setting the recovery action, configure notification details:
  - Select **Create new topic** for SNS notifications, provide a topic name, and enter an email address to receive notifications.
  - Click on **Create topic**.

### Step 7: Add Auto Scaling Action (Optional)
- If the instance is part of an Auto Scaling group, you might want to configure additional actions to notify your Auto Scaling group of the recovery action.

### Step 8: Review and Create the Alarm
- Review all configurations to ensure they meet your requirements.
- Click on **Create alarm**.
