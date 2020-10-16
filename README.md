# bTicino-MQTT-NodeRed-Home-Assistant

Install NodeRed

Install Mosquito

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

**command_on_template, 

**command_off_template,

**state_template

Create one for each light do you want to add to HA

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

**payload_on:

**payload_off:

**value_template:
