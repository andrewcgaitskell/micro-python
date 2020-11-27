# Overview

1. Find USB Port
2. Erase Flash Memory
3. Download Relevant Micropython
4. Burn to Flash
5. Connect to ESP32 Using Serial
6. Setup WiFi Connection
7. Connect to ESP32 Using WiFi

# Burning Micro Python to ESP32

## List USB Devices connected to Mac

ls /dev/tty*

### Specific to ESP32CAM

/dev/tty.usbserial-A50285BI

## Reference

https://docs.micropython.org/en/latest/esp32/tutorial/intro.html

Normal ESP32 - Serial Port on Mac : /dev/tty.SLAB_USBtoUART

## Install esptool

I have a Virtual Environment, to activate it: 

source /Users/andrewgaitskell/Code/PythonEnvs/env20201104/bin/activate

pip install esptool

## Erase Flash

esptool.py --port /dev/tty.usbserial-A50285BI erase_flash

## Write Flash

https://micropython.org/download/esp32/

cp /Users/andrewgaitskell/Downloads/esp32-idf3-20200902-v1.13.bin /Users/andrewgaitskell/Documents/MicroPython/esp32cam

cd /Users/andrewgaitskell/Documents/MicroPython/esp32cam

esptool.py --chip esp32 --port /dev/tty.usbserial-A50285BI write_flash -z 0x1000 esp32-idf3-20200902-v1.13.bin

__needed to press reset button for it to start__

Output:

Connecting........_____....._____....._____....._____...
Chip is ESP32-D0WDQ6 (revision 1)
Features: WiFi, BT, Dual Core, 240MHz, VRef calibration in efuse, Coding Scheme None
Crystal is 40MHz
MAC: 7c:9e:bd:06:47:d8
Uploading stub...
Running stub...
Stub running...
Configuring flash size...
Compressed 1448768 bytes to 926007...
Wrote 1448768 bytes (926007 compressed) at 0x00001000 in 82.0 seconds (effective 141.3 kbit/s)...
Hash of data verified.

Leaving...
Hard resetting via RTS pin...

# Connect to ESP32 for REPL

screen /dev/tty.usbserial-A50285BI* 115200

# Enable WEBREPL do the following

https://learn.adafruit.com/micropython-basics-esp8266-webrepl/access-webrepl

Connect ESP8266 to WiFi

import network
wlan = network.WLAN(network.STA_IF)
wlan.active(True)
wlan.connect('ssid', 'password')

Used when accessing via WEBREPL

ws://192.168.4.1:8266/

Found the following IP from my Router

ws://192.168.1.36:8266/
