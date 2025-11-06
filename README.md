# ESP32-P4-86-Panel-ETH-2RO LVGL Firmware 
ESPHome Configuration for the ESP32-P4-86-Panel-ETH-2RO with an LVGL UI.

**********CONFIGURATION COMING SOON**********

All credit for getting this working goes to https://github.com/alaltitov/Waveshare-ESP32-P4-86-Panel-ETH-2RO.
All credit and inspiration for the original UI and device configuration goes to https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/.
This is an updated port of my S3 box configuration https://github.com/chrisdunnname/esphome-s3-box-3-lvgl.

This firmware provides the ESP32-P4-86-Panel-ETH-2RO (and non ethernet version) with a voice assistant, timers, screen saver with analog/digital clock and sleep, 12/24 hour time, media controls, alarmo integration, alarm clock, internal and external audio, notifications with sound, and multiple pages for lights, thermostats, switches, media, scenes, locks other devices from your Home Assistant.

A large number of entities are exposed to Home Assistant including a notification text entity that provides the ability to push notifications to the device which will display on screen for 10 seconds (with an optional notification sound) and an Image URL entity that provides the ability to push the URL for a PNG image to the device which will display on screen for 30 seconds (with no notification sound). This can be used with a [JPG to PNG Converter](https://github.com/youkorr/hacs-jpg-to-png-converter) in an automation to capture a snapshot from a camera and push it to the device.

A UI Mode feature provides the ability to switch the user experience with 3 modes: Default, HAL, Home.
Each provides a different theme and voice assistant interface.
- Default provides the original theme and a more standard Home Assistant experience. 
- HAL provides a darker theme and an animated Space Odyssey inspired 2001 HAL voice assistant.
- Home provides a more subtle theme and an animated Google inspired voice assistant.

The wakeword is not tied to the UI Mode providing flexibility for your preferred experience.

The On Device Wake Word includes the standard ESPHome wakeword models (4) but also some experimental models including okay hal.
Additional experimental wake words for okay computer and hey home assistant and included in the config but disabled by default. 

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
