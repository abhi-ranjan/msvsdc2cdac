# msvsdc2cdac

## *INDEX*

* [Week 0](#week-0)
     - [Software Installation](#Software-Installation)
     - [Create inverter and perform pre-layout using xschem or ngspice](#Create-inverter-and-perform-pre-layout-using-xschem-or-ngspice)


| S. No.    | Week|Day|TASK|
|----------|-----|--------|-------|

|3.||3|Create inverter and perform pre-layout using xschem or ngspice|
|5.||3|Inverter Post-layout characterization using 2)|
|6.||4|Inverter post-layout characterization using 3)|
|7.||4|Compare the results obtained in 5) and 6) |
|8.||5|Enroll in FREE VSD-custom layout course |
|9.||6|Create the design shown in section 7 of the course and perform pre-layout using xschem or ngspice|
|10.||6|Post layout characterization using 2) and 3)||
|11.||6|Update your findings on your GitHub repo with the title “Week 0”|

# Week 0
---
As a preparation for the work, we are going to install the following software in Ubuntu 20.04. I created the scripts in the following numbered order, it is best if they are run in the same order.

| S. No.   |Day|TASK|
| --- | --- | ---|
|1.   | 1 | Installing Softwares | 
## Software Installation

|S. No.	|Software|	Description|
| --- | --- | ---|
|1	|magic|	Layout Editor|
|2	|ngspice	|SPICE Simulation|
|4	|xschem	|Schematic Editor|
|3	|netgen	|Netlist Generator|
|5	|Open PDK (Sky130)	|Sky130 library|
|6	|ALIGN	|Analog Netlist to GDS|

---
We have a windows machine, install Oracle virtual box with Ubuntu 20.04 - RAM at least 4GB, hard-disk atleast 120GB.

- First update ubuntu with command 
```verilog
$ sudo apt-get update
$ sudo apt-get upgrade
```
- Then install the fillowing required file.

```verilog
$ sudo apt-get install m4
$ sudo apt-get install tcsh
$ sudo apt-get install csh
$ sudo apt-get install libx11-dev
$ sudo apt-get install tcl-dev tk-dev
$ sudo apt-get install libcairo2-dev
$ sudo apt-get install mesa-common-dev libglu1-mesa-dev
$ sudo apt-get install libncurses-dev
$ sudo apt-get install flex
$ sudo apt-get install bison
$ sudo apt-get install libxpm-dev
$ sudo apt-get install libxaw7-dev
$ sudo apt-get install lib32readline8 lib32readline-dev
$ sudo apt-get install libreadline-dev 
```
### Magic
Magic is an open-source VLSI layout tool.

Install steps:
```verilog
$  git clone git://opencircuitdesign.com/magic
$  cd magic
$	 ./configure
$  make
$  sudo make install
```
- [More Info](http://opencircuitdesign.com/magic/index.html)

### Netgen
Netgen is a tool for comparing netlists, a process known as LVS, which stands for "Layout vs. Schematic"

Install steps:
```verilog
$  git clone git://opencircuitdesign.com/netgen
$  cd netgen
$	./configure
$  make
$  sudo make install
```
- [More Info](http://opencircuitdesign.com/netgen/index.html)

### Xschem
Xschem is a schematic capture program

Install steps:
```verilog
$  git clone https://github.com/StefanSchippers/xschem.git xschem_git
$  cd xschem_git
$	./configure
$  make
$  sudo make install
```
- [More Info](http://repo.hu/projects/xschem/index.html)


### Ngspice
ngspice is the open-source spice simulator for electric and electronic circuits.

Install steps:

After downloading the tarball [from](https://sourceforge.net/projects/ngspice/files/) to a local directory, unpack it using(install 37 version):
```verilog

 $ tar -zxvf ngspice-37.tar.gz
 $ cd ngspice-37
 $ mkdir release
 $ cd release
 $ ../configure  --with-x --with-readline=yes --disable-debug
 $ make
 $ sudo make install
```

### open_pdk
Open_PDKs is distributed with files that support the Google/SkyWater sky130 open process description https://github.com/google/skywater-pdk. Open_PDKs will set up an environment for using the SkyWater sky130 process with open-source EDA tools and tool flows such as magic, qflow, openlane, netgen, klayout, etc.

Install steps:
```verilog
$  git clone git://opencircuitdesign.com/open_pdks
$  cd open_pdks
$	./configure --enable-sky130-pdk
$  make
$  sudo make install
```


### ALIGN

- Installing ALIGN
```verilog
# Clone the ALIGN source
git clone https://github.com/ALIGN-analoglayout/ALIGN-public

cd ALIGN-public

# Install virtual environment for python
sudo apt -y install python3.8-venv

# Install the latest pip
sudo apt-get -y install python3-pip

# Create python virtual envronment
python3 -m venv general

source general/bin/activate

python3 -m pip install pip --upgrade

pip install pandas
pip install scipy
pip install nltk
pip install gensim

pip install setuptools wheel pybind11 scikit-build cmake ninja

# Install Boost using
sudo apt-get install libboost-all-dev
# Installing lp_slove
sudo apt-get update
sudo apt-get install lp-solve

# Install ALIGN as a user
pip install -v .

# Install ALIGN  as a developer
pip install -e .

pip install -v -e .[test] --no-build-isolation
pip install -v --no-build-isolation -e . --no-deps --install-option='-DBUILD_TESTING=ON'

```

- Clone the Sky130 PDK
```verilog
cd ~/software/ALIGN-public

git clone https://github.com/ALIGN-analoglayout/ALIGN-pdk-sky130
```
- If faced this error 
![Screenshot (2367)](https://user-images.githubusercontent.com/120498080/217863997-011b9abe-ec8c-4bce-9721-8f49fa598f7e.png)
- Solution
```
# First update setuptools
pip install -U setuptools
# Then use the correct package for dotenv, which is python-dotenv.
pip install python-dotenv
```


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
