# runu  extension

## Installation

See [Installing Extensions](https://github.com/siderolabs/extensions#installing-extensions).

## Usage

[runu](https://unikraft.org/docs/getting-started/integrations/container-runtimes) is a container runtime used to start unikernels alongside regular containers.
It requires KVM and and QEMU to be installed on the host machine.

## Testing

Apply the following manifest to run nginx pod via gVisor:

```yaml
apiVersion: node.k8s.io/v1
kind: RuntimeClass
metadata:
  name: runu
handler: runu
---
apiVersion: v1
kind: Pod
metadata:
  name: my-unikernel
spec:
  runtimeClassName: runu
  containers:
  - name: app
    image: unikraft.org/app-nginx
```

The pod should be up and running:

```bash
$ kubectl get pods -o wide
NAME           READY   STATUS    IP           NODE                
my-unikernel   1/1     Running   10.42.0.10   node-1
```
