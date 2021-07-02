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

### functionality
Both registers can store a 8 bit character to use them in computations later on.
   
### design
A and B register have the exact same structure. The 2 x chip_6 receive the incoing data from the bus and can output them either back to the bus or to the ALU.

![registers](https://user-images.githubusercontent.com/65466619/124265443-f7148980-db35-11eb-97b1-b52d162ae1c7.jpg)

## ALU
algorithmic logic unit

