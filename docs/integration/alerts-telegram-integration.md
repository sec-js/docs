title: Telegram Alerts Integration
description: Sematext threshold, anomaly and / or heartbeat Alerts integration with Telegram messenger. Use them together to get the information about each notification quickly and on any device.

## In Telegram

**1.** Setup your Telegram client and start chatting with a user named **BotFather**. This is a place where you can create your bot. Just type in:

```
/newbot
```

And in the next line type your bot name, e.g., **SematextNotificationBot**. 

Finally, type the bot username, it has to end with the **_bot** suffix, e.g., **SematextNotificationBot_bot**.

If everything went successfully you should get a message with the **Bot Token API key**:

<img class="content-modal-image" alt="Create Telegram Bot Token API Key" src="/docs/images/integrations/create-telegram-integration_bot_key.png" title="Create Telegram Bot Token API Key">

Copy the **Bot Token API key** somewhere, you will need it to configure the notification hook in Sematext.

**2.** Invite the bot to the channel to which it should send notifications. You can do that by including the bot in the administrators of the channel in your Telegram client. Let's follow the steps. 

First, message the bot using the Telegram client of your choice:

<img class="content-modal-image" alt="Create Telegram Integration - Message Bot" src="/docs/images/integrations/create-telegram-integration_bot_message.png" title="Create Telegram Integration - Message Bot">

Next, click the channel name:

<img class="content-modal-image" alt="Create Telegram Integration - Click Channel Name" src="/docs/images/integrations/create-telegram-integration_click_channel_name.png" title="Create Telegram Integration - Click Channel Name">

Click the **Administrators** to list the channel administrators:

<img class="content-modal-image" alt="Create Telegram Integration - List Administrators" src="/docs/images/integrations/create-telegram-integration_add_administrator.png" title="Create Telegram Integration - List Administrators">

Click the **Add Admin** button:

<img class="content-modal-image" alt="Create Telegram Integration - Add Admin" src="/docs/images/integrations/create-telegram-integration_add_new_administrator.png" title="Create Telegram Integration - Add Admin">

Find the created bot and click on it:

<img class="content-modal-image" alt="Create Telegram Integration - Add the Bot" src="/docs/images/integrations/create-telegram-integration_add_bot.png" title="Create Telegram Integration - Add the Bot">

Finally, review the permissions and click done:

<img class="content-modal-image" alt="Create Telegram Integration - Review Permissions" src="/docs/images/integrations/create-telegram-integration_add_bot_finish.png" title="Create Telegram Integration - Review Permissions">

**3.** Retrieve the channel identifier for the channel where the bot will send notifications. This can be done by running the following request:

``` bash
curl -s -k https://api.telegram.org/bot<BOT_TOKEN_API_KEY>/getUpdates
```

Just replace the **<BOT_TOKEN_API_KEY>** with the token that you got in the second step. The response should be similar to the following one:

``` json
{"ok":true,"result":[{"update_id":878583440,
"channel_post":{"message_id":2,"chat":{"id":-1001236826225,"title":"SematextNotifications","type":"channel"},"date":1598380548,"text":"Test test"}}]}
```

If the response is empty, just send a simple message to the channel you invited the bot to and re-run the request. We are interested in the chat identifier, so the **-1001236826225** value from the above response. Note it down.

We are now ready to add our Telegram notification hook to Sematext.

## In Sematext

**1.** Navigate to [Notification Hooks](https://apps.sematext.com/ui/hooks/create) (in [EU](https://apps.eu.sematext.com/ui/hooks/create)) and select Telegram card to create a new Telegram notification hook.

![Sematext Notification Hooks](https://sematext.com/docs/images/integrations/sematext-notification-hooks.png  "Sematext Notification Hook")

**2.** Add your Telegram **bot token** and **chat identifier**. 

<img class="content-modal-image" alt="Create Telegram Integration" src="/docs/images/integrations/create-telegram-integration.png" title="Create Telegram Integration">

Next, click the **Send Test Notification** button. Telegram should return status code **200** indicating everything is configured correctly. Check your Telegram channel for the test message from Sematext. 

Once the test message, is visible click the **Save Notification Hook** button to save your configuration. 
