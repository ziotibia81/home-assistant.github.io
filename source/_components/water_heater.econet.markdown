---
layout: page
title: "EcoNet water heater"
description: "Instructions on how to integrate Rheem EcoNet water heaters into Home Assistant."
date: 2017-12-28 14:51
sidebar: true
comments: false
sharing: true
footer: true
logo: econet.png
ha_category: Water heater
ha_release: 0.61.0
ha_iot_class: "Cloud Polling"
redirect_from: /components/climate.econet/
---


The `econet` water heater platform is consuming the information provided by a [EcoNet enabled Rheem water heater](http://www.rheem.com/EcoNet/Home). This platform allows you to set the temperature, the operation mode, and enable vaction mode.

## {% linkable_title Configuration %}

To enable the `econet` water heater platform, add the following information to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
water_heater:
  - platform: econet
    username: YOUR_ECONET_EMAIL
    password: YOUR_ECONET_PASSWORD
```

{% configuration %}
username:
  description: The username used to connect to your EcoNet account.
  required: true
  type: string
password:
  description: The password used to connect to your EcoNet account.
  required: true
  type: string
{% endconfiguration %}

### {% linkable_title Service `econet.add_vacation` %}

You can use the service `econet.add_vacation` to create a new vacation for your EcoNet water heaters.

| Service data attribute | Optional | Description |
| ---------------------- | -------- | ----------- |
| `entity_id` | yes | The entity id of the water heater to add the vaction to.
| `start_date` | yes | This is a Unix timestamp for when the vaction should start.
| `end_date` | yes | this is a Unix timestamp for when the vaction should end.

<p class='note'>
The Unix timestamps can be obtained from the `input_datetime` component. This will allow you to graphically set the start and end date.
</p>

### {% linkable_title Service `econet.delete_vacation` %}

You can use the service `econet.delete_vacation` to remove all vactions from an EcoNet water heater.

| Service data attribute | Optional | Description |
| ---------------------- | -------- | ----------- |
| `entity_id` | yes | The entity id of the water heater to remove the vaction from.

<p class='note'>
Econet water heaters use to live under the `climate` platform prior to release 0.81.
</p>
