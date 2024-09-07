# Home Assistant Add-on: Dahua VTO to MQTT Gateway

## How to use

This is just a wrapper for [Elad Bar's](https://gitlab.com/elad.bar) [Dahua VTO Gateway](https://gitlab.com/elad.bar/DahuaVTO2MQTT)

## Events

Are documented here https://gitlab.com/elad.bar/DahuaVTO2MQTT/-/blob/master/MQTTEvents.MD

## Commands

#### Open Door

By publishing MQTT message of {MQTT_BROKER_TOPIC_PREFIX}/Command/Open an HTTP request to the unit will be sent,
If the payload of the message is empty, default door to open is 1,
If unit supports more than 1 door, please add to the payload `Door` parameter with the number of the door

## Prometheus Exporter

`instance` is based pm MQTT Client ID, default is `DahuaVTO2MQTT`

`version` is based on the docker image, format is `Year.Month.Day.NumberOfSecondsSinceMidnight`

```prom
# HELP dahuavto2mqtt_mqtt_status MQTT Connectivity Status
# TYPE dahuavto2mqtt_mqtt_status gauge
dahuavto2mqtt_mqtt_status{instance="DahuaVTO2MQTT",version="2023.12.20.35999"} 1.0
# HELP dahuavto2mqtt_mqtt_incoming_messages MQTT Incoming Messages
# TYPE dahuavto2mqtt_mqtt_incoming_messages gauge
dahuavto2mqtt_mqtt_incoming_messages{instance="DahuaVTO2MQTT",topic="Command/Open",version="2023.12.20.35999"} 2.0
# HELP dahuavto2mqtt_mqtt_outgoing_messages MQTT Outgoing Messages
# TYPE dahuavto2mqtt_mqtt_outgoing_messages gauge
dahuavto2mqtt_mqtt_outgoing_messages{instance="DahuaVTO2MQTT",topic="AlarmLocal/Event",version="2023.12.20.35999"} 2.0
# HELP dahuavto2mqtt_mqtt_failed_outgoing_messages MQTT Failed Outgoing Messages
# TYPE dahuavto2mqtt_mqtt_failed_outgoing_messages gauge
# HELP dahuavto2mqtt_dahua_status Dahua Connectivity Status
# TYPE dahuavto2mqtt_dahua_status gauge
dahuavto2mqtt_dahua_status{instance="DahuaVTO2MQTT",version="2023.12.20.35999"} 1.0
# HELP dahuavto2mqtt_dahua_messages Dahua Messages
# TYPE dahuavto2mqtt_dahua_messages gauge
dahuavto2mqtt_dahua_messages{instance="DahuaVTO2MQTT",session_id="0",topic="global.login",version="2023.12.20.35999"} 1.0
# HELP dahuavto2mqtt_dahua_failed_messages Dahua Failed Messages
# TYPE dahuavto2mqtt_dahua_failed_messages gauge
dahuavto2mqtt_dahua_failed_messages{instance="DahuaVTO2MQTT",session_id="0",topic="incoming",version="2023.12.20.35999"} 1.0
```
