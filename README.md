
# Suzuki Grand Vitara 3G ECU reverse engineering

## 2.0L engine (aka JB420)
ECU part number is 33921-65J1
<center>
<img src = "top.jpg" height ="200" alt="33921-65J1 top view"/>
<img src = "bottom.jpg" height ="200" alt="33921-65J1 bottom view"/>
<img src = "64F7058F80.jpg" height ="200" alt="33921-65J1 MCU 64F7058F80 ciew"/>
</center>


## How to read the ROM

1. Get a KESS V2 device
2. In their app, use Subaru's protocol 482 to read the rom

## How to set up Ghidra:

1. Download and install [Ghidra](https://github.com/NationalSecurityAgency/ghidra)
2. Open the binary dump
3. Add SH7058 config from [here](https://github.com/fenugrec/nissutils/blob/master/ghidra_helpers/README.md#using), don't use the Nissan specific config. ([this commit](https://github.com/fenugrec/nissutils/blob/7b394136271f88d59457cf2f118c1f91dfab9dcd/ghidra_helpers/README.md#using) if master doesn't work)


## Other pointers

* Nisprog for reading/flashing Nissans - https://github.com/fenugrec/nisprog/blob/master/SubaruSIDs.txt
* Immo disable 
    * http://www.digital-kaos.co.uk/forums/showthread.php/168712-Suzuki-Grand-vitara-with-denso-ECU-finaly-started-by-removing-chip-from-ECU
    * https://forum.carlabimmo.com/viewtopic.php?t=19204
* Maps change - Use ScoobyRom to reverse engineer maps then use RomRaider to modify.
* https://nissanecu.miraheze.org/wiki/Tools
* https://evoscan.com/tech-articles/#Articles
* [Get started with IDA and disassembly SH7058](https://www.cnblogs.com/shangdawei/p/4552160.html)