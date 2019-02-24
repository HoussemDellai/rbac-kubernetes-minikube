# generate .key
openssl genrsa -out user1.key 2048

# generate .csr
openssl req -new \
    -key user1.key \
    -out user1.csr \
    -subj "/CN=user1/O=eralabs"

ls ~/.minikube/
# Check that the files ca.crt and ca.key exist in the location.

# generate .crt
openssl x509 -req \
    -in user1.csr \
    -CA ~/.minikube/ca.crt \
    -CAkey ~/.minikube/ca.key \
    -CAcreateserial \
    -out user1.crt \
    -days 500

kubectl config set-credentials user1 \
    --client-certificate=user1.crt \
    --client-key=user1.key

kubectl config set-context user1-context \
    --cluster=minikube \
    --namespace=default \
    --user=user1

kubectl config view

kubectl config use-context user1-context

kubectl config current-context

kubectl create namespace ns-test # Forbidden
kubectl get pods # Forbidden

# Role & RoleBinding

kubectl config use-context minikube

kubectl apply -f role.yaml

kubectl apply -f role-binding.yaml

kubectl get roles

kubectl get rolebindings

kubectl config use-context user1-context

kubectl create namespace ns-test

kubectl get pods