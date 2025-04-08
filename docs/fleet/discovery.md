title: Discovery Overview
description: Overview of Discovery - Service and Logs Autodiscovery

Discovery extends the capabilities of Fleet by automating the identification and categorization of services and collecting log data from various log sources. Below, you can explore some of the main benefits of Discovery:

- Centralized view of all the discovered services and their current configurations within one or more Monitoring and Logs Integrations
- Discovered services that can be automatically monitored through one of our [supported integrations](/docs/integration/), eliminating the need for manual tracking and configuration
- Automatic monitoring of newly discovered service instances, which is extremely useful in cluster and container environments
- Automatic correlation between discovered and [connected services and logs](/docs/guide/connected-apps/) using the [Split Screen](/docs/guide/split-screen/) feature

## Service Discovery
[Service Discovery](/docs/monitoring/autodiscovery/) is powered by the [Sematext Agent](/docs/agents/sematext-agent/) allowing for the automatic discovery and monitoring of services within your infrastructure without the need for additional configuration. Furthermore, it automatically correlates and configures discovered logs with each monitored service.

## Logs Discovery
[Logs Discovery](/docs/logs/discovery/intro/) functions similarly to Service Discovery, with a distinct emphasis on the automated discovery, classification, and shipping of your infrastructure and application logs.