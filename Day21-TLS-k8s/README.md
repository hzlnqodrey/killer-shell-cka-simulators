# generate openssl tls key with a key name
openssl genrsa -out example_my_user.key 2048

# so CSR or file format .csr will be create with key name
openssl req -new -key example_my_user.key -out example_my_user.csr -subj "/CN=example_my_user"
