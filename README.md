# ESP32-P4-86-Panel-ETH-2RO LVGL Firmware 
ESPHome Configuration for the ESP32-P4-86-Panel-ETH-2RO with an LVGL UI.

All credit and inspiration for the base configuration goes to https://github.com/alaltitov/Waveshare-ESP32-P4-86-Panel-ETH-2RO

This firmware provides the ESP32-P4-86-Panel-ETH-2RO with a voice assistant, UI and other devices from your Home Assistant.

The UI and Voice Assistant experience is implemented out of the box.
Configuration is required to integrate button actions into your Home Assistant.
This configuration is suitable for anyone with an understanding of ESPHOME, the ESP32-P4-86-Panel-ETH-2RO, Home Assistant and Wake Word Voice Assistants.

Key Components:
- Touchscreen: https://esphome.io/components/touchscreen/gt911.html
- Audio ADC: https://esphome.io/components/audio_adc/es7210.html
- Audio DAC: https://esphome.io/components/audio_dac/es8311.html
- Wake Word VA: https://github.com/esphome/wake-word-voice-assistants/
- Micro Wake Word Models: https://github.com/esphome/micro-wake-word-models/
- LVGL: https://esphome.io/components/lvgl/

Optional:
- Printed 86-Box: https://makerworld.com/en/models/475224-type-86-switch-desktop-base-123-gangs

# Requirements
Requires [ESP32-P4-86-Panel-ETH-2RO](https://www.waveshare.com/wiki/ESP32-P4-86-Panel-ETH-2RO).
Ethernet version is required to use ethernet and additional GPO Ports. Also required to mount in x86 box.

The minimum supported ESPHome version is 2025.10.0.
Last tested on Home Assistant 2025.10 and ESPHome Version 2025.10.

# More Information
To be continued...

# Configuration Guidance
LVGL functions differently to the standard ESPHOME UI. Instead of using lambda to construct pages and format them separate to the touch screen configuration, LVGL uses a hierarchical page structure combining the touchscreen and UI elements.
This means the LVGL section of the YAML contains all the UI elements including the pages and widgets. These widgets are interactive and have different actions associated to their type. 
Setting the status of these widgets is not done in the LVGL configuration. Instead each component forces appropriate updates to the UI. So when a switch is turned on or off it needs to update the lvgl switch widget to be checked or not checked.
This means the UI updates interactively so that as actions are performed which send service calls to home assistant or trigger local actions, the corresponding state changes in sensors can update the UI in response.
For each new or modified widget you need to update the LVGL to specify the action to take when a UI interaction occurs and in parallel you need to update the entity to update the UI on state changes.

The configuration supports wifi or ethernet. The appropriate section must be uncommented and the alternate section commented depending on your preferred implementation.
Two additional secrets are used for wifi credentials for connecting your device to yur wifi and these are wifi_ssid and wifi_password.
