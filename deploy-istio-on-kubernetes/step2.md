Istio is installed in two parts. The first part involves the CLI tooling that will be used to deploy and manage Istio backed services. The second part configures the Kubernetes cluster to support Istio.

## Install CLI tooling

The following command will install the Istio 1.3.0 release.

`curl -L https://git.io/getLatestIstio | ISTIO_VERSION=1.3.0 sh -`{{execute}}

After it has successfully run, add the bin folder to your path.

`export PATH="$PATH:/root/istio-1.3.0/bin"`{{execute}}

`cd /root/istio-1.3.0/bin"`{{execute}}

## Configure Istio CRD
Install all the Istio Custom Resource Definitions (CRDs) using kubectl apply, and wait a few seconds for the CRDs to be committed in the Kubernetes API-server:

`helm template install/kubernetes/helm/istio-init --name istio-init --namespace istio-system | kubectl apply -f -`{{execute}}


## Configure Istio

The core components of Istio are deployed via _istio.yaml_.

`kubectl apply -f istio/istio.yaml`{{execute}}

This will deploy Pilot, Mixer, Ingress-Controller, and Egress-Controller, and the Istio CA (Certificate Authority). These are explained in the next step.

## Check Status

All the services are deployed as Pods. Once they're running, Istio is correctly deployed.

`kubectl get pods -n istio-system`{{execute}}

## Deploy Katacoda Service
To make the sample BookInfo application and dashboards available to the outside world, in particular, on Katacoda, deploy the following Yaml

`kubectl apply -f /root/katacoda.yaml`{{execute}}

Without this, the bookInfo example and other dashboards will not be available.