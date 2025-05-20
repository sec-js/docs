title: Ingest parsed logs and metrics in InfluxDB
description: Convert any message object to influx-line protocol with InfluxDB plugin and for Logagent, light-weight log shipper, filebeat, fluentd or rsyslog alternative with out of the box and extensible log parsing, on-disk buffering, secure transport, bulk indexing to Elasticsearch/OpenSearch and Sematext logs management platform

## Output Plugin: InfluxDB

This plugin converts any message object to influx-line protocol: 

- Numeric fields are converted to InfluxDB fields
- Text fields are converted to InfluxDB tags 
- Field names in nested objects (e.g. from  JSON logs) are flatten using a dot as separator
- Messages should have a "measurement" field for the InfluxDB measurement name. When the "measurement" field is missing, the measurement name is taken from the "logSource" field.


### Configuration
```

input: 
  files: 
    - /var/log/sensor-data.log 

output: 
  sensor-data:
    module: output-influxdb
    # InfluxDB URL including optional name and password
    url: http://username:password@127.0.0.1:8086
    # InfluxdB datbase name
    db: sensor_data
    # static tags for all metrics
    tags: 
      role: backend
      region: eu
    # flush interval in seconds
    flushInterval: 5
    # max buffer size to force flush
    maxBufferSize: 100
    # Debug option to log influx-line protocol details to stderr
    debug: false
    # A list of message fields, which should be ignored in influxdb output. 
    # Note fields with highly variable content such as log messages could increase InfluxDB memory usage. 
    ignoreFields: 
      - message
      - id
    # Only messages matching the filter (RegEx) will be processed
    filter: 
      field: logSource
      match: .*

```

### Start logagent

```
logagent --config influxdb-output.yaml
```
