---
layout: page
title: "TED5000 electricity monitoring"
description: "How to add a TED5000 to Home Assistant."
date: 2016-09-27 11:19
sidebar: true
comments: false
sharing: true
footer: true
logo: ted.png
ha_category: Energy
ha_release: "0.30"
ha_iot_class: "Local Polling"
---

The `ted 5000` monitors electricity consumption/production by connecting to the [TED](http://www.theenergydetective.com/home) gateway, itself connected to one or several Measuring Transmitting Units (MTU). The platform creates up to two sensors per MTU, one for Wattage the other for Voltage.

If you want to enable the ted5000 sensor, add the following lines to your `configuration.yaml`:

```yaml
# Example configuration.yaml entry
sensor:
  - platform: ted5000
    host: 192.168.1.100
```


{% configuration %}
host:
  description: The IP address of your ted gateway.
  required: true
  type: string
port:
  description: The port of your ted gateway.
  required: false
  type: integer
  default: 80
name:
  description: Name of the ted gateway.
  required: false
  type: string
  default: ted
{% endconfiguration %}

For each plugged MTU, using an index starting at 1, the platform creates 2 sensors:

```yaml
sensor.<name>_mtu<MTU id>_power
sensor.<name>_mtu<MTU id>_voltage
```

