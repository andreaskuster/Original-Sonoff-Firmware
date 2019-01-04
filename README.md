# Original-Sonoff-Firmware
Backup of original Sonoff Firmware. 

![Sonoff Basic](https://sonoff.itead.cc/images/basicw.jpg)


## Hardware Requirements:
- Sonoff
- FTDI USB To TTL 3.3V & 5.5V Serial Adapter + Cable
- Female/Female Jumper Wires
- Personal Computer / Laptop
## Software Requirements:
- Python 2.x or 3.x: https://www.python.org/
- Esptool: https://github.com/espressif/esptool

## Step-by-Step Procedure:

1. Extract the contents of esptool compressed file to C:\. All the contents of esptool should be under  c:\esptool.
2. Open Command Prompt (Start > Run > cmd) and navigate to esptool folder.

`cd c:/esptool`

3. Install the esptool by issuing the command below. It takes few seconds to install aplication.

`python setup.py install` 

4. Connect FTDI to Sonoff Smart Switch and start Sonoff device in programming mode. 
![GPIO](https://recretronica.files.wordpress.com/2018/04/sonoff_pinout.jpg)
5. Now find the port under Control Panel > System > Device Manager > Ports at which Sonoff device is connected.

## Backup / Download Official Firmware:

`esptool.py --port COM5 read_flash 0x00000 0x100000 image1M.bin`

- Change COM5 to your own Port.
- Wait a minute and firmware binary file will be downloaded and saved in to c:\esptool
It takes few seconds to download firmware .

## Erase Flash Memory:
Erase the custom firmware from flash memory before uploading any new firmware.

`esptool.py --port COM5 erase_flash`
- Change COM5 to your own Port.
- It takes few seconds to erase firmware.

## Upload Official / Third Party Firmware:
Copy the official / any third party firmware binary file to  c:\esptool folder if it is not already there and upload it by issuing the command below.

`esptool.py --port COM5 write_flash -fs 1MB -fm dout 0x0 sonoff.bin`
- Change COM5 to your own Port.
- Change sonoff.bin to the name of your firmware file inside  c:\esptool folder.
It takes few seconds to upload firmware .

## Troubleshooting:
- Choosing Wrong COM Port will cause the following error.
~~~
c:\esptool>esptool.py --port COM5 write_flash -fs 1MB -fm dout 0x0 image1M.bin
esptool.py v2.3.1
Traceback (most recent call last):
File "C:\esptool\esptool.py", line 2637, in <module>
_main()
File "C:\esptool\esptool.py", line 2630, in _main
main()
File "C:\esptool\esptool.py", line 2349, in main
esp = ESPLoader.detect_chip(args.port, initial_baud, args.before, args.trace)
File "C:\esptool\esptool.py", line 222, in detect_chip
detect_port = ESPLoader(port, baud, trace_enabled=trace_enabled)
File "C:\esptool\esptool.py", line 193, in __init__
self._port = serial.serial_for_url(port)
File "build\bdist.win-amd64\egg\serial\__init__.py", line 88, in serial_for_url
File "build\bdist.win-amd64\egg\serial\serialwin32.py", line 62, in open
serial.serialutil.SerialException: could not open port 'COM5': WindowsError(2, 'The system cannot find the file specified.')
~~~

- If following output is shown, Sonoff is not correctly connected to FTDI, Check wire configuration or terminals.
~~~
c:\esptool>esptool.py --port COM3 write_flash -fs 1MB -fm dout 0x0 image1M.bin
esptool.py v2.3.1
Connecting........_____....._____....._____....._____....._____....._____....._____....._____....._____....._____
A fatal error occurred: Failed to connect to Espressif device: Timed out waiting for packet header
~~~


Source: https://hobbytronics.pk/sonoff-original-firmware-backup-restore/
