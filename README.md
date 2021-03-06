## Description

This module is a bit of a hack around the fact that AWS Chatbot managed to launch **without** API support (which means no native Terraform support) but does support configuration via Cloudformation. Behind the scenes this module is launching a Cloudformation stack on your behalf and managing things that way.

## Usage

### Basic Configuration

```hcl
module "chatbot_slack_configuration" {
  source  = "waveaccounting/chatbot-slack-configuration/aws"
  version = "1.0.0"

  configuration_name = "config-name"
  iam_role_arn       = "arn:aws:iam::1234567890:role/service-role/AwsChatBot"
  slack_channel_id   = "ABCDEADF"
  slack_workspace_id = "I342UFDS"

  sns_topic_arns = [
    "arn:aws:sns:us-west-1:1234567890:pipeline-notifications"
  ]

  tags = {
    Automation = "Terraform + Cloudformation"
  }
}
```

### Logging all events

```hcl
module "chatbot_slack_configuration" {
  source  = "waveaccounting/chatbot-slack-configuration/aws"
  version = "1.0.0"

  configuration_name = "config-name"
  iam_role_arn       = "arn:aws:iam::1234567890:role/service-role/AwsChatBot"
  logging_level      = "INFO"
  slack_channel_id   = "ABCDEADF"
  slack_workspace_id = "I342UFDS"

  sns_topic_arns = [
    "arn:aws:sns:us-west-1:1234567890:pipeline-notifications"
  ]

  tags = {
    Automation = "Terraform + Cloudformation"
  }
}
```

<!--- BEGIN_TF_DOCS --->
## Requirements

| Name | Version |
|------|---------|
| terraform | >= 0.12 |

## Providers

| Name | Version |
|------|---------|
| aws | n/a |
| local | n/a |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| configuration\_name | The name of the configuration. | `any` | n/a | yes |
| iam\_role\_arn | The ARN of the IAM role that defines the permissions for AWS Chatbot. This is a user-defined role that AWS Chatbot will assume. This is not the service-linked role. For more information, see [IAM Policies for AWS Chatbot](https://docs.aws.amazon.com/chatbot/latest/adminguide/chatbot-iam-policies.html). | `any` | n/a | yes |
| logging\_level | Specifies the logging level for this configuration. This property affects the log entries pushed to Amazon CloudWatch Logs. Logging levels include ERROR, INFO, or NONE. | `string` | `"ERROR"` | no |
| slack\_channel\_id | The ID of the Slack channel. To get the ID, open Slack, right click on the channel name in the left pane, then choose Copy Link. The channel ID is the 9-character string at the end of the URL. For example, ABCBBLZZZ. | `any` | n/a | yes |
| slack\_workspace\_id | The ID of the Slack workspace authorized with AWS Chatbot. To get the workspace ID, you must perform the initial authorization flow with Slack in the AWS Chatbot console. Then you can copy and paste the workspace ID from the console. For more details, see steps 1-4 in [Setting Up AWS Chatbot with Slack](https://docs.aws.amazon.com/chatbot/latest/adminguide/setting-up.html#Setup_intro) in the AWS Chatbot User Guide. | `any` | n/a | yes |
| sns\_topic\_arns | The ARNs of the SNS topics that deliver notifications to AWS Chatbot. | `list(string)` | n/a | yes |
| tags | Additional tags (e.g. `map('BusinessUnit','XYZ')` | `map(string)` | `{}` | no |

## Outputs

| Name | Description |
|------|-------------|
| configuration\_arn | The ARN of the Chatbot Slack configuration |
| stack\_id | The unique identifier for the stack. |

<!--- END_TF_DOCS --->
