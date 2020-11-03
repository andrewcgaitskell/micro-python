https://docs.micropython.org/en/latest/esp32/tutorial/intro.html


/dev/tty.SLAB_USBtoUART


esptool.py --port /dev/ttyUSB0 erase_flash

esptool.py --port /dev/tty.SLAB_USBtoUART erase_flash

pip show -f esptool


/Users/andrewgaitskell/Library/Python/2.7/lib/python/site-packages/esptool.py --port /dev/tty.SLAB_USBtoUART erase_flash

following worked :

python /Users/andrewgaitskell/Library/Python/2.7/lib/python/site-packages/esptool.py --port /dev/tty.SLAB_USBtoUART erase_flash


esptool.py --chip esp32 --port /dev/ttyUSB0 write_flash -z 0x1000 esp32-20180511-v1.9.4.bin


python /Users/andrewgaitskell/Library/Python/2.7/lib/python/site-packages/esptool.py --chip esp32 -port /dev/tty.SLAB_USBtoUART write_flash -z 0x1000 esp32-20180511-v1.9.4.bin

