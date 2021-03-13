gcloud auth list
gcloud config list project

gcloud container clusters create demo-cluster --num-nodes 3 --zone us-central1-f
helm repo add stable https://charts.helm.sh/stable
helm repo update
helm install mycache stable/memcached --set replicaCount=3

kubectl get pods

kubectl get service mycache-memcached -o jsonpath="{.spec.clusterIP}" ; echo
kubectl get endpoints mycache-memcached
kubectl run -it --rm alpine --image=alpine:3.6 --restart=Never nslookup mycache-memcached.default.svc.cluster.local
kubectl run -it --rm python --image=python:3.6-alpine --restart=Never python

kubectl run -it --rm python --image=python:3.6-alpine --restart=Never sh

##### Once you get a shell prompt (/ #) install the pymemcache library:
pip install pymemcache
python

##### In the Python console (>>>), run the following:

import socket
from pymemcache.client.hash import HashClient
_, _, ips = socket.gethostbyname_ex('mycache-memcached.default.svc.cluster.local')
servers = [(ip, 11211) for ip in ips]
client = HashClient(servers, use_pooling=True)
client.set('mykey', 'hello')
client.get('mykey')


kubectl run -it --rm alpine --image=alpine:3.6 --restart=Never telnet mycache-memcached-0.mycache-memcached.default.svc.cluster.local 11211

helm delete mycache
helm install mycache stable/mcrouter --set memcached.replicaCount=3
kubectl get pods

#Task 3:
MCROUTER_POD_IP=$(kubectl get pods -l app=mycache-mcrouter -o jsonpath="{.items[0].status.podIP}")
kubectl run -it --rm alpine --image=alpine:3.6 --restart=Never telnet $MCROUTER_POD_IP 5000

#####In telnet Prompt enter:

set anotherkey 0 0 15
Mcrouter is fun

get anotherkey




#### In Cloud Shell Enter:

cat <<EOF | kubectl create -f -
apiVersion: apps/v1
kind: Deployment
metadata:
  name: sample-application-py
spec:
  replicas: 5
  selector:
    matchLabels:
      app: sample-application-py
  template:
    metadata:
      labels:
        app: sample-application-py
    spec:
      containers:
        - name: python
          image: python:3.6-alpine
          command: [ "sh", "-c"]
          args:
          - while true; do sleep 10; done;
          env:
            - name: NODE_NAME
              valueFrom:
                fieldRef:
                  fieldPath: spec.nodeName
EOF

kubectl get pods
