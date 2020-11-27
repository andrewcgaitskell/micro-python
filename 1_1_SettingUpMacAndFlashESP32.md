# Overview

1. Find USB Port
2. Erase Flash Memory
3. Download Relevant Micro Python Firmware
4. Burn to Flash
5. Connect to ESP32 Repl Using Serial
6. Setup and Enable WebRepl
6. Setup WiFi Connection
7. Connect to ESP32 using WebRepl

# Burning Micro Python to ESP32

## List USB Devices connected to Mac

ls /dev/tty*

### Specific to ESP32CAM

/dev/tty.usbserial-A50285BI

## Reference

https://docs.micropython.org/en/latest/esp32/tutorial/intro.html

Normal ESP32 - Serial Port on Mac : /dev/tty.SLAB_USBtoUART

## Install esptool

See first step if you do not have a Virtual Environment.

I have an existing Virtual Environment, to activate it: 

source /Users/andrewgaitskell/Code/PythonEnvs/env20201104/bin/activate

Install esptool

    pip install esptool

## Erase Flash

ESP32 needs to be empty

    esptool.py --port /dev/tty.usbserial-A50285BI erase_flash

## Write Flash

Download firmware from:

https://micropython.org/download/esp32/

Copy to working directory:

    cp /Users/andrewgaitskell/Downloads/esp32-idf3-20200902-v1.13.bin /Users/andrewgaitskell/Documents/MicroPython/esp32cam

Change to working directory:

    cd /Users/andrewgaitskell/Documents/MicroPython/esp32cam

Flash Firmware:

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

# ESP32Cam needs to be in write mode during Flash only

Needed to remove jumper from pins

Press reset

# Connect to ESP32 for REPL

screen /dev/tty.usbserial-A50285BI 115200

# Enable WEBREPL

## Reference:

https://learn.adafruit.com/micropython-basics-esp8266-webrepl/access-webrepl

## Do following:

at >>> paste

    import webrepl_setup

agree to enable, set password, reboot 

upload a boot.py which included enabling webrepl and conection to Wifi

Example boot file:

    # This file is executed on every boot (including wake-boot from deepsleep)
    #import esp
    #esp.osdebug(None)
    import uos, machine
    #uos.dupterm(None, 1) # disable REPL on UART(0)
    import gc
    import webrepl
    webrepl.start()
    gc.collect()


    def do_connect():
        import network
        wlan = network.WLAN(network.STA_IF)
        wlan.active(True)
        if not wlan.isconnected():
            print('connecting to network...')
            wlan.connect('ssid', 'password')
            while not wlan.isconnected():
                pass
        print('network config:', wlan.ifconfig())
    do_connect()


Found the following IP from my Router

192.168.1.43

Address for WebRepl as follows:

ws://192.168.1.43:8266/


Open up WebRepl webpage and enter the IP address of the ESPCam

Enter password

Should be offered Micro Python prompt:

        >>>
        
        
        
