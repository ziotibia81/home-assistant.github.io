---
layout: page
title: "OpenSky Network"
description: "Instructions on how to integrate OpenSky Network into Home Assistant."
date: 2017-04-14 10:00
sidebar: true
comments: false
sharing: true
footer: true
logo: opensky.png
ha_category: Transport
featured: false
ha_release: 0.43
ha_iot_class: "Cloud Polling"
---

The `opensky` sensor allows one to track overhead flights in a given region. It uses crowd-sourced data from the [OpenSky Network](https://opensky-network.org/) public API. It will also fire Home Assistant events when flights enter and exit the defined region.

## {% linkable_title Configuration %}

To enable this sensor, add the following lines to your `configuration.yaml` file:

```yaml
sensor:
  - platform: opensky
    radius: 10
```

Configuration options for the OpenSky Network sensor:

- **radius** (*Required*): Radius of region to monitor, in kilometers.
- **latitude** (*Optional*): Region latitude. Defaults to home zone latitude.
- **longitude** (*Optional*): Region longitude. Defaults to home zone longitude.
- **altitude** (*Optional*): The maximum altitude (in meters) for planes to be detected in, 0 sets it to unlimited. Defaults to 0).
- **name** (*Optional*): Sensor name. Defaults to opensky.

## {% linkable_title Events %}

- **opensky_entry**: Fired when a flight enters the region.
- **opensky_exit**: Fired when a flight exits the region.

Both events have two attributes:

- **sensor**: Name of `opensky` sensor that fired the event.
- **callsign**: Callsign of the flight.
- **altitude**: Altitude of the flight in meters.

To receive notifications of the entering flights, add the following lines to your `configuration.yaml` file:

{% raw %}
```yaml
automation:
  - alias: 'Flight entry notification'
    trigger:
      platform: event
      event_type: opensky_entry
    action:
      service: notify.ios_YOURIPHONENAME
      data_template:
        message : 'Flight entry of {{ trigger.event.data.callsign }} '
```
{% endraw %}
