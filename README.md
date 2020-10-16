# bTicino-MQTT-NodeRed-Home-Assistant

Install NodeRed

Install Mosquito

**LIGHT

Open config.yaml and under light add this code:

```

- platform: mqtt
  schema: template
  name: 'ingresso'
  command_topic: 'lights/cmd'
  state_topic: 'bticino/out'
  command_on_template: '{"idx": 15, "nvalue": "1" }'
  command_off_template: '{"idx": 15, "nvalue": "0" }'
  state_template: '{% if value_json.idx == 15 %} {% if value_json.nvalue == 1 %} on {% else %} off {% endif %} {% endif %}'
  optimistic: false
```
This will create a light in HA

where
>**name:** name of light you want to create

>**"idx":** unique ID of light

for each light you have to change the 3 idx values, in the example number 15 in 

>**command_on_template, 

>**command_off_template,

>**state_template

Create one for each light do you want to add to HA


**SWITCH

Under switch add this code:

```

- platform: mqtt
  name: 'presaterrazzo'
  icon: mdi:power-plug
  command_topic: 'switch/cmd'
  state_topic: 'bticino/out'
  payload_on: '{"idx": 81, "nvalue": "1" }'
  payload_off: '{"idx": 81, "nvalue": "0" }'
  state_on: 'on'
  state_off: 'off'
  value_template: '{% if value_json.idx == 81 %} {% if value_json.nvalue == 1 %} on {% else %} off {% endif %} {% endif %}'
  optimistic: false
  
```

This will create a switch in HA

where
>**name:** name of switch you want to create

>**"idx":** unique ID of switch

for each switch you have to change the 3 idx values, in the example number 81 in 

>**payload_on:

>**payload_off:

>**value_template:


**SENSOR

Under sensor add this code

The sensors are used to integrate the part relating to the thermal control unit.
The control unit can have several thermostats installed in different points of the house.
The various points are identified by a value, fixed with the jupers during the physical installation of the single thermostat
The control unit can have several thermostats installed in different points of the house.

The following data is currently integrated:

>Temperature value measured by the probe of the single thermostat

>Temperature value set for the single thermostat

>Any off set set directly on the single thermostat


>The on / off value of the actuator of the single thermostat is reported through a switch component of HA

```
- platform: mqtt
  device_class: 'Temperature'
  name: "T Zona Notte"
  state_topic: "bticino/sensor/t11"
  value_template: '{{value_json.nvalue }}'
  ```
this will create a sensor for Temperature value
for each point you want to create change

>**state_topic:** the number at the end bticino/sensor/t**xx**

the value you use could be the one you want no rule, but I suggest to use same number used to configure the hardware during installation of the plant

```
- platform: mqtt
  device_class: 'Temperature'
  name: "set T Zona Notte"
  state_topic: "bticino/sensor/sett11"
  value_template: '{{value_json.nvalue }}'
  ```
this will create a sensor for the set Temperature value, 
for each point you want to create change

>**state_topic:** the number at the end bticino/sensor/sett**xx**

the value you use could be the one you want no rule, but I suggest to use same number used to configure the hardware during installation of the plant


```
- platform: mqtt
  device_class: 'Temperature'
  name: "offset T Zona Notte"
  state_topic: "bticino/sensor/offsett11"
  value_template: '{{value_json.nvalue }}'
  ```
this will create a sensor for the offset Temperature value

>**state_topic:** the number at the end bticino/sensor/offsett**xx**
the value you use could be the one you want no rule, but I suggest to use same number used to configure the hardware during installation of the plant

add under switch this code
```
- platform: mqtt
  name: 'Valvola Zona Notte'
  icon: mdi:power-plug
  command_topic: 'bticino/switchcmd/valv11'
  state_topic: 'bticino/switch/valv11'
  state_on: 'on'
  state_off: 'off'
  value_template: '{% if value_json.nvalue == 1 %} on {% else %} off {% endif %}'
```
This will create a switch for actuator of thermostat
for each point you want to create change

>**command_topic:** the numeber at the end bticino/switchcmd/valv**xx**

>**state_topic:** the number at the end bticino/switch/valv**xx**


the value you use could be the one you want no rule, but I suggest to use same number used to configure the hardware during installation of the plant

