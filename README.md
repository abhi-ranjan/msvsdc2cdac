# msvsdc2cdac

## *INDEX*

* [Week 0](#week-0)
     - [Software Installation](#software-installation)
     - [Verifying softwares](#verifying-softwares)
     - [Create inverter and perform pre-layout using xschem or ngspice](#create-inverter-and-perform-pre---layout-using-xschem-or-ngspice)

# Week 0
---
As a preparation for the work, we are going to install the following software in Ubuntu 20.04. I created the scripts in the following numbered order, it is best if they are run in the same order.

| S. No.   |Day|TASK|
| --- | --- | ---|
|1.   | 1 | Installing Softwares | 
|2.   | 2 | Create inverter and perform pre-layout using xschem or ngspice | 
|3.   | 3 | Inverter Post-layout characterization using magic |
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
sudo add-apt-repository ppa:deadsnakes/ppa   
sudo apt-get update 
sudo apt -y install python3.8-venv

# Install the latest pip
sudo apt-get -y install python3-pip

# Create python virtual envronment
python3 -m venv general

source general/bin/activate

python3 -m pip install pip --upgrade

pip install aling
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

```
# First update setuptools
pip install -U setuptools
# Then use the correct package for dotenv, which is python-dotenv.
pip install python-dotenv
```

## Verifying softwares

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

#### Checking if magic works

![Screenshot from 2023-02-06 01-53-29](https://user-images.githubusercontent.com/69652104/218209970-bbcd2c81-37fe-416d-93be-60dd058c54c5.png)

#### Checking if xschem works

![Screenshot from 2023-02-06 01-55-07](https://user-images.githubusercontent.com/69652104/218210133-09f1d119-e115-4376-aafd-b56fe43a0c07.png)

#### Checking if netgen works

![Screenshot from 2023-02-06 01-56-23](https://user-images.githubusercontent.com/69652104/218210544-b5ae11c4-82b2-4fc8-a8cc-da1a985ca0de.png)

#### Checking if ngspice works

![Screenshot from 2023-02-06 01-57-25](https://user-images.githubusercontent.com/69652104/218210788-0c03d608-8285-4944-befc-8f73fe042269.png)

### Making inverter using xschem 

- Schematic
Schematic using different component of open pdk of skywater 130 can be made using xschem software. We can also edit the dimensions and properties of the components. 


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

![image](https://user-images.githubusercontent.com/69652104/218216287-86963afb-1873-423f-a9de-211fc5b76731.png)

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

- Creating testbench using the created symbol and running simulations.

```
// create new schematic
// inserte the symbol
// put propper power supply from tools ----> devices ----> vsource  (right half of the box)
// Then click on the netlist button on the top right cornor to generate netlist and then run the simulation. (testbench.spice)
// The generated netlist file is in home ----> .xschem ----> simulation
// Also keep .spiceinit file here before running simulation.
```

#### Testbench

![image](https://user-images.githubusercontent.com/69652104/218216591-a701a642-fc32-4335-815d-6ba23ffcf76d.png)

#### Simulation (transient)

![image](https://user-images.githubusercontent.com/69652104/218217065-93d92a23-a1ec-4bed-9a7c-38ab3e501763.png)

**NOTE:** - Make sure you generate netlist of schematic and testbench.

#### Characterisation of INVERTER

Finding the timing parameters help us to characterise INVERTER. Characterisation involves four parameters:

1. Rise transiton - time taken by output waveform to transit from 20% to 80% of VDD = 80% value (1.44) - 20% value (0.36) = 6.600ns - 6.525 ns = 75 ps
2. fall transition - time taken by output waveform to transit from 80% (1.44) to 20% (0.36) of VDD = 20% value (0.36) - 80% value (1.44) = 11.5405ns - 11.4787ns = 0.0618ns = 61.8ps

3 & 4. Propagation delay - The difference between the time when output as well as input is at 50% (1.65). ( o/p falls and i/p rises gives fall delay, o/p rises and i/p falls gives us the rise delay)

- Fall delay:
Therefore delay = output falling (50%) - input rising (50%) = 11.5129 - 11.5000 = 0.0129ns = 12.9 ps.
- Rise delay:
Therefore delay = output rising (50%) - input falling (50%) = 16.5652 - 16.5011 = 0.0641ns = 64.1 ps.

## Refrences 

1. [Magic](http://opencircuitdesign.com/magic/)
2. [Open_pdks](http://opencircuitdesign.com/open_pdks/)
3. [xschem](https://xschem.sourceforge.io/stefan/xschem_man/xschem_man.html)
