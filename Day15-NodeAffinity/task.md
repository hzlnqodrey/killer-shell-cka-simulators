TASK:

[V] create a pod with nginx as the image and add the nodeffinity with property requiredDuringSchedulingIgnoredDuringExecution and condition disktype = ssd
  # HINT

	> look file redis-pod-affinity.yaml
	> apply with:
	k apply -f redis-pod-affinity.yaml

[V] check the status of the pod and see why it is not scheduled
  # HINT
        k describe pod/redis-aff

	>   Warning  FailedScheduling  13s   default-scheduler  0/3 nodes are available: 1 node(s) had untolerated taint {node-role.kubernetes.io/control-plane: }, 2 node(s) didn't match Pod's node affinity/selector. preemption: 0/3 nodes are available: 3 Preemption is not helpful for scheduling.

	short answer:
	> no node can scheduled the pod bcs of NodeAffinity (this pod is too picky about where he gonna placed *U(K)
	
[V] add the label to your worker01 node as distype=ssd and then check the status of the pod
  # HINT

	# Labeling nodes
	> k label nodes hzln-cluster-kind-worker disktype=ssd

	# result
	k get nodes --show-labels
	hzln-cluster-kind-worker          Ready    <none>          9m54s   v1.32.0   beta.kubernetes.io/arch=arm64,beta.kubernetes.io/os=linux,disktype=ssd,kubernetes.io/arch=arm64,kubernetes.io/hostname=hzln-cluster-kind-worker,kubernetes.io/os=linux
	
	k describe nodes hzln-cluster-kind-worker
	k describe nodes hzln-cluster-kind-worker | grep -n -i -A5 "disktype" -B5
		A5 (  after 5)
		B5 ( before 5)


[V] It should be scheduled on worker node 1
  # HINT

	# Running on worker node 1
	kgp
		Running
		redis-aff   1/1     Running   0          6m38s

	kd po/redis-aff | grep -n -i -A5 -B5 "node"
		5:Node:             hzln-cluster-kind-worker/172.18.0.3

[V] create a new pod with redis as the image and add the nodeaffinity with property requiredDuringSchedulingIgnoredDuringExecution and condition disktype without any value
  # HINT
  
	# EXISTS Operator
  	# in the node affinity section, remove disktype values, change the oprator value to Exists
	
	# pod redis-aff is still running, why?
	#  because the pod just choose and check any label only, even thought it only has "disktype" key label, and pod choose it


[] add the label to worker02 node with disktype and no value ensure that pod2 should be scheduled on worker02 node
  # HINT

	# how you do it
	>kubectl label nodes hzln-cluster-kind-worker2 disktype=
		# node/hzln-cluster-kind-worker2 labeled

	# assign any new pod with only has affinity requirred= disktype label and operator exists
	

[] add prefer
