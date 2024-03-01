<!-- note marker start -->
NOTE: This repo contains only the documentation for the private BoltsOps repo code.
Original file: https://github.com/boltops-learn/kubernetes-app-organization-with-namespaces/blob/master/env-namespaces/README.md
The docs are publish so they are available for interested subscribers.
For access to the source code, you can become a BoltOps subscriber.
See: https://learn.boltops.com

<!-- note marker end -->

# App Namespace Organization Demo

[![BoltOps Badge](https://img.boltops.com/boltops/badges/boltops-badge.png)](https://www.boltops.com)

We'll create these Kubernetes resources:

1. [deployment](deployment.yaml): Run nginx web server pods.
2. [service](service.yaml): Expose an endpoint to reach the nginx pods.

## Namespace

Should create namespaces outside of kubes lifecycle.

    kubectl create ns dev
    kubectl create ns prod
    kubectl create ns bob
    kubectl create ns kevin

## Deploy All

    for app in app1 app2 ; do
      for i in dev prod kevin bob ; do
        APP=$app KUBES_ENV=$i kubes deploy
      done
    done

## Confirm

    kubectl config set-context --current --namespace=app1
    kubectl get all

## Filtering

    kubectl get all -l env=dev
    kubectl get all -l env=prod
    kubectl get all -l env=bob

## Delete All

    for app in app1 app2 ; do
      for i in dev prod kevin bob ; do
        APP=$app KUBES_ENV=$i kubes delete -y
      done
    done
