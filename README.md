# epd-driver

The E-Paper display driver written in C from Embedded Artists is modified to be used with ARMv7 SOM from Toradex(R)

## Requirement on the Colibri VF 50 board

The following changes were required to be made for the E-Paper display interface.

5 GPIO were required for the interface. The SPI was already in the default dtb configuration. Since the resources needed the modifications, a patch is created for additional reference. For this implementation UART1 and UART2 is scavanged. While the CAN1 is introduced for need of application not dependent on E-Paper Display.

## Project management

The project is editied using visual studio code with following plugins:
    - C/C++ extension from Microsoft.
    - CMake language support plugin from twxs
    - CMake language support plugin from vector-of-bool

The compiler tools are
    - ARM compiler toolchain for Toradex boards as described in the page.

## Targets

There are 3 project targets:

### epd-fuse

This generates the fuse library enabled part that will be later used as a /dev/epd device using FUSE as discussed in the original Embedded Artists repository.

The board had to be updated with the necessary fuse library using "opkg install fuse".

### epd_test

The test program that is already part of Embedded Artists code and toggles the varioud images from the "image" folder after 5 seconds. The /dev/epd need not be installed for this to work.

### epd_app

The application program which is specific. The intention is to update the connected interface and it's ethernet IP on the display every minute using cron. Thus whenever the device is connected to network, the IP always is available to ssh in the device.