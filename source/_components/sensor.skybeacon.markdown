---
layout: page
title: "Skybeacon sensor"
description: "Instructions on how to integrate MiFlora BLE plant sensor with Home Assistant."
date: 2017-01-17 10:00
sidebar: true
comments: false
sharing: true
footer: true
ha_category: DIY
ha_release: 0.37
ha_iot_class: "Local Polling"
---

The `skybeacon` sensor platform supports [CR2477](http://cnsky9.en.alibaba.com)-powered [iBeacon](https://en.wikipedia.org/wiki/IBeacon)/eddystone sensors that come with temperature/sensor module.

## {% linkable_title Configuration %}

To use your Skybeacon sensor in your installation, add the following to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
sensor:
  - platform: skybeacon
    mac: "xx:xx:xx:xx:xx:xx"
    monitored_conditions:
      - temperature
      - humidity
```

{% configuration %}
mac:
  description: "The MAC address of your sensor. You can find this be running `hcitool lescan` from command line."
  required: true
  type: string
name:
  description: The name of the Skybeacon sensor.
  required: false
  type: string
  default: Skybeacon
monitored_conditions:
  description: The parameters that should be monitored.
  required: false
  type: map
  keys:
    temperature:
      description: Temperature at the sensor's location.
    humidity:
      description: Humidity at the sensor's location.
{% endconfiguration %}

