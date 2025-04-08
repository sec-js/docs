title: Custom Webhooks Alerts Integration
description: Sematext threshold, anomaly and / or heartbeat Alerts integration with generic webhooks. Use them together for seamless infrastructure and application monitoring integration with alert-messaging, and begin sending real-time notifications 

Automate incident management of your IT services when a metric alert is triggered with our custom generic Webhooks-based integration. Sematext has threshold, anomaly and / or heartbeat Alerts integration with custom webhooks used to trigger a POST request to the URL you set in JSON format. 

Webhooks are real-time notifications that send you a specially formatted message whenever an alert occurs in your applications. Using this approach, whenever problem in your environment that affects real users is detected, a webhook triggers an HTTP POST request to a target URL that you specify. The payload message of the HTTP POST request is completely customizable, as long as it represents valid JSON syntax.

Your devops team will be able to:

- quickly respond to service failures and minimize downtime
- proactively use Sematext APM services to identify performance issues before the user experience is affected
- pinpoint the root cause of the problem and focus on fixing rather than investigating your IT infrastructure and application issues

## **In Sematext**

Navigate to [Sematext Navigation Hooks](https://apps.sematext.com/ui/hooks/create) ([EU](https://apps.eu.sematext.com/ui/hooks/create)) and select Custom Webhooks card to create a new notification hook.

![Sematext Notification Hooks](/docs/images/integrations/sematext-notification-hooks.png "Sematext Notification Hook")

Enter required parameters and additional parameters and headers can be added as well. Click Test button to confirm that Sematext app is sending data and save your custom webhook integration.

![Custom Webhooks Integration](/docs/images/integrations/custom-webhook.png "Create Custom Webhooks Integration")

**Done.** Use as many generic Webhooks-based integration as you wish.  Besides custom Webhooks there are also numerous other third party integrations services like PagerDuty, Slack, MS Teams, OpsGenie, Telegram, etc. Check [Integrations](/docs/integration/) for more details.

## Custom Parameters

Sematext Notification Hooks support a set of variables exposed as [Custom Notification Hooks Parameters](/docs/integration/alerts-webhooks-custom-params/) that you can use to customize which data is included in the request sent to your webhook.
