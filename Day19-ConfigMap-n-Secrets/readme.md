# what is a config map in Kubernetes

- When your manifest grows it becoems difficult to manage multiple env vars
- You can take this out of the manifest and store as config map object in the key-value pair
- Then you can inject that config map into the pod (MOUNTING with VOLUME / PVC)
- You can reuse the same config map into multiple pods

### sample command to create a config map in CLI
```sh
- kubectl create cm <configmap-name> --from-literal=color=blue \ --from-literal=color=red
```

where color=clue is the key and value of the config map


## Secrets
Follow the doc: ttps://kubernetes.io/docs/tasks/inject-data-application/distribute-credentials-secure/#define-container-environment-variables-using-secret-data

### Sample YAML

- CM file
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-cm
stringData:
  firstname: hazlan
  lastname: qodrey
```

- CM file injected in a pod
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
  labels:
    app.kubernetes.io/name: myapp
spec:
  containers:
  - name: myapp-container
    image: busybox:1.28
    command: ['sh', '-c', 'echo The app is running! && sleep 3600']
    env:
    - name: FIRSTNAME
      valueFrom:
        configMapKeyRef:
          name: app-cm
          key: firstname
```
