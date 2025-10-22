# task

# one ref
Perform the task given here : https://kubernetes.io/docs/tasks/inject-data-application/distribute-credentials-secure/#define-container-environment-variables-using-secret-data

  # HINT:

	# https://kubernetes.io/docs/tasks/inject-data-application/distribute-credentials-secure/#define-container-environment-variables-using-secret-data
	# /proc/<pid>/environ
	# kubectl create secret generic backend-user --from-literal=backend-username='backend-users'
	# k apply -f <file>
	# k exec --it <name-pod> -- /bin/sh

# all ref
Configure all key-value pairs in a Secret as container environment variables : https://kubernetes.io/docs/tasks/inject-data-application/distribute-credentials-secure/#configure-all-key-value-pairs-in-a-secret-as-container-environment-variables
## Note:
## This functionality is available in Kubernetes v1.6 and later.

