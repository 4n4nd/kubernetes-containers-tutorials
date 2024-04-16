# Deploying an application on Kubernetes (k8s)

## Setting up a namespace to deploy our application

We need a namespace for our application to be deployed in. We can create a namespace using `kubectl`:

```bash
kubectl create namespace demo-app-ns
```

## Getting our container image ready

We need to make our container image available to our kind k8s cluster.

```bash
kind load docker-image demo-flask-app:0.1.0 --name my-cluster
```
Depending on your system, this might take a minute or two.

## Configuring our application deployment
A simple pod configuration for k8s looks like:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: demo-app-pod
  labels:
    app: demo-app
spec: # <- This is the Pod spec. It contains the spec for all containers inside the pod>
  containers: # <- A pod can have multiple containers in it>
  - name: webserver
    image: demo-flask-app:0.1.0 # <- container image>
    imagePullPolicy: IfNotPresent
    ports: # <- Ports from the container that we want to expose>
    - containerPort: 5000
```

## Deploy our application pod
Once you have configured your pod.yaml file, we can deploy it on our k8s cluster.

```bash
kubectl apply -f ./pod.yaml -n demo-app-ns
```

In the above command, `-n demo-app-ns` specifies which namespace the pod should be deployed to.

## Checking the status of the pod

1. You can see if the pod is running or is in failed state by listing all the pods in `demo-app-ns` namespace 

    ```bash
    kubectl get pods -n demo-app-ns
    ```

    Expected output:
    ```bash
    NAME           READY   STATUS    RESTARTS   AGE
    demo-app-pod   1/1     Running   0          5m47s
    ```
    You should see 1 pod running. Here `1/1` in `Ready` column means 1 out of 1 containers in the pod are ready and running.

2. You can also look at the logs produced by our application

    ```bash
    kubectl logs demo-app-pod -n demo-app-ns
    ```
    Expected output:
    ```log
        * Serving Flask app 'flask-app'
        * Debug mode: off
      WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
        * Running on all addresses (0.0.0.0)
        * Running on http://127.0.0.1:5000
        * Running on http://10.244.0.6:5000
    ```
    Once you have confirmed the application status, we can try to access the web page.

## Accessing the application web page

The web page currently is accessible from within the pod. To make it temporarily available to our local machine, we can set up port forwarding from that pod using `kubectl`

```bash
kubectl port-forward -n demo-app-ns pods/demo-app-pod 5000:5000
```

Now you should be able to access the wepage on your local machine at [`http://127.0.0.1:5000/`](http://127.0.0.1:5000/). This will work as long as the port-forwarding is on.