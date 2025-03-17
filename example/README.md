# To create K8s example

1.Execute below command
kind create cluster --config config.yaml

2.Deploy Ingress-Nginx
kubectl create -f https://ghfast.top/https://raw.githubusercontent.com/lyzhang1999/resource/main/ingress-nginx/ingress-nginx.yaml

3.Deploy Metric Server to enable HPA
kubectl apply -f https://ghfast.top/https://raw.githubusercontent.com/lyzhang1999/resource/main/metrics/metrics.yaml

4.Create namespace
kubectl create namespace example

5.Create Postgres DB
Use `-n` to specify namespace. All resources should follow the same setting.
kubectl apply -f https://ghfast.top/https://raw.githubusercontent.com/lyzhang1999/kubernetes-example/main/deploy/database.yaml -n example

6.Create Deployment & Service
kubectl apply -f https://ghfast.top/https://raw.githubusercontent.com/lyzhang1999/kubernetes-example/main/deploy/frontend.yaml -n example

kubectl apply -f https://ghfast.top/https://raw.githubusercontent.com/lyzhang1999/kubernetes-example/main/deploy/backend.yaml -n example


7.Create HPA policy and Ingress for application
kubectl apply -f https://ghfast.top/https://raw.githubusercontent.com/lyzhang1999/kubernetes-example/main/deploy/ingress.yaml -n example

Sometimes need to clear nginx webhook cert with below command
kubectl delete validatingwebhookconfigurations ingress-nginx-admission
kubectl delete secret ingress-nginx-admission -n ingress-nginx
kubectl delete job ingress-nginx-admission-create ingress-nginx-admission-patch -n ingress-nginx


kubectl apply -f https://ghfast.top/https://raw.githubusercontent.com/lyzhang1999/kubernetes-example/main/deploy/hpa.yaml -n example


We can execute below command to apply all config. It will read Manifest under the folder and deploy to K8s cluster.

cd example
kubectl apply -f deploy -n example


8.Open browser and access "http://127.0.0.1"