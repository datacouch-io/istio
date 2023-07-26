# Istall Istio and start your cluster

> Adapted from the [Istio Quick Start](https://istio.io/docs/setup/kubernetes/quick-start/)

Start your minikube cluster with the below command:
```
minikube start --memory=4096
```
## 1.1 Deploy Istio

Go to the Istio release page below to download the installation file for your OS, or download and extract the latest release automatically (Linux or macOS):
https://github.com/istio/istio/releases/tag/1.18.1

Move to the Istio package directory. For example, if the package is istio-1.18.1:
```
cd istio-1.18.1
```
The installation directory contains:

>Sample applications in samples/

>The istioctl client binary in the bin/ directory.

Add the istioctl client to your path (Linux or macOS):

>export PATH=$PWD/bin:$PATH


## 1.2 Install Istio

For this installation, we use the demo configuration profile. It’s selected to have a good set of defaults for testing, but there are other profiles for production or performance testing.


```
istioctl install --set profile=demo -y
```
Add a namespace label to instruct Istio to automatically inject Envoy sidecar proxies when you deploy your application later:

```
kubectl label namespace default istio-injection=enabled
```

## 1.3 Deploy the sample application

Deploy the Bookinfo sample application:

```
kubectl apply -f samples/bookinfo/platform/kube/bookinfo.yaml
```

The application will start. As each pod becomes ready, the Istio sidecar will be deployed along with it.

```
kubectl get services
```
and

```
kubectl get pods
```


## 1.4 Check what's running

Run the below command on a new terminal
```
minikube tunnel
```
Execute the following command to determine if your Kubernetes cluster is running in an environment that supports external load balancers:
```
kubectl get svc istio-ingressgateway -n istio-system
```

```
kubectl get all

docker info
```
