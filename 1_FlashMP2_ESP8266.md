# Plug in ESP8266

# Find out which Serial Port it is connected to

To list all connected USB devices on a Mac

ls /dev/tty*

I was using a 4 port hub and did not realise they gave different numbers to the same device

/dev/tty.usbserial-14110

/dev/tty.usbserial-14130

# Erase Flash

create Python Virtual Environment

Activate it

    source /Users/andrewgaitskell/Code/PythonEnvs/env20201104/bin/activate

    pip install esptool

    esptool.py --port /dev/tty.usbserial-14130 erase_flash


# Flash Memory

Download relevant Firmware

    cp /Users/andrewgaitskell/Downloads/esp8266-20200911-v1.13.bin /Users/andrewgaitskell/Documents/MicroPython/esp8266    
    
    cd /Users/andrewgaitskell/Documents/MicroPython/esp8266

Flash to device

    esptool.py --chip esp8266 write_flash -z 0x1000 esp8266-20200911-v1.13.bin

## Connect to REPL Prompt on Mac

screen /dev/tty.usbserial-14110 115200

## To make available via WiFi

at REPL prompt - type:

    import webrepl_setup

enable and set password

## connect to esp8266 using WebRepl Client

WebRepl Client - Download and extract following:

https://github.com/micropython/webrepl/archive/master.zip

upload the following as a boot.py file

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

Reboot device.

# Install Jupyter into Virtualenv 

Follow link to next stage:

https://github.com/andrewcgaitskell/micro-python/blob/main/2_CreateEnv%2BInstallKernel.md

source /Users/andrewgaitskell/Code/PythonEnvs/env20201104/bin/activate

# Important to Keep Track of IP Addresses

192.168.1.37

ws://192.168.4.1:8266/

ws://192.168.1.37:8266/


