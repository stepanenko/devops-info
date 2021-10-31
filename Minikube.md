
Start cluster: `minikube start`

Checkout created cluster: `kubectl get po -A`

Open dashboard in the browser: `minikube start`

Create deployment: `kubectl create deployment mongo-depl --image=mongo`

Edit deployment: `kubectl edit deployment mongo-depl`

List all: `kubectl get pod/node/deployment/replicaset/service...`

Open info about pod: `kubectl describe pod mongo-depl-5fd6b7d4b4-txzlv`

Open container terminal: `kubectl exec -it mongo-depl-5fd6b7d4b4-txzlv -- bin/bash` where `-it` means interactive terminal

---
More: https://minikube.sigs.k8s.io/docs/start/
