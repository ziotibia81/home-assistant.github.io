---
layout: page
title: "Neato Robotics Vacuum"
description: "Instructions on how to integrate a Neato Botvac Connected Vacuum within Home Assistant."
date: 2017-10-18 16:11
sidebar: true
comments: false
sharing: true
footer: true
logo: neato.png
ha_category: Vacuum
ha_release: 0.57
ha_iot_class: "Cloud Polling"
redirect_from: /components/sensor.neato/
---

The `neato` vacuum platform allows you to control your [Neato Botvac Connected](https://www.neatorobotics.com/robot-vacuum/botvac-connected-series/).
The status will contain attributes on the robots last clean session.

<p class='note'>
If you notice the robot stops responding to commands check the state to see if the robot is "unavailable". If you see "unavailable" first try to restart the vacuum and wait about 5 minutes to see if it is no longer "unavailable". If you are still having issues check the Neato app and make sure your robot is connected and working. If it is not then follow the steps in the app to reset your robot and give it the same name as before then restart Home Assistant.
</p>

## {% linkable_title Configuration %}

To add `neato` vacuum to your installation, please follow instructions in [Neato component](/components/neato/).

Currently supported services are:

- `start`
- `pause`
- `stop`
- `return_to_base`
- `locate`
