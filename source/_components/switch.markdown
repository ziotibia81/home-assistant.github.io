---
layout: page
title: "Switches"
description: "Instructions on how to setup your switches with Home Assistant."
date: 2015-01-24 14:39
sidebar: true
comments: false
sharing: true
footer: true
---

Keeps track which switches are in your environment, their state and allows you to control them.

 * Maintains a state per switch and a combined state `all_switches`.
 * Registers services `switch.turn_on`, `switch.turn_off`, and `switch.toggle` to control switches.

### {% linkable_title Use the services %}

In the frontend open the sidebar. At the bottom, under **Developer Tools**, click **Services**. From the Service dropdown menu choose `switch.turn_on` or `switch.turn_off` from the list of available services. In the Entity dropdown menu choose or enter the entity ID you want to work with. This will enter something like the sample below into the **Service Data** field. Now hit **CALL SERVICE**.

```json
{"entity_id":"livingroom_pin2"}
```

| Service data attribute | Optional | Description |
| ---------------------- | -------- | ----------- |
| `entity_id`            |      yes | Only act on a specific switch. Otherwise it targets all switches.
