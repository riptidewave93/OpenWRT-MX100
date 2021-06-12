# OpenWRT-MX100
Bringup for the Cisco Meraki MX100 on OpenWRT.

Building
-----
#### Build Only
`./build.sh`

#### Modify Configs and Build
`./build.sh modify`

Note that you will need to run a modify on the first compile to select the x86 target, x86_64 subtarget in the menuconfig.

UART Pinout
-----
Look for a 4 pin header named CONN11 in the middle of the PCB. Pin 1 is the marked pin on the PCB closest to the CPU.

Pin 1 = VCC
Pin 2 = TX
Pin 3 = RX
Pin 4 = GND

Booting
-----
 * Flash/burn one of the images from this repo to a flash drive.
 * Take the top off the MX100, and unplug the SATA cable from the HDD.
 * Hook up UART to the MX100, plug in the USB drive, and then power up the device.
 * At the BIOS prompt, quickly press F7 and then scroll to the Save & Exit tab.
 * Scroll down to Boot Override, and select the UEFI entry for your jumpdrive.

**Note:** UEFI booting will fail if the SATA cable for the HDD is plugged in. The issue is explained under the Flashing section of this document.

Flashing
-----
 * Take the top off the MX100, and unplug the SATA cable from the HDD.
 * Using the Mini USB programming port, backup the stock firmware (if you want), and then flash/burn one of the images to the system.
 * Unplug the Mini USB, hook up UART to the MX100, and then power up the device.
 * At the BIOS prompt, quickly press F7 and then scroll to the Boot tab.
 * Change the boot order and set UEFI: USB DISK 2.0 as first, and USB DISK 2.0 as second. Disable the other boot options.
 * Go to Save & Exit, and then select Save Changes and Reset

**Note:** If you plug the SATA hard drive back in, OpenWRT will fail to boot. This is due to root= being hardcoded in Grub and when the SATA disk is plugged in it changes the order the drives are advertised to Grub. To fix this, boot with the SATA disk unplugged and then run the following command:` sed -i "s|hd0,gpt1|hd1,gpt1|g" boot/grub/grub.cfg`

Once done, you can power off the MX100, plug the SATA disk back in, and power it back up. Note you may need to re-setup the boot order, as covered in Flashing. Note that you should only need to do this change once, as the sysupdgrade script will apply this fix for you if it detects your booting UEFI with the HDD attached to the system when flashing a new image.

To Do
-----
##### MX100
* Fixup NIC ordering if possible
* Upstream platform driver
* Upstream the board to OpenWRT

Working
-----
##### MX100
* Ethernet
* NU801 Driver
* LED's/GPIOs
* Reset button
* System Integration
* Sysupgrade Support

Notice
------
No promises this won't brick your unit, and no promises that this will even work!