# bTicino-MQTT-NodeRed-Home-Assistant

Install NodeRed

Install Mosquito

Open config.yaml and under light add this code:

yaml
- platform: mqtt
  schema: template
  name: 'ingresso'
  command_topic: 'lights/cmd'
  state_topic: 'bticino/out'
  command_on_template: '{"idx": 15, "nvalue": "1" }'
  command_off_template: '{"idx": 15, "nvalue": "0" }'
  state_template: '{% if value_json.idx == 15 %} {% if value_json.nvalue == 1 %} on {% else %} off {% endif %} {% endif %}'
  optimistic: false
