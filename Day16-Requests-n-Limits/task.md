## Task 16/40

In this exercise, you will explore Resource requests and limits in Kubernetes

### Task details
[V] login to your cluster and create a new namespace with the name mem-example
[V] Install metrics server using the yaml provided in this repo
[V]Perform the steps given in the below doc:
  
https://kubernetes.io/docs/tasks/configure-pod-container/assign-memory-resource/#specify-a-memory-request-and-a-memory-limit

[Cases]:
 [V] Reasonable resources
 [V] Over Provisioned Resources

	# Result:
	# OOM-Killed and CLBO (CrassLoopBackOff)
│ memory-demo  ●  0/1   CrashLoopBackOff         2   0   0    n/a    n/a      0      0 10.244.1.3  hzln-cluster-kin │
│ memory-demo  ●  0/1   OOMKilled         3   0   0    n/a    n/a      0      0 10.244.1.3  hzln-cluster-kind-worke │
 Warning  BackOff    12s (x5 over 59s)  kubelet            Back-off restarting failed container memory-demo-hzln │
│  in pod memory-demo_mem-example(12b61141-fed6-44d7-950d-3eb3a73453ee) 
