---
layout: page
title: "Picture Glance Card"
sidebar_label: Picture Glance
description: "Show an image card and corresponding entity states as icon"
date: 2018-07-01 10:28 +00:00
sidebar: true
comments: false
sharing: true
footer: true
---

Show an image card and corresponding entity states as icon. The entities on the right side allow toggle actions, others show the more-info-dialog.

<p class='img'>
  <img src='/images/lovelace/lovelace_picture_glance.gif' alt='Picture glance card for a living room'>
  Picture glance card for a living room.
</p>

{% configuration %}
type:
  required: true
  description: picture-glance
  type: string
entities:
  required: true
  description: List of entities or entity objects.
  type: list
title:
  required: false
  description: The card title.
  type: string
navigation_path:
  required: false
  description: Navigate to path on tap action.
  type: string
image:
  required: false
  description: Background image URL.
  type: string
camera_image:
  required: false
  description: Camera entity as Background image.
  type: string
state_image:
  required: false
  description: Background image based on entity state.
  type: object
  keys:
    state:
      type: string
      required: false
      description: "`state: image-url`, check the example below."
aspect_ratio:
  required: false
  description: "Forces the height of the image to be a ratio of the width. You may enter a value such as: `16x9`, `16:9`, `1.78`."
  type: string
entity:
  required: false
  description: Entity to use for `state_image`.
  type: string
{% endconfiguration %}

## {% linkable_title Options For Entities %}

If you define entities as objects instead of strings, you can add more customization and configuration:

{% configuration %}
entity:
  required: true
  description: Home Assistant entity ID.
  type: string
icon:
  required: false
  description: Overwrites default icon.
  type: string
{% endconfiguration %}

## {% linkable_title Examples %}

```yaml
- type: picture-glance
  title: Living room
  entities:
    - switch.decorative_lights
    - light.ceiling_lights
    - lock.front_door
    - binary_sensor.movement_backyard
    - binary_sensor.basement_floor_wet
  image: /local/living_room.png
```

Display a camera image as background:

```yaml
- type: picture-glance
  title: Living room
  entities:
    - switch.decorative_lights
    - light.ceiling_lights
  camera_image: camera.demo_camera
```

Use different images based on entity state:

```yaml
- type: picture-glance
  title: Living room
  entities:
    - switch.decorative_lights
    - light.ceiling_lights
  state_image:
    "on": /local/living_room_on.png
    "off": /local/living_room_off.png
  entity: group.living.room
```
