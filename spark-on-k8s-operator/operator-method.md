# Using Kubernetes Operator for Apache Spark

```sh
helm repo add spark-operator https://googlecloudplatform.github.io/spark-on-k8s-operator

helm repo update

helm install my-release spark-operator/spark-operator --namespace spark-operator --create-namespace

helm status --namespace spark-operator my-release
```

need to set the `metadata.namespace` and `spec.driver.serviceAccount`. use `spark-pi-sa.yaml`:
```sh
kubectl apply -f examples/spark-pi-sa.yaml
kubectl get pods --all-namespaces
kubectl get sparkapplications spark-pi -o=yaml

kubectl logs spark-pi-driver -n spark-operator | grep "Pi is"
kubectl describe sparkapplication spark-pi -n spark-operator

kubectl delete sparkapplications spark-pi -n spark-operator
```