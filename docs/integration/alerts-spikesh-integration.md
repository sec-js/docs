title: Spike.sh Alerts Integration
description: Sematext threshold, anomaly and / or heartbeat Alerts integration with Spike.sh. Use them together to get the information about each notification quickly and on any device.

## In Spike.sh

To receive incoming notifications from Sematext add and configure a new integration in Spike.sh:

**1.** Go to the **Integrations** page and click **New integration**:

<img class="content-modal-image" alt="Create Spike.sh Integration - New Integration" src="/docs/images/integrations/create-spikesh-integration-integrations.png" title="Create Spike.sh Integration - New Integration">

**2.** Choose the **Sematext** integration from the integrations list: 

<img class="content-modal-image" alt="Create Spike.sh Integration - Sematext" src="/docs/images/integrations/create-spikesh-integration-sematext.png" title="Create Spike.sh Integration - Sematext">

**3.** Provide the name, description of the integration. Choose the service that it should be added to, the escalation policy and the acknowledgment time:

<img class="content-modal-image" alt="Create Spike.sh Integration - Integration Description" src="/docs/images/integrations/create-spikesh-integration-add-integration.png" title="Create Spike.sh Integration - Integration Description">

**4.** Once the account is created click the **Copy Webhook** link:

<img class="content-modal-image" alt="Create Spike.sh Integration - Copy Webhook" src="/docs/images/integrations/create-spikesh-integration-copy.png" title="Create Spike.sh Integration - Copy ">

**5.** Finally, click **Copy** button in the displayed modal window:

<img class="content-modal-image" alt="Create Spike.sh Integration - URL copy" src="/docs/images/integrations/create-spikesh-integration-copy-webhook.png" title="Create Spike.sh Integration - URL copy">

With the **Integration** configured we can now use the **Webhook URL** to configure the Spike.sh notification hook in Sematext.

## In Sematext

**1.** Navigate to [Notification Hooks](https://apps.sematext.com/ui/hooks/create) (in [EU](https://apps.eu.sematext.com/ui/hooks/create)) and select Spike.sh card to create a new Spike.sh notification hook.

![Sematext Notification Hooks](https://sematext.com/docs/images/integrations/sematext-notification-hooks.png  "Sematext Notification Hook")

**2.** Add your Spike.sh **Webhook URL**. 

<img class="content-modal-image" alt="Create Spike.sh Integration" src="/docs/images/integrations/create-spikesh-integration.png" title="Create Spike.sh Integration">

Next, click the **Send Test Notification** button. Spike.sh should return **OK** indicating everything is configured correctly. Check your Spike.sh integration for the test message from Sematext. 

Once the test message is visible, click the **Save Notification Hook** button to save your configuration. 
