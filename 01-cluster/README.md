# Running Kubernetes

## Locally

To install and run a lightweight Kubernetes cluster locally

* Install Kind (You should have done this from the prerequisite step)
* Type in `kind create cluster`

You should receive an outcome like this:

``` bash
kind create cluster
Creating cluster "kind" ...
 ✓ Ensuring node image (kindest/node:v1.21.1) 🖼
 ✓ Preparing nodes 📦
 ✓ Writing configuration 📜
 ✓ Starting control-plane 🕹️
 ✓ Installing CNI 🔌
 ✓ Installing StorageClass 💾
Set kubectl context to "kind-kind"
You can now use your cluster with:

kubectl cluster-info --context kind-kind

Not sure what to do next? 😅  Check out https://kind.sigs.k8s.io/docs/user/quick-start/
```

If it fails and you receive this below, make sure Docker Daemon is running.

``` bash
ERROR: failed to create cluster: failed to list clusters: command "docker ps -a --filter label=io.x-k8s.kind.cluster=kind --format '{{.Names}}'" failed with error: exit status 1
Command Output: Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?
```

If all goes to plan then congratulations!. You've just spun up your first local Kubernetes cluster.

## AWS

If you're using AWS then please go to the AWS Console -> Elastic Kubernetes Service -> Click on Add Cluster (Right of the screen) -> Configure a public EKS cluster.

Once it's spun up - you can execute this AWS cli command to gain access to the cluster

``` bash
aws eks update-kubeconfig --name <name-of-cluster>  --region <region> <any-additional-args-required-for-aws-account>
```
