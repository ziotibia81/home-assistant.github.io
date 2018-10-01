---
layout: page
title: "Fritzbox"
description: "Instructions on how to integrate the AVM Fritzbox Smart Home components."
date: 2018-02-18 17:10
sidebar: true
comments: false
sharing: true
footer: true
logo: avm.png
ha_category: Hub
ha_release: 0.68
ha_iot_class: "Local Polling"
---

The [AVM](https://en.avm.de) Fritzbox component for Home Assistant allows you to integrate the switch and climate devices.

#### {% linkable_title Tested Devices %}

- [FRITZ!Box 6490 Cable](https://en.avm.de/products/fritzbox/fritzbox-6490-cable/)
- [FRITZ!Box 7590](https://en.avm.de/products/fritzbox/fritzbox-7590/)
- [FRITZ!DECT 200](https://en.avm.de/products/fritzdect/fritzdect-200/)
- [Eurotronic Comet DECT](https://www.eurotronic.org/en/products/comet-dect.html)


## {% linkable_title Setup %}

```yaml
# Example configuration.yaml entry
fritzbox:
  devices:
    - host: fritz.box
      username: YOUR_USERNAME
      password: YOUR_PASSWORD
```

{% configuration %}
devices:
  description: A list of Fritzbox devices.
  required: true
  type: map
  keys:
    host:
      description: The hostname or IP address of the Fritzbox.
      required: true
      type: optional
    username:
      description: The username for Smart Home access.
      required: true
      type: string
    password:
      description: The password of the user.
      required: true
      type: string
{% endconfiguration %}
