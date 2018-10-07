---
layout: page
title: "BMW Connected Drive"
description: "Instructions on how to setup your BMW Connected Drive account with Home Assistant."
date: 2018-01-10 23:00
sidebar: true
comments: false
sharing: true
footer: true
logo: bmw.png
ha_category: Car
ha_release: 0.64
---

The `bmw_connected_drive` component lets you retrieve data of your BMW vehicle from the BMW Connected Drive portal. You need to have a working BMW Connected Drive account, and a Connected Drive enabled vehicle for this to work.

For compatibility with your BMW vehicle check the [bimmer_connected page](https://github.com/m1n3rva/bimmer_connected) on github.

This component provides the following platforms:

 - Binary Sensors: Doors, windows, condition based services, check control messages, parking lights, door lock state, charging status (electric cars) and connections status (electric cars).
 - Device tracker: The location of your car.
 - Lock: Control the lock of your car.
 - Sensors: Mileage, remaining range, remaining fuel, charging time remaing (electric cars), charging status (electric cars), remaing range electric (electric cars).

To enable this component in your installation, add the following to your
`configuration.yaml` file:

```yaml
# Example configuration.yaml entry
bmw_connected_drive:
  name:
    username: USERNAME_BMW_CONNECTED_DRIVE
    password: PASSWORD_BMW_CONNECTED_DRIVE
    region: one of "north_america", "china", "rest_of_world"
```

{% configuration %}
bmw_connected_drive:
  description: configuration
  required: true
  type: map
  keys:
    name:
      description: Name of your account in Home Assistant.
      required: true
      type: string
    username:
      description: Your BMW Connected Drive username.
      required: true
      type: string
    password:
      description: Your BMW Connected Drive password.
      required: true
      type: string
    region:
      description: "The region of your Connected Drive account. Please use one of these values: `north_america`, `china`, `rest_of_world`"
      required: true
      type: string
    read_only:
      description: In read only mode, all services including the lock of the vehicle are disabled.
      required: false
      type: boolean
      default: false
{% endconfiguration %}

## {% linkable_title Services %}

The `bmw_connected_drive` component offers several services. In case you need to provide the vehicle identification number (VIN) as a parameter, you can see the VIN in the attributes of the device tracker for the vehicle. The VIN is a 17 digit alphanumeric string, e.g., `WBANXXXXXX1234567`.

Using these services will impact the state of your vehicle. So use these services with care!

### {% linkable_title Locking and unlocking %}

The vehicle can be locked and unlocked via the lock component that is created automatically for each vehicle. Before invoking these services, make sure it's safe to lock/unlock the vehicle in the current situation.

### {% linkable_title Air condition %}

The air condition of the vehicle can be activated with the service `bmw_connected_drive.activate_air_conditioning`.

What exactly is started here depends on the type of vehicle. It might range from just ventilation over auxiliary heating to real air conditioning. If your vehicle is equipped with auxiliary heating, only trigger this service if the vehicle is parked in a location where it is safe to use it (e.g., not in an underground parking or closed garage). 

The vehicle is identified via the parameter `vin`.

### {% linkable_title Sound the horn %}

The service `bmw_connected_drive.sound_horn` sounds the horn of the vehicle. This option is not available in some countries (among which  the UK). Use this feature responsibly, as it might annoy your neighbors. The vehicle is identified via the parameter `vin`. 

### {% linkable_title Flash the lights %}

The service `bmw_connected_drive.light_flash` flashes the lights of the vehicle. The vehicle is identified via the parameter `vin`.

### {% linkable_title Update the state %}

The service `bmw_connected_drive.update_state` fetches the last state of the vehicles of all your accounts from the BMW server. This does *not* trigger an update from the vehicle; it gets the data from the BMW servers. So this service does *not* interact with your vehicles. 

This service does not require any attributes.

## {% linkable_title Disclaimer %}

This software is not affiliated with or endorsed by BMW Group. 
