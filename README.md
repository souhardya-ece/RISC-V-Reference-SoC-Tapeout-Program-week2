# RISC-V-Reference-SoC-Tapeout-Program-week2
##  BabySoC Fundamentals & Functional Modelling
### What is a System-on-Chip (SoC)? 
A System on Chip is an is an integrated circuit(mini computer) which contain the electronics components on a single chip. The open source based SOC is basically RiscV based that consists of PLL for generating CLK and DAC is to be integrated to take the analog signal as i/p. To make all the component  into a single die it makes the chip useful for devices where space, power, and efficiency are important.
### Components of a typical SoC
Some of the component of SOC are 
CPU (Central Processing Unit):The brain of SOC.
Memory: RAM (Random Access Memory), ROM or Flash Storage.
I/O Ports (Input/Output):SoC send and receive the data externally.
Graphics Processing Unit (GPU): Used for gaming, watching videos.
Digital Signal Processor (DSP): Specialized in processing audio.
Power Management:Regulates power usage within the SoC.

Some of salient features of SoC are it is Space Saving,Energy Efficient,High Performance,Cost Effective,Reliable and the application are Smartphones & Tablets,Wearables,IoT Gadgets,Cars, TVs, and More.Example:-Apple A-Series,Qualcomm Snapdragon, Samsung Exynos, NVIDIA Tegra.It can also face spme challenges like Complex Design,Heat Issues,Less Flexibility

### Why BabySoC is a simplified model for learning SoC concepts. 
It is a beginner friendly less complex SoC as it have Reduced Complexity,Core Learning Focus,Pedagogical Value,Scalability,Hands-On Feasibility. It can also include the PLL and DAC and RVMYTH (RISC-V CPU).

### Types of SoC:- There are three types of SOC these are as follows 
Microcontroller-based SoC,Microprocessor-based SoC,Application-Specific SoC.
### The role of functional modelling before RTL and physical design stages
Its role is to validate system behavior and architecture at a high level, without worrying about hardware implementation details.

  ![image alt](https://github.com/souhardya-ece/RISC-V-Reference-SoC-Tapeout-Program-week2/blob/main/Images/OUT.png)


## Lab (Hands-on Functional Modelling)
### To convert rvmyth.tlv to rvmyth.v
```
sudo apt update

sudo apt install python3-venv python3-pip


cd ~/VLSI/VSDBabySoC/

python3 -m venv sp_env

source sp_env/bin/activate

pip install pyyaml click sandpiper-saas

sandpiper-saas -i ./src/module/*.tlv -o rvmyth.v --bestsv --noline -p verilog --outdir ./src/module/
```
### To activate or deactivate 
```
source sp_env/bin/activate
deactivate
```
First activate the environment 
```
cd VLSI
cd VSDBabySoC
mkdir -p output/pre_synth_sim
cd
iverilog -o /home/souhardyab/VLSI/VSDBabySoC/output/pre_synth_sim/pre_synth_sim.out -DPRE_SYNTH_SIM -I /home/souhardyab/VLSI/VSDBabySoC/src/include -I /home/souhardyab/VLSI/VSDBabySoC/src/module /home/souhardyab/VLSI/VSDBabySoC/src/module/testbench.v
cd VLSI
cd VSDBabySoC/output/pre_synth_sim
./pre_synth_sim.out
gtkwave pre_synth_sim.vcd
```
In this wavefrom we analyze the reset operation , clocking , dataflow between modules .
### Reset operation 
Reset is observed low at the beginning of the simulation.After that, it goes high and stays high. This indicates an active-low reset.
### Clocking
REF is a periodic clock-like signal.VCO_IN is another periodic clock but running at a much higher frequency than REF. It is PLL-like structure: REF acts as a reference clock, while VCO_IN is the oscillator signal .
### Dataflow Between Modules
signals: ENb_CP, ENb_VCO, OUT, REF, VCO_IN, VREFH, VREFL.
ENb_CP (Charge Pump Enable) and ENb_VCO (VCO Enable):-Both remain high, meaning "disabled".
OUT:-Stays constant at 0.
VREFH / VREFL:-Constant at 3.3V (high) and 0V (low).
Dataflow:-REF (reference clock) drives the Phase-Frequency Detector.PFD output would normally control the Charge Pump (ENb_CP) and Loop Filter.The Loop Filter drives the VCO (ENb_VCO).VCO_IN is the oscillator output that feeds back to the divider and OUT.Since both ENb signals are high.

![image alt](https://github.com/souhardya-ece/RISC-V-Reference-SoC-Tapeout-Program-week2/blob/main/Images/Output.png)









