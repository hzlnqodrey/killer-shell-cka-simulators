# Day 16/40 - Kubernetes Requests and Limits

## Check out the video below for Day16 👇

[![Day12/40 - Kubernetes Requests and Limits](https://img.youtube.com/vi/Q-mk6EZVX_Q/sddefault.jpg)](https://youtu.be/Q-mk6EZVX_Q)


# Understanding Kubernetes Request and Limits

Welcome to the Kubernetes Requests & Limits guide! This document complements our video explaining managing resource allocation in your Kubernetes cluster. Let’s explore the essentials of Requests and Limits, why they matter, and how to use them effectively.


## 🏙️ What's the Deal with Requests & Limits?

Think of your kubernetes as a bustling city and pods as tenants in an apartement building. Each tenant (pod) requires sepcific resources like CPU and memory to fucntion:

- **Requests**: This is a minimum amnt of resouces a pod needs to operate smoothly. Think of it as a guaranted reservation for the pod.
- **Limits**: This is a maximum amnt of resouces a pod can use. It acts as a safety cap to prevent any pod from consuming more than its fair share and distrupting others


## Why are the Requests & Limits Important ?

- **Resources Control**: by setting limits, you prevent a single pod from monopolozing resources, which can lead to issues like out-of-memory (OOM) kills or CPU starvation. Why OOM can be a good thing? because it kills the pod; otherwise, the container would have consumed all the memory and could kill the node. Killing the pod is a better option than killing a node itslef
- **Predictability:**: Requests help the scheduler allocate resources  efficiently and ensure pods have the necessary resources to run effectively.

## Exploring RCM (Resource Management) in Action:

Yaml experiment

1. **Exceeding Available Memory**:
- A pod requesting more memory than is available will be killed due to an OOM (Out Of Memory) error.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: backend-service
  namespace: backend
spec:
  containers:
  - name: backend-service-1
    image: polinux/stress
    resources:
      requests:
        memory: "50Mi"
      limits:
        memory: "100Mi"
    command: ["stress"]
    args: ["--vm", "1", "--vm-bytes", "250M", "--vm-hang", "1"]
```

2. Pod below will be scheduled because below the limits
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: backend-service
  namespace: backend
spec:
  containers:
  - name: backend-service-1
    image: polinux/stress
    resources: 
      requests:
        memory: "100Mi"
      limits:
        memory: "250Mi"
    command: ["stress"]
    args: ["--vm", "1", "--vm-bytes", "150M", "--vm-hang", "1"]
```

