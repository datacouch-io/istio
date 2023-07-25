# Installing Istio

Before you continue, make sure you have a running Kubernetes cluster. You can run `kubectl cluster-info` to check everything is good.

1. Download the latest Istio:
```
curl -L https://git.io/getLatestIstio | sh -
```

2.  In the terminal/console, open the `istio-x` folder (or the folder where you downloaded/extracted the Istio to).

3. Install the demo profile of Istio:

    ```bash
    istioctl manifest apply --set profile=demo
    ```

4.  Verify the installation/wait for all pods to be in the **Running** state:

    ```code
    $ kubectl get pods -n istio-system
    ```

    ```bash

    NAME                                    READY   STATUS    RESTARTS   AGE
    istio-egressgateway-5bb5844-llc84       1/1     Running   0          76s
    istio-ingressgateway-5948b68c88-spxrb   1/1     Running   0          76s
    istiod-845c49bbfd-hvpft                 1/1     Running   0          94s
    ```

Once you see output similar to the one above, you have successfully installed Istio on your Kubernetes cluster. Next, we are going to label the default namespace, so anything we deploy in that namespace will have the Envoy proxy automatically injected:

```bash
kubectl label namespace default istio-injection=enabled
```

## Uninstalling Istio

To remove all Istio resources installed on the cluster, run:

```
istioctl manifest generate --set profile=demo | kubectl delete -f -
```

## What next?

Now that you have everything set up, you can continue with the exercises below:

- [Traffic management](./traffic/README.md)
- [Resiliency](./resiliency/README.md)
- [Security](./security/README.md)
