---
layout: page
title: "Rain Bird Switch"
description: "Instructions on how to integrate your Rain Bird LNK WiFi Module as Switches within Home Assistant."
date: 2017-08-25 12:00
sidebar: true
comments: false
sharing: true
footer: true
logo: rainbird.png
ha_category: Irrigation
ha_release: 0.57
ha_iot_class: "Local Polling"
---

This `rainbird` switch platform allows interacting with [LNK WiFi](http://www.rainbird.com/landscape/products/controllers/LNK-WiFi.htm) module of the Rain Bird Irrigation system in Home Assistant.

## {% linkable_title Configuration %}

Once you have enabled the [Rain Bird component](/components/rainbird), add the following to your `configuration.yaml` file:

```yaml
switch:
  - platform: rainbird
    switches:
      sprinkler_1:
        zone: 1
        friendly_name: "Front sprinklers"
        trigger_time: 10
        scan_interval: 10
      sprinkler_2:
        friendly_name: "Back sprinklers"
        zone: 2
        trigger_time: 20
        scan_interval: 10
```

{% configuration %}
zone:
  description: Station zone identifier.
  required: true
  type: string
friendly_name:
  description: Just a friendly name for the station.
  required: false
  type: string
trigger_time:
  description: The default duration to sprinkle the zone.
  required: true
  type: integer
scan_interval:
  description: How fast to refresh the switch.
  required: false
  type: integer
{% endconfiguration %}

Please note that due to the implementation of the API within the LNK Module, there is a concurrency issue. For example, the Rain Bird app will give connection issues (like already a connection active).
