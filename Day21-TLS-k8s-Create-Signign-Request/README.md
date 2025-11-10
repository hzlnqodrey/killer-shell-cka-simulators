# generate openssl tls key with a key name
openssl genrsa -out example_my_user.key 2048

# so CSR or file format .csr will be create with key name
openssl req -new -key example_my_user.key -out example_my_user.csr -subj "/CN=example_my_user"


# YOU, as kubernetes admin that who has full access privileges, will create new file, named csr.yaml

# to approve user certificate to RBAC k8s (cluster auth), that you state in csr.yaml .metadata.name
> k certificate approve <user>

# check the cert
k get csr <usr> -oyaml > x.yaml
