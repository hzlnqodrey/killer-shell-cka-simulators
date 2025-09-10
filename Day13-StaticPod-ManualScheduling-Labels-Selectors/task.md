[]

[V] Create a pod and try to schedule it manually without the scheduler.
	hint: add attr nodeName in pods manifest

[V] Login to the control plane node and go to the directory of default static pod manifests and try to restart the control plane components
	hint: if using kind, look at docker ps - and exec it (the node you set in the pod)

docker exec -it hzln-cluster-kind-control-plane bash
root@hzln-cluster-kind-control-plane:/# cd /etc/kubernetes/manifests/
root@hzln-cluster-kind-control-plane:/etc/kubernetes/manifests# ls -lah
total 28K
drwxr-xr-x 1 root root 4.0K Sep 10 14:00 .
drwxr-xr-x 1 root root 4.0K Sep 10 14:00 ..
-rw------- 1 root root 2.6K Sep 10 14:00 etcd.yaml
-rw------- 1 root root 3.9K Sep 10 14:00 kube-apiserver.yaml
-rw------- 1 root root 3.4K Sep 10 14:00 kube-controller-manager.yaml
-rw------- 1 root root 1.7K Sep 10 14:00 kube-scheduler.yaml


[V] Create 3 pods with the name as pod1, pod2 and pod3 based on the nginx image and use labels as env:test, env:dev and env:prod for each of these pods respectively.

[V] Then using the kubectl commands, filter the pods that have labels dev and prod.
