# react-java_helm
Metalbb configuration

kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.13.4/config/manifests/metallb-native.yaml


2) vim address.pool.yml
apiVersion: metallb.io/v1beta1
kind: IPAddressPool
metadata:
  name: first-pool
  namespace: metallb-system
spec:
  addresses:
  - 192.168.1.240-192.168.1.250  #This ip address must be unical, we doesn't take a master and worker IP addresses. We take IPs from dhcp exclude
  
3) vim l2.yml
apiVersion: metallb.io/v1beta1
kind: L2Advertisement
metadata:
  name: example
  namespace: metallb-system
spec:
  ipAddressPools:
  - first-pool
  
  
kubectl apply -f address.pool.yml
kubectl apply -f l2.yml
