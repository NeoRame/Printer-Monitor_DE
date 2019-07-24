/* The MIT License (MIT)

Copyright (c) 2019 NeoRame (originally 2018 David Payne)

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NON-INFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
*/

# Printer Monitor DE (OctoPrint 3D Drucker Monitor)

## Features:
* Displays the print status from OctoPrint Server
* Estimated time remaining
* Time Printing
* Percentage complete
* Progress bar
* Bed and Tool Temperature
* Screen turns off when printer is turned off or disconnected
* Screen turns on when printer is Operational or connected
* Option to display a clock screen instead of sleep mode
* Option to display a clock screen and Weather as "Screensaver" when Printer is Operational
* Option to display 24 hour clock or AM/PM style
* Option to display Current Weather when printer is off
* Sample rate is every 60 seconds when not printing
* Sample rate is every 10 seconds when printing
* Fully configurable from the web interface (not required to update Settings.h)
* Supports OTA (loading firmware over WiFi connection on same LAN)
* Basic Authentication to protect your settings
* Version 2.2 added the ability to update firmware through web interface from a compiled binary
* Can query the Octoprint [PSU Control plugin](https://plugins.octoprint.org/plugins/psucontrol/) to enter clock or blank mode when PSU is off
* Video: https://youtu.be/niRv9SCgAPk
* Detailed build video by Chris Riley: https://youtu.be/Rm-l1FSuJpI

## Required Parts:
* Wemos D1 Mini: https://amzn.to/2JWdKZA
* 0.96" OLED I2C 128x64 Display (12864) SSD1306:  https://amzn.to/2Lxr2PF
* (optional) 1.3" I2C OLED Display: https://amzn.to/2LAh2ow (must uncomment #define DISPLAY_SH1106 in the Settings.h to use the 1.3" SSH1106 display)  

Note: Using the links provided here help to support these types of projects. Thank you for the support.  

## Wiring for the Wemos D1 Mini to the I2C SSD1306 OLED
SDA -> D2  
SCL -> D5  
VCC -> 5V+  
GND -> GND-  

![Printer Monitor Wire Diagram](/images/printer_monitor_wiring.jpg)  

## 3D Printed Case by NeoRame:  
https://www.thingiverse.com/thing:3755795 -- for the 0.96" OLED Display
## 3D Printed Case by Qrome:  
https://www.thingiverse.com/thing:2884823 -- for the 0.96" OLED Display  
https://www.thingiverse.com/thing:2934049 -- for the 1.3" OLED Display

## Upgrading from version 2.2 or Higher
Version 2.2 introduced the ability to upgrade pre-compiled firmware from a binary file.  In version 2.3 and on you should find binary files that can be uploaded to your printer monitor via the web interface.  From the main menu in the web interface select "Firmware Update" and follow the prompts.
* **printermonitor.ino.d1_mini_SSD1306.bin** - compiled for Wemos D1 Mini for the smaller 0.96" SSD1306 OLED (default)
* **printermonitor.ino.d1_mini_SH1106.bin** - compiled for Wemos D1 Mini for the larger 1.3" SH1106 OLED

## Compiling and Loading to Wemos D1 Mini
It is recommended to use Arduino IDE.  You will need to configure Arduino IDE to work with the Wemos board and USB port and installed the required USB drivers etc.  
* USB CH340G drivers:  https://wiki.wemos.cc/downloads
* Enter http://arduino.esp8266.com/stable/package_esp8266com_index.json into Additional Board Manager URLs field. You can add multiple URLs, separating them with commas.  This will add support for the Wemos D1 Mini to Arduino IDE.
* Open Boards Manager from Tools > Board menu and install esp8266 platform (and don't forget to select your ESP8266 board from Tools > Board menu after installation).
* Select Board:  "WeMos D1 R2 & mini"
* Set 1M SPIFFS -- this project uses SPIFFS for saving and reading configuration settings.

## Loading Supporting Library Files in Arduino
Use the Arduino guide for details on how to installing and manage libraries https://www.arduino.cc/en/Guide/Libraries  
**Packages** -- the following packages and libraries are used (download and install):  
ESP8266WiFi.h  
ESP8266WebServer.h  
WiFiManager.h --> https://github.com/tzapu/WiFiManager  
ESP8266mDNS.h  
ArduinoOTA.h  --> Arduino OTA Library  
"SSD1306Wire.h" --> https://github.com/ThingPulse/esp8266-oled-ssd1306  
"OLEDDisplayUi.h"  

Note Printer-Monitor version 2.5 and later include ArduinoJson (version 5.13.1).   

## Initial Configuration
All settings may be managed from the Web Interface, however, you may update the **Settings.h** file manually -- but it is not required.  There is also an option to display current weather when the print is off-line.  
* Your OctoPrint API Key from your OctoPrint -> User Settings -> Current API Key  
* Optional OpenWeatherMap API Key -- if you want current weather when not printing.  Get the api key from: https://openweathermap.org/  

NOTE: The settings in the Settings.h are the default settings for the first loading. After loading you will manage changes to the settings via the Web Interface. If you want to change settings again in the settings.h, you will need to erase the file system on the Wemos or use the “Reset Settings” option in the Web Interface.  

## Web Interface
The Printer Monitor uses the **WiFiManager** so when it can't find the last network it was connected to
it will become a **AP Hotspot** -- connect to it with your phone and you can then enter your WiFi connection information.

After connected to your WiFi network it will display the IP addressed assigned to it and that can be
used to open a browser to the Web Interface.  **Everything** can be configured there.

<p align="center">
  <img src="/images/shot_01.jpg" width="200"/>
  <img src="/images/shot_02.png" width="200"/>
  <img src="/images/shot_03.jpg" width="200"/>
  <img src="/images/shot_04.jpg" width="200"/>
</p>

## Donate or Tip
Please do not feel obligated, but donations and tips are warmly welcomed.  I have added the donation button at the request of a few people that wanted to contribute and show appreciation.  Thank you, and enjoy the application and project.  

[![paypal](https://www.paypalobjects.com/de_DE/DE/i/btn/btn_donate_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=VCAKUYHVUGRBG)

Or -- you can buy me something from my Amazon Wishlist: https://www.amazon.de/gp/registry/wishlist/L9U2EBYU761T/ref=cm_wl_huc_view  

## Contributors
NeoRame -- This Fork and German Translation
David Payne -- Principal developer and architect  
Daniel Eichhorn -- Author of the TimeClient class and OLEDDisplayUi  
Florian Schütte -- added flip display to web interface  
Owen Carter -- Added psu control setting (v2.4)

Contributing to this software is warmly welcomed. You can do this basically by
forking from master, committing modifications and then making a pulling requests to be reviewed (follow the links above
for operating guide).  Detailed comments are encouraged.  Adding change log and your contact into file header is encouraged.
Thanks for your contribution.

![Screensaver](/images/video_print_monitor.jpg)
![Printer Monitor Temps](/images/temperatures.jpg)  
![Printer Monitor Time Remaining](/images/time_remaining.jpg)  
![Printer Monitor Printing Time](/images/printing_time.jpg)
