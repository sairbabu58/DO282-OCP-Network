
#### How CNI Works

```
ADD
The engine calls this operation when it starts a pod. The plug-in creates the network interface inside the pod's namespace, connects it to the host network, and assigns an IP address.

DEL
The engine calls this operation when it deletes a pod. The plug-in releases the IP address back to the pool and removes the network interface and associated routes.

CHECK
The engine calls this operation to verify that the pod's networking is still configured correctly.```

```
#### CNI Configurations on node side

```
$ oc debug no/name
$vi  /etc/cni/net.d/


{
  "cniVersion": "1.0.0",
  "name": "ovn-kubernetes", 1
  "type": "ovn-k8s-cni-overlay", 2
  "ipam": {
    "type": "host-local", 3
    "subnet": "10.128.0.0/14"
  }
}
```
#### Network Configuration path

```
user@host:~$ oc get network.config.openshift.io cluster -o yaml
apiVersion: config.openshift.io/v1
kind: Network
...output omitted...
spec:
  clusterNetwork: 1
  - cidr: 10.8.0.0/14
    hostPrefix: 23
...output omitted...
  networkType: OVNKubernetes 2
  serviceNetwork:
  - 172.30.0.0/16 3
status:
  clusterNetwork: 4
  - cidr: 10.8.0.0/14
...output omitted..

```
user@host:~$ oc get network.operator.openshift.io cluster -o yaml
apiVersion: operator.openshift.io/v1
kind: Network
metadata:
  name: cluster
spec:
  clusterNetwork:
  - cidr: 10.8.0.0/14
    hostPrefix: 23
  defaultNetwork:
    ovnKubernetesConfig:
      egressIPConfig: {}
      gatewayConfig:
        ipv4: {}
        ipv6: {}
        routingViaHost: false 1
      genevePort: 6081 2
      ipsecConfig:
        mode: Disabled
      mtu: 1400 3
      policyAuditConfig:
        destination: "null"
        maxFileSize: 50
        maxLogFiles: 5
        rateLimit: 20
        syslogFacility: local0
    type: OVNKubernetes 4
...output omitted...
```

```
user@host:~$ oc get node master01 -o yaml | grep node-subnets
    k8s.ovn.org/node-subnets: '{"default":["10.10.0.0/23"]}'
```

```
user@host:~$ oc get pods -n openshift-multus -o wide
```
