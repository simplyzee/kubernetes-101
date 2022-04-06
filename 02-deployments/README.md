# Kubernetes Deployments

We're going to be looking at Kubernetes Deployments. Deployments will help us understand the k8s terminology between different workloads e.g. Pods, ReplicaSets, HorizontalPodAutoscaler, etc.
In the manifest folder, there will be a bunch of deployments (written in YAML). YAML is the preferred language for applying changes to a Kubernetes cluster.

## Dashboard

Let's look at the first deployment which is the Kubernetes Dashboard. This deployment will help give you a frontend visual of what happens inside a k8s cluster.

Inside manifests/dashboard - you can apply the deployment for dashboard by doing:

``` bash
kubectl apply -f manifest/dashboard/deployment.yaml
```

(I will explain and go into detail why I use `apply` over `create`)

Once this is deployed, you should see an outcome like this:

``` bash
namespace/kubernetes-dashboard created
serviceaccount/kubernetes-dashboard created
service/kubernetes-dashboard created
secret/kubernetes-dashboard-certs created
secret/kubernetes-dashboard-csrf created
secret/kubernetes-dashboard-key-holder created
configmap/kubernetes-dashboard-settings created
role.rbac.authorization.k8s.io/kubernetes-dashboard created
clusterrole.rbac.authorization.k8s.io/kubernetes-dashboard created
rolebinding.rbac.authorization.k8s.io/kubernetes-dashboard created
clusterrolebinding.rbac.authorization.k8s.io/kubernetes-dashboard created
deployment.apps/kubernetes-dashboard created
service/dashboard-metrics-scraper created
deployment.apps/dashboard-metrics-scraper created
```

We can confirm the pods are running by executing - `kubectl get pods -n kubernetes-dashboard` OR for short `kubectl get po -n kubernetes-dashboard` (notice po - there's a few of these in lots of area's of k8s)

``` bash
kubectl get po -n kubernetes-dashboard
NAME                                        READY   STATUS    RESTARTS   AGE
dashboard-metrics-scraper-c45b7869d-xmxlx   1/1     Running   0          11s
kubernetes-dashboard-764b4dd7-t824s         1/1     Running   0          11s
```

## Let's look at it via the browser

Because we don't have ingress set up locally, we'll have to proxy ourselves to the api via `kubectl proxy` - this will then bind us to the api server on port `8001` (or you're chosen port)

``` bash
kubectl proxy
Starting to serve on 127.0.0.1:8001
```

Go to: [http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/#/login](http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/#/login)

## Service Accounts

Now you would've noticed it asked for a token or a kubeconfig file. This is for authentication - Authentication in kubernetes happens generally with `ServiceAccounts`
There is another file in the manifest folder called `admin-sa.yaml` - let's take a look and then apply it.

Once it's applied, let's retrieve the bearer token with

``` bash
kubectl -n kubernetes-dashboard get secret $(kubectl -n kubernetes-dashboard get sa/admin-user -o jsonpath="{.secrets[0].name}") -o go-template="{{.data.token | base64decode}}"
```

Use the contents from that command as the token. Paste that token into the Dashboard UI and you should have master access within Kubernetes.
