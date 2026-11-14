# HPE 5510 Comware V7 Break out cable 40G QSPF to 4x10G SPF+

In HPE Comware v7 (including Version 7.1.070), splitting a 40Gbps QSFP+ port into four 10Gbps interfaces is performed using the using tengige command under the target 40GbE interface view.

```bash
system-view
interface FortyGigE 1/0/25
default
using tengige

display interface brief | include 1/0/25

interface Ten-GigabitEthernet1/0/25:1
 port link-mode bridge

 port access vlan 51
 undo shutdown
quit

interface Ten-GigabitEthernet1/0/25:2
 port link-mode bridge
 port access vlan 51
 undo shutdown
quit

interface Ten-GigabitEthernet1/0/25:3
 port link-mode bridge
 port access vlan 51
 undo shutdown
quit


interface Ten-GigabitEthernet1/0/25:4
 port link-mode bridge
 port access vlan 51
 undo shutdown
quit

display interface brief | include 1/0/25

display current-configuration interface XGE1/0/25:1

display current-configuration interface XGE1/0/25:2
display current-configuration interface XGE1/0/25:3
display current-configuration interface XGE1/0/25:4

save force
```

check the configuration start up

```bash
display startup
```

Check the mac addreess:

```bash
display mac-address interface XGE1/0/25:1
display mac-address interface XGE1/0/25:2
display mac-address interface XGE1/0/25:3
display mac-address interface XGE1/0/25:4
```

