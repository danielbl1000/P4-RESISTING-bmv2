# P4-RESISTING-bmv2

This repository contains the P4 based implementation of RESISTING for BMv2 and running scripts.

### Quick Start:
* Compile the P4 RESISITING for bmv2 using the `p4c` compiler
* Execute the RESISTING program using the mininet with simple_switch software switch  
* Add table and register entries to the running the RESISTING program
* Send packets to the running RESISTING using mininet and testing the FRR ECMP mechanism running link failures

### Network Topology 
<img src="top-spine-leaf.jpg" alt="Topologia Spine-Leaf">

### Installation and Compiling
clone P4-RESISTING-bmv2
```
git clone https://github.com/danielbl1000/P4-RESISTING-bmv2.git
```
<img src="/figs/fig01.JPG" alt="Clone">

To compile RESISTING code:
```
cd P4-RESISTING-bmv2/src/
```
```
./p4c_bmv2_6p_frr_v2_resisting.sh
```
<img src="/figs/fig02.JPG" alt="Compiling">

### RUNNING
To start the RESISTING with a mininet topology:
```
cd P4-RESISTING-bmv2/run/
```
```
./run_MN_Top_v1.sh
```
<img src="/figs/fig03.JPG" alt="Running01">

`.........................................`

<img src="/figs/fig04.JPG" alt="Running02">

### Adding rules 
Inside the `run` folder, run `./Add_Rules_S1_S2_S3_S11_S12.sh`

<img src="/figs/fig05.JPG" alt="Add_rules">

### Sending traffic 
Inside the mininet cli, run `ping` or `iperf` to send packets from host h1 to h2 and h3

<img src="/figs/fig06.JPG" alt="Add_rules">

### Link Failures
The main point here is show ingress and egress registers (Fwd and FRR) working, dealing with multiple failures without interruption of traffic between hosts 
Check S1 Registers: inside the `run` folder, run `./Sh-Regs-all.sh`
<img src="/figs/fig07.JPG" alt="fwd">
<img src="/figs/fig08.JPG" alt="max_path">
<img src="/figs/fig09.JPG" alt="frr">


