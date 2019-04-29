# Microservices Sandbox

This project contains configuration files to deploy [AIST Microservices SandBox](https://github.com/AITestingOrg?q=aist-sandbox).

## Prerequisites

This project uses Elasticsearch to store the Microservices' logs. In order to run this environment it's recommended to have these minimum resources configured for the docker environment:
- 2 CPUs
- 8GB RAM
- 30GB Hard drive

Once your docker environment is running, update `vm.max_map_count` in order to Elasticsearch to run properly: 
```sh
$ sudo sysctl -w vm.max_map_count=262144
```

## Deploy containers with Fluentd

To deploy the Microservices including [EFK](https://docs.fluentd.org/v0.12/articles/docker-logging-efk-compose) for logging, run: 

```sh
$ docker-compose -f deploy/docker-compose/docker-compose.yml up --build -d
```

Check the containers are running with:
```sh
$ docker ps
```

## Deploy Minikube with Fluentd

To deploy the Microservices, run: 

```sh
$ kubectl create -f deploy/kubernetes/manifests
```

Run the logging pods with [EFK](https://docs.fluentd.org/v0.12/articles/docker-logging-efk-compose):
```sh
kubectl create -f deploy/kubernetes/manifests-logging
```

Check the containers are running with:
```sh
$ kubectl get pods --namespace="rideshare"
```

## Check FrontEnd

Navigate to `http://localhost:4200/`, to load the FrontEnd Microservices webUI.

## Check logs

To check the logs, navigate to `http://localhost:5601/` and configure the `Index pattern` with the value `fluentd-*`. 

On `Time Filter field name` select `@timestamp`

Click on the button `Create`

After that you can filter the logs to search for a specific pattern in the logs' fields.
