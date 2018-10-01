---
layout: page
title: "Facebox"
description: "Detect and recognize faces with Facebox."
date: 2018-05-03 00:00
sidebar: true
comments: false
sharing: true
footer: true
logo: machine-box.png
ha_category: Image Processing
featured: false
ha_release: 0.70
---

The `facebox` image processing platform allows you to detect and recognize faces in a camera image using [Facebox](https://machinebox.io/docs/facebox). The state of the entity is the number of faces detected, and recognized faces are listed in the `matched_faces` attribute. An `image_processing.detect_face` event is fired for each recognized face, and the event `data` provides the `confidence` of recognition, the `name` of the person, the `image_id` of the image associated with the match, the `bounding_box` that contains the face in the image, and the `entity_id` that processing was performed on.

## {% linkable_title Setup %}

Facebox runs in a Docker container and it is recommended that you run this container on a machine with a minimum of 2 GB RAM. On your machine with Docker, run the Facebox container with:

```bash
MB_KEY="INSERT-YOUR-KEY-HERE"

sudo docker run --name=facebox --restart=always -p 8080:8080 -e "MB_KEY=$MB_KEY"  machinebox/facebox
```
You can run Facebox with a username and password by adding `-e "MB_BASICAUTH_USER=my_username" -e "MB_BASICAUTH_PASS=my_password"` but bare in mind that the component does not encrypt these credentials and this approach does not guarantee security on an unsecured network. 

If you only require face detection (number of faces) you can disable face recognition by adding `-e "MB_FACEBOX_DISABLE_RECOGNITION=true"` to the `docker run` command.

## {% linkable_title Configuration %}

To enable this platform in your installation, add the following to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
image_processing:
  - platform: facebox
    ip_address: 192.168.0.1
    port: 8080
    source:
      - entity_id: camera.local_file
        name: my_custom_name
```

{% configuration %}
ip_address:
  description: The IP address of your machine hosting Facebox.
  required: true
  type: string
port:
  description: The port which Facebox is exposed on.
  required: true
  type: string
username:
  description: The Facebox username if you have set one.
  required: false
  type: string
password:
  description: The Facebox password if you have set one.
  required: false
  type: string
source:
  description: The list of image sources.
  required: true
  type: map
  keys:
    entity_id:
      description: A camera entity id to get picture from.
      required: true
      type: string
    name:
      description: This parameter allows you to override the name of your `image_processing` entity.
      required: false
      type: string
{% endconfiguration %}

## {% linkable_title Automations %}

Use the `image_processing.detect_face` events to trigger automations, and breakout the `trigger.event.data` using a [data_template](https://www.home-assistant.io/docs/automation/templating/). The following example automation sends a notification when Ringo Star is recognized:

{% raw %}
```yaml
- id: '12345'
  alias: Ringo Starr recognised
  trigger:
    platform: event
    event_type: image_processing.detect_face
    event_data:
      name: 'Ringo_Starr'
  action:
    service: notify.platform
    data_template:
      message: Ringo_Starr recognised with probability {{ trigger.event.data.confidence }}
      title: Door-cam notification
```
{% endraw %}

## {% linkable_title Service `facebox_teach_face` %}

The service `facebox_teach_face` can be used to teach Facebox faces.  

| Service data attribute | Optional | Description |
| ---------------------- | -------- | ----------- |
| `entity_id` | no | Entity ID of Facebox entity.
| `name` | no | The name to associate with a face.
| `file_path` | no | The path to the image file.

A valid service data example:

{% raw %}
```yaml
{
  "entity_id": "image_processing.facebox_local_file",
  "name": "superman",
  "file_path": "/images/superman_1.jpeg"
}
```
{% endraw %}

You can use an automation to receive a notification when you train a face:

{% raw %}
```yaml
- id: '1533703568569'
  alias: Face taught
  trigger:
  - event_data:
      service: facebox_teach_face
    event_type: call_service
    platform: event
  condition: []
  action:
  - service: notify.pushbullet
    data_template:
      message: '{{ trigger.event.data.service_data.name }} taught 
      with file {{ trigger.event.data.service_data.file_path }}'
      title: Face taught notification
```
{% endraw %}

Any errors on teaching will be reported in the logs. If you enable [system_log](https://www.home-assistant.io/components/system_log/) events:

```yaml
system_log:
  fire_event: true
```

you can create an automation to receive notifications on Facebox errors:

{% raw %}
```yaml
- id: '1533703568577'
  alias: Facebox error
  trigger:
    platform: event
    event_type: system_log_event
  condition:
    condition: template
    value_template: '{{ "facebox" in trigger.event.data.message }}'
  action:
  - service: notify.pushbullet
    data_template:
      message: '{{ trigger.event.data.message }}'
      title: Facebox error
```
{% endraw %}

## {% linkable_title Optimising resources %}

[Image processing components](https://www.home-assistant.io/components/image_processing/) process the image from a camera at a fixed period given by the `scan_interval`. This leads to excessive processing if the image on the camera hasn't changed, as the default `scan_interval` is 10 seconds. You can override this by adding to your config `scan_interval: 10000` (setting the interval to 10,000 seconds), and then call the `image_processing.scan` service when you actually want to perform processing.
