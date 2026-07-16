# ESP32-P4-86-Panel-ETH-2RO LVGL Firmware 
ESPHome Configuration for the ESP32-P4-86-Panel-ETH-2RO with an LVGL UI.

All credit for getting this working goes to https://github.com/alaltitov/Waveshare-ESP32-P4-86-Panel-ETH-2RO.
All credit and inspiration for the original UI and device configuration goes to https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/.

This is a port of my S3 box configuration https://github.com/chrisdunnname/esphome-s3-box-3-lvgl.

This firmware provides the ESP32-P4-86-Panel-ETH-2RO (and non ethernet version) with a voice assistant, timers, screen saver with analog/digital clock and sleep, 12/24 hour time, media controls, alarm integration, alarm clock, internal and external audio, notifications with sound, and multiple pages for lights, thermostats, switches, media, scenes, locks other devices from your Home Assistant.
A weather service from Home Assistant (e.g. open weather map) can provide temperature and condition for the screen saver.

A large number of entities are exposed to Home Assistant including a notification text entity that provides the ability to push notifications to the device which will display on screen for 10 seconds (with an optional notification sound) and an Image URL entity that provides the ability to push the URL for a PNG image to the device which will display on screen for 30 seconds (with no notification sound). This can be used with a [JPG to PNG Converter](https://github.com/youkorr/hacs-jpg-to-png-converter) in an automation to capture a snapshot from a camera and push it to the device.

A UI Mode feature provides the ability to switch the UI theme with 4 modes: Default, Dark, Grey, Light.
A VA Mode feature provides the ability to switch the voice assistant animated UI with 3 modes: Default, HAL, Home.
Each provides a different theme and voice assistant interface.
- Default provides a standard ESPHome and Home Assistant experience. 
- HAL provides an animated Space Odyssey inspired 2001 HAL voice assistant.
- Home provides an animated Google inspired voice assistant.

A no animation YAML configuration is provided that provides the UI Mode but the VA mode does not apply for much smaller firmware.

The wakeword is not tied to the VA Mode providing flexibility for your preferred experience.

The On Device Wake Word includes the standard ESPHome wakeword models (4) but also some experimental models including okay hal and hey luna.
Additional experimental wake words for okay computer and hey home assistant and included in the config but disabled by default. 

The UI and Voice Assistant experience is implemented out of the box.
Only basic configuration is required to integrate the standard features with your Home Assistant.

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
Requires variants of [ESP32-P4-86-Panel-ETH-2RO](https://www.waveshare.com/wiki/ESP32-P4-86-Panel-ETH-2RO).
 Wifi is recommended over Ethernet and both models of this device are supported. Ethernet version is required to mount in x86 box.

The minimum supported ESPHome version is 2026.7.0.
Last tested on Home Assistant 2026.7 and ESPHome Version 2026.7.

# Loading

![loading](https://github.com/user-attachments/assets/bc6c3b87-54bb-4726-88f8-fc815d243f2d)

# Home

![Home](https://github.com/user-attachments/assets/090f5618-d5b3-4cca-9809-47ea9067c8e6)

**Home Page Functions**

- The page title, menu icons and page navigation are configurable.
- Tapping on the time will show the alarm clock page.
- An alarm clock indicator will appear when the alarm clock is enabled and will launch the alarm settings page. 
- A timer status indicator will appear while a timer is running and will launch the time remaining page
- The alarm status indicator shows current alarm status and launches the security page
- The microphone indicator is a mute switch
- The home assistant indicator indicates if the API is connected
- The wifi status indicator indicates if the WIFI is connected and launches the wifi page
- The power indicator shows when powered on.

- The top right button on the device will switch from Home page to screensaver, stop a ringing timer, or a long 10s press will perform a factory reset.
- The bottom right button on the device will reboot the device. 

# Voice Assistant

- Standard experience in Default VA Mode

**Voice Timer Started**


- Standard experience in Default VA Mode

**Timer Time Remaining**



**Timer or Alarm Finished**

- Snooze button only shows for Alarm (snooze duration can be set in Home Assistant - default 5 minutes)

# Alarm Clock

- Access this page by clicking on the toolbar clock. Allows enabling alarm and setting a time.
- Up to 2 alarms can be set and a button will show which alarm is being viewed and allow switching between the two.
- Alarm Clock can be turned off from same page or is available as a switch so it can be turned off from voice assistant.
- Snooze duration can be set in Home Assistant (default 5 minutes).

# Climate

![climate](https://github.com/user-attachments/assets/30a43196-fd34-4161-9c09-14a5f33dd7dc)
- The page title is configurable.

**Air Conditioner**

Tap the change temperature buttons to move slightly or long press to change faster.

# Lights

![lights](https://github.com/user-attachments/assets/53c305bc-e213-47fa-964b-dc8a9ce7419f)
- The page title is configurable.
- The lights page provides buttons to toggle six configurable lights which can be any entity that supports a toggle function including switch, light, media_player, climate, fan, humidifier, cover, script or siren.

# Controls

![controls](https://github.com/user-attachments/assets/e4f0e6c6-2d10-4a20-9c41-bb84cdd7bdc2)
- The icon of this home page button and the page title are configurable.
- The controls page provides buttons to toggle configurable controls which can be any entity that supports a toggle function including switch, light, media_player, climate, fan, humidifier, cover, script or siren. Icons can be configured for on and off states and must exist in the icon glyphs (default is switch icon).
- The second row of controls buttons include an additional substitution to allow more complex implementations where the sensor for the state is a different entity to the one for the switch. If both the action and state entity are the same for a button these operate the same as the other controls. These three controls are configured with icons to show a garage door, dishwasher and a vacuum cleaner.

# Media
**Internal Audio**

- The page title is configurable.
- This is the default media view if external output is disabled but an optional toggle can be displayed to allow accessing the external audio view.
- The volume controls on the media page control the volume of the S3 box including the Voice Assistant.

**External Audio**

![media](https://github.com/user-attachments/assets/693a625a-7cc2-4523-b6a3-f508334f3232)
- This is the default media view if external output is enabled but an optional toggle can be displayed to allow accessing the internal audio view.

# Screens

![screens](https://github.com/user-attachments/assets/3c97f641-b16e-4f99-8a35-0b176ceaa6d8)
- The icon of this home page button and the page title are configurable.
- This page provides buttons to toggle six configurable items which can be any entity that supports turn_on, turn_off functions including switch, light, media_player, climate, fan, humidifier, cover, script or siren. Icons for the On and Off state can be configured for each entity and must exist in the icon glyphs (default is screen on/off icons).

# Security

![p4_security_new](https://github.com/user-attachments/assets/40c24b27-711c-418b-9ea3-0d3e1b4f9c55)
- The page title and code page title are configurable.
- The security page provides buttons to toggle three security items. These will work for locks or any other entity that supports a toggle function including switch, light, media_player, climate, fan, humidifier, cover, script or siren. Icons for the On and Off state can be configured for each entity and must exist in the icon glyphs (default is padlock lock/unlock icons).
- Icons on this page are red for off and green for on to indicate security status.
- Keypad - Pin code is required for alarm deactivation or changing modes, but not activation.
- The device background which defaults to black will change color based on alarm status. The colors are configurable.

# Screensaver

![p4_digital_screensaver](https://github.com/user-attachments/assets/c0119bf4-0970-47eb-8e49-f71bb348fb83)
- The page title is configurable.
- The top centre will show the upcoming alarm clock time if active but can be disabled.
- The top left corner of the screen shows device Temperature and Humidity from sensors defined in substitutions. These additional substitutions will show temperature or temperature and humidity based on the available entities.
- The top right side of the screen shows your specified weather entity temperature and condition and will not be shown if a valid entity is not specified.  Forecast outside temperature and condition can be provided by Open Weather Map or another weather forecast entity in HA.
- The lower left and right corners include can be configured via substitutions to show any sensor value and any unit of measure. For example these could be air quality indicators. These only show if available. 

# Settings

**Voice Settings**


- WakeWord Location can be changed from On Device to Home Assistant
- VA Mode changes the animated voice assistant
- Mute Responses will mute any response
- Show Responses will display the conversation on the voice assistant screens.
- Wake Sound will play a wake sound when voice assistant wakes

**Screensaver Settings**


- Screensaver turns on screensaver after the specified delay
- Settings opens next page to adjust timeouts
- Wake on Presence wakes the device when the radar detects motion
- Turn Screen Off turns off the screen after the specified delay

**Screensaver Timeout Settings**


- Delay Secs is the time until the screensaver starts
- Screen Off Delay is the time until the screen turns off.
- The brightness slider allows setting the screensaver brightness.


**Info**



**Device Settings**


- External Audio outputs audio to the external audio player configured in the substitions section.
- Notify sound triggers a sound when a text notification is sent to the device. This is different to the wake sound.
- Brightness slider controls screen brightness

**UI Settings**

- Time Format provides 12 or 24 HR time shown in all places
- ScreenSaver Clock allows Analog or Digital clock to be shown
- Temperature Unit updates all displayed temperatures to be Celsius or Fahrenheit
- UI Mode provides the ability to choose the theme.

# Wifi


# OTA Updates
- OTA is supported.

# Getting Started

**First Time?**

The easy way to get started is to create an entry in ESPHome for your new device and paste in the contents of the esp32-p4-86-panel.yaml file in this repository. You can edit the device names as required.
See the basics below to ensure you have added the 3 required secrets to your ESPHome before compiling. 
For your new configuration choose Install>Download and compile the code for your device. When this process completes, download the file in modern format for the ESPHome Web Installer.
Connect your new device to your computer and open this site: [https://web.esphome.io/?dashboard_install](https://web.esphome.io/?dashboard_install)
Follow the steps to Connect your device and load the file you downloaded earlier to flash the device. 
Once complete your device should reboot and start. 

Your Home Assistant will recognize the device so you can add it.

When you add the device there is one more option you will need. If you want to use the capabilities of the box to control devices in your Home Assistant you have to give it permission. 
In Devices>EspHome find the device and click the cog next to it.

![devices-esphome](https://github.com/user-attachments/assets/b2b65e1a-f0a4-41d1-aed0-be1a18f3f057)

Then choose to allow the device to perform Home Assistant Actions.

![allowdeviceactions](https://github.com/user-attachments/assets/9cebb38a-4398-4040-bfd4-b1b20f2d2111)

You can keep the name from your initial installation but change the rest with the content from this file and then compile this and install the updated configuration wirelessly. See the basics below to ensure you have the three required secrets configured before you compile.
The configuration provided will work out of the box but you won't have any buttons to control lights or switches and it won't connect to an external speaker for audit. This is where the configuration options in the config come into play. The first 200 lines are all options that can be adjusted to tailor your box for you and push out new wireless updates to test your changes. 

**Configuration**

See [CONFIGURATION.md](https://github.com/chrisdunnname/esphome-p4-86-panel-eth-2ro-lvgl/blob/main/CONFIGURATION.md) for further details on the YAML configuration.

**Additional Information**

See [USAGE.md](https://github.com/chrisdunnname/esphome-p4-86-panel-eth-2ro-lvgl/blob/main/USAGE.md) for further details of the available Home Assistant entities and how they can be used.

**Thank You!**

If you are stuck or unsure or have a suggestion raise an issue or reach out as this configuration is the result of requests from fellow users and benefits from your support and involvement.

<a href="https://www.buymeacoffee.com/chrisdunn" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" style="height: 60px !important;width: 217px !important;" ></a>
