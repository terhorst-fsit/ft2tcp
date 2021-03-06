#FTDI EEPROM configuration

The EEPROM configuration is mandatory for using the FT245 synchronous fifo.

cha_type=FIFO is the line which causes the ft232h starts as usb<->fifo converter. Don't forget it!

You probably should check the version of the main.c of the ftdi_eeprom program to see if the option is present otherwise check for another version of this program (or
as Stallman said, you can modify it and then share it....).

#Installation

## Windows
FTDI provides [ft_prog](http://www.ftdichip.com/Support/Utilities.htm).

## Linux
*Warning*: The version provided by Ubuntu 16.04 LTS (0.17) is too old and can't be used to set the channel mode to fifo.

install libftdi1.2-dev
	- download package, untar the archive
	- go into, mkdir build
	- go into build folder
	- cmake ..
	- make
	- make install

## EEPROM programming
* Get the sample configuration [file](./ft232h.conf).
* Use ftdi_eeprom program and to configure the eeprom type:
```ftdi_eeprom --flash-eeprom ft232h.conf```

expected output:

```
FTDI eeprom generator v0.17
(c) Intra2net AG and the libftdi developers <opensource@intra2net.com>
FTDI read eeprom: 0
EEPROM size: 256
FIXME: Build FT232H specific EEPROM settings
Used eeprom space: 220 bytes
FTDI write eeprom: 0
Writing to file: eeprom.new
FTDI close: 0
```

It will also dump a ```eeprom.new```.

Then you can start to use a program which opens the ft232h as a USB<->FIFO converter, using ```setBitMode(..... BITMODE_SYNC_FIFO);```. You can find all the options in the definition
of the ```ftdi.h``` file.