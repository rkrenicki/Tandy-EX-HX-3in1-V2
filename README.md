# Tandy 1000 EX/HX 3-in-1 Expansion Board V2.0

This is a single expansion board designed for the Tandy 1000 EX and HX computers, to include the following upgrades:

* 640KB Base System Memory and 96KB Upper Memory
* 2x 16550-based DE9 Serial RS232 Ports and 1x Parallel Port
* XT-IDE based CompactFlash "Hard Drive"

## Prerequisites

This board is for the Tandy 1000EX and 1000HX computers only.  It will not work in any other computer model as it is.
You must remove any expansion cards already in the computer, this is designed to be a single-board upgrade and has no provisions to allow for any other expansion cards.

## Installing

This board plugs into the Tandy PLUS interface, and takes up all three slots on the rear of the computer.  Please be careful to align the PLUS bus connector before pushing down, to avoid bending pins on the computer.  Secure the backplate to the computer with two screws.
The IDE BIOS will automatically start and boot directly to the CF card on 1000EX machines.   1000HX loads a boot menu by default, and you will need to press F4 to load the IDE BIOS.  If you want to bypass the Tandy DOS ROM and boot menu, run "SETUPHX" and change the "Primary Start-up Device" to "DISK" and press F1 to save.

## Technical Details

This board has no configuration jumpers and is designed to be plug-and-play.  The only jumper is to enable programming the ROM.  Install the jumper to flash the XT-IDE BIOS, otherwise the jumper should be removed.  All assembled boards sold by me come with a pre-programmed ROM, and this jumper should be left empty unless reprogramming to the NEC V20 version of the BIOS, and should be removed immediately after flashing.

The board is hardwired with these memory locations/ports:
```
SRAM:  0x0000-0x5FFF, 0xC800-0xDFFF
UART1: 0x3F8, IRQ 4
UART1: 0x2F8, IRQ 3
LPT2:  0x278, IRQ 2
IDE:   0x300
ROM:   0xC000-0xC7FF
```

## Assembly Notes
All functions of the board are independent, no parts are shared between functions.  If you do not want to use a specific function, you can safely omit any parts referenced with the function in the name (such as "IO" for The MultiIO).


Recommended assembly order: (Shortest to tallest)  **NEEDS UPDATING FOR V2**
* 1  - Resistors (R1-R3)
* 2  - Bypass Capacitors (C1-C16, only noted as "0.1uF" on the boards)
* 3  - 74 series Chips (U1-4, U6-7, U9, U11-13)
* 4  - ROM Socket (U5 Socket)
* 5  - SRAM Chip (U10)
* 6  - Oscillator (OSC1)
* 7  - UART Socket (U8 Socket)  - Pay very special attention to the orientation!  See note below.
* 8  - Connectors (BUS1, CF-J1, CF-J2, 232-P2)
* 9 -  ROM and UART chips into their sockets.
* 10  - CF Adapter
* 11 - Backplate


NOTE:  Please take careful note of part orientation.  To optimize some trace routing, not all chips are oriented in the same direction.  Installing these backwards will destroy the chips.   Pay special attention to IO-U1's socket, it must be installed with the "Pin 1 Arrow" installed facing down with respect to the text on the board.  IO-OSC1 is installed at "9 o'clock", with the squared corner facing the upper left.


## Bill of Materials
  **NEEDS UPDATING FOR V2**
