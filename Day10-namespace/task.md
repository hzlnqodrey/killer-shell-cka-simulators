https://github.com/piyushsachdeva/CKA-2024/blob/main/Resources/Day10/task.md#task-details

[V] Create two namespaces and name them ns1 and ns2
[V] Create a deployment with a single replica in each of these namespaces with the image as nginx and name as 
deploy-ns1 and deploy-ns2, respectively
[V] Get the IP address of each of the pods (Remember the kubectl command for that?)
[V] Exec into the pod of deploy-ns1 and try to curl the IP address of the pod running on deploy-ns2
[V] Your pod-to-pod connection should work, and you should be able to get a successful response back.
[V] Now scale both of your deployments from 1 to 3 replicas.
[V] Create two services to expose both of your deployments and name them svc-ns1 and svc-ns2
[V] exec into each pod and try to curl the IP address of the service running on the other namespace.
[V] This curl should work.
[V] Now try curling the service name instead of IP. You will notice that you are getting an error and cannot resolve
 the host.
[V] Now use the FQDN of the service and try to curl again, this should work.

[V] In the end, delete both the namespaces, which should delete the services and deployments underneath them.


# HINT: to see FQDN (Fully Qualified Domain Name in pod)
#     : look inside pod: /etc/resolv.conf
