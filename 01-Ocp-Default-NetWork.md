
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
