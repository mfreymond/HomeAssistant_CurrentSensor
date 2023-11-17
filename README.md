# HomeAssistant Doorbell Button Sensor


Parts used in this project:

- [ESP 8266 Module](https://www.amazon.ca/gp/product/B07S5Z3VYZ/?&_encoding=UTF8&tag=mfreymond-20&linkCode=ur2&linkId=ecc55e3b7b3f051e2c1d24567067ee74&camp=15121&creative=330641)
- [Inductive Current Pickup](https://www.amazon.ca/gp/product/B00WS2QXG8/?&_encoding=UTF8&tag=mfreymond-20&linkCode=ur2&linkId=c5e86372a718adf1b25d73bab336b25f&camp=15121&creative=330641)
- 5 x 1N4148 Diode
- 1 x 1N4007 Diode
- 1 x 4.7µF 15v Capacitor (value not super specific)
- 2 x 27µF 50v Capacitor (value not super specific)
- 1 x 0.1µF 15v Capacitor 
- 1 x 3.3v Zener Diode
- 1 x 10kΩ Resistor
- 1 x 82 Ω 1/2 watt resistor (used to drop the voltage for the 7805 regulator.  Adjust as needed.)
- 1 x 7805 Voltage Regulator
- ### Optional
- 1 x Generic LED
- 1 x 330Ω Resistor (used as LED current limit.  Adjust as desired).

## Temative Board image
![Board Image](https://github.com/mfreymond/HomeAssistant_Doorbell/blob/main/Images/Doorbell%20Current%20sensor_Doorbell.png)

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
    
binary_sensor:
  - platform: gpio
    pin: D1
    name: "Door Bell Button"
    device_class: door


```
