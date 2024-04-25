# ACL_Client_ESP32-IDF

This is a stand-alone ESP-IDF program for an ESP32 based board. The purpose is to implement an RFID reading controller to limit access to Fort Collins Creator Hub equipment such laser cutters and machine tools. It uses the second microcontroller UART for communication with a Seeed Studio Grove RFID reader. This sketch will wait for an RFID to be sent by the reader and then validate it with the Creator Hub's ACL server API via WiFi. It assumes four outputs in addition to the Serial and Serial1 ports:
* "Connection" LED - indicates a valid WiFi connection when lit. It flashes when an HTTP error is detected.
* "Access" LED - indicates thati an RFID with the correct acccess rights for the equipment has been detected. It flashes when an RFID without correct permission has been detected.
* Relay output - connected to a transistor that controls a relay connected to the equipment - typically a low voltage signal.
* Reader output - connected to a transistor that controls the power to the RFID reader. This is needed for equipment that needs a "level triggered" control (as opposed to a door controller where "edge triggered" suffices). Most readers will not reliably keep sending data when an RFID is left in front of the reader. To get around this, when a valid RFID is detected (not necessarily with the correct permissions), the reader is powered down and then brought back up to force it to re-detect the card.

# Development

See the [developer guide](docs/README-dev.md) for information re: how to build the software.
