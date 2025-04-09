title: Logs Discovery
description: Logs Discovery Introduction

Logs discovery, a component of [Fleet & Discovery](/docs/fleet/), automates the classification and shipping of your infrastructure, application, and container log files. With a user-friendly interface, you can easily explore and manage discovered log sources across bare-metal/virtual machines and containers.

![Logs Discovery](/docs/images/fleet/fnd-discovery-services.png)

## Features

### Contextual log discoveries

Each log file is linked to the service that's writing to it. Log file metadata reveals some fundamental attributes of a file, like the disk device where it is located, size, inode number and so on.

### Automatic log shipping

Setting up log shipping is straightforward and it boils down to selecting your logs destination and optional include/exclude glob matters. This also eliminates tedious tasks that stem from the provisioning of log shippers.

### Log parsing

A predefined set of regular expression patterns are automatically applied to a log file making it convenient to get started without additional hassle. Log parsing structures the raw log events into events with meaningful fields out of the box making them suitable for dashboarding and the creation of precise alert rules. Sematext Logs supports a wide array of [integrations](/docs/integration/) with prebuilt reports and alert rules.

### Glob patterns

Include and exclude glob patterns provide fine-grained control over which log files are shipped to Sematext.
