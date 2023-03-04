# RemoteESP32-Board
Stand alone 12V ESP32 module with SD card and RS485 and CAN bus interfaces

# Usage
This board is intended to be used with this firmware: https://github.com/Pete9008/esp32-web-interface/tree/Remote485 which currently supports use of the RS485 interface in either half or full duplex mode.

The BOM reflects the build for full duplex (4-wire RS485).  To use this the following line in the firmware needs to be commented out:
line88 - //#define RS485_HALF_DUPLEX 1

To use in half duplex mode (2-wire RS485) resistors R23 and R24 must have zero ohm links fitted (Note - This mode is not compatible with the standard OpenInverter firmware.

The firmware does not currently support CAN bus operation.  The CAN interface is currently untested.

# Powering
The board needs a 12V power supply connected on header J4.

0V connects to Pin-2
12V connects to Pin-1 (WiFi only mode)
12V connects to Pin-3 (SD card logging mode)

If power is supplied on Pin-1 then SD card logging is disabled (SD card files can still be read over the web interface though).

If power is supplied on Pin-3 then SD card logging will start (but only while there is no connection on the WiFi).

Note - Not all OpenInverter firmware versions support logging.

# SD Card Interface
The SD card uses the SDIO interface to allow high speed logging.  This requires a pull up on the D2 line (GPIO12) which prevents ESP32-WROOM-32E modules from booting from internal flash.

If the SD card is not used do not populate R9 (D2 pullup).

If the SD card is required then the module must have the flash voltage selection eFuses burned BEFORE resistor R9 is fitted.  See https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-reference/peripherals/sd_pullup_requirements.html for details of the fuse burning process.

# Programming Interface
Header J3 provides a programming interface for the board.  An external USB to 3V3 TTL 232 converter dongle is required to connect to this header.  To place the ESP32 into programming mode pins 1 and 2 of the header must be linked.  Pin-6 on the header can then either be grounded manually to reset the ESP32 and enter programming mode or can connected to RTS on the dongle (a reset will then be generated automatically by the esptool programming software).  The Tx line on the dongle connects to header Pin-4 and the Rx line to header Pin-5.  Header Pin-1 should connect to dongle 0V/GND.

Power during programming must be supplied by connecting 12V on the power header J4.

# Enclosure
Two versions of a 3D printable enclosure are included:
RemoteESP32_Enclosure_NoBat.FCStd - Slim enclosure but without enough space for the RTC backup battery.
RemoteESP32_Enclosure_Bat.FCStd - Larger enclosure with space for the RTC battery.

Both are in FreeCAD format.  .stl files for the enclosure base and lid are also included.






