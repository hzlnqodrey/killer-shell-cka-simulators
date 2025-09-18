==== [Task details] ====

[V] Taint both of your worker nodes as below

[V] worker01--> gpu=true:NoSchedule , worker02--> gpu=false:NoSchedule

  # Hint:
  	# WK01
	> k taint nodes hzln-cluster-kind-worker gpu=true:NoSchedule
	> k get nodes hzln-cluster-kind-worker -o yaml | grep -i -n "taints"
	
	# WK02
	> k taint nodes hzln-cluster-kind-worker2 gpu=false:NoSchedule
	

[V] Create a new pod with the image nginx and see why it's not getting scheduled on worker nodes and control plane nodes.

  # Hint:
	# nginx-pod
	> k run nginx-pod --image=nginx
	  Status: Pending

	> kd pod/nginx-pod
	Events:
  Type     Reason            Age   From               Message
  ----     ------            ----  ----               -------
  Warning  FailedScheduling  12s   default-scheduler  0/3 nodes are available: 1 node(s) had untolerated taint {gpu: false}, 1 node(s) had untolerated taint {gpu: true}, 1 node(s) had untolerated taint {node-role.kubernetes.io/control-plane: }. preemption: 0/3 nodes are available: 3 Preemption is not helpful for scheduling.

  # Answer: 0/3 node available.
		1 node for control-plane
		1 node there is taint[gpu=true]
		1 node there is taint[gpu=false]

[] Create a toleration on the pod gpu=true:NoSchedule to match with the taint on worker01

  # HINT
	# create pod yaml file from CLI
	> kubectl run nginx-tolerate --image=nginx --dry-run=client -o yaml > new-nginx-pod.yaml

	# apply yaml file nginx-fix.yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: nginx-fix
  name: nginx-fix
spec:
  containers:
  - image: nginx
    name: nginx-fix
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
  tolerations:
  - key: "gpu"
    operator: "Equal"
    value: "true"
    effect: "NoSchedule"
status: {}



[V] The pod should be scheduled now on worker01

[V] Delete the taint on the control plane node

  # Hint
	# look for taint setting on the Control Plane Node
	> k get nodes hzln-cluster-kind-control-plane -o yaml | grep -i -n "taint"
	> k get node hzln-cluster-kind-control-plane -o yaml	
	> k taint nodes hzln-cluster-kind-control-plane node-role.kubernetes.io/control-plane:NoSchedule-
	
	  node/hzln-cluster-kind-control-plane untainted

[V] Create a new pod with the image redis , it should be scheduled on control plane node

  # HINT

	> k run redis-tolerate --image=redis

  # answer:
	# yes they are running on the control plane node

NAME             READY   STATUS    RESTARTS   AGE     IP           NODE                              NOMINATED NODE   READINESS GATES
nginx-fix        1/1     Running   0          5m49s   10.244.1.3   hzln-cluster-kind-worker          <none>           <none>
nginx-pod        1/1     Running   0          33m     10.244.0.5   hzln-cluster-kind-control-plane   <none>           <none>
redis-tolerate   1/1     Running   0          27s     10.244.0.6   hzln-cluster-kind-control-plane   <none>           <none>


[V] Add the taint back on the control plane node(the one that was removed)

  # HINT

	# add taint back
	>  k taint nodes hzln-cluster-kind-control-plane node-role.kubernetes.io/control-plane:NoSchedule


[================]

# So Summary

	# Taints and Tolerations
	[NODE POV] is to repel and reject pod that not matched

		# Effects of scheduling:
		- NoSchedule : (for NEWER PODS)
		- NoExecute  : (maybe EXISTING PODS / NEWER PODS)
		- PreferNoScheduly: (No Guarantee 5050)

	# NodeSelectors
	[POD POV] Pod chooses which node suits them
	for example: this pod need to be placed on AI/ML Cluster because has higher gpu resource

	> nodeSelectors:
	    - gpu: true


