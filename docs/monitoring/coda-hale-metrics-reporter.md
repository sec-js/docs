title: Coda Hale Metric Reporter
description: Sematext extension for Metrics, a powerful toolkit of modules for common libraries providing a full-stack visibility and ways to measure the behavior of critical components in your production devops environment

[Sematext-metrics-reporter](https://github.com/sematext/sematext-metrics-reporter)
is an extension for the [ Coda Hale Metrics](http://metrics.dropwizard.io/) library version 2.2.0 and 3.x for
sending metrics to [Sematext Monitoring](/docs/monitoring/).  Under the
hood sematext-metrics Java library is used to send metrics as [Custom Metrics](/docs/monitoring/custom-metrics) to Sematext Monitoring.

### Quick Start

To start sending metrics just create and start `SematextMetricsReporter`:

``` java
MetricRegistry metrics = new MetricRegistry();

SematextClient.initialize("monitoring token here");
SematextMetricsReporter reporter = SematextMetricsReporter.forClient(SematextClient.client())
  .withFilter(MetricFilter.ALL)
  .withRegistry(metrics)
  .withDurationUnit(TimeUnit.MILLISECONDS)
  .build();

reporter.start(1, TimeUnit.MINUTES);
```

