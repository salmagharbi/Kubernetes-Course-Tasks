# Kubernetes-Course-Tasks
# Task 1: nginx "hello" page on a 3-node minikube cluster
## Cluster setup
```bash
minikube start --nodes 3 --cni=calico --cpus=2 --memory=2200
kubectl get nodes
```

## Deployment
Files: `deployment.yaml`
```bash
kubectl create namespace webapp
kubectl apply -f deployment.yaml
kubectl get pods -n webapp -o wide
```


## Timestamp updates
```bash
kubectl port-forward -n webapp deploy/web-deployment 8080:80
```



## Step 5: Failing init container
Answers:
- **Status of the new Pod:** `Init:Error` then `Init:CrashLoopBackOff` (0/2), because the init container exits with code 1.
- **Do nginx and time-updater start?** No. Init containers must complete successfully first.
- **Is the page still reachable?** Yes. The rolling update keeps the 3 old healthy Pods running until a new Pod becomes Ready.



## Step 6: Fix
Restored the init command to `echo done`.

## Verification checks

