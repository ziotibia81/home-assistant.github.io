---
layout: page
title: "Modbus"
description: "Instructions on how to integrate Modbus within Home Assistant."
date: 2015-04-25 9:16
sidebar: true
comments: false
sharing: true
footer: true
logo: modbus.png
ha_category: Hub
ha_release: pre 0.7
ha_iot_class: "Local Push"
---


[Modbus](http://www.modbus.org/) is a serial communication protocol to control PLCs (Programmable logic controller). It currently supports sensors and switches which can be controlled over serial, TCP, and UDP connections.

## {% linkable_title Configuration %}

To add modbus to your installation, add the following to your `configuration.yaml` file:

For a network connection:

```yaml
# Example configuration.yaml entry for a TCP connection
modbus:
  type: tcp
  host: IP_ADDRESS
  port: 2020
```

{% configuration %}
type:
  description: Type of the connection to Modbus. Possible values are `tcp` (Modbus TCP protocol according to "MODBUS Messaging Implementation Guide version 1.0b" provided by Schneider Automation.), `udp`(Modbus TCP form, but using UDP for transport. It removes the overheads required for TCP.) and `rtuovertcp` (Modbus RTU message transmitted with a TCP/IP wrapper and sent over a network instead of serial lines.).
  required: true
  type: string
host:
  description: The IP address of your Modbus device, e.g., 192.168.1.1.
  required: true
  type: string
port:
  description: The port for the communication.
  required: true
  type: integer
timeout:
  description: Timeout for slave response in seconds.
  required: false
  default: 3
  type: integer
{% endconfiguration %}

For a serial connection:

```yaml
# Example configuration.yaml entry for a serial connection
modbus:
  type: serial
  method: rtu
  port: /dev/ttyUSB0
  baudrate: 9600
  stopbits: 1
  bytesize: 8
  parity: N
```

{% configuration %}
type:
  description: Type of the connection to Modbus.
  required: true
  type: string
method:
  description: Method of the connection to Modbus.
  required: true
  type: string
port:
  description: The port where your Modbus device is connected to your Home Assistant host.
  required: true
  type: string
baudrate:
  description: The speed for the serial connection.
  required: true
  type: integer
stopbits:
  description: The stopbits for the serial connection.
  required: true
  type: integer
bytesize:
  description: The bytesize for the serial connection.
  required: true
  type: integer
parity:
  description: The parity for the serial connection.
  required: true
  type: string
timeout:
  description: Timeout for slave response in seconds.
  required: false
  default: 3
  type: integer
{% endconfiguration %}

### {% linkable_title Services %}


| Service | Description |
| ------- | ----------- |
| write_register | Write register. Requires `unit`, `address` and `value` fields. `value` can be either single value or an array |


## {% linkable_title Building on top of Modbus %}

 - [Modbus Binary Sensor](/components/binary_sensor.modbus/)
 - [Modbus Sensor](/components/sensor.modbus/)
 - [Modbus Switch](/components/switch.modbus/)
