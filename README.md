# Digital Meter script for the P1 port
Script to parse P1 output of a (Dutch) electricity meter.

Prerequisites:
==============
Hardware:
- Digital Meter (Sagecom S211: Single phase, Sagecom T211-D : Three-phase and Flonidan - G4SRTV: Natural gas (as slave of the first two)
- Cable to connect to the meter (RJ11/RJ12). I used this one: https://webshop.cedel.nl/Slimme-meter-kabel-P1-naar-USB .

Software
Most universal is to use requirements.txt:
```
pip install -r requirements.txt;
```

If, like me, you want to attach the USB cable to your Synology diskstation (which I happen to keep in the meter cupboard) running DSM6, you'll probably find it doesn't work out-of-the-box. For some reason (probably some udev rules somewhere) the kernel doesn't load the correct modules when the USB-device is inserted. You can fix this manually when logged into your DiskStation over SSH:

```
$ ssh diskstation
user@diskstation$ sudo insmod /lib/modules/usbserial.ko
user@diskstation$ sudo insmod /lib/modules/ftdi_sio.ko

```
Also, you probably don't have pip on your DiskStation. I installed it with some commands as listed here: https://stackoverflow.com/a/51794225. No need to download and run any get-pip.py scripts. I recall commands like these:

```
user@diskstation$ python3 -m venv env
user@diskstation$ python3 -m ensurepip 
```

Adjustments/configuration:
==========================
At the beginning of the script, you can change the following:
- Serial port:
```
serialport = '/dev/ttyUSB0'
```
- Enable debug:
```
debug = False
```
- Add/update OBIS codes:
```
obiscodes = {}
```

More information
================
I based this on a script from Jensd, who created a blogpost where he elaborates about P1 port and data format to parse
This can be found here: https://jensd.be/1183/linux/read-data-from-the-belgian-digital-meter-through-the-p1-port
