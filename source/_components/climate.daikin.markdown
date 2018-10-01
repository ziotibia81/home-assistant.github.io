---
layout: page
title: "Daikin AC"
description: "Instructions on how to integrate Daikin AC(s) with Home Assistant."
date: 2017-12-03 05:00
sidebar: true
comments: false
sharing: true
footer: true
logo: daikin.png
ha_category: Climate
ha_release: 0.59
ha_iot_class: "Local Polling"
---


The `daikin` climate platform integrates Daikin air conditioning systems into Home Assistant, enabling control of setting the following parameters:

- **mode** (cool, heat, dry, fan only or auto)
- **fan speed** (on supported models)
- **target temperature**
- **swing mode** (on supported models)

Current temperature is displayed.

## {% linkable_title Configuration %}

To enable the platform, add the following lines to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
climate:
  - platform: daikin
    host: 10.0.0.1
```

{% configuration %}
host:
  description: IP or hostname of the device.
  required: true
  type: string
name:
  description: If the device has a name previously set by the user than that name will be used.
  required: false
  type: string
{% endconfiguration %}

