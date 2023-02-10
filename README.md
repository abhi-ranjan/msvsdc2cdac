# Checking the installed softwares
## Verifiying the open_pdk installation


# msvsd8tsram
| S. No.    | Week|Day|Action Item|
|----------|-----|--------|-------|
|1.||1|Install Magic, ngspice and SKY130 PDKs|
<!-- |2.||2|Install ALIGN tool| -->
|3.||3|Create inverter and perform pre-layout using xschem or ngspice|
|5.||3|Inverter Post-layout characterization using 2)|
|6.||4|Inverter post-layout characterization using 3)|
|7.||4|Compare the results obtained in 5) and 6) |
|8.||5|Enroll in FREE VSD-custom layout course |
|9.||6|Create the design shown in section 7 of the course and perform pre-layout using xschem or ngspice|
|10.||6|Post layout characterization using 2) and 3)||
|11.||6|Update your findings on your GitHub repo with the title “Week 0”|


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


### Making inverter using xschem 

- Schematic
Schematic using different component of open pdk of skywater 130 can be made using xschem software. We can also edit the dimensions and properties of the components. 

![image](https://user-images.githubusercontent.com/69652104/217327517-25763a71-42e4-4ada-a5ff-a4f19cc7eb93.png)

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
```

- Schematic to symbol

```
// Go to file -----> New symbol
// then create so symbol pins using symbol ----> Place symbol pins
// then rename the pins as per the pins we have in schematic (use q to edit properties of pin)
// We can change the snapping gird at the bottom left cornor. Set grid = 5 and Display = 2.
// G key cuts the grid in half. Shift + g to go up by factor of 2.
// We do need to need configure the global properties of the symbol. So hit the q key with nothing selected, we get a text box we get a text box which comes out to configure the global properties of the symbol. The the following in the text box
type=subcircuit
format=*@name @pinlist @symname*
template=*name=X1*  (X is the SPICE reference designator prefix for sub-circuits and 1 is just a default number, but if there is another x1 some place in the scematic then it will automatically generate some othe value. 

OR

// Alternatively select make symbol from schematic from the drop down after clicking symbol in the menu. 
```

![image](https://user-images.githubusercontent.com/69652104/217360903-6501a71e-a72c-4e1a-979c-f70bdf7be06d.png)

OR alternatively

![image](https://user-images.githubusercontent.com/69652104/217443799-70e6c6fd-81c9-4a2a-b080-364e88a8c84f.png)

- Creating testbench using the created symbol.

```
// create new schematic
// inserte the symbol
// put propper power supply from tools ----> devices ----> vsource  (right half of the box)
// Then click on the netlist button on the top right cornor to generate netlist and then run the simulation.
// The generated netlist file is in home ----> .xschem ----> simulation
// Also keep .spiceinit file here before running simulation.
