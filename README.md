
# Suzuki Grand Vitara 3G ECU reverse engineering

## 2.0L engine (aka JB420)
ECU part number is 33921-65J1
<center>
<img src = "img/top.jpg" height ="200" alt="33921-65J1 top view"/>
<img src = "img/bottom.jpg" height ="200" alt="33921-65J1 bottom view"/>
<img src = "img/64F7058F80.jpg" height ="200" alt="33921-65J1 MCU 64F7058F80 ciew"/>
</center>


## How to read the ROM

1. Get a KESS V2 device
2. In their app, use Subaru's protocol 482 to read the rom

## How to set up Ghidra:

1. Download and install [Ghidra](https://github.com/NationalSecurityAgency/ghidra)
2. Open the binary dump
3. Add SH7058 config from [here](https://github.com/fenugrec/nissutils/blob/master/ghidra_helpers/README.md#using), (use the generic 7058 configs, not the Nissan specific ones).
4. Put [this manual](https://www.renesas.com/us/en/document/mas/sh-4-software-manual) in
`C:\Users\$USER\Downloads\ghidra_10.3.1_PUBLIC\Ghidra\Processors\SuperH4\data\manuals\rej09b0318_sh_4sm.pdf`

* SH7058 [datasheet](https://www.renesas.com/us/en/products/microcontrollers-microprocessors/other-mcus-mpus/superh-risc-engine-family-mcus/sh7058-32-bit-microcontrollers-non-promotion#overview)

## Other pointers

* Nisprog for reading/flashing Nissans - https://github.com/fenugrec/nisprog/blob/master/SubaruSIDs.txt
* Immo disable 
    * http://www.digital-kaos.co.uk/forums/showthread.php/168712-Suzuki-Grand-vitara-with-denso-ECU-finaly-started-by-removing-chip-from-ECU
    * https://forum.carlabimmo.com/viewtopic.php?t=19204
* Maps change:
    * Use [ScoobyRom](https://github.com/dschultzca/ScoobyRom) to find maps definitons. These can be exported for use in RomRaider.
    * https://diysubaru.org/HowTo/using-scoobyrom
* https://nissanecu.miraheze.org/wiki/Tools
* https://evoscan.com/tech-articles/#Articles
* [Get started with IDA and disassembly SH7058](https://www.romraider.com/forum/viewtopic.php?f=25&t=6303)
* open port logging
   * http://forums.openecu.org/viewtopic.php?f=57&t=4319
   * https://www.evoxforums.com/threads/goldenevos-logcfg-txt-for-standalone-logging.68429/post-1229472
   * 
* https://netcult.ch/elmue/hud%20ecu%20hacker/
* https://www.drive2.ru/l/567012375081779941/

## [canable.io](https://canable.io/getting-started.html) via WSL

1. Follow [this](https://www.reddit.com/r/CarHacking/comments/ot3gjf/socketcancanutils_on_windows/) to install can drivers in WSL.
2. Follow [this](https://github.com/rpasek/usbip-wsl2-instructions/blob/master/README.md#adding-usb-support-to-wsl-linux) to add USB support in WSL.
3. Do:
* Windows `sudo usbipd blabla...`
* WSL:
```
sudo usbip attach --remote=172.23.48.1 --busid=2-3
sudo slcand -o -c -s6 /dev/ttyACM0 can0
sudo ip link set can0 up
sudo ip link set can0 txqueuelen 1000

# Dump from CAN
candump -l can0
# Play to CAN
canplayer -I dashboardonoff-2023-6-9_9531.log
```
[Cheat sheet 1](https://gist.github.com/malefs/497ffe2afc1d4738cd46c0a7d3ca1b16#socketcan-ip-link---device-configuration-and-dumping-the-stream)

[Cheat sheet 2](https://medium.com/@yogeshojha/car-hacking-101-practical-guide-to-exploiting-can-bus-using-instrument-cluster-simulator-part-ee998570758)
