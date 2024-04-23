## Creating an AWS EventBridge Rule to Forward All Events to a Remote Region

Forwarding all events from one AWS region to another within the same account can help with centralized logging, monitoring, and responding to events across multiple regions. This guide will walk you through the process of setting up an EventBridge rule for this purpose.

### Step 1: Sign in to AWS Management Console
- **Access the Console**: Open your web browser and navigate to the [AWS Management Console](https://aws.amazon.com/console/).
- **Log in** with your AWS account credentials.

### Step 2: Navigate to the EventBridge Console
- Open the **Services** menu and select **EventBridge** under the Application Integration section.

### Step 3: Create a New Event Bus in the Target Region
- Before creating the rule, ensure that there is an event bus in your target region where the events will be forwarded.
- Switch to the target region by selecting it from the region dropdown menu at the top right of the AWS Management Console.
- In the EventBridge console, go to **Event buses** and click **Create event bus**.
- Name your event bus, e.g., `CentralEventBus`.
- Click **Create**.

### Step 4: Create a New Rule in the Source Region
- Switch back to the source region where your original events are generated.
- In the EventBridge console, click on **Rules** in the left-hand navigation pane.
- Click **Create rule**.

### Step 5: Configure the Rule
- **Name your rule**: Enter a descriptive name, such as `ForwardAllEventsToRemoteRegion`.
- **Description** (optional): Provide a brief description of the rule's purpose.
- Under **Define pattern**, select **Event pattern**.
- Choose **Pre-defined pattern by service** and select **All Events**.

### Step 6: Select the Event Bus
- Ensure the **Event bus** is set to **default**. This setting indicates that the rule will apply to all events on the default bus.

### Step 7: Set the Target
- Under **Select targets**, choose **Event bus in another AWS account**.
- For the **Target event bus**, specify the ARN of the event bus you created in the target region. The ARN format should be like: 
```text
arn:aws:events:<target-region>:<account-id>:event-bus/<event-bus-name>
```text
- **Account ID**: Enter your AWS account ID.

### Step 8: Configure Additional Settings (optional)
- Specify settings such as input transformations or dead-letter queues if necessary for your use case.

### Step 9: Create the Rule
- Review your settings to ensure everything is configured correctly.
- Click **Create** to finalize the rule.
