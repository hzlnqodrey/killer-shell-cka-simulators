# generate openssl tls
openssl genrsa -out example_my_user.key 2048
openssl req -new -key example_my_user.key -out example_my_user.csr -subj "/CN=example_my_user"
