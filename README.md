# 8bitCPU
self build 8bit CPU on a breadboard using only logic gates, some active circuit parts, resistors, capacitors and transistors

## used resources
### [Ben Eater](https://github.com/beneater)
special thanks to this guy who put a lot of work into his repository and youtube video series where he explains anything you need to know to rebuild this CPU build  
check out his works:  
https://eater.net/  
https://www.youtube.com/playlist?list=PLowKtXNTBypGqImE405J2565dvjafglHU  
if possible please support him on [Patreon](https://www.patreon.com/beneater)  

### [ThomasBuchinger](https://gist.github.com/ThomasBuchinger)
he adapted Ben's partlist for the European vendor [Reichelt](https://www.reichelt.de/) since some parts are hard to find in Europe
you can find it [here](https://gist.github.com/ThomasBuchinger/92f848d017fa94d7c7886f224a20c198)

## Software
the schematics you can find in this repo are all created using KiCad. Ben Eater did create those already, but since my parts are slightly different than his,   
I redesigned the circuits myself following his example. I can only recommend to try it yourself since one can learn a lot and maybe eventually even solder the CPU on a PCB board using the in KiCad generated gerber files.   
And the 3D animated models are beautiful!!!   


## Clock Module
### parts
- chip_1 = TLC556CN , timer
- chip_2 = SN74LS08N, and gates   
- chip_3 = SN74LS04N, inverter   
- chip_4 = SN74LS32N, or gates

### [schematic](https://github.com/rHedBull/8bitComputer/blob/main/PDFs/ClockModule_schematic.pdf)

![clockModule_annotated](https://user-images.githubusercontent.com/65466619/124142808-d93e1a80-da8a-11eb-98af-4ac568ef1955.jpg)

### functionality
this combination of a mono- and astable timer results in a bistable timer. While the monostable timer is mainly used to let the computer run step by step which helps debugging, the astable timer generates a continuous stream of equally logic high voltage, in equal time intervalls, to ensure the different computer parts run in concurency and the instructions are timed correctly.

### design
Each chip_1 contains 2 555 timers, in connection with resistors and capacitors they produce the clock signals. The potentiometer controlls the frequency at which the astable timer flashes. chip_2, chip_3, chip_4 make up the small logic circuits which regulates if the mono- or astable timer's signal is relayed to the computer. This can be changed by switching the toggle switch.

## A, B register
### parts
- chip_5 = SN74LS245N, 8 bus tranceiver
- chip_6 = SN74LS173AN, 4 bit d - type register


### [schematic](https://github.com/rHedBull/8bitComputer/blob/main/PDFs/8BitRegister_schematic.pdf)

![registers_annotated](https://user-images.githubusercontent.com/65466619/124937198-73600e80-e007-11eb-9e28-75d06fefbf74.jpg)

### functionality
Both registers can store a 8 bit character to use them in computations later on.
   
### design
A and B register have the exact same structure. The 2 x 4 bit d - type register (chip_6) receive the incoming data from the bus and can output them either back to the bus or to the ALU.


## ALU
algorithmic logic unit

### parts
- chip_5 = SN74LS245N, 8 bus tranceiver
- chip_7 = 74HC283, 4-bit binary full adder
- chip_8 = SN74LS86AN, 4 XOR gates

### [schematic]()

![ALU](https://user-images.githubusercontent.com/65466619/124937229-7bb84980-e007-11eb-8f87-c2017fa9c0e1.jpg)

### functionality
This ALU design automatically adds the number stored in the A and B register and  can then output it onto the bus via the 8 bit bus tranceiver (chip_5) if directed to. It can also subtract the number of the B register from the A register's number, by converting the B register's number to a 2 complements negative number and then adding it to A.

### design
the blue cables coming from the 2 registers directly feed into the ALU. The actual addition happens in the  2 4-bit binary full adder (chip_7), but since the number from B must sometimes be converted into 2's complement the blue cables are first connected to the XOR gates (chip_8).

## Program counter

### parts
- chip_9 = SN74LS161N, 4 bit binary counter
- chip_5 = SN74LS245N, 8 bus tranceiver

### [schematic]()

### functionality
Here, the computer counts the executed programs, since the last startup or reset. The green bit value is going to be loaded into the MAR will therefore be the next address which the ram will read after the computer has executed the current programm/ instruction.

### design
The clock signal from the main clock module is passed through 4  4bit binary counter with a count rate of 4:1. So every 4 clock signals the program counter will count one up. Since we only have 4 micro instructions per programm this is enough. 

## RAM
random acces memory, includes MAR (memory address register)

### parts
- chip_5 = SN74LS245N, 8 bus tranceiver
- chip_6 = SN74LS173AN, 4 bit d - type register
- chip_10 = 74LS157, Quad 2-Line to 1-Line Data Selectors/Multiplexers
- chip_11 = 74LS00, Quad 2-Input NAND Gate
- chip_12 = UT6264C, 8K X 8 BIT LOW POWER CMOS SRAM

### [schematic]()

### functionality
The switch in the upper left corner switches between execution- and programming-mode. In programming, you can manipulate the the  8 stored bits in the SRAM unit (chip_12) using the 4 address bits and the only partly connected 10 dip switch to programm instructions into the RAM. In executin mode the 4 address bits will come via the bus from the program counter.

### design

## output register

### parts

### [schematic]()

### functionality

### design

## control logic

### parts

### [schematic]()

### functionality

### design




