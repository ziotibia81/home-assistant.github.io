---
layout: page
title: "Asterisk Call Data Recorder"
description: "Instructions on how to integrate an Asterisk CDR within Home Assistant."
date: 2018-09-12 06:30
sidebar: true
comments: false
sharing: true
footer: true
logo: asterisk.png
ha_category: Mailbox
ha_release: 0.79
---

The Asterisk Call Data Recorder provides access to Asterisk call logs on the Asterisk PBX server. This mailbox is enabled automatically through the [Asterisk Voicemail component](/components/asterisk_mbox/) configuration if the `asterisk_mbox_server` is configured to provide CDR data.  More information on configuring the server can be found in the [Asterisk PBX configuration guide](/docs/asterisk_mbox/).
