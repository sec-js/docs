title: Using the Synthetics API for creating and editing monitors
description: How to use the Synthetics API for creating and editing monitors.

You’ll need your [API key](/docs/synthetics/using-the-api#getting-the-api-key) and [App ID](/docs/synthetics/using-the-api#getting-the-app-id-monitor-id) for the API requests below.

The create monitor API can be triggered by sending an HTTP request with the below configuration:

| Type | Region | Endpoint
| --- | --- | --- |
| Browser Monitor | US | `https://apps.sematext.com/synthetics-api/api/apps/<appId>/monitors/browser` |
| Browser Monitor | EU | `https://apps.eu.sematext.com/synthetics-api/api/apps/<appId>/monitors/browser` |
| HTTP Monitor | US | `https://apps.sematext.com/synthetics-api/api/apps/<appId>/monitors/http` |
| HTTP Monitor | EU | `https://apps.eu.sematext.com/synthetics-api/api/apps/<appId>/monitors/http` |

**HTTP Method** - `POST`

**Request Headers** - `Authorization: apiKey <apiKey>`

#### Create an HTTP Monitor

To create an HTTP Monitor, we would send an HTTP request as follows:
```
curl -L -X POST 'https://apps.sematext.com/synthetics-api/api/apps/17174/monitors/http' \
-H 'Authorization: apiKey 9bddb0a6-xxxx-xxxx-xxxx-397d15806cfd' \
-H 'Content-Type: application/json' \
--data-raw '{
    "name": "Example HTTP monitor name",
    "interval": "1m",
    "enabled": true,
    "locations": [
        1
    ],
    "url": "https://www.google.com/",
    "method": "GET",
    "conditions": [
        {
            "id": 1,
            "type": "ERROR",
            "operator": "=",
            "value": "",
            "enabled": true
        },
        {
            "id": 2,
            "type": "RESPONSE_CODE",
            "operator": "=",
            "value": "200",
            "enabled": true
        },
        {
            "id": 3,
            "type": "METRIC",
            "key": "synthetics.time.response",
            "operator": "<",
            "value": "20000",
            "enabled": true
        }
    ],
    "alertRule": {
        "schedule": [
            {
                "day": "Monday",
                "index": 2,
                "label": "MON",
                "intervals": [],
                "type": "ACTIVE"
            },
            {
                "day": "Tuesday",
                "index": 3,
                "label": "TUE",
                "intervals": [],
                "type": "ACTIVE"
            },
            {
                "day": "Wednesday",
                "index": 4,
                "label": "WED",
                "intervals": [],
                "type": "ACTIVE"
            },
            {
                "day": "Thursday",
                "index": 5,
                "label": "THU",
                "intervals": [],
                "type": "ACTIVE"
            },
            {
                "day": "Friday",
                "index": 6,
                "label": "FRI",
                "intervals": [],
                "type": "ACTIVE"
            },
            {
                "day": "Saturday",
                "index": 7,
                "label": "SAT",
                "intervals": [],
                "type": "ACTIVE"
            },
            {
                "day": "Sunday",
                "index": 1,
                "label": "SUN",
                "intervals": [],
                "type": "ACTIVE"
            }
        ],
        "priority": "WARN",
        "minDelayBetweenNotificationsInMinutes": "10",
        "backToNormalNeeded": true,
        "failedRunCountToAlert": 1,
        "notificationsEnabled": true,
        "useOnlyAlertRuleIntegrations": false
    },
    "monitorSSLExpiry": true,
    "monitorSSLChange": true,
    "allowInsecureSSL": false
}'
```

> Make sure you’re using the correct API endpoint for your region, and replace the placeholders with your actual API Key and App ID.

You can adjust the request body parameters to fit your needs. Check [here](#api-reference-http-monitor) to see the full list of available parameters.

> Refer to the [Bulk Add Monitors via Apps Script](/docs/synthetics/bulk-add-monitors-api/) page to learn how to bulk add or edit HTTP monitors using Google Sheets and Apps Script.

#### Create a Browser Monitor
When creating a Browser Monitor which uses a User Journey script, special characters in the [User Journey script](/docs/synthetics/user-journey-scripts/overview/) **should be correctly escaped**.
To create a Browser Monitor which monitors a URL using a User Journey script, we would send an HTTP request as follows:
```
curl -L -X POST 'https://apps.sematext.com/synthetics-api/api/apps/17174/monitors/browser' \
-H 'Authorization: apiKey 9bddb0a6-xxxx-xxxx-xxxx-397d15806cfd' \
-H 'Content-Type: application/json' \
--data-raw '{
    "name": "Example Browser Monitor with a User Journey script",
    "interval": "10m",
    "enabled": true,
    "locations": [
        1,
        2
	],
    "url": "",
    "script": "// Example script\n async function testPage(page) {\n   await page.goto(\"https://www.google.com/\");\n   await page.screenshot({ path: '\''screenshot.jpg'\'' });\n }\n module.exports = testPage;",
    "scriptBased": true,
	"isPlaywright": true,
    "conditions": [
        {
            "id": 1,
            "type": "ERROR",
            "operator": "=",
            "value": "",
            "enabled": true
        },
        {
            "id": 2,
            "type": "METRIC",
            "key": "synthetics.time.response",
            "operator": "<",
            "value": "20000",
            "enabled": true
        }
    ],
    "alertRule": {
        "schedule": [
            {
                "day": "Monday",
                "index": 2,
                "label": "MON",
                "intervals": [],
                "type": "ACTIVE"
            },
            {
                "day": "Tuesday",
                "index": 3,
                "label": "TUE",
                "intervals": [],
                "type": "ACTIVE"
            },
            {
                "day": "Wednesday",
                "index": 4,
                "label": "WED",
                "intervals": [],
                "type": "ACTIVE"
            },
            {
                "day": "Thursday",
                "index": 5,
                "label": "THU",
                "intervals": [
                  {
                     "start": "12:00",
                     "end": "13:00"
                  },
                  {
                     "start": "12:00",
                     "end": "13:00"
                  }
                ],
                "type": "CUSTOM"
            },
            {
                "day": "Friday",
                "index": 6,
                "label": "FRI",
                "intervals": [],
                "type": "ACTIVE"
            },
            {
                "day": "Saturday",
                "index": 7,
                "label": "SAT",
                "intervals": [],
                "type": "ACTIVE"
            },
            {
                "day": "Sunday",
                "index": 1,
                "label": "SUN",
                "intervals": [],
                "type": "ACTIVE"
            }
        ],
        "priority": "WARN",
        "minDelayBetweenNotificationsInMinutes": "10",
        "backToNormalNeeded": true,
        "failedRunCountToAlert": 1,
        "notificationsEnabled": true,
        "useOnlyAlertRuleIntegrations": false
    }
}'
```

> Make sure you’re using the correct API endpoint for your region, and replace the placeholders with your actual API Key and App ID.

To create a Browser Monitor which monitors a URL without using a User Journey script, we would send an HTTP request as follows:
```
curl -L -X POST 'https://apps.sematext.com/synthetics-api/api/apps/17174/monitors/browser' \
-H 'Authorization: apiKey 9bddb0a6-xxxx-xxxx-xxxx-397d15806cfd' \
-H 'Content-Type: application/json' \
--data-raw '{
    "name": "Example browser monitor without a User Journey script",
    "interval": "10m",
    "enabled": true,
    "locations": [
        1,
        2
    ],
    "url": "https://www.google.com/",
    "script": "",
    "scriptBased": false,
    "conditions": [
        {
            "id": 1,
            "type": "ERROR",
            "operator": "=",
            "value": "",
            "enabled": true
        },
        {
            "id": 2,
            "type": "METRIC",
            "key": "synthetics.time.response",
            "operator": "<",
            "value": "20000",
            "enabled": true
        }
    ],
    "alertRule": {
        "schedule": [
            {
                "day": "Monday",
                "index": 2,
                "label": "MON",
                "intervals": [],
                "type": "ACTIVE"
            },
            {
                "day": "Tuesday",
                "index": 3,
                "label": "TUE",
                "intervals": [],
                "type": "ACTIVE"
            },
            {
                "day": "Wednesday",
                "index": 4,
                "label": "WED",
                "intervals": [],
                "type": "ACTIVE"
            },
            {
                "day": "Thursday",
                "index": 5,
                "label": "THU",
                "intervals": [],
                "type": "ACTIVE"
            },
            {
                "day": "Friday",
                "index": 6,
                "label": "FRI",
                "intervals": [],
                "type": "ACTIVE"
            },
            {
                "day": "Saturday",
                "index": 7,
                "label": "SAT",
                "intervals": [],
                "type": "ACTIVE"
            },
            {
                "day": "Sunday",
                "index": 1,
                "label": "SUN",
                "intervals": [],
                "type": "ACTIVE"
            }
        ],
        "priority": "WARN",
        "minDelayBetweenNotificationsInMinutes": "10",
        "backToNormalNeeded": true,
        "failedRunCountToAlert": 1,
        "notificationsEnabled": true,
        "useOnlyAlertRuleIntegrations": false
    }
}'
```

> Make sure you’re using the correct API endpoint for your region, and replace the placeholders with your actual API Key and App ID.

You can adjust the request body parameters to fit your needs. Check [here](#api-reference-browser-monitor) to see the full list of available parameters.

Refer to the [Bulk Add Monitors via Apps Script](/docs/synthetics/bulk-add-monitors-api/) page to learn how to bulk add or edit Browser monitors using Google Sheets and Apps Script.

## Edit Monitors Using the API

To edit monitors using the API, you need to send a **PUT** request with the full request body with the updated parameters, depending on what you want to change. In the example below, we've added an additional location to the User Journey script-based Browser monitor we created above.

You’ll also need to include the ID of the monitor you want to edit in the URL.

The `<monitorId>` can be extracted from the URL of the Monitor Overview page. For example, if the Monitor Overview page URL is `https://apps.sematext.com/ui/synthetics/12345/monitors/276` then the `monitorId` is `276`.

```
curl -L -X PUT 'https://apps.eu.sematext.com/synthetics-api/api/apps/17174/monitors/browser/11605' \
-H 'Authorization: apiKey 9bddb0a6-xxxx-xxxx-xxxx-397d15806cfd' \
-H 'Content-Type: application/json' \
--data-raw '{
    "name": "Example Browser Monitor with a User Journey script",
    "interval": "10m",
    "enabled": true,
    "locations": [
        1,
        2,
		9
	],
    "url": "",
    "script": "// Example script\n async function testPage(page) {\n   await page.goto(\"https://www.google.com/\");\n   await page.screenshot({ path: '\''screenshot.jpg'\'' });\n }\n module.exports = testPage;",
    "scriptBased": true,
	"isPlaywright": true,
    "conditions": [
        {
            "id": 1,
            "type": "ERROR",
            "operator": "=",
            "value": "",
            "enabled": true
        },
        {
            "id": 2,
            "type": "METRIC",
            "key": "synthetics.time.response",
            "operator": "<",
            "value": "20000",
            "enabled": true
        }
    ],
    "alertRule": {
        "schedule": [
            {
                "day": "Monday",
                "index": 2,
                "label": "MON",
                "intervals": [],
                "type": "ACTIVE"
            },
            {
                "day": "Tuesday",
                "index": 3,
                "label": "TUE",
                "intervals": [],
                "type": "ACTIVE"
            },
            {
                "day": "Wednesday",
                "index": 4,
                "label": "WED",
                "intervals": [],
                "type": "ACTIVE"
            },
            {
                "day": "Thursday",
                "index": 5,
                "label": "THU",
                "intervals": [
                  {
                     "start": "12:00",
                     "end": "13:00"
                  },
                  {
                     "start": "12:00",
                     "end": "13:00"
                  }
                ],
                "type": "CUSTOM"
            },
            {
                "day": "Friday",
                "index": 6,
                "label": "FRI",
                "intervals": [],
                "type": "ACTIVE"
            },
            {
                "day": "Saturday",
                "index": 7,
                "label": "SAT",
                "intervals": [],
                "type": "ACTIVE"
            },
            {
                "day": "Sunday",
                "index": 1,
                "label": "SUN",
                "intervals": [],
                "type": "ACTIVE"
            }
        ],
        "priority": "WARN",
        "minDelayBetweenNotificationsInMinutes": "10",
        "backToNormalNeeded": true,
        "failedRunCountToAlert": 1,
        "notificationsEnabled": true,
        "useOnlyAlertRuleIntegrations": false
    }
}'
```

## API Reference

### API Reference: HTTP Monitor

| Key | Type | Value | Description | Required
| --- | --- | --- | --- | --- |
| name | STRING | User-defined | Title of the monitor | YES |
| interval | STRING | -- | Interval to run the monitor | YES |
| | | 1m | 1 minute intervals | |
| | | 5m | 5 minute intervals | |
| | | 10m | 10 minute intervals | |
| | | 15m | 15 minute intervals | |
| enabled | BOOLEAN | -- | Enable/Disable the monitor | YES |
| | | true | Enabled state | |
| | | false | Disabled state  | |
| locations | ARRAY | -- | Locations to run the monitor from | YES |
| | | 1 | N. Virginia, USA | |
| | | 2 | Ireland | |
| | | 3 | Mumbai, India | |
| | | 4 | Singapore | |
| | | 5 | Sydney, Australia | |
| | | 6 | Frankfurt, Germany | |
| | | 7 | Sao Paulo, Brazil | |
| | | 8 | N. California, USA| |
| | | 9 | Montreal, Canada | |
| url | STRING | User-defined | URL to monitor | YES |
| method | STRING | -- | HTTP method | YES |
| | | GET | Perform a GET request | |
| | | POST | Perform a POST request | |
| | | PUT | Perform a PUT request | |
| | | DELETE | Perform a DELETE request | |
| | | PATCH | Perform a PATCH request | |
| body | STRING | User-defined | Request body | NO - Optional |
| headers | Array of JSON Objects | *See [API Reference: headers](#api-reference-headers) | Request headers | NO - Optional |
| params | Array of JSON Objects | *See [API Reference: params](#api-reference-params) | Request params | NO - Optional |
| cookies | Array of JSON Objects | *See [API Reference: cookies](#api-reference-cookies) | Request cookies | NO - Optional |
| conditions | Array of JSON Objects | *See [API Reference: conditions](#api-reference-conditions) | Alert Conditions | YES |
| alertRule | JSON Object | *See [API Reference: alertRule](#api-reference-alertrule) | Alert Settings | YES |
| monitorSSLExpiry | BOOLEAN | -- | Alert when SSL certificate is expiring in 28, 14, 7, and 3 days | YES |
| | | true | SSL expiry alert enabled | |
| | | false | SSL expiry alert disabled | |
| monitorSSLChange | BOOLEAN | -- | Alert when SSL certificate change is detected | YES |
| | | true | SSL certificate change alert enabled | |
| | | false | SSL certificate change alert disabled | |
| allowInsecureSSL | BOOLEAN | -- | SSL Certificate validation | YES |
| | | true | Skip SSL Certificate validation | |
| | | false | Validate SSL Certificates | |

### API Reference: Browser Monitor

| Key | Type | Value | Description | Required
| --- | --- | --- | --- | --- |
| name | STRING | User-defined | Title of the monitor | YES |
| interval | STRING | -- | Interval to run the monitor | YES |
| | | 1m | 1 minute intervals | |
| | | 5m | 5 minute intervals | |
| | | 10m | 10 minute intervals | |
| | | 15m | 15 minute intervals | |
| enabled | BOOLEAN | -- | Enable/Disable the monitor | YES |
| | | true | Enabled state | |
| | | false | Disabled state  | |
| locations | ARRAY | -- | Locations to run the monitor from | YES |
| | | 1 | N. Virginia, USA | |
| | | 2 | Ireland | |
| | | 3 | Mumbai, India | |
| | | 4 | Singapore | |
| | | 5 | Sydney, Australia | |
| | | 6 | Frankfurt, Germany | |
| | | 7 | Sao Paulo, Brazil | |
| | | 8 | N. California, USA| |
| | | 9 | Montreal, Canada|
| url | STRING | User-defined | URL to monitor | YES - Empty for User Journey |
| script | STRING | User-defined | User Journey script | YES - Empty for Website Monitor |
| scriptBased | BOOLEAN | -- | Browser Monitor mode | YES |
| | | true | Monitor a User Journey | |
| | | false | Monitor a Website | |
| conditions | Array of JSON Objects | *See [API Reference: conditions](#api-reference-conditions) | Alert Conditions | YES |
| alertRule | JSON Object | *See [API Reference: alertRule](#api-reference-alertrule) | Alert Settings | YES |
| allowInsecureSSL | BOOLEAN | -- | SSL Certificate validation | YES |
| | | true | Skip SSL Certificate validation | |
| | | false | Validate SSL Certificates | |

#### API Reference: headers
| Key | Type | Value | Description | Required
| --- | --- | --- | --- | --- |
| Name | STRING | User-defined | Custom header name | YES |
| Value | STRING | User-defined | Custom header value | YES |

#### API Reference: params
| Key | Type | Value | Description | Required
| --- | --- | --- | --- | --- |
| Name | STRING | User-defined | Custom parameter name | YES |
| Value | STRING | User-defined | Custom parameter value | YES |

#### API Reference: cookies
| Key | Type | Value | Description | Required
| --- | --- | --- | --- | --- |
| Name | STRING | User-defined | Custom cookie name | YES |
| Value | STRING | User-defined | Custom cookie value | YES |

#### API Reference: conditions
| Key | Type | Value | Description | Required
| --- | --- | --- | --- | --- |
| id | INTEGER | User-defined | Alert condition line number | YES |
| type | STRING | -- | Alert condition type | YES |
| | | METRIC | Metric | |
| | | RESPONSE_BODY | Response Body | Only for HTTP monitor |
| | | RESPONSE_BODY_JSON | Response Body JSON | Only for HTTP monitor |
| | | RESPONSE_HEADER | Response Header | Only for HTTP monitor |
| | | RESPONSE_CODE | Response Code | Only for HTTP monitor |
| | | ERROR | Error | |
| | | SSL_CERT_EXPIRY | SSL Certificate Expiry (days) | *Only > operator available |
| key | STRING | -- | Alert condition field | Only for the following value in type: |
| | | synthetics.http.time.dns | DNS time (ms) | METRIC |
| | | synthetics.http.time.connect | Connect time (ms) | METRIC |
| | | synthetics.http.time.tls | TLS time (ms) | METRIC |
| | | synthetics.http.time.firstbyte | Time to first byte (ms) | METRIC |
| | | synthetics.http.time.download | Download time (ms) | METRIC |
| | | synthetics.browser.transfer.size  | Bytes Transferred (Bytes) | METRIC - Only for Browser monitor |
| | | synthetics.browser.request.count | Request Count | METRIC - Only for Browser monitor |
| | | synthetics.time.response | Response time (ms) | METRIC |
| | | synthetics.http.response.size | Response size (bytes) | METRIC |
| | | User-defined | JSON path | RESPONSE_BODY_JSON |
| | | User-defined | Header name | RESPONSE_HEADER |
| operator | STRING | -- | Operator type | YES |
| | | contains | Contains | *See [API Reference: operator](#api-reference-operator)  |
| | | does not contain | Does Not Contain | *See [API Reference: operator](#api-reference-operator) |
| | | > | Greater Than | *See [API Reference: operator](#api-reference-operator) |
| | | < | Less Than | *See [API Reference: operator](#api-reference-operator)|
| | | = | Equal To | *See [API Reference: operator](#api-reference-operator) |
| | | !=  | Not Equal To | *See [API Reference: operator](#api-reference-operator) |
| | | Starts With | Starts With | *See [API Reference: operator](#api-reference-operator) |
| value | STRING | User-defined | Rule value | YES |
| enabled | BOOLEAN | -- | Enable/Disable the line | YES |
| | | true | Line enabled | |
| | | false | Line disabled | |

#### API Reference: operator

**HTTP Monitor**

| Operator | Alert Condition Availability
| --- | --- |
| Contains | -- |
| | Response Body |
| | Response Body JSON |
| | Response Header |
| | Response Code |
| | Error |
| Does Not Contain | -- |
| | Metric |
| | Response Body |
| | Response Body JSON |
| | Response Header |
| | Response Code |
| | Error |
| > | -- |
| | Metric |
| | Response Body JSON |
| | Response Code |
| | SSL Certificate Expiry (days) |
| < | -- |
| | Metric |
| | Response Body JSON |
| | Response Code |
| = | -- |
| | Metric |
| | Response Body |
| | Response Body JSON |
| | Response Header |
| | Response Code |
| | Error |
| != | -- |
| | Metric |
| | Response Body |
| | Response Body JSON |
| | Response Header |
| | Response Code |
| | Error |
| Starts With | -- |
| | Response Body |
| | Response Body JSON |
| | Response Header |
| | Response Code |
| | Error |

**Browser Monitor**

| Operator | Alert Condition Availability
| --- | --- |
| Contains | Error |
| Does Not Contain | -- |
| | Metric |
| | Error |
| > | Metric |
| < | Metric |
| = | -- |
| | Metric |
| | Error |
| != | -- |
| | Metric |
| | Error |
| Starts With | Error |

### API Reference: alertRule
| Key | Type | Value | Description | Required
| --- | --- | --- | --- | --- |
| schedule | Array of JSON Objects | *See [API Reference: schedule](#api-reference-schedule) | Notifications Schedule | YES |
| priority | STRING | -- | Alert priority | YES |
| | | INFO | Info | |
| | | WARN | Warning | |
| | | ERROR | Error | |
| | | CRITICAL | Critical | |
| minDelayBetweenNotificationsInMinutes | INTEGER | 1-90 | Delay in minutes between notifications (1-90) | YES |
| backToNormalNeeded | BOOLEAN | -- | Alert when the value goes back to non-alert level | YES |
| | | true | Enabled | |
| | | false | Disabled | |
| failedRunCountToAlert | INTEGER | 1-5 | Alert after N failed runs from a location (1-5) | YES |
| notificationsEnabled | BOOLEAN | -- | Enable/Disable notifications | YES |
| | | true | Enable notifications | |
| | | false | Disable notifications | |
| useOnlyAlertRuleIntegrations | BOOLEAN | -- | Use account-default notification hooks for this alert | YES |
| | | true | Enable account-default notification hooks | |
| | | false | Disable account-default notification hooks |

### API Reference: schedule
| Key | Type | Value | Description | Required
| --- | --- | --- | --- | --- |
| day | STRING | -- | Day of the week | YES |
| | | Monday | Monday | |
| | | Tuesday | Tuesday | |
| | | Wednesday | Wednesday | |
| | | Thursday | Thursday | |
| | | Friday | Friday | |
| | | Saturday | Saturday | |
| | | Sunday | Sunday | |
| index | INTEGER | -- | Day index | YES |
| | | 1 | Sunday | |
| | | 2 | Monday | |
| | | 3 | Tuesday | |
| | | 4 | Wednesday | |
| | | 5 | Thursday | |
| | | 6 | Friday | |
| | | 7 | Saturday | |
| label | STRING | -- | Day label | YES |
| | | MON | Monday | |
| | | TUE | Tuesday | |
| | | WED | Wednesday | |
| | | THU | Thursday | |
| | | FRI | Friday | |
| | | SAT | Saturday | |
| | | SUN | Sunday | |
| intervals | Array of JSON Objects | *See [API Reference: intervals](#api-reference-intervals) | Notifications Schedule | YES - Empty for All Day or Inactive |
| type | STRING | -- | Schedule Type | YES |
| | | ACTIVE | All Day | |
| | | CUSTOM | Intervals | |
| | | INACTIVE | Inactive All Day | |

### API Reference: intervals
| Key | Type | Value | Description | Required
| --- | --- | --- | --- | --- |
| start | STRING | HH:MM | Start time HH:MM | YES |
| end | STRING | HH:MM | End time HH:MM | YES |
