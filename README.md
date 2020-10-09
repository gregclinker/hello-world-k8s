# hello-world-k8s

K8s hello world example.

**To Run on GCP K8s**
```shell script
#
# example script to create a simple k8s cluster and deploy a hello world to it.
# you will need to do a gcloud init before running this script
#
mvn -DskipTests com.google.cloud.tools:jib-maven-plugin:build -Dimage=gcr.io/kubernetes-demo-291914/hello-world:v1
gcloud services enable compute.googleapis.com container.googleapis.com
gcloud container clusters create gregs-cluster   --num-nodes 2   --machine-type n1-standard-1   --zone us-central1-c
kubectl create deployment hello-world --image=gcr.io/kubernetes-demo-291914/hello-world:v1
kubectl get deployments
kubectl get pods
kubectl create service loadbalancer hello-world --tcp=8080:8080
kubectl get services
kubectl get deployment
kubectl get deployments
kubectl scale deployment hello-world --replicas=3
kubectl get deployments
mvn package -DskipTests com.google.cloud.tools:jib-maven-plugin:build -Dimage=gcr.io/kubernetes-demo-291914/hello-world:v2
kubectl set image deployment/hello-world hello-world=gcr.io/kubernetes-demo-291914/hello-world:v2
kubectl get deployments
```
