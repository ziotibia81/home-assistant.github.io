---
layout: page
title: "Security of Home Assistant"
description: "Security of Home Assistant."
date: 2017-02-13 12:50
sidebar: true
comments: false
sharing: true
footer: true
---

As Home Assistant is like every other service or daemon that is running on a computer system that allows access over a network connection, certain measurement were taken to increase the overall security while still staying operational.

[Secure your installation](/docs/configuration/securing/) once you've finished with the installation process regardless of your use case.

Home Assistant is NOT able to change the configuration of your router or firewall. This means that you need to setup [port-forwarding](/docs/configuration/remote/) and adjusting firewall rules if you want to allow access from the internet. By default your frontend and your Hass.io add-ons like Mosquitto, SSH and your Samba shares are only accessible from your local network.

## {% linkable_title Server banner %}

Further [details about the fingerprint/server banner](/docs/security/webserver/) of a Home Assistant instance are available. 

## {% linkable_title Porosity %}

The default port of Home Assistant is 8123. This is the port where the [`frontend`](/components/frontend/) and the [`API`](/components/api/) is served. Both are depending on the [`http`](/components/http/) component which contains the capability to adjust the settings like `server_host` or `server_port`.

See the [open ports](/docs/security/porosity/) of a Hass.io instance with various add-ons.

## {% linkable_title HTTP SSL/TLS %}

Home Assistant is following the [Mozilla's Operations Security team recommendations](https://wiki.mozilla.org/Security/Server_Side_TLS) for Server side SSL/TLS settings. To allow the users to access Home Assistant with most devices the target is **Intermediate compatibility**.

## {% linkable_title SSH %}

The SSH connection for [debugging](https://developers.home-assistant.io/docs/en/hassio_debugging.html) on port 22222 is not enabled by default and can only be used with keys.

Is SSH used with the [SSH server add-on](/addons/ssh/) then the user is responsible for the configuration and security. 

## {% linkable_title Source code %}

Due to the lack of resources we are not able to review all of our dependencies and inspect them for malicious behavior, leakage of information or compliance with GDPR. But we have a keen interest in the development of our dependencies are try to work closely with the upstream developer.

