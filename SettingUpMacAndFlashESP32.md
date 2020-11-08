# Burning Micro Python to ESP32

https://docs.micropython.org/en/latest/esp32/tutorial/intro.html

Serial Port on Mac : /dev/tty.SLAB_USBtoUART

Following is what was was suggested, but did not work on my mac

esptool.py --port /dev/ttyUSB0 erase_flash

esptool.py --port /dev/tty.SLAB_USBtoUART erase_flash

To find where esptool was installed, use following command: 

pip show -f esptool


following worked :

python /Users/andrewgaitskell/Library/Python/2.7/lib/python/site-packages/esptool.py --port /dev/tty.SLAB_USBtoUART erase_flash

## Started with ESP32

Recommended :

esptool.py --chip esp32 --port /dev/ttyUSB0 write_flash -z 0x1000 esp32-20180511-v1.9.4.bin

Actual :

python /Users/andrewgaitskell/Library/Python/2.7/lib/python/site-packages/esptool.py --chip esp32 -port /dev/tty.SLAB_USBtoUART write_flash -z 0x1000 esp32-20180511-v1.9.4.bin

# Download and Flash to ESP32

https://micropython.org/download/esp32/

python /Users/andrewgaitskell/Library/Python/2.7/lib/python/site-packages/esptool.py --chip esp32 write_flash -z 0x1000 esp32-idf4-20200902-v1.13.bin                          
Output:

esptool.py v2.8
Found 3 serial ports
Serial port /dev/cu.usbserial-0001
/dev/cu.usbserial-0001 failed to connect: [Errno 16] could not open port /dev/cu.usbserial-0001: [Errno 16] Resource busy: '/dev/cu.usbserial-0001'
Serial port /dev/cu.SLAB_USBtoUART
Connecting........__
Chip is ESP32D0WDQ6 (revision 1)
Features: WiFi, BT, Dual Core, 240MHz, VRef calibration in efuse, Coding Scheme None
Crystal is 40MHz
MAC: b4:e6:2d:b3:ec:f1
Uploading stub...
Running stub...
Stub running...
Configuring flash size...
Auto-detected Flash size: 4MB
Compressed 1456544 bytes to 928552...
Wrote 1456544 bytes (928552 compressed) at 0x00001000 in 82.2 seconds (effective 141.8 kbit/s)...
Hash of data verified.

Leaving...
Hard resetting via RTS pin...
andrewgaitskell@Andrews-MacBook-Air MicroPython 


https://docs.micropython.org/en/latest/esp8266/tutorial/index.html#esp8266-tutorial

picocom /dev/cu.SLAB_USBtoUART -b115200

screen /dev/cu.SLAB_USBtoUART* 115200

https://learn.adafruit.com/micropython-basics-esp8266-webrepl/access-webrepl

import network
wlan = network.WLAN(network.STA_IF)
wlan.active(True)
wlan.connect('ssid', 'password')

ws://192.168.4.1:8266/

ws://192.168.1.36:8266/