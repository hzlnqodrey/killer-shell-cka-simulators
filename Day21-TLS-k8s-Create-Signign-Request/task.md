In this exercise, you to work with TLS certificates in Kubernetes

Task details

1. Generate a PKI private key and CSR and name it as learner.key and learner.csr

  # HINT
  	# Generate PKI
	openssl genrsa -out learner.key 2048
  
	# Generate CSR
	openssl req -new -key learner.key -out learner.csr -subj "/CN=learner"

2. Create a CertificateSigningRequest for learner and set the expiration date to 1 week
  # HINT
  	# create CertificateSigningRequest yaml
apiVersion: certificates.k8s.io/v1
kind: CertificateSigningRequest
metadata:
  name: learner
spec:
  request: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURSBSRVFVRVNULS0tLS0KTUlJQ1Z6Q0NBVDhDQVFBd0VqRVFNQTRHQTFVRUF3d0hiR1ZoY201bGNqQ0NBU0l3RFFZSktvWklodmNOQVFFQgpCUUFEZ2dFUEFEQ0NBUW9DZ2dFQkFKTkpJczJvT04rRnlpOVBkSFBVZFJ5NkVvclN5KzdsbjhMT1NXV1RzczF6CkdyczF6M09qVzVwcHpNZ2hUaXJMaGNROHBWWTh2ZUFaS2k0ak1qOTE2QXNZcnZKaTMyQjVLL3VvZERjcUljdHQKY2k3VmlPWXFydEdQZ2hZZmNkK2Rad0xUbGFLRUphRldKamFQWm5XQlhqaTlwTk9ZVDFKVFk1ZGZWRm9CWktzbApkRm1xc3M3UFdaQnRUeW1ObkFFOWk1eU5DWHJIYnV6Z2pyeDZGb1JhQWhWcWpxaFlySTd5N2lJSmRDWFNsZURUClFodDA1T2RCbVBPbWFzcWxTdE9yTjRvM2VmQThiZmJOUTdJRTNQMUdSMGZIWVdpRHU1WTlXMExleWhLNm5kbjIKV2ZJUDBVYVV6K1NzSjlSVXV0UktWelVuM0thelpWKzM4c01BQXlrVktMOENBd0VBQWFBQU1BMEdDU3FHU0liMwpEUUVCQ3dVQUE0SUJBUUE2ZkR0Wm5aVGN2WEt5NnRlSFBGNnpsQklRQ0tMdHBPQmNpamtMNUlzUEZtbU93Rms3CmdTRVNsblM2L2VtZWY2RXhNRDNURUdtNDZNc2dqZVBCYVdJa21KeTN3Wk95Z013cTdGaVJIVWZHK0RiU2lDNUgKRkhuNkpOYXpmamdGZTV2L3JXaVo2dkpyUldMV3Z4Um1XZ0ZFa3NVbGMvL0JkdmpDZVZKTGx6dlpHcUp3QU0vRwpMNzhBTkx0N0RmUzBQV09janFZU3BoMTBTUXZCZTkvdFp1LzlyeSt4WkxhOFQxY1lreTRNcEJrcDNReU8raFVKCjJQbVZFZ2RpZ3BSZTVKZTVtaWlXOC8xTDRBd3R4SU12ZjMyaXJxSnl6VnMrbWFaTjFkdUpsWmZyUG9PRmF5dzUKaDZRWG4vcjA1VjZ6b1lWZ3lMNDRoZmtFaTZJd1NOWTFqWjZ3Ci0tLS0tRU5EIENFUlRJRklDQVRFIFJFUVVFU1QtLS0tLQo=
  signerName: kubernetes.io/kube-apiserver-client
  expirationSeconds: 604800
  usages:
    - client auth

3. Make sure to use the encoded value of csr in the request field

  # hint

	base64 -i <csr_file / .csr>

4. Approve the csr

  # hint

	> kubectl certificate approve learner

5. Retrieve the certificate from the CSR

  # hint

	> kubectl get csr/learner -oyaml > learner_certificate.yaml

	# in .status.certificate - get the certificate and decoded with:
	> echo "<xxx>" | base64 -d

6. Export the issued certificate from the CertificateSigningRequest to a yaml

  # hint

	> kubectl get csr/learner -oyaml > learner_certificate.yaml

7. Redirect the certificate value to learner.crt file after decoding it

	echo "<xxx>" | base64 -d > learner.crt

8. Verify the steps one more time, we will use these details in the next task.

