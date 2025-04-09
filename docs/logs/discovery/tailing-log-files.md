title: Shipping Log Files
description: Shipping Log File Sources

Enabling automatic logs shipping is accomplished by triggering the "Set Up" button that opens the flyout for configuring log file shipping.

![Setup Log Files](/docs/logs/discovery/images/setup-log-files.png)

In the flyout panel, you have to repeat the following steps to start shipping logs for the log file source:

1. Enable the "Automatically ship <group-name> logs" toggle
2. Select the destination Logs App. If the Logs App doesn't exist, you'll be able to create one from the same screen
3. Click the `Save Changes` button

The log shipper will automatically start tailing any log file that pertains to the service type or process name for which the log shipping was set up.

![Enable Log Shipping](/docs/logs/discovery/images/logfile-flyout.png)

## Defining glob patterns

To narrow down which log files should be tailed, you can define include/exclude [glob](https://en.wikipedia.org/wiki/Glob_(programming)) patterns. The following glob wildcards are supported:

- `*` matches any sequence of non-separator characters
- `**` matches any sequence of characters, including directory separator character
- `?` matches any single non-separator character
- `[0-9]` matches character ranges
- `{log,txt}` - matches any of comma separated patterns

 When defining glob patterns, you can either specify include and/or exclude glob expressions. Exclude glob patterns take precedence over include patterns. This means that a log file that matches an include pattern will not be shipped if it also matches an exclude pattern.

![Include and Exclude Glob Patterns](/docs/logs/discovery/images/include-exclude-globs.png)

As you're inputting the glob pattern, you'll be automatically getting feedback on how many and which exact log files are matched by include/exclude glob patterns.

![Matched Hints](/docs/logs/discovery/images/matched-globs.png)

Going back to the main table, you'll notice two kinds of visual indicators that signal whether a particular log file source is included or excluded by the glob expression. By hovering over the `✓` or `✕` icons, you'll be able to figure out exact glob pattern(s) matching the log file. If the log file is excluded from shipping, it is grayed out in the table row.

The orange/yellow circles reflect log file shipping state. If you hover over them, the count of log files that are configured for shipping is shown.

![Globs Main Table](/docs/logs/discovery/images/globs-main-table.png)

## Exploring log file metadata

Each log file discovered is accompanied by meta information that you can access by clicking on the log file instance. The following attributes are displayed:

- `Command Line` reveals the command line arguments of the process that has opened the log file and it is writing to it
- `Process` is the name of the process that is writing to the log file
- `Pid` is the identifier of the process that is writing to the log file
- `Device` represents the disk device where the log file is stored
- `File System Type` designates the file system of the disk device where the log file is located
- `Size` shows the approximate size of the log file
- `User` is the user name that owns the file
- `Group` is the group name to which the log file pertains
- `Last Tail Time` represents the last time the log file was tailed

![Log File Metadata](/docs/logs/discovery/images/log-file-meta.png)
