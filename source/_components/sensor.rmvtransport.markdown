---
layout: page
title: "RMV"
description: "Instructions on how to integrate Rhein-Main public transport departure times into Home Assistant."
date: 2018-08-02 22:00
sidebar: true
comments: false
sharing: true
footer: true
logo: RMV.png
ha_category: Transport
ha_release: 0.76
ha_iot_class: "Cloud Polling"
---

The `rvmtransport` sensor will give you the departure time of the next bus, tram, subway, or train at the next station or stop in the Rhein-Main area public transport network. Additional details such as the line number and destination are present in the attributes.

## {% linkable_title Configuration %}

To enable this sensor, add the following lines to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
sensor:
  - platform: rmvtransport
    next_departure:
     - station: STATION_OR_STOP_ID
```

{% configuration %}
name:
  description: Name to use in the frontend.
  required: false
  default: The default is the station name.
  type: string
stationId:
  description: ID of the stop or station, e.g. 3000010. Visit [the RMV OpenData web site](https://opendata.rmv.de) to find a list of valid IDs.
  required: true
  type: string
destinations:
  description: "One or multiple final stop names, e.g., 'Frankfurt (Main) Hauptbahnhof' or ['Frankfurt (Main) Hauptbahnhof','Frankfurt (Main) Stadion']. This can be used to only consider a particular direction of travel."
  required: false
  type: [string]
lines:
  description: "One or more line numbers, e.g., `'S8'` or `['S8', 'RB33', '41']`"
  required: false
  default: The default is the station name.
  type: [string, int]
products:
  description: "One or more modes of transport `['U-Bahn', 'Tram', 'Bus', 'S-Bahn', 'RB', 'RE', 'EC', 'IC', 'ICE']`."
  required: false
  default: Defaults to all.
  type: [string]
time_offset:
  description: Do not display departures leaving sooner than this number of minutes. Useful if you are a couple of minutes away from the stop.
  required: false
  default: The defaults is 0.
  type: int
max_journeys:
  description: Specify the maximal number of journeys.
  required: false
  default: The default is 5.
  type: string
{% endconfiguration %}

## {% linkable_title Examples %}

### {% linkable_title Full configuration %}

The example below shows a full configuration with three sensors that showcase the various configuration options.

```yaml
# Example configuration.yaml entry
sensor:
  - platform: rmvtransport
    next_departure:
      - station: 3000010
        time_offset: 5
        destinations:
          - 'Frankfurt (Main) Flughafen Regionalbahnhof'
          - 'Frankfurt (Main) Stadion'
        products:
          - 'RB'
          - 'RE'
          - 'Bus'
          - 'S'
      - station: 3006907
        products: 'Bus'
        destinations: ['Wiesbaden Dernsches Gelände', 'Mainz Hauptbahnhof']
        name: Destination
      - station: 3006904
        lines: 'S8'
        max_journeys: 5
        products: 'S'
```

The first sensor will return S-Bahn, bus, RB and RE trains departures from Frankfurt Hauptbahnhof to Frankfurt Airport or Stadium that are at least 5 minutes away.

The second sensor returns bus departures from Wiesbaden Hauptbahnhof going to Dernsches Gelände and Mainz Hauptbahnhof. To retrieve the time of the second departure, you would use states.sensor.ENTITY_NAME.attributes.departures[1].time.

The third sensor returns all S-Bahn trains from Mainz Hauptbahnhof for line S8.
