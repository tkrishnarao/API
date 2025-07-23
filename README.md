This is my attempt at making a personal API using the open-source version of Gloo Gateway and connecting it to a personal database. This repository also contains example manifests for routing requests through *Gloo Gateway* to a sample petstore service.

## Prerequisites

- Access to a Kubernetes cluster
- kubectl configured for that cluster
- Gloo Gateway installed

## Deploy the sample service

Apply the Deployment and Service:

bash
kubectl apply -f YAML/default-petstore.yaml


Wait until the default-petstore Pod is running.

## Apply the Gloo Gateway configuration

Create the upstream and virtual service:

bash
kubectl apply -f YAML/petstore-upstream.yaml
kubectl apply -f YAML/virtualservice.yaml


## Port-forward the gateway

Run the following command in a separate terminal:

bash
kubectl -n gloo-system port-forward deploy/gateway-proxy 8080


Leave this command running so that the gateway is reachable at http://localhost:8080.

## Test the route

Send a request to the gateway:

bash
curl http://localhost:8080/


You should see the petstore API response.
