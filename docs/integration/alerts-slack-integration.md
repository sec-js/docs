title: Slack Alerts Integration
description: Sematext threshold, anomaly and / or heartbeat Alerts integration with Slack's real-time messaging communication tool. Use them together for seamless infrastructure and application monitoring integration with alert-messaging, and begin sending webhook notifications to your customized devops team channel

Slack Integration with Sematext Monitoring Alerts can be created:

- using incoming WebHooks with URL
- using Slack API with a Token

For any Slack-specific parameters check their:

- [Incoming WebHooks Documentation](https://api.slack.com/incoming-webhooks)
- [Slack Web API Documentation](https://api.slack.com/web)

Once your WebHooks integration is complete you will receive alert notifications via Slack.

## Incoming Webhooks Integration

### In Slack

Navigate to Slack's Custom Integrations Section “/apps/manage/custom-integrations”

![Slack Webhook Custom Integration](https://sematext.com/docs/images/integrations/slack-integration-webhook.png  "Slack Webhook Custom Integration")

Choose “Incoming Webhook”. Create Webhook and copy provided Webhook URL.

### In Sematext

Navigate to [Notification Hooks](https://apps.sematext.com/ui/hooks/create) (in [EU](https://apps.eu.sematext.com/ui/hooks/create)) and select Slack card to create a new Slack notification hook.

![Sematext Notification Hooks](https://sematext.com/docs/images/integrations/sematext-notification-hooks.png  "Sematext Notification Hook")


Enter required parameters and copy incoming webhook Slack URL into url field. Click Test button to confirm that Sematext app is sending data to Slack and save your Slack notification hook.


![Slack Incoming Webhooks Integration](https://sematext.com/docs/images/integrations/create-slack-integration.png  "Create Slack Incoming Webhooks Integration")

## Slack API Integration

### In Slack

There are two types of integration with Slack API

- using Legacy Tokens
- building Slack apps

For Legacy Tokens visit [api.slack.com/custom-integrations/legacy-tokens](https://api.slack.com/custom-integrations/legacy-tokens).

Token custom integrations is an older way for teams to build into their Slack team. To securely utilize the newest platform features like message buttons & the Events API a new Slack App needs to be created.

Visit [Building Slack apps](https://api.slack.com/slack-apps) for more information.

### In Sematext

Navigate to [Sematext Navigation Hooks](https://apps.sematext.com/ui/webhook-create) and select Slack card to create a new Slack notification hook.

![Sematext Notification Hooks](https://sematext.com/docs/images/integrations/sematext-notification-hooks.png  "Sematext Notification Hook")

Select **Slack Web API** option in the form, enter required parameters and copy Slack **TOKEN** into token field. Click Test button to confirm that Sematext app is sending data to Slack and save your Slack notification hook.

![Slack Incoming Webhooks Integration](https://sematext.com/docs/images/integrations/slack-api-integration.png  "Slack API integration")

That's it. Notifications sent to Slack can also be sent via other channels such as e-mail, PagerDuty, Nagios, etc. Check [Alerts](/docs/integration) to learn more about other channels and types of alerts available.  

We hope you enjoy using Sematext App and Infrastructure Monitoring and Log Management tools. If you need further support or have any feedback regarding our products, please don't hesitate to [contact us](mailto:support@sematext.com) ! You can also contact / talk to us using chat widget at the bottom right corner of the page or give us a shout [@Sematext](http://twitter.com/sematext).