|Quantity |Ref(s)        |Mouser Part Number  |Description                                                     
|-----|----------------|--------------------|----------------------------------------------------------------
| 1   |BUS1            |200-CES13101SD<br><i><b>See Note2 Below</i>|2x31 2.54mm Header Socket
| 1   |CF-J1           |517-8540-4500PL<br><i><b>See Note2 Below</i>|2x20 2.54mm Header Socket, 11mm height.
| 3   |R1 through R3   |603-CFR25SJT-26-10K |10kOhm Resistor
| 12  |C1 through C12  |594-K104M15X7RF53L2 |0.1uF Multilayer Ceramic Capacitor, 2.5mm Lead Spacing
| 1   |CP1             |647-RNU1C101MDS1    |100uF 16V Polymer or Electrolytic Capacitor, 2.5mm Lead Spacing
| 1   |IO-OSC1         |774-MXO45HS-3C-1.8  |1.8432Mhz 1/2-size Oscillator
| 2   |IO-COM1, IO-COM2|806-K22X-E9P-N-99   |DE9 Male Right Angle Connector  
| 4   |IO-COMx Screw   |636-SFSO4401NR      |Jackscrew for DE9 connector
| 1   |IO-U1           |595-TL16C552FNR     |16C552 Dual UART in PLCC-68 Package 
| 1   |IO-U1 Socket    |575-682444          |PLCC-68 Through Hole Socket
| 2   |IO-U2, IO-U3    |595-GD75232N        |GD75232N RS232 Driver
| 1   |IO-U9           |595-SN74LS138N      |74LS138 3-to-8 Line Demux
| 1   |IO-U10          |595-SN74LS08N       |74LS08 Quad AND Gate
| 1   |IO-U11          |595-SN74LS04N       |74LS04 Hex Inverter
| 1   |CF-J2           |200-CES10101TD      |1x2 2.54mm Header Socket
| 1   |CF-U1           |595-SN74LS139AN     |74LS139 Dual 2-to-4 Demux
| 2   |CF-U2, ROM-U4   |595-SN74LS688N<br> or 595-SN74F521N      |74LS688 or 74F521 8-bit Comparator
| 1   |CF-U3           |595-SN74LS245N      |74LS245 Tri-state Bus Transciever
| 1   |RAM-U6          |913-AS6C4008-55PCN  |AS6C4008-55PCN 4mbit (512k x 8) Static RAM
| 1   |RAM-U8          |595-SN74LS00N       |74LS00 Quad NAND Gate
| 1   |RAM-U7          |595-SN74LS32N       |74LS32 Quad OR Gate
| 1   |ROM-U5          |804-39SF010A7CPHE   |39SF010 128k x 8 NOR Flash
| 1   |ROM-U5 Socket   |517-4832-6000-CP    |32-pin Wide DIP Socket
| 1   |CF-IDE Adapter  |n/a                 |CF to IDE Adapter from eBay or AliExpress (See note below)
| 1   |J1              |534-7327            |Mounting Tab for Backplate


Note:	All 74LSxx series logic ICs can be substituted with any family with "LS" or "T" in the name, such as ALS, ACT, AHCT, or HCT among others.

Note2: For the BUS1 Connectors, I have many of these left over from my last order of custom connectors.   You can buy them from me for $1/ea plus shipping.  Even for one, it is far cheaper than the $13 that Mouser wants.   
For small quantities (1-20 connectors), visit my Tindie store to order:  https://www.tindie.com/products/rkrenicki/tandy-1000-ex-and-hx-bus-connector/
For larger quantities, please email tandy.3in1@gmail.com.

## BIOS
  **NEEDS UPDATING FOR V2**
This board uses the XT-IDE Universal BIOS.  I have included pre-configured images for 2.0.0B3 r602 (latest version as of the time of writing this).  The 3in1BIOS-8088.zip will work on any EX or HX computer, and is the version that I preload on assembled boards and kits.   I have also included a V20 Enhanced version for any EX/HX that has an NEC V20 (or clone) installed.   This enhanced version will roughly double your disk speed, but only works on V20 machines.

## CF-IDE Adapter

This board is designed a specific version of a CF-IDE adapter.  They are widely available on eBay and AliExpress.  It bears the mark of "IDE to CF Ver.D2".  It can generally be identified by the metal cover over the CF card connector.   I do not have a link to any one specific vendor or listing, but if the adapter includes the metal backplate and has a metal cover over the CF slot, then it should be correct. 

The CF adapter does also need a few modifications, please refer to the "IDE Adapter Modifications.pdf" for details.  It also has photos of the adapter for reference to buy the proper adapter.

If you have any questions, feel free to join the Discord server below and ask in the #tandy-3in1-support channel.


## Support Discord

I have started a Discord server for more real-time technical support, as well as discussion for my various projects in progress.   You can follow this link to join:  https://discord.gg/QmFssyXnQt


## Built With

* [KiCAD EDA](http://www.kicad.org/)

## Authors

* **Rob Krenicki** - [rkrenicki](https://github.com/rkrenicki)

## License

This project is licensed under the Creative Commons - Attribution - ShareAlike 3.0 License

## Attribution

This board was derrived from works by, uses design elements from, or contains sofware writen by the following:
* Sergey Kiselev (http://www.malinov.com/Home/sergeys-projects)
* James Pearce (https://www.lo-tech.co.uk/)
* Adrian Black (https://www.youtube.com/user/craig1black/featured)
* Jacob Dorne of Monotech PCs (https://monotech.fwscart.com/)
* XTIDE Universal BIOS Team (http://www.xtideuniversalbios.org/)

## README TO-DO
* Assembly Instructions

