---
layout: page
title: "Upgrading Hassbian"
description: "Instructions on how to upgrade Hassbian to the latest version."
date: 2018-06-03 11:00
sidebar: true
comments: false
sharing: true
footer: true
redirect_from: /docs/hassbian/upgrading/
---

Hassbian is based on Raspbian and uses the same repositories. Any changes to Raspbian will be reflected in Hassbian. To update and upgrade system packages and installed software (excluding Home Assistant) do the following.
Log in as the `pi` account and execute the following commands:

```bash
$ sudo apt-get update
$ sudo apt-get -y upgrade
```

#### {% linkable_title Updating Home Assistant %}
<p class='note'>
You can use `hassbian-config` to automate the process by running `sudo hassbian-config upgrade homeassistant`
</p>

To update the Home Assistant installation execute the following command as the `pi` user.

```bash
$ sudo systemctl stop home-assistant@homeassistant.service
$ sudo -u homeassistant -H -s
$ source /srv/homeassistant/bin/activate
$ pip3 install --upgrade homeassistant
$ exit
$ sudo systemctl start home-assistant@homeassistant.service
```
