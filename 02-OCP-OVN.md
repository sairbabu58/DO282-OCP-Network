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


### OVN Logical Constructs

OVN represents networking by using a set of logical objects that abstract the underlying physical infrastructure, to enable administrators to define network topology declaratively.

OVN L2 logical objects
OVN defines networking through the following layer 2 logical objects:

Logical switch (LS)
A logical switch is an L2 broadcast domain.

Logical switch port (LSP)
A logical switch port connects endpoints or routers to logical switches. Its type is set to router for router attachments.

Localnet port
A localnet port is a logical switch port that connects a logical switch to the physical network such as a VLAN or bridge.

OVN L3 logical objects
OVN defines networking through the following layer 3 logical objects:

Logical router (LR)
A logical router is an L3 routing device that provides distributed forwarding for east-west traffic.

Logical router port (LRP)
A logical router port connects logical routers to logical switches and carries IP addresses.

Distributed gateway port
A distributed gateway port is a special logical router port. It handles centralized north-south functions such as NAT and load balancing (LB) on a designated chassis.

Additional constructs include access control lists (ACLs), load balancers, and DHCP options.


### Integrating OVN

OVN-Kubernetes creates the following cluster topology features:

OVN-Kubernetes creates one central distributed cluster router named ovn_cluster_router.

OVN-Kubernetes creates per-node logical switches with individual subnets for local pods.

Pod interfaces connect to the per-node logical switches via LSPs and veth pairs.

A join switch connects the per-node logical switches to the central cluster router.

Distributed gateway ports on the cluster router handle egress NAT and ingress load balancing.

Kubernetes services map to OVN load balancers.

Kubernetes network policies map to OVN ACLs.
