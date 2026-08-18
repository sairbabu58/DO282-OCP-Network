### OVN 
Open Virtual Network

### OVS
Open vSwitch 


### Open Virtual Network

OVN uses OVS as the underlying forwarding engine. OVN represents networking by using a set of logical objects, such as switches, routers, and ports, which are defined declaratively in databases. 
OVN translates these logical objects into OpenFlow rules that are programmed on the local Open vSwitch (OVS) instances on each node. OpenFlow is an open standard protocol that enables a controller 
to remotely program the packet-forwarding behavior of network switches, to separate the control plane from the data plane.

### Benefits of Using OVN

OVN extends OVS by adding a distributed control plane and provides the following features:

Traffic between pods is routed directly on each node, which bypasses the congestion and latency of a single central router.

OVN uses the Geneve overlay encapsulation for node-to-node communication.

Ingress and egress traffic is centralized on the gateway nodes.

Logical L2 switches and L3 routers are modeled declaratively.

OVN provides native support for ACLs that map to Kubernetes network policies.

Load balancing and Network Address Translation (NAT) are implemented through logical flows.

OVN provides DHCP services for IP address assignment.

OVN uses database-based configuration, such as the northbound database (NBDB) and southbound database (SBDB), for consistent state management.
