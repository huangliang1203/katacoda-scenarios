## Deploy your application

`kubectl apply -f samples/bookinfo/platform/kube/bookinfo.yaml`{{execute}}

checkout out the service

`kubectl get svc`{{execute}}

```
NAME          TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
details       ClusterIP   10.110.194.143   <none>        9080/TCP   6s
kubernetes    ClusterIP   10.96.0.1        <none>        443/TCP    16m
productpage   ClusterIP   10.101.169.36    <none>        9080/TCP   5s
ratings       ClusterIP   10.97.117.42     <none>        9080/TCP   6s
reviews       ClusterIP   10.96.28.85      <none>        9080/TCP   5s
```

transform the service to service mesh one by one

`istioctl experimental  add-to-mesh service details`{{execute}}
`istioctl experimental  add-to-mesh service productpage`{{execute}}
`istioctl experimental  add-to-mesh service ratings`{{execute}}
`istioctl experimental  add-to-mesh service reviews`{{execute}}


## Check Status

`kubectl get pods`{{execute}}

When the Pods are starting, you may see initiation steps happening as the container is created. This is configuring the Envoy sidebar for handling the traffic management and authentication for the application within the Istio service mesh.

Once running the application can be accessed via the path _/productpage_.

https://[[HOST_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com/productpage

The ingress routing information can be viewed using `kubectl describe ingress`{{execute}}

The architecture of the application is described in the next step.
