---
layout: page
title: "UniFi Video Camera"
description: "Instructions on how to integrate UVC cameras within Home Assistant."
date: 2016-02-07 10:00
sidebar: true
comments: false
sharing: true
footer: true
logo: ubiquiti.png
ha_category: Camera
ha_release: 0.13
ha_iot_class: "Local Polling"
---

The `uvc` camera platform allows you to integrate [UniFi Video Camera (UVC)](https://www.ubnt.com/products/#unifivideo) into Home Assistant.

The platform connects to the Unifi NVR software and automatically discovers/adds any camera connected to the NVR.

### {% linkable_title Setup %}

It is recommended that you create a new user for this platform in the NVR software and only give the user the permissions it need to operate.

- The API key is found in the specific user's `API Access` tab in the NVR software.
- The camera password is found in `Settings` -> `Camera Settings` -> `Camera Password` in the NVR software.

### {% linkable_title Configuration %}

To enable, add the following to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
camera:
  - platform: uvc
    nvr: IP_ADDRESS
    key: API_KEY
```

{% configuration %}
nvr:
  description: The IP or hostname of the NVR (Network Video Recorder) server.
  required: true
  type: string
port:
  description: The port number to use for accessing the NVR.
  required: false
  type: int
  default: 7080
key:
  description: The API key available from the NVR web interface.
  required: true
  type: string
password:
  description: The camera password.
  required: false
  type: string
  default: ubnt
{% endconfiguration %}

