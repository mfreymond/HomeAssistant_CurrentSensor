# HomeAssistant Doorbell Button Sensor


Parts used in this project:

- [ESP 8266 Module](https://www.amazon.ca/gp/product/B07S5Z3VYZ/?&_encoding=UTF8&tag=mfreymond-20&linkCode=ur2&linkId=ecc55e3b7b3f051e2c1d24567067ee74&camp=15121&creative=330641)
- [Inductive Current Pickup](https://www.amazon.ca/gp/product/B00WS2QXG8/?&_encoding=UTF8&tag=mfreymond-20&linkCode=ur2&linkId=c5e86372a718adf1b25d73bab336b25f&camp=15121&creative=330641)
- 5 x 1N4148 Diode or similar
- 1 x 1N4007 Diode or similar
- 1 x 4.7µF 15v Capacitor (value not super specific)
- 2 x 27µF 50v Capacitor (value not super specific).  Multiple holes provided for a variaty of lead spacing.
- 1 x 0.1µF 15v Capacitor 
- 1 x 3.3v Zener Diode
- 1 x 10kΩ Resistor (may need to be varied based on your specific doorbell transformer)
- 1 x 82 Ω 1/2 watt resistor (used to drop the voltage for the 7805 regulator.  Adjust as needed.)
- 1 x 7805 Voltage Regulator
- ### Optional
- 2 x Generic LED (1 for power, 1 for an indicator)
- 2 x 330Ω Resistor (used as LED current limit.  Adjust as desired).

## Temative Board image
![Board Image](https://github.com/mfreymond/HomeAssistant_Doorbell/blob/main/Images/Doorbell%20Current%20sensor_Doorbell.png)

Board is 95mm x 95mm.

## ESPHome Configuration:

```
esphome:
  name: doorbell-button
  friendly_name: Doorbell_Button

esp8266:
  board: nodemcu

# Enable logging
logger:

# Enable Home Assistant API
api:
  encryption:
    key: "itsasecret"

ota:
  password: "itsasecret"

wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password

  # Enable fallback hotspot (captive portal) in case wifi connection fails
  ap:
    ssid: "Doorbell-Button Fallback Hotspot"
    password: "itsasecret"

captive_portal:


switch: # controls the LED on the nodemcu8266
  - platform: gpio
    name: "$devicename LED"
    id: ledlight
    pin:
      number: D4 # GPIO2 Blue LED pin
      inverted: yes

binary_sensor:
  - platform: gpio
    pin: D1
    name: "Door Bell Button"
    device_class: door
    on_press:
        - switch.turn_on: ledlight
    on_release:
        - switch.turn_off: ledlight



```
