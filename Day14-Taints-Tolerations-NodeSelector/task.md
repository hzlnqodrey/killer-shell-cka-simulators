==== [Task details] ====

[] Taint both of your worker nodes as below

[] worker01--> gpu=true:NoSchedule , worker02--> gpu=false:NoSchedule

[] Create a new pod with the image nginx and see why it's not getting scheduled on worker nodes and control plane nodes.

[] Create a toleration on the pod gpu=true:NoSchedule to match with the taint on worker01

[] The pod should be scheduled now on worker01

[] Delete the taint on the control plane node

[] reate a new pod with the image redis , it should be scheduled on control plane node

[] Add the taint back on the control plane node(the one that was removed)

