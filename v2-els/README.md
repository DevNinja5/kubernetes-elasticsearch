# ElasticSearch On Kubernetes

## Deploy elasticsearch on minikube node

### 1. Run Minikube

Elasticsearch requires more cpu and memory \
Run the following command.
```bash
minikube start --cpus=3 --memory=5g
```

### 2. Create resources

```bash
kubectl apply -f storage.yml
kubectl apply -f statefulset.yml
kubectl apply -f services.yml
kubectl apply -f data-node-sts.yml
```

### 3. Check all pods are in running status

```bash
kubectl get po -w
```

**Output will look like**

```text
NAME                      READY   STATUS    RESTARTS   AGE
data-0                    1/1     Running   0          175m
data-1                    1/1     Running   0          174m
master-0                  1/1     Running   0          3h
master-1                  1/1     Running   0          3h
```
### 4. To check the API data use **port-forward** on 9200

```
kubectl port-forward master-0 9200:9200
```
**Output will look like:**

```
Forwarding from 127.0.0.1:9200 -> 9200
Forwarding from [::1]:9200 -> 9200


```
### 5. Check on your broswer

```
localhost:9200/_cat/nodes
```