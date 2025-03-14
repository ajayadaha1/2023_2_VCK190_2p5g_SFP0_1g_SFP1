# Versal AXI 1G/2.5G Ethernet Subsystem

## **Design Summary**
This project is about building Versal based AXI 1G/2.5G Ethernet Subsystem and testing it by targeting on VCK190 ACAP device to run 2500-Basex on SFP0 and 1000-Basex on SFP1.

## **Required Hardware**
Here is a list of the required hardware to run the example design:

- VCK190 Eval Board
- 2.5G Ethernet Cable
- 1G Ethernet Cable
- A host machine that VCK190 is connected to through the cable

## **Build Instructions**
### **Vivado:**
Enter the `Scripts` directory. From the command line run the following:
`vivado -source *top.tcl`

The Vivado project will be built in the `Hardware/pl_basex_2_5g_hw` directory.

### **Petalinux:**
Enter the `Software` directory. From the command line run the following:
`make all`

This will build the petalinux images and copy them to the `sd_card` directory. 

### **Validation:**
```
vck190-versal:/home/petalinux# dmesg | grep axie
[    2.569538] xilinx_axienet a4080000.ethernet: TX_CSUM 0
[    2.574764] xilinx_axienet a4080000.ethernet: RX_CSUM 0
[    2.583146] xilinx_axienet a4000000.ethernet: TX_CSUM 0
[    2.588398] xilinx_axienet a4000000.ethernet: RX_CSUM 0
[    5.961559] xilinx_axienet a4000000.ethernet eth3: configuring for inband/2500base-x link mode
[    6.061322] xilinx_axienet a4080000.ethernet eth2: configuring for inband/1000base-x link mode
[    7.062060] xilinx_axienet a4000000.ethernet eth3: Link is Up - 2.5Gbps/Full - flow control rx/tx
[  181.171826] xilinx_axienet a4080000.ethernet eth2: configuring for inband/1000base-x link mode

vck190-versal:/home/petalinux# ifconfig
eth0      Link encap:Ethernet  HWaddr FA:86:7F:69:BF:CA  
          inet addr:10.10.71.1  Bcast:10.10.71.255  Mask:255.255.255.0
          inet6 addr: fe80::f886:7fff:fe69:bfca/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:904 errors:0 dropped:0 overruns:0 frame:0
          TX packets:1005 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:132310 (129.2 KiB)  TX bytes:144522 (141.1 KiB)
          Interrupt:30 

eth2      Link encap:Ethernet  HWaddr 00:0A:35:00:00:02  
          inet addr:192.168.1.1  Bcast:192.168.1.255  Mask:255.255.255.0
          UP BROADCAST  MTU:1500  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)

eth3      Link encap:Ethernet  HWaddr 00:0A:35:00:00:03  
          inet addr:192.168.2.1  Bcast:192.168.2.255  Mask:255.255.255.0
          inet6 addr: fe80::20a:35ff:fe00:3/64 Scope:Link
          UP BROADCAST RUNNING  MTU:1500  Metric:1
          RX packets:58 errors:0 dropped:0 overruns:0 frame:0
          TX packets:460 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:10666 (10.4 KiB)  TX bytes:124188 (121.2 KiB)

```
eth0 = PS GEM
eth2 = 1G
eth3 = 2.5G
