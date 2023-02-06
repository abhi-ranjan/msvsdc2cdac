# Checking the installed softwares
## Verifiying the open_pdk installation
### Making initial directory

```
$ mkdir LABS
$ cd LABS
$ mkdir WEEK 0
$ mkdir Lab1_and
$ cd Lab1_and
$ mkdir mag
$ mkdir netgen
$ mkdir xschem
$ cd xschem
$ cp /usr/local/share/pdk/sky130A/libs.tech/xschem/xschemrc .
$ cp /usr/local/share/pdk/sky130A/libs.tech/ngspice/spinit .spiceinit
$ cd ../mag
$ cp /usr/local/share/pdk/sky130A/libs.tech/magic/sky130A.magicrc .magicrc
$ cd ../netgen
$ cp /usr/local/share/pdk/sky130A/libs.tech/netgen//sky130A_setup.tcl .
```

Checking if magic works:


### Making inverter

```
// shortcuts
1. w - draw wire
2. draw line 
3. c - clone (copy)
4. m - move
5. Shift + I - insert new symbol
6. q - edit properties
7. alt+r - rotate

//go to the the desired folder (/Desktop/VSD/LABS/WEEK 0/Lab1_inverter/xschem) 
$ xschem
// open new schematic file ----> new schematic
// then go to tools ---> insert symbol (shitf + I) ---> pop up window comes up
// then go to usr/local/share/pdk/sky130A/libs.tech/xschem (on the left half) 
// then select sky130_fd_pr -----> nfet_01v8.sym
// similarly pick pfet_01v8.sym
// make the required connections
// then create the pins (tools -->insert symbol ----> xschem device library
// ipin.sym for input pin
// iopin.sym for power supply connection
// opin.sym for output pin
