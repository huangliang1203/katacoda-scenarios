Istio is installed in two parts. The first part involves the CLI tooling that will be used to deploy and manage Istio backed services. The second part configures the Kubernetes cluster to support Istio.

## Install CLI tooling

The following command will install the Istio 1.3.0 release.

`curl -L https://git.io/getLatestIstio | ISTIO_VERSION=1.3.0 sh -`{{execute}}

After it has successfully run, add the bin folder to your path.

`export PATH="$PATH:/root/istio-1.3.0/bin"`{{execute}}

`cd /root/istio-1.3.0/bin"`{{execute}}

## Install with Helm via helm template
Choose this option if your cluster doesn’t have Tiller deployed and you don’t want to install it.

Create a namespace for the istio-system components:

`kubectl create namespace istio-system`{{execute}}

Install all the Istio Custom Resource Definitions (CRDs) using kubectl apply, and wait a few seconds for the CRDs to be committed in the Kubernetes API-server:

`helm template install/kubernetes/helm/istio-init --name istio-init --namespace istio-system | kubectl apply -f -`{{execute}}

Verify that all 23 Istio CRDs were committed to the Kubernetes api-server using the following command:

`kubectl get crds | grep 'istio.io' | wc -l`{{execute}}

### Istio CNI enabled
Install the Istio CNI components:

`helm template install/kubernetes/helm/istio-cni --name=istio-cni --namespace=kube-system | kubectl apply -f -`{{execute}}

Enable CNI in Istio by setting --set istio_cni.enabled=true in addition to the settings for your chosen profile. For example, to configure the default profile:

`helm template install/kubernetes/helm/istio --name istio --namespace istio-system --set istio_cni.enabled=true | kubectl apply -f -`{{execute}}


## Check Status

All the services are deployed as Pods. Once they're running, Istio is correctly deployed.

`kubectl get pods -n istio-system`{{execute}}
