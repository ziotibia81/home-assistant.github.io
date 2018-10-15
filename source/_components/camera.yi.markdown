---
layout: page
title: "Yi Home Camera"
description: "Instructions on how to integrate a video feed (via FFmpeg) as a camera within Home Assistant."
date: 2017-10-10 13:00
sidebar: true
comments: false
sharing: true
footer: true
logo: yi.png
ha_category: Camera
ha_release: 0.56
ha_iot_class: "Local Polling"
---

The `yi` camera platform allows you to utilize [Yi Home Cameras](https://www.yitechnology.com/) within Home Assistant. Specifically, this platform supports the line of Yi Home Cameras that are based on the Hi3518e Chipset. This includes:

* Yi Home 17CN / 27US / 47US
* Yi 1080p Home
* Yi Dome
* Yi 1080p Dome

To successfully implement this platform, the Home Assistant host should be capable of multiple simultaneous reads. For every concurrent Home Assistant user, a connection will be made to the camera every 10 seconds. This should normally not be a problem.

## {% linkable_title Preparing the Device %}

### {% linkable_title Installing Alternative Firmware %}

In order to integrate the camera with Home Assistant, it is necessary to install a custom firmware on the device. Instructions for doing so can be found via the [yi-hack-v3 GitHub project](https://github.com/shadow-1/yi-hack-v3).

Once installed, please ensure that you have enabled FTP and Telnet on your device.

 <p class='note warning'>
Currently, version 0.1.4-beta2 of the custom firmware is the highest supported without having to make additional modifications. Firmwares higher than this version use [Pure-FTPd](https://www.pureftpd.org/project/pure-ftpd), which has a bug that prevents FFmpeg from correctly rendering video files. To use higher firmware versions you must also follow [this workaround](https://github.com/shadow-1/yi-hack-v3/issues/129#issuecomment-361723075) to revert back to ftpd.
</p>

<p class='note warning'>
Hassbian users: don't forget to install ffmpeg support on your platform, otherwise, you'll not see video.
</p>

<p class='note warning'>
Some alternative Yi firmwares enable an experimental RTSP server, which will allow you to connect to your camera via other Home Assistant camera platforms. However, this RTSP server disables the ability to use the supremely-useful Yi Home app. In order to maintain both Home Assistant compatibility _and_ the native app, this platform retrieves videos via FTP.
</p>

### {% linkable_title Changing the FTP Password %}

Once the custom firmware is installed, a password must be added to the FTP
server. To do so:

1. Telnet into your camera: `telnet <IP ADDRESS>`.
2. Enter `root` as the username and `<blank>` as the password.
3. Type `passwd` and hit `<Enter>`.
4. Enter your new password twice.
5. Log out of Telnet.

## {% linkable_title Configuring the Platform %}

To enable the platform, add the following lines to your`configuration.yaml` file:

```yaml
camera:
  - platform: yi
    name: Camera
    host: '192.168.1.100'
    password: my_password_123
```

{% configuration %}
name:
  description: A human-friendly name for the camera.
  required: true
  type: string
host:
  description: The IP address or hostname of the camera.
  required: true
  type: string
password:
  description: The password for the FTP server running on the camera. Can be any string as the current firmware doesn't allow setting FTP passwords.
  required: true
  type: string
path:
  description: The path to the raw MP4 files.
  required: false
  default: /media/mmcblk0p1/record
  type: string
username:
  description: The user that can access the FTP server.
  required: false
  default: root
  type: string
ffmpeg_arguments:
  description: Extra options to pass to `ffmpeg` (e.g., image quality or video filter options).
  required: false
  type: string
{% endconfiguration %}

## {% linkable_title Image quality %}

Any option supported by [`ffmpeg` camera](/components/camera.ffmpeg/) can be utilized via the `ffmpeg_arguments` configuration parameter.

One particularly useful adjustment deals with video size. Since Yi videos are fairly large (especially on the 1080p cameras), the following configuration will bring them down to a manageable size:

```yaml
camera:
  - platform: yi
    name: My Camera
    host: '192.168.1.100'
    password: my_password_123
    path: /home/camera/feed
    ffmpeg_arguments: '-vf scale=800:450'
```
