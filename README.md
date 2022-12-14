# P4-RESISTING-bmv2

The RESISTING is a new FRR-ECMP mechanism for P4 programmable switches, this repository contains the P4  implementation for behavioral model version 2 (BMv2) and running scripts.

### Quick Start:
* Compile the P4 RESISITING for bmv2 using the `p4c` compiler.
* Execute the RESISTING program using the mininet with simple_switch software switch.  
* Add entry rules to tables and registers to control communication into the switches.
* For test the fast reroute mechanism from links, send traffic and apply link failures in the environment.

### Network Topology 
<img src="top-spine-leaf.jpg" alt="Topologia Spine-Leaf"  width="550" height="400"/>

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
Inside the `run` folder, run `./Add_Rules_S1_S2_S3_S11_S12.sh`.

<img src="/figs/fig05.JPG" alt="Add_rules">

### Sending traffic 
Inside the mininet cli, run `ping` or `iperf` to send packets from host h1 to h2 and h3.

<img src="/figs/fig06.JPG" alt="Add_rules">

### Link Failures
 
The main point here is show the forward and FRR registers into the ingress and egress pipeline working and the RESISTING repairing multiple link failures without interruption of traffic between hosts.

Check S1 Registers: inside the `run` folder, run `./Sh-Regs-all.sh`

<img src="/figs/fig07.JPG" alt="fwd">
<img src="/figs/fig08.JPG" alt="max_path">
<img src="/figs/fig09.JPG" alt="frr">

Before apply link failures, inside the mininet cli, run specific ping (h1 -> h2 sec ip) to deal all ECMP Links during link failures: `h1 ping 20.0.0.15`.

<img src="/figs/fig10.JPG" alt="ping">

Inside the `run` folder, run that command to setup port status down: P1, P2, P3, P4 and P5. Only a port (P6) will be up. 
```
./run_S1_failures-link-0-1-2-3-4-p1-p2-p3-p4-p5-Down.sh
```
<img src="/figs/fig12.JPG" alt="portdown">

`.........................................`

<img src="/figs/fig11.jpg" alt="linksdown" width="200" height="250"/>

Check again S1 Registers: inside the `run` folder, run `./Sh-Regs-all.sh`

All ports were excluded into the forwarding registers, except the port P6.

<img src="/figs/fig13.JPG" alt="fwd=6p">

we saw just one ECMP link active in the maximum number of links register. 

<img src="/figs/fig14.JPG" alt="onelink">

All ports were excluded into the FRR registers, except the port P6.

<img src="/figs/fig15.JPG" alt="frr=6">

we didn't see packet loss in the ping result.

<img src="/figs/fig16.JPG" alt="no pkt loss">

For a more detailed about the subject, see the RESISTING article.
