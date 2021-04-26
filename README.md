# FOKOOS Odin 5 F3 Folding 3D Printer

Some free information about and resources for the [FOKOOS Odin 5 F3](https://amzn.to/3vjz3ue) Folding 3D printer. This repository is not sponsored by or affiliated with FOKOOS in any way.

## Parts List

### Motherboard

* The printer is controlled by a standard open source board, the [Robin Nano v1.2](https://github.com/makerbase-mks/MKS-Robin-Nano-V1.X) made by [Makerbase](https://makerbase.com.cn/en/products/).
* There is a slot for a WiFi card, but no WiFi card is shipped with the printer. It can be purchased for ~$8 from [AliExpress](https://www.aliexpress.com/item/32816882694.html). Instructions can be found [here](https://github.com/makerbase-mks/MKS-Robin-Nano-V2.X/wiki/Use-MKS_Robin_WIFI-on-Robin-Nano). Unfortunately the WiFi on these boards is apparently too slow to be usable for printing. An alternative is to run [OctoPrint](https://octoprint.org/) on a [Raspberry Pi](https://raspberrypi.org).

### Power Supply

* The printer uses a [CL-C240W-24V](https://www.3dprinterstore.online/products/cl-c240w-24v-switching-power-supply-sapphire-pro-printer-adapter-led-strip-light-transformer-12v-for-3d-printer-part) PSU. This is a fanless 240W, 24V supply.

### Hardware

* 5x 42BYGH604-A-24D stepper motors: one for the X-axis, one for the Y-axis, two for the Z-axis, and one for the extruder.
* GL-8H proximity sensor for the Z-axis.
* Delrin V-wheels.
* 0.4mm nozzle (spares included).

### Fans

* Three FD4010S4H-AP00 40x10mm axial fans from [fzytv.com](http://www.fzytv.com/). These are rated for and are running at 24V. There are two in the base and one on the cold end of the extruder.
* One FD4010S4U-BP00 40x10mm blower fan for the part cooler, from the same company, also rated at 24V. This is the loudest of the fans.

## Software

The software on the supplied microSD card includes FOKOOS Slicer for Windows, and Mac and Windows drivers for the CH340G USB to Serial chip. No source code is provided on the microSD card, and as of 2021-04-24, [the FOKOOS website](https://www.fokoos.com/) does not yet offer any downloads.

### Fokoos Slicer

The slicer provided on the SD card is a reskin of the open source [Ultimaker Cura](https://ultimaker.com/software/ultimaker-cura). The version number has been replaced with v1.0.1 so it isn't immediately obvious which version of Cura they based it on. However, the changes they made are very minimal, essentially just changing the icon and adding definition files for their printers and extruders, so it is very easy to use the original Cura and simply add the definition files.

To do this on Windows, copy the following files from the FOKOOS Slicer installation into your Cura installation directory. For convenience you can download the files directly from this repository. Once you have done this, the printer will be listed under the FOKOOS brand in Cura's printer list when adding a non-networked printer.

* `odin_5_f3.def.json` -> `C:\Program Files\Ultimaker Cura <VERSION>\resources\definitions`
* `odin_5_f4.def.json` -> `C:\Program Files\Ultimaker Cura <VERSION>\resources\definitions`
* `odin_5_f3_extruder_0.def.json` -> `C:\Program Files\Ultimaker Cura <VERSION>\resources\extruders`
* `odin_5_f4_extruder_0.def.json` -> `C:\Program Files\Ultimaker Cura <VERSION>\resources\extruders`

### Firmware

The printer's firmware is closely based on the [Robin Nano](https://github.com/makerbase-mks/MKS-Robin-Nano-Firmware) firmware, possibly with no changes and has an identical interface. This is a Marlin-based firmware. FOKOOS has not yet provided the source to the firmware. The firmware can be upgraded, but using the Robin Nano firmware requires editing the headers to configure the firmware for the printer - instructions can be found [here](https://github.com/martinbogo/Marlin-2.0-for-Odin-5-F3).

## 3rd Party Compatibility

### BLtouch

FOKOOS claims on the Amazon page that the slicer is BLtouch compatible. There is an open connector for the BLtouch on the motherboard, and BLtouch support seems to be enabled in the firmware.

### OctoPrint

[OctoPrint](https://octoprint.org/) works very well with this board when connected by USB. I'm currently using a Raspberry Pi 3B+ to control the printer and everything works perfectly, except for a slight (10%) increase in print times, which is normal when using OctoPrint to control the printer via the relatively slow serial connection (over USB).

There is just enough space in the base to squeeze in the Raspberry Pi. The Pi could be powered using a 24V to 5V DC to DC buck regulator (~$5) attached to the spare terminals on the PSU. It might even be possible to share the motherboard's 5V regulator, which is rated for 1A, but using a separate regulator would be safer. It should be possible to directly connect the Raspberry Pi's serial port to the Robin Nano, perhaps by using the WiFi module's serial port, but this would likely require recompiling the Nano's firmware.
