<h2>"Welcome to DigitalOcean!" using the Apache HTTP server.</h2>

## Overview

This project demonstrates a simple web application deployed on a DigitalOcean Kubernetes cluster. This repository contains the configuration files for deploying a simple Apache web application to DigitalOcean Kubernetes. 

## Prerequisites

*   A DigitalOcean account.
*   Docker Desktop (for windows machine) installed locally.
*   kubectl configured to connect to your Kubernetes cluster. configure it from [https://kubernetes.io/docs/tasks/tools/]
*   A Docker Hub account (or another container registry).
*   `doctl` command-line tool (for interacting with DigitalOcean). Install it from [https://docs.digitalocean.com/cli/doctl/install/](https://docs.digitalocean.com/cli/doctl/install/)

## Files

*   `Dockerfile`: Instructions for building the Docker image. This file is present in the docker directory
*   `index.html`: The HTML file for the webpage. This file is present in the docker directory
*   `deployment-app.yaml`: Kubernetes deployment configuration.
*   `amiteshlb.yaml`: Kubernetes service configuration (LoadBalancer).
*   `namespaceamitesh.yaml`: Kubernetes namespace configuration (optional, but recommended).
*   `deployment-app-hpa.yaml`: kubernetes hpa configuration.

## Building and Pushing the Docker Image

1.  Clone this repository:

    ```bash
    git clone https://github.com/amiteshpandey/digital-ocean-test.git
    ```

2.  Navigate to the project directory:

    ```bash
    cd docker  # Or the name of your project directory
    ```

3.  You will see `index.html` and `Dockerfile`

4.  Docerfile will help you to create an image.

5.  Build the Docker image:

    ```bash
    docker build -t your-image-name .
    ```

6.  Log in to Docker Hub:

    ```bash
    docker login
    ```

7.  Tag and push the image to your *public* Docker Hub repository:

    ```bash
    docker tag your-image-name <your-dockerhub-username>/your-image-name
    
    docker push <your-dockerhub-username>/your-image-name
    ```

## Creating a DigitalOcean Kubernetes Cluster

### Using the DigitalOcean Control Panel (UI):

1.  Log in to your DigitalOcean account.
2.  Navigate to the Kubernetes section.
3.  Click "Create Cluster".
4.  Choose a region, Kubernetes version, and node size.
5.  Configure the number of nodes in your node pool.
6.  Click "Create Cluster".

## Using `doctl` (CLI):

1.  Authenticate `doctl`:

    ```bash
    doctl auth init
    ```

2.  Create the Kubernetes cluster:

    ```bash
    doctl kubernetes cluster create my-cluster \
      --region <your-region> \
      --version <kubernetes-version> \
      --node-pool name=pool-0 size=<node-size> count=<number-of-nodes> \
      --auto-scale min-nodes=<min-nodes> max-nodes=<max-nodes> # Optional autoscaling
    ```

    Example:

    ```bash
    doctl kubernetes cluster create my-cluster \
      --region nyc3 \
      --version latest \
      --node-pool name=pool-0 size=s-2vcpu-4gb count static website.</h1>
  
## Connect to the kubernetes cluster:

1. using doctl --

```bash
 doctl kubernetes cluster kubeconfig save <your-cluster-name>
```

2. using kubectl

```bash
kubectl config get-contexts (You should see your DigitalOcean Kubernetes cluster context listed.  If you have multiple contexts, you might need to switch to the correct one:)

kubectl config use-context <your-cluster-context-name>
```

 ## Deploy the application
 
 ```bash

 kubectl apply -f  namespaceamitesh.yaml

kubectl apply -f . (this will deploy all the files together)

 ```

Let's delve into the concepts of Pods, Services, namespace, and Deployments in Kubernetes

```bash

* Since a dedicated namespace has been created for this application, it's crucial to specify the namespace when executing kubectl commands.  You can do this in two ways:

			 1. kubectl get pods -n <namespace-name>
			 2. Setting the default namespace for the current context: kubectl config set-context --current --namespace=<namespace-name>

* check the pod status using - kubectl get pods pod-name

* if any errors, cehck the pods logs using - kubectl logs pod-name

* check the status of the service - kubectl get svc

* Access the application in your browser using the external IP of the load balancer.

* To get information about resource in the namespace use - kubectl get all
```

## Destroy the application

To delete the application

```bash
kubectl delete -f .
```

To delete the cluster

```bash
doctl kubernetes cluster delete <your-cluster-name>
```
