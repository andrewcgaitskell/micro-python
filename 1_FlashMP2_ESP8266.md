Plug in ESP8266

# Find out which Serial Port it is connected to

To list all connected USB devices on a Mac

ls /dev/tty*

I was using a 4 port hub and did not realise they gave different numbers to the same device

/dev/tty.usbserial-14110
/dev/tty.usbserial-14130

# Erase Flash

python /Users/andrewgaitskell/Library/Python/2.7/lib/python/site-packages/esptool.py --port /dev/tty.usbserial-14130 erase_flash

cd /Users/andrewgaitskell/code/MicroPython

# Flash Memory

==== Ignore from here

python /Users/andrewgaitskell/Library/Python/2.7/lib/python/site-packages/esptool.py --baud 460800 write_flash --flash_size=detect 0 /Users/andrewgaitskell/Documents/MicroPython/esp8266/esp8266-20200911-v1.13.bin

port was not required:

python /Users/andrewgaitskell/Library/Python/2.7/lib/python/site-packages/esptool.py --port /dev/tty.usbserial-14130 --baud 460800 write_flash --flash_size=detect 0 esp8266-20200911-v1.13.bin

======== to here

Run this to Flash

Auto detects port

python /Users/andrewgaitskell/Library/Python/2.7/lib/python/site-packages/esptool.py --chip esp8266 write_flash -z 0x1000 esp8266-20200911-v1.13.bin

python /Users/andrewgaitskell/Library/Python/2.7/lib/python/site-packages/esptool.py --chip esp8266 write_flash -z 0x1000 esp8266-20200911-v1.13.bin 
esptool.py v2.8
Found 2 serial ports
Serial port /dev/cu.usbserial-14110
Connecting....
Chip is ESP8266EX
Features: WiFi
Crystal is 26MHz
MAC: 98:f4:ab:da:a3:63
Uploading stub...
Running stub...
Stub running...
Configuring flash size...
Auto-detected Flash size: 4MB
Compressed 638928 bytes to 419659...
Wrote 638928 bytes (419659 compressed) at 0x00001000 in 40.7 seconds (effective 125.7 kbit/s)...
Hash of data verified.

Leaving...
Hard resetting via RTS pin...

## Connect to REPL Prompt on Mac

screen /dev/tty.usbserial-14110 115200

## To make available via WiFi

import webrepl_setup

# Installed Jupyter into Virtualenv 

https://github.com/andrewcgaitskell/micro-python/blob/main/2_CreateEnv%2BInstallKernel.md

source /Users/andrewgaitskell/Code/PythonEnvs/env20201104/bin/activate

# Keep Track of IP Addresses

192.168.1.37

ws://192.168.4.1:8266/

ws://192.168.1.37:8266/


