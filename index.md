---
layout: default
title: "Welcome!"
---


##  Welcome to
# The World’s First Fully Distributed Scavenger Hunt!

---


First, we are going to need a Kubernetes cluster. The easiest way to play this game is with a 3 node Amazon EKS cluster, don't worry you won't need it running for too long to find your secret and bring it by the booth.  For expert Kubernetes users, you could run this just about anywhere. Though some strategic alterations to the guide we give would be required...


For the EKS route, your going to want to install `eksctl` and set it up.  Head over to <a href="https://eksctl.io">https://eksctl.io</a> and follow their instructions to get things up and running.


Once you have eksctl setup and connected, you'll need a kubernetes cluster.  This config should help:



```yaml
apiVersion: eksctl.io/v1alpha5
kind: ClusterConfig

metadata:
  region: us-east-1
  name: k8ssandra-demo
availabilityZones: ["us-east-1a", "us-east-1b", "us-east-1c"]
nodeGroups:
  - name: m5
    instanceType: m5.xlarge
    desiredCapacity: 3
    volumeSize: 100
```

then,

```bash
eksctl create cluster -f config.yaml
```

When that spins up, you'll need to deploy this container:

```bash
kubectl run atw --image=k8ssandra/around-the-world:latest --port=4000
kubectl port-forward atw 4000:4000
```

Then connect to it on port 4000 with a web browser for further instructions.

## Good Luck!

