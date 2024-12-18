Comandos para la ejecución del proyecto

mkdir p5 

cd p5 

minikube start

minikube dashboard


fase 1


kubectl create -f aravaca.yaml

kubectl create -f simancas.yaml

kubectl get namespaces

kubectl create -f simancas_deployment.yaml -n simancas-p5

kubectl create -f aravaca_deployment.yaml -n aravaca-p5

kubectl apply -f simancas_service.yaml -n simancas-p5

kubectl apply -f aravaca_service.yaml -n aravaca-p5

sudo apt-get update

sudo apt install python3-pip

pip install prometheus-client

chmod u+r+x ./lanzar_sensores.sh

./lanzar_sensores.sh


fase 2


mkdir data

minikube mount /home/upm/p5/data/:/data/

docker exec -ti minikube bash

ls /data/

mkdir /home/upm/p5/data/aravaca   #añadir el rules y el prom.yml

mkdir /home/upm/p5/data/simancas  #añadir el rules y el prom.yml

kubectl create -f prom-deployment-simancas.yaml -n simancas-p5

kubectl create -f prom-deployment-aravaca.yaml -n aravaca-p5

kubectl apply -f prom-simancas_service.yaml -n simancas-p5

kubectl apply -f prom-aravaca_service.yaml -n aravaca-p5


fase 3


minikube addons enable ingress

sudo nano /etc/hosts  #192.168.49.2 simancas.monitor.es

                       192.168.49.2 aravaca.monitor.es

kubectl apply -f aravaca_ingress.yaml -n aravaca-p5

kubectl apply -f simancas_ingress.yaml -n simancas-p5

docker compose up

