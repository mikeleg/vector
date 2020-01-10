---
delivery_guarantee: "best_effort"
description: "The Vector `prometheus` source ingests data through the Prometheus text exposition format and outputs `metric` events."
event_types: ["metric"]
issues_url: https://github.com/timberio/vector/issues?q=is%3Aopen+is%3Aissue+label%3A%22source%3A+prometheus%22
operating_systems: ["linux","macos","windows"]
sidebar_label: "prometheus|[\"metric\"]"
source_url: https://github.com/timberio/vector/tree/master/src/sources/prometheus.rs
status: "beta"
title: "Prometheus Source"
unsupported_operating_systems: []
---

The Vector `prometheus` source ingests data through the Prometheus text exposition format and outputs [`metric`][docs.data-model.metric] events.

<!--
     THIS FILE IS AUTOGENERATED!

     To make changes please edit the template located at:

     website/docs/reference/sources/prometheus.md.erb
-->

## Configuration

import CodeHeader from '@site/src/components/CodeHeader';

<CodeHeader fileName="vector.toml" learnMoreUrl="/docs/setup/configuration/"/ >

```toml
[sources.my_source_id]
  type = "prometheus" # must be: "prometheus"
  hosts = ["http://localhost:9090"] # example
  scrape_interval_secs = 1 # example
```

## Options

import Fields from '@site/src/components/Fields';

import Field from '@site/src/components/Field';

<Fields filters={true}>


<Field
  common={true}
  defaultValue={null}
  enumValues={null}
  examples={[["http://localhost:9090"]]}
  name={"hosts"}
  nullable={false}
  path={null}
  relevantWhen={null}
  required={true}
  templateable={false}
  type={"[string]"}
  unit={null}
  >

### hosts

Host addresses to scrape metrics from.


</Field>


<Field
  common={true}
  defaultValue={null}
  enumValues={null}
  examples={[1]}
  name={"scrape_interval_secs"}
  nullable={false}
  path={null}
  relevantWhen={null}
  required={true}
  templateable={false}
  type={"int"}
  unit={null}
  >

### scrape_interval_secs

The interval between scrapes in seconds.


</Field>


</Fields>

## Output

The `prometheus` source ingests data through the Prometheus text exposition format and outputs [`metric`][docs.data-model.metric] events.
For example:


import Tabs from '@theme/Tabs';

<Tabs
  block={true}
  defaultValue="counter"
  values={[{"label":"Counter","value":"counter"},{"label":"Gauge","value":"gauge"}]}>

import TabItem from '@theme/TabItem';

<TabItem value="counter">

Given the following input:

```text
# TYPE promhttp_metric_handler_requests_total counter
promhttp_metric_handler_requests_total{code="200"} 100
```

A metric event will be output with the following structure:

```json
{
  "name": "promhttp_metric_handler_requests_total",
  "kind": "absolute",
  "timestamp": "2019-05-02T12:22:46.658503Z" // current time / time ingested
  "tags": {
    "code": "200"
  },
  "value": {
    "type": "counter",
    "value": 100.0
  }
}
```

</TabItem>

<TabItem value="gauge">

Given the following input:

```text
prometheus_remote_storage_samples_in_total 57011636
```

A metric event will be output with the following structure:

```json
{
  "name": "prometheus_remote_storage_samples_in_total",
  "kind": "absolute",
  "timestamp": "2019-05-02T12:22:46.658503Z" // current time / time ingested
  "tags": null,
  "value": {
    "type": "gauge",
    "value": 57011636.0
  }
}
```

</TabItem>
</Tabs>

## How It Works

### Environment Variables

Environment variables are supported through all of Vector's configuration.
Simply add `${MY_ENV_VAR}` in your Vector configuration file and the variable
will be replaced before being evaluated.

You can learn more in the [Environment Variables][docs.configuration#environment-variables]
section.


[docs.configuration#environment-variables]: /docs/setup/configuration/#environment-variables
[docs.data-model.metric]: /docs/about/data-model/metric/