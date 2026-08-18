
#### How CNI Works

```
ADD
The engine calls this operation when it starts a pod. The plug-in creates the network interface inside the pod's namespace, connects it to the host network, and assigns an IP address.

DEL
The engine calls this operation when it deletes a pod. The plug-in releases the IP address back to the pool and removes the network interface and associated routes.

CHECK
The engine calls this operation to verify that the pod's networking is still configured correctly.```

```
