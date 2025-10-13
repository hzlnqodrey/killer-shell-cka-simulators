# TASK

[V] Login to your cluster and create a pod with the image name as registry.k8s.io/busybox
[V] use the below command for the container touch /tmp/healthy; sleep 30; rm -f /tmp/healthy; sleep 600
[V] create a livenessprobe that executes the command cat /tmp/healthy after every 5 seconds, the first check should be after 5 seconds
[V] create another pod with the image name as registry.k8s.io/e2e-test-images/agnhost:2.40
[V] add the liveness and readiness probes that perform health checks on port 8080 on the path /healthz , the checks should start after 5 seconds for every 10 seconds

  # output
  # Every 2.0s: kubectl get pod                                               hzlnqodrey-MacBook-Air: 20:08:44
#                                                                                             in 0.073s (0)
#NAME            READY   STATUS    RESTARTS      AGE
#liveness-exec   1/1     Running   0             9m12s
#liveness-http   0/1     Running   2 (17s ago)   108s
