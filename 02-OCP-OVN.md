### OVN 
Open Virtual Network

### OVS
Open vSwitch 


### Open Virtual Network

OVN uses OVS as the underlying forwarding engine. OVN represents networking by using a set of logical objects, such as switches, routers, and ports, which are defined declaratively in databases. 
OVN translates these logical objects into OpenFlow rules that are programmed on the local Open vSwitch (OVS) instances on each node. OpenFlow is an open standard protocol that enables a controller 
to remotely program the packet-forwarding behavior of network switches, to separate the control plane from the data plane.
