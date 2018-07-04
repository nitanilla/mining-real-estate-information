// Create the Mysql Database
kubectl create -f ./../rs-mysql-db/mysql-deployment.yaml

kubectl run -it --rm --image=mysql:5.6 --restart=Never mysql-client -- mysql -h mysql -proot
mysql> CREATE DATABASE rs_db;

// Create de Docker Images, if you haven't
cd ./../rs-catalog-api/
docker build -t gcr.io/real-estate-186513/rs-catalog-api:v1 .

cd ./../rs-property-api/
docker build -t gcr.io/real-estate-186513/rs-property-api:v1 .

cd ./../rs-publication-api/
docker build -t gcr.io/real-estate-186513/rs-publication-api:v1 .

// Deploy de APIs

kubectl create -f ./../rs-catalog-api/deployment.yaml

kubectl create -f ./../rs-publication-api/deployment.yaml

kubectl create -f ./../rs-property-api/deployment.yaml

kubectl create -f ./../rs-catalog-api/service.yaml

kubectl create -f ./../rs-publication-api/service.yaml

kubectl create -f ./../rs-property-api/service.yaml


// Deploy de Ingress

kubectl create -f ./../rs-ingress/ingress.yaml

// ISSUES Minikube

// If the image could not be pulled ...
eval $(minikube docker-env)
docker images