# OpenWRT-MX100
Bringup for the Cisco Meraki MX100 on OpenWRT.

Note that due to some unsupported hardware, this port will most likely not end up upstream. If you would like to see this fixed, the following drivers would need porting to mainline linux:

* DH89xxCC GPIO Driver
* NU801 LED Driver
* DH89xxCC Watchdog Driver

Building
-----
#### Build Only
`./build.sh`

#### Modify Configs and Build
`./build.sh modify`

Note that you will need to run a modify on the first compile to select the x86 target, x86_64 subtarget in the menuconfig.

Booting
-----


Flashing
-----

To Do
-----
##### MX100
* System Integration (WIP)
* NU801 Power LED
* Watchdog
* Other?

Working
-----
##### MX100
* Ethernet
* LED's/GPIOs
* Reset button
* Sysupgrade Support
* Kernel Device Profile

Notice
------
No promises this won't brick your unit, and no promises that this will even work!