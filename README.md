# TinyGRBLSender
This is a hardware design for a low cost device that will send a GCode file to an EleksMaker
laser engraver running GRBL firmware.

Normally, such laser engravers are driven from a computer connected via a USB cable, but for
production use, it is nice to have a self-contained setup where you can just turn on the
machine and push a button.  Previously, I implemented such a setup using a Raspberry Pi running
Linux as the controlling computer.  That worked, but Pis can take the better part of a minute
to boot, and sometimes longer if the file system needs to checked.  There were cases where you
had to retry several times before it would boot successfully.  Furthermore, the cabling was
cumbersome, as you needed a separate power supply for the Pi.  Finally, while Pis are ostensibly
inexpensive, the cost starts to add up by the time you add the case, power supply, LCD display
(so you don't need a monitor), and SD card.

This device solves all those problems.  The hardware cost is about $6 without the optional
OLED display and $12 with it.  It is powered directly from the same supply that powers the
laser engraver.  It is so small that it can be mounted directly to the side of the laser
controller.  It boots in 2 seconds - the same time that it takes for the laser controller
itself to become ready.  The user interface is a pushbutton and a multicolor LED.  Press the
pushbutton to start sending the GCode file that is stored in the on-board FLASH.
The LED color tells you the status (BOOTING / READY / RUNNING / ERROR). 

The device is built around a $4 "WeMOS D1 Mini" ESP8266 module that contains a CPU and a WiFi
interface.  (In this incarnation, the WiFi in not used, although it would be easy enough to
extend the software for WiFi control.)  That module is stacked atop a D1 Mini Prototyping
Shield that has the pushbutton, status LED, and a header connector that attaches to the laser
controller.  Optionally, a WeMOS D1 Mini OLED Shield may be added to the stack, displaying
more detailed status in text form - but the LED color status is fine for most uses.

The software is written in the Forth language, using my cforth implementation
https://github.com/MitchBradley/cforth , and included in that repo.
